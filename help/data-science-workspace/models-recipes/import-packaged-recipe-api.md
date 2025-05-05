---
keywords: Experience Platform;importar fórmula empaquetada;Data Science Workspace;temas populares;recetas;api;aprendizaje automático de sensei;crear motor
solution: Experience Platform
title: Importar una fórmula empaquetada mediante la API de aprendizaje automático de Sensei
type: Tutorial
description: Este tutorial utiliza la API de aprendizaje automático de Sensei para crear un motor, también conocido como Fórmula en la interfaz de usuario.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 3%

---

# Importar una fórmula empaquetada mediante la API de aprendizaje automático de Sensei

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Este tutorial usa [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) para crear un [Motor](../api/engines.md), también conocido como una fórmula en la interfaz de usuario.

Antes de comenzar, es importante tener en cuenta que Adobe Experience Platform [!DNL Data Science Workspace] utiliza términos diferentes para hacer referencia a elementos similares dentro de la API y la interfaz de usuario. Los términos de la API se utilizan en este tutorial y la siguiente tabla describe los términos correlacionados:

| Término IU | Término de API |
| ---- | ---- |
| Fórmula | [Motor](../api/engines.md) |
| Modelo | [MLInstance](../api/mlinstances.md) |
| Capacitación y evaluación | [Experimento](../api/experiments.md) |
| Servicio | [MLService](../api/mlservices.md) |

Un motor contiene algoritmos de aprendizaje automático y lógica para resolver problemas específicos. El diagrama siguiente proporciona una visualización que muestra el flujo de trabajo de la API en [!DNL Data Science Workspace]. Este tutorial se centra en la creación de un motor, el cerebro de un modelo de aprendizaje automático.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introducción

Este tutorial requiere un archivo de fórmula empaquetado en forma de URL de Docker. Siga el tutorial de [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) para crear un archivo de fórmula empaquetado o proporcione el suyo propio.

- `{DOCKER_URL}`: una dirección URL a una imagen Docker de un servicio inteligente.

Este tutorial requiere que haya completado el tutorial [Autenticación en Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a las API [!DNL Experience Platform]. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- `{ACCESS_TOKEN}`: valor de token de portador específico proporcionado después de la autenticación.
- `{ORG_ID}`: las credenciales de su organización se encontraron en su integración de Adobe Experience Platform única.
- `{API_KEY}`: se encontró el valor de clave de API específico en la integración de Adobe Experience Platform única.

## Crear un motor

Los motores se pueden crear realizando una petición POST al extremo /engines. El motor creado se configura según el formulario del archivo de recetas empaquetado que debe incluirse como parte del solicitud API.

### Crear un motor con un Docker URL {#create-an-engine-with-a-docker-url}

Para crear un motor con un archivo de fórmula empaquetado almacenado en un contenedor de Docker, debe proporcionar la URL de Docker al archivo de fórmula empaquetado.

>[!CAUTION]
>
> Si está usando [!DNL Python] o R, utilice la solicitud siguiente. Si utiliza PySpark o Scala, utilice el ejemplo de solicitud PySpark/Scala situado debajo del ejemplo Python/R.

**Formato de API**

```http
POST /engines
```

**Solicitar Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
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

| Propiedad | Descripción |
| -------  | ----------- |
| `engine.name` | El nombre deseado para el motor. La Fórmula correspondiente a este Motor heredará este valor para ser mostrada en [!DNL Data Science Workspace] usuario interfaz como el nombre de la Fórmula. |
| `engine.description` | Una descripción opcional del motor. La Fórmula correspondiente a este Motor heredará este valor para ser mostrada en [!DNL Data Science Workspace] usuario interfaz como descripción de la Fórmula. No elimine esta propiedad, deje que este valor sea una cadena vacía si decide no proporcionar una descripción. |
| `engine.type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se desarrolla la imagen Docker. Cuando se proporciona una URL de Docker para crear un motor, `type` es `Python`, `R`, `PySpark`, `Spark` (Scala) o `Tensorflow`. |
| `artifacts.default.image.location` | Su `{DOCKER_URL}` se va aquí. Una dirección URL de Docker completa tiene la siguiente estructura: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Un nombre adicional para el archivo de imagen Docker. No elimine esta propiedad, deje que este valor sea una cadena vacía si decide no proporcionar un nombre de archivo de imagen Docker adicional. |
| `artifacts.default.image.executionType` | Tipo de ejecución de este motor. Este valor corresponde al idioma en el que se desarrolla la imagen de Docker. Cuando se proporciona un URL de Docker para crear un motor, `executionType` es , `Python` `R`, `PySpark`, `Spark` (Scala) o `Tensorflow`. |

**Solicitar PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para mostrarlo en la interfaz de usuario como el nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La Fórmula correspondiente a este Motor heredará este valor para ser mostrada en IU como la descripción de la Fórmula. Esta Propiedad es obligatoria. Si no desea proporcionar una descripción, defina su valor para que sea una cadena vacía. |
| `type` | Tipo de ejecución del motor. Este valor corresponde al idioma en el que la imagen de Docker se basa en &quot;PySpark&quot;. |
| `mlLibrary` | Campo obligatorio al crear motores para las recetas PySpark y Scala. |
| `artifacts.default.image.location` | La ubicación de la imagen de Docker a la que está vinculado una URL de Docker. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen Docker sobre &quot;Spark&quot;. |

**Solicitar Scala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para mostrarlo en la interfaz de usuario como el nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para mostrarlo en la interfaz de usuario como la descripción de la fórmula. Esta propiedad es obligatoria. Si no desea proporcionar una descripción, establezca su valor como una cadena vacía. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que la imagen de Docker se basa en &quot;Spark&quot;. |
| `mlLibrary` | Campo necesario al crear motores para recetas de PySpark y Scala. |
| `artifacts.default.image.location` | La ubicación de la imagen de Docker a la que está vinculado una URL de Docker. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen Docker sobre &quot;Spark&quot;. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor [!DNL Python]. Las claves `executionType` y `type` cambian según el POST proporcionado.

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Una respuesta correcta muestra una carga útil JSON con información sobre el motor recién creado. La `id` clave representa el identificador de motor único y se requiere en los tutorial siguientes para crear una MLInstance. Asegúrese de guardar el identificador del motor antes de continuar con los siguientes pasos.

## Pasos siguientes {#next-steps}

Ha creado un motor utilizando la API y se ha obtenido un identificador de motor único como parte del cuerpo de la respuesta. Puede usar este identificador de motor en el siguiente tutorial mientras aprende a [crear, entrenar y evaluar un modelo mediante la API](./train-evaluate-model-api.md).
