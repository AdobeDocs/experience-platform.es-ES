---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Empaquetar archivos de origen en una fórmula
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Empaquetar archivos de origen en una fórmula

Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de archivo, que se puede utilizar para crear una fórmula en el espacio de trabajo de ciencia de datos de la plataforma de experiencia de Adobe siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o mediante la API.

Conceptos para comprender:

- **Fórmulas**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, la lógica de procesamiento y la configuración necesarios para crear y ejecutar un modelo capacitado y, por tanto, ayuda a resolver problemas comerciales específicos.
- **Archivos** de origen: Archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos

- [Acoplador](https://docs.docker.com/install/#supported-platforms)
- [Python 3 y pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Maven](https://maven.apache.org/install.html)

## Creación de fórmulas

inicios de creación de fórmulas con empaquetado de archivos de origen para crear un archivo de archivo. Los archivos de origen definen la lógica de aprendizaje automático y los algoritmos utilizados para resolver un problema específico que se encuentra en la mano, y se escriben en Python, R, PySpark o Scala. Los archivos de archivo creados toman la forma de una imagen de Docker. Una vez creado, el archivo empaquetado se importa en el área de trabajo de ciencias de datos para crear una fórmula [en la interfaz de usuario](./import-packaged-recipe-ui.md) o [mediante la API](./import-packaged-recipe-api.md).

### Creación de modelos basados en el acoplamiento {#docker-based-model-authoring}

Una imagen de Docker permite a un desarrollador empaquetar una aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y enviarla como un paquete.

La imagen de Docker creada se inserta en el Registro de Contenedor de Azure mediante las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

Para obtener las credenciales de Azure Contenedor Registry, inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>. En la columna de navegación izquierda, navegue a **Flujos de trabajo**. Seleccione **Importar fórmula** , luego seleccione **Iniciar**. Consulte la captura de pantalla siguiente para obtener referencia.

![](../images/models-recipes/package-source-files/import.png)

Se abre la página *Configurar* . Proporcione un nombre **de** fórmula adecuado, por ejemplo, &quot;Fórmula de ventas minoristas&quot;, y opcionalmente proporcione una dirección URL de documentación o descripción. Una vez completada, haga clic en **Siguiente**.

![](../images/models-recipes/package-source-files/configure.png)

Seleccione el *motor de ejecución* correspondiente y, a continuación, elija una **clasificación** para el *tipo*. Las credenciales del Registro de Contenedor de Azure se generan una vez finalizadas.

>[!NOTE]
>*El tipo *es la clase de problema de aprendizaje automático para el que está diseñada la fórmula y se utiliza después de la formación para ayudar a adaptar la ejecución de la formación.

>[!TIP]
>- Para las fórmulas de Python, seleccione el tiempo de ejecución de **Python** .
>- Para las fórmulas R, seleccione el tiempo de ejecución de **R** .
>- Para las fórmulas de PySpark, seleccione el tiempo de ejecución de **PySpark** . Se rellena automáticamente un tipo de artefacto.
>- Para las fórmulas de escala, seleccione el tiempo de ejecución de **Spark** . Se rellena automáticamente un tipo de artefacto.


![](../images/models-recipes/package-source-files/docker-creds.png)

Tenga en cuenta los valores de Host *de* Docker, *Nombre de usuario* y *Contraseña*. Estos se utilizan para crear e insertar la imagen del Docker en los flujos de trabajo que se describen a continuación.

>[!NOTE]
>La dirección URL de origen se proporciona después de completar los pasos que se describen a continuación. El archivo de configuración se explica en tutoriales posteriores que se encuentran en los [próximos pasos](#next-steps).

### Empaquetar los archivos de origen

Inicio mediante la obtención del código base de muestra que se encuentra en el repositorio de referencia <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">de</a> Experience Platform Data Science Workspace.

- [Generar imagen de acoplamiento Python](#python-docker)
- [Generar imagen de acoplamiento R](#r-docker)
- [Generar imagen de acoplador de PySpark](#pyspark-docker)
- [Generar imagen de acoplador Scala (Spark)](#scala-docker)

### Generar imagen de acoplamiento Python {#python-docker}

Si no lo ha hecho, clona el repositorio github en su sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Aquí encontrará los scripts `login.sh` y `build.sh` se utiliza para iniciar sesión en Docker y crear la imagen de python Docker. Si tiene las credenciales [de](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que, al ejecutar la secuencia de comandos de inicio de sesión, debe proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

### Generar imagen de acoplamiento R {#r-docker}

Si no lo ha hecho, clona el repositorio github en su sistema local con el siguiente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue al directorio `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro del repositorio clonado. Aquí encontrará los archivos `login.sh` y `build.sh` que utilizará para iniciar sesión en Docker y crear la imagen del R Docker. Si tiene las credenciales [de](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Tenga en cuenta que, al ejecutar la secuencia de comandos de inicio de sesión, debe proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

### Generar imagen de acoplador de PySpark {#pyspark-docker}

Inicio clonando el repositorio github en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Las secuencias de comandos `login.sh` y `build.sh` se encuentran aquí y se utilizan para iniciar sesión en el Docker y crear la imagen del Docker. Si tiene las credenciales [de](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que, al ejecutar la secuencia de comandos de inicio de sesión, debe proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

### Generar imagen de acoplador escalofriante {#scala-docker}

Inicio clonando el repositorio github en su sistema local con el siguiente comando en terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

A continuación, vaya al directorio `experience-platform-dsw-reference/recipes/scala/retail` donde puede encontrar las secuencias de comandos `login.sh` y `build.sh`. Estas secuencias de comandos se utilizan para iniciar sesión en Docker y crear la imagen del Docker. Si tiene las credenciales [del](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en terminal en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Al ejecutar la secuencia de comandos de inicio de sesión, debe proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

## Pasos siguientes {#next-steps}

Este tutorial pasó a empaquetar archivos de origen en una fórmula, el paso previo para importar una fórmula en el área de trabajo de ciencia de datos. Ahora debe tener una imagen de Docker en el Registro de Contenedor de Azure junto con la URL de imagen correspondiente. Ya está listo para iniciar el tutorial sobre la **importación de una fórmula empaquetada en Data Science Workspace**. Seleccione uno de los vínculos de tutorial siguientes para empezar.

- [Importación de una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md)
- [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)

## Creación de binarios (desaprobada)

>[!CAUTION]
> Los binarios no son compatibles con las nuevas fórmulas de PySpark y Scala y se van a eliminar en una versión futura. Siga los flujos de trabajo [de](#docker-based-model-authoring) Docker cuando trabaje con PySpark y Scala. Los siguientes flujos de trabajo solo son aplicables a las fórmulas de Spark 2.3.

### Generar binarios de PySpark (desaprobado)

Si no lo ha hecho, clona el repositorio github en su sistema local con el siguiente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue hasta el repositorio clonado en su sistema local y ejecute los siguientes comandos para generar el archivo requerido `.egg` para importar una fórmula PySpark:

```BASH
cd recipes/pyspark
./build.sh
```

El `.egg` archivo se genera en la `dist` carpeta.

Ahora puede pasar a los [siguientes pasos](#next-steps).

#### Generar binarios Scala (desaprobado)

Si aún no lo ha hecho, ejecute el siguiente comando para clonar el repositorio de Github en su sistema local:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Para crear el `.jar` artefacto utilizado para importar una fórmula Scala, navegue hasta el repositorio clonado y siga los pasos a continuación:

```BASH
cd recipes/scala/
./build.sh
```

El `.jar` artefacto generado con dependencias se encuentra en el `/target` directorio.

Ahora puede pasar a los [siguientes pasos](#next-steps).