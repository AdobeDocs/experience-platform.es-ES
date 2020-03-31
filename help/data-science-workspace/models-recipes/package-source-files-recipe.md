---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Empaquetar archivos de origen en una fórmula
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Empaquetar archivos de origen en una fórmula

Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de archivo, que se puede utilizar para crear una fórmula en el espacio de trabajo de ciencia de datos de la plataforma de experiencia de Adobe siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o mediante la API.

Conceptos para comprender:

- **Fórmulas**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, la lógica de procesamiento y la configuración necesarios para crear y ejecutar un modelo capacitado y, por tanto, ayuda a resolver problemas comerciales específicos.
- **Archivos** de origen: Archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos

- <a href="https://docs.docker.com/install/#supported-platforms" target="_blank">Acoplador</a>
- <a href="https://docs.conda.io/en/latest/miniconda.html" target="_blank">Python 3 y pip</a>
- <a href="https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883" target="_blank">Scala</a>
- <a href="https://maven.apache.org/install.html" target="_blank">Maven</a>

## Creación de fórmulas

inicios de creación de fórmulas con empaquetado de archivos de origen para crear un archivo de archivo. Los archivos de origen definen la lógica de aprendizaje automático y los algoritmos utilizados para resolver un problema específico que se encuentra en la mano, y se escriben en Python, R, PySpark o Scala Spark. Según el idioma en que se escriban los archivos de origen, los archivos de archivo creados serán una imagen de Docker o un archivo binario. Una vez creado, el archivo empaquetado se importa en el área de trabajo de ciencias de datos para crear una fórmula [en la interfaz de usuario](./import-packaged-recipe-ui.md) o [mediante la API](./import-packaged-recipe-api.md).

### Creación de modelos basados en el acoplamiento

Una imagen de Docker permite a un desarrollador empaquetar una aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y enviarla como un paquete.

La imagen de Docker creada se insertará en el Registro de Contenedor de Azure mediante las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

>[!NOTE] Solo los archivos de origen escritos en **Python**, **R** y **Tensorflow** requieren las credenciales del Registro de Contenedor de Azure.

Para obtener las credenciales de Azure Contenedor Registry, inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>. En la columna de navegación izquierda, navegue a **Flujos de trabajo**. Seleccione **Importar fórmula desde archivo** de origen e **inicie** un nuevo procedimiento de importación. Consulte la captura de pantalla siguiente para obtener referencia.

![](../images/models-recipes/package-source-files/workflow_ss.png)

Proporcione un nombre **de** fórmula adecuado, por ejemplo, &quot;Fórmula de ventas minoristas&quot;, y opcionalmente proporcione una dirección URL de documentación o descripción. Una vez completada, haga clic en **Siguiente**.

![](../images/models-recipes/package-source-files/recipe_info.png)

Seleccione el **motor de ejecución** correspondiente y, a continuación, elija **Clasificación** para el **tipo**. Se generarán las credenciales del Registro de Contenedor de Azure.

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

Tenga en cuenta los valores de Host **de** Docker, **Nombre de usuario** y **Contraseña**. Estos se utilizarán más adelante para crear y insertar la imagen del Docker.

Una vez insertada, usted y otros usuarios pueden acceder a la imagen a través de la dirección URL. El campo Archivo **** de origen espera esta dirección URL como entrada.

### Creación de modelos binarios

Para los archivos de origen escritos en Scala o PySpark, se generará un archivo binario. La creación del archivo binario es tan sencilla como la ejecución del script de compilación proporcionado.
>[!NOTE] Solo los archivos de origen escritos en ScalaSpark o PySpark generarán un archivo binario al ejecutar el script de compilación.

### Empaquetar los archivos de origen

Inicio mediante la obtención del código base de muestra que se encuentra en el repositorio de referencia <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">de</a> Experience Platform Data Science Workspace. Dependiendo del lenguaje de programación en el que se escriban los archivos de origen de ejemplo, la creación de sus respectivos archivos de archivo varía según el procedimiento.

- [Generar imagen de acoplamiento Python](#build-python-docker-image)
- [Generar imagen de acoplamiento R](#build-r-docker-image)
- [Generar binarios de PySpark](#build-pyspark-binaries)
- [Generar binarios Scala](#build-scala-binaries)

#### Generar imagen de acoplamiento Python

Si no lo ha hecho, clona el repositorio github en su sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Aquí encontrará las secuencias de comandos `login.sh` y `build.sh` que utilizará para iniciar sesión en Docker y crear la imagen de python Docker. Si tiene las credenciales [de](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar la secuencia de comandos de inicio de sesión, deberá proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

#### Generar imagen de acoplamiento R

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

Tenga en cuenta que al ejecutar la secuencia de comandos de inicio de sesión, deberá proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

#### Generar binarios de PySpark

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

#### Generar binarios Scala

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

## Pasos siguientes

Este tutorial pasó a empaquetar archivos de origen en una fórmula, el paso previo para importar una fórmula en el área de trabajo de ciencia de datos. Ahora debe tener una imagen de Docker en el Registro de Contenedor de Azure junto con la URL de la imagen correspondiente o un archivo binario almacenado localmente en el sistema de archivos. Ya está listo para iniciar el tutorial sobre la **importación de una fórmula empaquetada en Data Science Workspace**. Seleccione uno de los vínculos de tutorial siguientes para empezar.

- [Importación de una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md)
- [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)