---
keywords: Experience Platform;archivos de origen de paquetes;Data Science Workspace;temas populares;Docker;imagen de docker
solution: Experience Platform
title: Empaquetar archivos de origen en una fórmula
topic-legacy: tutorial
type: Tutorial
description: Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo, que se puede utilizar para crear una fórmula en Adobe Experience Platform Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o utilizando la API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# Empaquete archivos de origen en una fórmula

Este tutorial proporciona instrucciones sobre cómo empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo, que se puede utilizar para crear una fórmula en Adobe Experience Platform [!DNL Data Science Workspace] siguiendo el flujo de trabajo de importación de fórmulas, ya sea en la interfaz de usuario o utilizando la API.

Conceptos para comprender:

- **Fórmulas**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, lógica de procesamiento y configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayuda a resolver problemas empresariales específicos.
- **Archivos** de origen: Archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creación de fórmula

La creación de fórmulas comienza con el empaquetado de archivos de origen para crear un archivo. Los archivos de origen definen la lógica y los algoritmos de aprendizaje automático utilizados para resolver un problema específico que se encuentra en la mano y están escritos en [!DNL Python], R, PySpark o Scala. Los archivos archivados creados toman la forma de una imagen Docker. Una vez creado, el archivo empaquetado se importa en [!DNL Data Science Workspace] para crear una fórmula [en la interfaz de usuario](./import-packaged-recipe-ui.md) o [utilizando la API](./import-packaged-recipe-api.md).

### Creación de modelos basados en Docker {#docker-based-model-authoring}

Una imagen Docker permite a un desarrollador empaquetar una aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y enviarla como un paquete.

La imagen Docker creada se inserta en el Registro de contenedores de Azure utilizando las credenciales proporcionadas durante el flujo de trabajo de creación de la fórmula.

Para obtener las credenciales del Registro de contenedores de Azure, inicie sesión en [Adobe Experience Platform](https://platform.adobe.com). En la columna de navegación izquierda, vaya a **[!UICONTROL Workflows]**. Seleccione **[!UICONTROL Import Recipe]** seguido de **[!UICONTROL Launch]**. Consulte la captura de pantalla siguiente para obtener referencia.

![](../images/models-recipes/package-source-files/import.png)

Se abre la página **[!UICONTROL Configure]**. Proporcione un **[!UICONTROL Recipe Name]** apropiado, por ejemplo, &quot;Receta de ventas minoristas&quot;, y opcionalmente proporcione una descripción o una dirección URL de documentación. Una vez finalizado, haga clic en **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleccione el *Runtime* correspondiente y, a continuación, elija **[!UICONTROL Classification]** para *Type*. Las credenciales del Registro de contenedores de Azure se generan una vez finalizadas.

>[!NOTE]
>
>** Escriba la clase de problema de aprendizaje automático para la que está diseñada la fórmula y se utiliza después de la formación para ayudar a adaptar la evaluación de la ejecución de la formación.

>[!TIP]
>
>- Para las fórmulas [!DNL Python] seleccione el tiempo de ejecución **[!UICONTROL Python]**.
>- Para las fórmulas R, seleccione el tiempo de ejecución **[!UICONTROL R]**.
>- Para las fórmulas de PySpark, seleccione el tiempo de ejecución **[!UICONTROL PySpark]**. Un tipo de artefacto se rellena automáticamente.
>- Para las fórmulas de Scala, seleccione el tiempo de ejecución **[!UICONTROL Spark]**. Un tipo de artefacto se rellena automáticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Tenga en cuenta los valores del host Docker, el nombre de usuario y la contraseña. Se utilizan para crear y insertar la imagen [!DNL Docker] en los flujos de trabajo descritos a continuación.

>[!NOTE]
>
>La dirección URL de origen se proporciona después de completar los pasos descritos a continuación. El archivo de configuración se explica en tutoriales posteriores que se encuentran en [pasos siguientes](#next-steps).

### Empaquete los archivos de origen

Comience por obtener el código de base de ejemplo que se encuentra en el repositorio <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>.

- [Generar imagen Python Docker](#python-docker)
- [Generar imagen R Docker](#r-docker)
- [Crear imagen de Docker de PySpark](#pyspark-docker)
- [Generar imagen de acoplador Scala (Spark)](#scala-docker)

### Generar [!DNL Python] Imagen de Docker {#python-docker}

Si no lo ha hecho, clone el repositorio [!DNL GitHub] en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/python/retail`. Aquí, encontrará las secuencias de comandos `login.sh` y `build.sh` utilizadas para iniciar sesión en Docker y crear la imagen [!DNL Python Docker]. Si tiene sus [Credenciales del Docker](#docker-based-model-authoring) listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, es necesario proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez finalizada la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

### Generar imagen R [!DNL Docker] {#r-docker}

Si no lo ha hecho, clone el repositorio [!DNL GitHub] en el sistema local con el siguiente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro del repositorio clonado. Aquí, encontrará los archivos `login.sh` y `build.sh` que utilizará para iniciar sesión en Docker y para crear la imagen de R Docker. Si tiene sus [Credenciales del Docker](#docker-based-model-authoring) listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, es necesario proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez finalizada la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

### Generar imagen de Docker de PySpark {#pyspark-docker}

Comience clonando el repositorio [!DNL GitHub] en su sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/pyspark/retail`. Los scripts `login.sh` y `build.sh` se encuentran aquí y se utilizan para iniciar sesión en Docker y para crear la imagen Docker. Si tiene sus [Credenciales del Docker](#docker-based-model-authoring) listas, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, es necesario proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez finalizada la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

### Generar imagen de Scala Docker {#scala-docker}

Comience clonando el repositorio [!DNL GitHub] en su sistema local con el siguiente comando en terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

A continuación, vaya al directorio `experience-platform-dsw-reference/recipes/scala` donde puede encontrar los scripts `login.sh` y `build.sh`. Estas secuencias de comandos se utilizan para iniciar sesión en Docker y crear la imagen Docker. Si tiene sus [Credenciales del Docker](#docker-based-model-authoring) listas, introduzca los siguientes comandos en terminal en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si está recibiendo un error de permiso al intentar iniciar sesión en Docker utilizando la secuencia de comandos `login.sh`, intente utilizar el comando `bash login.sh`.

Al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, es necesario proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez finalizada la secuencia de comandos de compilación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

## Pasos siguientes {#next-steps}

Este tutorial ha pasado el empaquetado de archivos de origen a una fórmula, el paso previo para importar una fórmula a [!DNL Data Science Workspace]. Ahora debe tener una imagen de Docker en el Registro de contenedores de Azure junto con la URL de la imagen correspondiente. Ya está listo para iniciar el tutorial sobre la importación de una fórmula empaquetada en [!DNL Data Science Workspace]. Seleccione uno de los vínculos del tutorial a continuación para empezar:

- [Importar una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md)
- [Importar una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)
