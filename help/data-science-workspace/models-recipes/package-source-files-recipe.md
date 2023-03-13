---
keywords: Experience Platform;archivos de origen de paquetes;Data Science Workspace;temas populares;Docker;imagen docker
solution: Experience Platform
title: Empaquetar archivos de origen en una fórmula
type: Tutorial
description: Este tutorial proporciona instrucciones sobre cómo puede empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de almacenamiento, que se puede utilizar para crear una fórmula en Adobe Experience Platform Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o mediante la API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Empaquetar archivos de origen en una fórmula

Este tutorial proporciona instrucciones sobre cómo puede empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo, que se puede utilizar para crear una fórmula en Adobe Experience Platform [!DNL Data Science Workspace] siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o utilizando la API.

Conceptos para comprender:

- **Fórmulas**: una fórmula es el término que utiliza un Adobe para especificar un modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayudar a solucionar problemas empresariales específicos.
- **Archivos de origen**: archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creación de fórmula

La creación de la fórmula comienza con los archivos de origen de los paquetes para crear un archivo. Los archivos de origen definen la lógica de aprendizaje automático y los algoritmos utilizados para resolver un problema específico, y están escritos en [!DNL Python], R, PySpark o Scala. Los archivos de almacenamiento creados toman la forma de una imagen Docker. Una vez creado, el archivo empaquetado se importa en [!DNL Data Science Workspace] para crear una fórmula [en la IU de](./import-packaged-recipe-ui.md) o [uso de la API](./import-packaged-recipe-api.md).

### Creación de modelos basados en Docker {#docker-based-model-authoring}

Una imagen Docker permite a un desarrollador empaquetar una aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y distribuirla como un paquete.

La imagen Docker creada se inserta en el Registro de contenedores de Azure con las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

Para obtener sus credenciales de Azure Container Registry, inicie sesión en [Adobe Experience Platform](https://platform.adobe.com). En la columna de navegación de la izquierda, navegue hasta **[!UICONTROL Flujos de trabajo]**. Seleccionar **[!UICONTROL Importar fórmula]** seguido de una selección **[!UICONTROL Launch]**. Consulte la captura de pantalla siguiente como referencia.

![](../images/models-recipes/package-source-files/import.png)

El **[!UICONTROL Configurar]** se abre la página. Proporcione un **[!UICONTROL Nombre de fórmula]**, por ejemplo, &quot;Fórmula de ventas minoristas&quot; y, opcionalmente, proporcione una descripción o una URL de documentación. Una vez finalizado, haga clic en **[!UICONTROL Siguiente]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleccione el adecuado *Runtime* y, a continuación, elija una **[!UICONTROL Clasificación]** para *Tipo*. Las credenciales del Registro de contenedores de Azure se generan una vez completadas.

>[!NOTE]
>
>*Tipo* es la clase de problema de aprendizaje automático para el que está diseñada la fórmula y se utiliza después del aprendizaje para ayudar a adaptar la evaluación de la ejecución del aprendizaje.

>[!TIP]
>
>- Para [!DNL Python] recetas seleccione la **[!UICONTROL Python]** runtime.
>- Para recetas R, seleccione la **[!UICONTROL R]** runtime.
>- Para las recetas PySpark seleccione la **[!UICONTROL PySpark]** runtime. Se rellena automáticamente un tipo de artefacto.
>- Para recetas de Scala, seleccione la **[!UICONTROL Spark]** runtime. Se rellena automáticamente un tipo de artefacto.


![](../images/models-recipes/package-source-files/docker-creds.png)

Tenga en cuenta los valores de host, nombre de usuario y contraseña de Docker. Se utilizan para crear y publicar su [!DNL Docker] en los flujos de trabajo descritos a continuación.

>[!NOTE]
>
>La URL de origen se proporciona después de completar los pasos descritos a continuación. El archivo de configuración se explica en los tutoriales posteriores que se encuentran en [pasos siguientes](#next-steps).

### Empaquetar los archivos de origen

Comience obteniendo el código base de muestra que se encuentra en <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Referencia de Data Science Workspace de Experience Platform</a> repositorio.

- [Crear imagen de Python Docker](#python-docker)
- [Crear imagen de Docker R](#r-docker)
- [Crear imagen PySpark Docker](#pyspark-docker)
- [Crear imagen de Docker de Scala (Spark)](#scala-docker)

### Generar [!DNL Python] Imagen de Docker {#python-docker}

Si no lo ha hecho, clone el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/python/retail`. Aquí encontrará los scripts. `login.sh` y `build.sh` se utiliza para iniciar sesión en Docker y crear el [!DNL Python Docker] imagen. Si tiene su [Credenciales de Docker](#docker-based-model-authoring) listo, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, debe proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez completado el script de generación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esta dirección URL y continúe con la [pasos siguientes](#next-steps).

### Compilación R [!DNL Docker] imagen {#r-docker}

Si no lo ha hecho, clone el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro del repositorio clonado. Aquí, encontrará los archivos. `login.sh` y `build.sh` que utilizará para iniciar sesión en Docker y crear la imagen de R Docker. Si tiene su [Credenciales de Docker](#docker-based-model-authoring) listo, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, debe proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez completado el script de generación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esta dirección URL y continúe con la [pasos siguientes](#next-steps).

### Crear imagen PySpark Docker {#pyspark-docker}

Comience por clonar el [!DNL GitHub] repositorio en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/pyspark/retail`. Los scripts `login.sh` y `build.sh` se encuentran aquí y se utilizan para iniciar sesión en Docker y crear la imagen de Docker. Si tiene su [Credenciales de Docker](#docker-based-model-authoring) listo, introduzca los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, debe proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez completado el script de generación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie esta dirección URL y continúe con la [pasos siguientes](#next-steps).

### Crear imagen de Scala Docker {#scala-docker}

Comience por clonar el [!DNL GitHub] repositorio en el sistema local con el siguiente comando en terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

A continuación, vaya al directorio `experience-platform-dsw-reference/recipes/scala` donde puede encontrar los scripts `login.sh` y `build.sh`. Estos scripts se utilizan para iniciar sesión en Docker y crear la imagen de Docker. Si tiene su [Credenciales de Docker](#docker-based-model-authoring) listo, introduzca los siguientes comandos en el terminal en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si recibe un error de permiso al intentar iniciar sesión en Docker con el `login.sh` script, intente utilizar el comando `bash login.sh`.

Al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, debe proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez completado el script de generación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esta dirección URL y continúe con la [pasos siguientes](#next-steps).

## Pasos siguientes {#next-steps}

Este tutorial trata sobre el empaquetado de archivos de origen en una fórmula, el paso previo para importar una fórmula en [!DNL Data Science Workspace]. Ahora debe tener una imagen Docker en el Registro de contenedores de Azure junto con la URL de imagen correspondiente. Ya está listo para comenzar el tutorial sobre la importación de una fórmula empaquetada en [!DNL Data Science Workspace]. Seleccione uno de los siguientes vínculos para empezar:

- [Importación de una fórmula empaquetada en la IU](./import-packaged-recipe-ui.md)
- [Importación de una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)
