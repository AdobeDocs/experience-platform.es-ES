---
keywords: Experience Platform;archivos de origen de paquetes;Data Science Workspace;temas populares;Docker;imagen docker
solution: Experience Platform
title: Empaquetar archivos de Source en una fórmula
type: Tutorial
description: Este tutorial proporciona instrucciones sobre cómo puede empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de almacenamiento, que se puede utilizar para crear una fórmula en Adobe Experience Platform Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas en la interfaz de usuario o mediante la API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Empaqueta archivos de origen en una fórmula

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

Este tutorial proporciona instrucciones sobre cómo puede empaquetar los archivos de origen de muestra de ventas minoristas proporcionados en un archivo de almacenamiento, que se puede usar para crear un fórmula en Adobe Experience Platform [!DNL Data Science Workspace] siguiendo el flujo de trabajo de importación de fórmula en el IU o mediante la API.

Conceptos a entender:

- **Fórmulas**: una fórmula es el término de un Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de inteligencia artificial o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarios para generar y ejecutar un modelo entrenado y, por lo tanto, ayudar a solucionar problemas empresariales específicos.
- **Archivos de Source**: Archivos individuales del proyecto que contienen la lógica de una fórmula.

## Requisitos previos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creación de fórmula

La creación de la fórmula comienza con los archivos de origen de los paquetes para crear un archivo. Los archivos de Source definen la lógica de aprendizaje automático y los algoritmos utilizados para solucionar un problema específico, y están escritos en [!DNL Python], R, PySpark o Scala. Los archivos de almacenamiento creados toman la forma de una imagen Docker. Una vez generado, el archivo de almacenamiento empaquetado se importa a [!DNL Data Science Workspace] para crear un fórmula [en el IU](./import-packaged-recipe-ui.md) o [utilizando la API](./import-packaged-recipe-api.md).

### Creación de modelos basada en Docker {#docker-based-model-authoring}

Una imagen de Docker permite a un desarrollador empaquetar un aplicación con todas las partes que necesita, como bibliotecas y otras dependencias, y enviarlo como un solo paquete.

La imagen Docker creada se inserta en el Registro de contenedores de Azure con las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

