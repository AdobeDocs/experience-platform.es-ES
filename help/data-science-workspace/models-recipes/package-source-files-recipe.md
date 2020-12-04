---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics;Docker;docker image
solution: Experience Platform
title: Empaquetar archivos de origen en una fórmula
topic: tutorial
type: Tutorial
description: Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de archivo, que se puede utilizar para crear una fórmula en Adobe Experience Platform Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o mediante la API.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Empaquetar archivos de origen en una fórmula

Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de archivo, que se puede utilizar para crear una fórmula en Adobe Experience Platform [!DNL Data Science Workspace] siguiendo el flujo de trabajo de importación de fórmulas ya sea en la interfaz de usuario o mediante la API.

Conceptos para comprender:

- **Fórmulas**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarias para crear y ejecutar un modelo capacitado y, por lo tanto, ayuda a resolver problemas comerciales específicos.
- **Archivos** de origen: Archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos 

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creación de fórmulas

Inicios de creación de fórmulas con empaquetado de archivos de origen para crear un archivo de archivo. Los archivos de origen definen la lógica de aprendizaje automático y los algoritmos utilizados para resolver un problema específico que se encuentra en la mano, y se escriben en [!DNL Python], R, PySpark o Scala. Los archivos de archivo creados toman la forma de una imagen de Docker. Una vez creado, el archivo empaquetado se importa en [!DNL Data Science Workspace] para crear una fórmula [en la interfaz de usuario](./import-packaged-recipe-ui.md) o [mediante la API](./import-packaged-recipe-api.md).

### Creación de modelos basados en el acoplamiento {#docker-based-model-authoring}

Una imagen de Docker permite a un desarrollador empaquetar una aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y enviarla como un paquete.

La imagen de Docker creada se inserta en el Registro de Contenedor de Azure mediante las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

Para obtener las credenciales del Registro de Contenedor de Azure, inicie sesión en [Adobe Experience Platform](https://platform.adobe.com). En la columna de navegación izquierda, navegue a **[!UICONTROL Flujos de trabajo]**. Seleccione **[!UICONTROL Importar fórmula]** , luego seleccione **[!UICONTROL Iniciar]**. Consulte la captura de pantalla siguiente para obtener referencia.

![](../images/models-recipes/package-source-files/import.png)

Se abre la página **[!UICONTROL Configurar]** . Proporcione un nombre **[!UICONTROL de]** fórmula adecuado, por ejemplo, &quot;Fórmula de ventas minoristas&quot;, y opcionalmente proporcione una dirección URL de documentación o descripción. Una vez completada, haga clic en **[!UICONTROL Siguiente]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleccione el *motor de ejecución* correspondiente y, a continuación, elija una **[!UICONTROL clasificación]** para el *tipo*. Las credenciales del Registro de Contenedor de Azure se generan una vez finalizadas.

>[!NOTE]
>
>*El tipo* es la clase de problema de aprendizaje automático para el que está diseñada la fórmula y se utiliza después de la formación para ayudar a adaptar la ejecución de la formación.

>[!TIP]
>
>- Para [!DNL Python] las fórmulas, seleccione el tiempo de ejecución de **[!UICONTROL Python]** .
>- Para las fórmulas R, seleccione el tiempo de ejecución de **[!UICONTROL R]** .
>- Para las fórmulas de PySpark, seleccione el tiempo de ejecución de **[!UICONTROL PySpark]** . Se rellena automáticamente un tipo de artefacto.
>- Para las fórmulas de escala, seleccione el tiempo de ejecución de **[!UICONTROL Spark]** . Se rellena automáticamente un tipo de artefacto.


![](../images/models-recipes/package-source-files/docker-creds.png)

Tenga en cuenta los valores del host, el nombre de usuario y la contraseña del Docker. Se utilizan para generar e insertar la [!DNL Docker] imagen en los flujos de trabajo que se describen a continuación.

>[!NOTE]
>
>La dirección URL de origen se proporciona después de completar los pasos que se describen a continuación. El archivo de configuración se explica en tutoriales posteriores que se encuentran en los [próximos pasos](#next-steps).

### Empaquetar los archivos de origen

Inicio mediante la obtención del código base de muestra que se encuentra en el repositorio de referencia <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">de</a> Experience Platform Data Science Workspace.

- [Generar imagen de acoplamiento Python](#python-docker)
- [Generar imagen de acoplamiento R](#r-docker)
- [Generar imagen de acoplador de PySpark](#pyspark-docker)
- [Generar imagen de acoplador Scala (Spark)](#scala-docker)

### Generar [!DNL Python] imagen de acoplamiento {#python-docker}

Si no lo ha hecho, clona el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Aquí, encontrará los scripts `login.sh` y `build.sh` utilizados para iniciar sesión en Docker y para crear la [!DNL Python Docker] imagen. Si tiene las credenciales [de](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en orden:

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

### Generar [!DNL Docker] imagen R {#r-docker}

Si no lo ha hecho, clona el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

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

Inicio clonando el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

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

Inicio clonando el [!DNL GitHub] repositorio en el sistema local con el siguiente comando en terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

A continuación, vaya al directorio `experience-platform-dsw-reference/recipes/scala` donde puede encontrar las secuencias de comandos `login.sh` y `build.sh`. Estas secuencias de comandos se utilizan para iniciar sesión en Docker y crear la imagen del Docker. Si tiene las credenciales [del](#docker-based-model-authoring) Docker listas, introduzca los siguientes comandos en terminal en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si recibe un error de permiso al intentar iniciar sesión en Docker mediante la `login.sh` secuencia de comandos, intente utilizar el comando `bash login.sh`.

Al ejecutar la secuencia de comandos de inicio de sesión, debe proporcionar el host, el nombre de usuario y la contraseña del Docker. Al compilar, debe proporcionar el host de Docker y una etiqueta de versión para la compilación.

Una vez que se haya completado la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esta URL y continúe con los [siguientes pasos](#next-steps).

## Pasos siguientes {#next-steps}

Este tutorial pasó a empaquetar archivos de origen en una fórmula, el paso previo para importar una fórmula en [!DNL Data Science Workspace]. Ahora debe tener una imagen de Docker en el Registro de Contenedor de Azure junto con la URL de imagen correspondiente. Ya está listo para comenzar el tutorial sobre la importación de una fórmula empaquetada en [!DNL Data Science Workspace]. Seleccione uno de los vínculos de tutorial siguientes para comenzar:

- [Importación de una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md)
- [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)