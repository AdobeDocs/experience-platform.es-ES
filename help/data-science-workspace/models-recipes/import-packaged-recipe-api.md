---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importación de una fórmula empaquetada (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# Importación de una fórmula empaquetada (API)

Este tutorial utiliza la API [de aprendizaje automático](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei para crear un [motor](../api/engines.md), también conocido como una fórmula en la interfaz de usuario.

Antes de comenzar, es importante tener en cuenta que Adobe Experience Platform Data Science Workspace utiliza términos diferentes para hacer referencia a elementos similares dentro de la API y la interfaz de usuario. Los términos de API se utilizan en este tutorial y la siguiente tabla describe los términos correlativos:

| Término de interfaz de usuario | Término de API |
| ---- | ---- |
| Fórmula | [Motor](../api/engines.md) |
| Modelo | [MLInance](../api/mlinstances.md) |
| Formación y evaluación | [Experimento](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Un motor contiene algoritmos de aprendizaje automático y lógica para resolver problemas específicos. En el diagrama siguiente se muestra una visualización del flujo de trabajo de la API en el área de trabajo de ciencias de datos. Este tutorial se centra en la creación de un motor, el cerebro de un modelo de aprendizaje automático.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Primeros pasos

Este tutorial requiere un archivo de fórmula empaquetado en forma de artefacto binario o de URL de Docker. Siga los archivos de origen del [paquete en un tutorial de fórmula](./package-source-files-recipe.md) para crear un archivo de fórmula empaquetado o proporcionar el suyo propio.

- Objeto binario: El artefacto binario (p. ej. JAR, EGG) utilizado para crear un motor.
- `{DOCKER_URL}` :: Dirección URL de una imagen de Docker de un servicio inteligente.

Este tutorial requiere que haya completado el tutorial [](../../tutorials/authentication.md) Autenticación a la plataforma de Adobe Experience para realizar correctamente llamadas a las API de plataforma. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- `{ACCESS_TOKEN}`:: Su valor de token de portador específico proporcionado después de la autenticación.
- `{IMS_ORG}`:: Sus credenciales de organización de IMS se encuentran en su integración única de Adobe Experience Platform.
- `{API_KEY}`:: Su valor clave de API específica se encuentra en su integración única de Adobe Experience Platform.

## Crear un motor

Según la forma del archivo de fórmula empaquetado que se incluirá como parte de la solicitud de API, se crea un motor de dos formas:
- [Crear un motor con un artefacto binario](#create-an-engine-with-a-binary-artifact)
- [Creación de un motor con una URL de acoplamiento](#create-an-engine-with-a-docker-url)

### Crear un motor con un artefacto binario

Para crear un motor con un artefacto empaquetado `.jar` o `.egg` binario local, debe proporcionar la ruta absoluta al archivo de artefacto binario en el sistema de archivos local. Considere desplazarse al directorio que contiene el artefacto binario en un entorno Terminal y ejecutar el comando `pwd` Unix para la ruta absoluta.

La siguiente llamada crea un motor con un artefacto binario:

#### Formato de API

```http
POST /engines
```

#### Solicitud

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` :: Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor que se mostrará en la interfaz de usuario de Área de trabajo de ciencia de datos como nombre de la fórmula.
- `engine > description` :: Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor que se mostrará en la interfaz de usuario de Área de trabajo de ciencia de datos como la descripción de la fórmula. No elimine esta propiedad, deje que este valor sea una cadena vacía si decide no proporcionar una descripción.
- `engine > type`:: El tipo de ejecución del motor. Este valor corresponde al lenguaje en el que se desarrolló el artefacto binario.

   >[!NOTE] Al cargar un artefacto binario para crear un motor, `type` es `Spark` o `PySpark`.

- `defaultArtifact` :: Ruta absoluta al archivo de artefacto binario utilizado para crear el motor.

   >[!NOTE] Asegúrese de incluir `@` antes de la ruta del archivo.

#### Respuesta

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

Una respuesta correcta muestra una carga útil JSON con información acerca del motor recién creado. La `id` clave representa el identificador único del motor y es necesaria en el siguiente tutorial para crear una instancia MLI. Asegúrese de guardar el identificador del motor antes de continuar con los [siguientes pasos](#next-steps).

### Creación de un motor con una URL de acoplamiento

Para crear un motor con un archivo de fórmula empaquetado almacenado en un contenedor de Docker, debe proporcionar la URL de Docker al archivo de fórmula empaquetado.

La siguiente llamada crea un motor con una URL de acoplamiento:

#### Formato de API

```http
POST /engines
```

#### Solicitud

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

- `engine > name` :: Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor que se mostrará en la interfaz de usuario de Área de trabajo de ciencia de datos como nombre de la fórmula.
- `engine > description` :: Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor que se mostrará en la interfaz de usuario de Área de trabajo de ciencia de datos como la descripción de la fórmula. No elimine esta propiedad, deje que este valor sea una cadena vacía si decide no proporcionar una descripción.
- `engine > type`:: El tipo de ejecución del motor. Este valor corresponde al idioma en el que se desarrolla la imagen del Docker.

   >[!NOTE] Cuando se proporciona una URL de Docker para crear un motor, `type` es `Python`, `R`o `Tensorflow`.

- `artifacts > default > image > location` :: Tu `{DOCKER_URL}` va aquí. Una URL completa del Docker tiene la siguiente estructura:

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` :: Un nombre adicional para el archivo de imagen del Docker. No elimine esta propiedad, deje que este valor sea una cadena vacía si decide no proporcionar un nombre de archivo de imagen de Docker adicional.
- `artifacts > default > image > executionType` :: El tipo de ejecución de este motor. Este valor corresponde al idioma en el que se desarrolla la imagen del Docker.

   >[!NOTE] Cuando se proporciona una URL de Docker para crear un motor, `executionType` es `Python`, `R`o `Tensorflow`.

#### Respuesta

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Una respuesta correcta muestra una carga útil JSON con información acerca del motor recién creado. La `id` clave representa el identificador único del motor y es necesaria en el siguiente tutorial para crear una instancia MLI. Asegúrese de guardar el identificador del motor antes de continuar con los pasos siguientes.

## Pasos siguientes

Ha creado un motor con la API y se obtuvo un identificador de motor único como parte del cuerpo de respuesta. Puede utilizar este identificador de motor en el siguiente tutorial a medida que aprenda a [crear, entrenar y evaluar un modelo con la API](./train-evaluate-model-api.md).