Para obtener sus credenciales de Azure Container Registry, inicie sesión en [Adobe Experience Platform](https://platform.adobe.com). En la columna de navegación de la izquierda, navegue hasta **[!UICONTROL Flujos de trabajo]**. Seleccione **[!UICONTROL Importar fórmula]** seguido de **[!UICONTROL Iniciar]**. Consulte la captura de pantalla siguiente como referencia.

![](../images/models-recipes/package-source-files/import.png)

Se abre la página **[!UICONTROL Configurar]**. Proporcione un **[!UICONTROL Nombre de fórmula]** apropiado, por ejemplo, &quot;Fórmula de ventas minoristas&quot;, y opcionalmente proporcione una descripción o una URL de documentación. Una vez finalizado, haga clic en **[!UICONTROL Siguiente]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleccione el *Runtime* adecuado y, a continuación, elija una **[!UICONTROL clasificación]** para *Type*. Las credenciales del Registro de contenedores de Azure se generan una vez completadas.

>[!NOTE]
>
>*Tipo* es la clase de problema de aprendizaje automático para el que está diseñada la fórmula y se utiliza después del aprendizaje para ayudar a adaptar la evaluación de la ejecución del aprendizaje.

>[!TIP]
>
>- Para [!DNL Python] recetas, selecciona el tiempo de ejecución de **[!UICONTROL Python]**.
>- Para las recetas R, seleccione el tiempo de ejecución **[!UICONTROL R]**.
>- Para las recetas de PySpark, selecciona el tiempo de ejecución de **[!UICONTROL PySpark]**. Se rellena automáticamente un tipo de artefacto.
>- Para las recetas de Scala, seleccione el tiempo de ejecución de **[!UICONTROL Spark]** . Se rellena automáticamente un tipo de artefacto.

![](../images/models-recipes/package-source-files/docker-creds.png)

Tenga en cuenta los valores de host, nombre de usuario y contraseña de Docker. Se utilizan para generar e insertar la imagen [!DNL Docker] en los flujos de trabajo descritos a continuación.

>[!NOTE]
>
>La dirección URL de Source se proporciona después de completar los pasos descritos a continuación. El archivo de configuración se explica en los tutoriales subsiguientes que se encuentran en [pasos siguientes](#next-steps).

### Empaquetar los archivos de origen

Inicio obteniendo el código de base de ejemplo que se encuentra en la repositorio de referencia de Espacio de trabajo de ciencia</a> de <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">datos de Experience Platform.

- [Crear imagen de Docker de Python](#python-docker)
- [Generar imagen de Docker de R](#r-docker)
- [Crear imagen de Docker de PySpark](#pyspark-docker)
- [Crear imagen de Docker de Scala (Spark)](#scala-docker)

### Generar imagen de Docker [!DNL Python] {#python-docker}

Si no lo ha hecho, clone el repositorio [!DNL GitHub] en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/python/retail`. Aquí encontrará los scripts `login.sh` y `build.sh` utilizados para iniciar sesión en Docker y crear la imagen [!DNL Python Docker]. Si tiene sus [credenciales de Docker](#docker-based-model-authoring) listas, escriba los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al compilar, debe proporcionar el host de Docker y un etiqueta de versión para el versión.

Una vez finalizado el script de versión, se le asigna un URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

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

Vaya al directorio `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro del repositorio clonado. Aquí encontrará los archivos `login.sh` y `build.sh` que utilizará para iniciar sesión en Docker y crear la imagen de R Docker. Si tiene sus [credenciales de Docker](#docker-based-model-authoring) listas, escriba los siguientes comandos en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Tenga en cuenta que al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al compilar, debe proporcionar el host de Docker y un etiqueta de versión para el versión.

Una vez finalizado el script de versión, se le asigna un URL de archivo de origen de Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto gustar:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

### Crear imagen PySpark Docker {#pyspark-docker}

Comience por clonar el repositorio [!DNL GitHub] en el sistema local con el siguiente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Vaya al directorio `experience-platform-dsw-reference/recipes/pyspark/retail`. Los scripts `login.sh` y `build.sh` se encuentran aquí y se utilizan para iniciar sesión en Docker y crear la imagen de Docker. Si tiene sus [credenciales de Docker](#docker-based-model-authoring) listas, escriba los siguientes comandos en orden:

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

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

### Crear imagen de Scala Docker {#scala-docker}

Comience por clonar el repositorio [!DNL GitHub] en el sistema local con el siguiente comando en el terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Siguiente, desplácese hasta el directorio `experience-platform-dsw-reference/recipes/scala` donde encontrará los scripts `login.sh` y `build.sh`. Estos scripts se utilizan para inicio de sesión a Docker y versión la imagen de Docker. Si tiene sus [credenciales](#docker-based-model-authoring) de Docker listas, ingrese los siguientes comandos al terminal en orden:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si recibe un error de permiso al intentar iniciar sesión en Docker con el script `login.sh`, intente usar el comando `bash login.sh`.

Al ejecutar el script de inicio de sesión, debe proporcionar el host Docker, el nombre de usuario y la contraseña. Al crear, debe proporcionar el host Docker y una etiqueta de versión para la compilación.

Una vez completado el script de generación, se le proporcionará una URL de archivo de origen Docker en la salida de la consola. Para este ejemplo específico, tendrá un aspecto similar al siguiente:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esta dirección URL y continúe con los [pasos siguientes](#next-steps).

## Pasos siguientes {#next-steps}

Este tutorial analizó el empaquetado de archivos de origen en una fórmula, el paso previo para importar una fórmula en [!DNL Data Science Workspace]. Ahora debe tener una imagen de Docker en Azure Container Registry junto con el URL de imagen correspondiente. Ya está listo para comenzar la tutorial de importación de un fórmula empaquetado en [!DNL Data Science Workspace]. Seleccione uno de los siguientes vínculos de tutorial para comenzar:

- [Importar una receta empaquetada en el IU](./import-packaged-recipe-ui.md)
- [Importación de una fórmula empaquetada mediante la API](./import-packaged-recipe-api.md)
