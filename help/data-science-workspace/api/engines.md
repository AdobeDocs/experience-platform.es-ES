---
keywords: Experience Platform;guía para desarrolladores;punto final;Área de trabajo de ciencias de datos;temas populares;motores;API de aprendizaje del equipo sensei
solution: Experience Platform
title: Extremo de API de motores
topic: Developer guide
description: Los motores son la base de los modelos de aprendizaje automático en el área de trabajo de ciencias de datos. Contienen algoritmos de aprendizaje automático que resuelven problemas específicos, conductos de funciones para realizar ingeniería de funciones o ambos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---


# Extremo de motores

Los motores son la base de los modelos de aprendizaje automático en el área de trabajo de ciencias de datos. Contienen algoritmos de aprendizaje automático que resuelven problemas específicos, conductos de funciones para realizar ingeniería de funciones o ambos.

## Buscar el registro del Docker

>[!TIP]
>
>Si no tiene una URL de Docker, visite el tutorial [Empaquetar archivos de origen en una fórmula](../models-recipes/package-source-files-recipe.md) para obtener un tutorial paso a paso sobre la creación de una URL de host de Docker.

Se requieren las credenciales del Registro de Docker para cargar un archivo de fórmula empaquetado, incluyendo la dirección URL del host de Docker, el nombre de usuario y la contraseña. Puede buscar esta información realizando la siguiente solicitud de GET:

**Formato de API**

```https
GET /engines/dockerRegistry
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del registro del Docker, incluyendo la URL del Docker (`host`), el nombre de usuario (`username`) y la contraseña (`password`).

>[!NOTE]
>
>La contraseña del Docker cambia cada vez que se actualiza su `{ACCESS_TOKEN}`.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Crear un motor con direcciones URL de Docker {#docker-image}

Puede crear un motor realizando una solicitud de POST mientras proporciona sus metadatos y una URL de Docker que haga referencia a una imagen de Docker en formularios de varias partes.

**Formato de API**

```https
POST /engines
```

**Solicitar Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como la descripción de la fórmula. Esta es una propiedad obligatoria. Si no desea proporcionar una descripción, establezca su valor en una cadena vacía. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker y puede ser &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |
| `algorithm` | Una cadena que especifica el tipo de algoritmo de aprendizaje automático. Los tipos de algoritmo admitidos son &quot;Clasificación&quot;, &quot;Regresión&quot; o &quot;Personalizado&quot;. |
| `artifacts.default.image.location` | Ubicación de la imagen del Docker vinculada por una URL del Docker. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker y puede ser &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |

**Solicitar PySpark/Scala**

Cuando se realiza una solicitud para las fórmulas de PySpark, `executionType` y `type` es &quot;PySpark&quot;. Cuando se realiza una solicitud para las fórmulas de Scala, `executionType` y `type` es &quot;Spark&quot;. En el siguiente ejemplo de fórmula Scala se utiliza Spark:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como la descripción de la fórmula. Esta es una propiedad obligatoria. Si no desea proporcionar una descripción, establezca su valor en una cadena vacía. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker. El valor se puede establecer en Spark o PySpark. |
| `mlLibrary` | Campo que se requiere al crear motores para las fórmulas de PySpark y Scala. Este campo debe establecerse en `databricks-spark`. |
| `artifacts.default.image.location` | Ubicación de la imagen del Docker. Solo se admite Azure ACR o Public (no autenticado) Dockerhub. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker. Puede ser &quot;Spark&quot; o &quot;PySpark&quot;. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor Python. Todas las respuestas del motor siguen este formato:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Crear un motor de canalización de funciones mediante direcciones URL de acoplamiento {#feature-pipeline-docker}

Puede crear una canalización de funciones Motor realizando una solicitud de POST mientras proporciona sus metadatos y una URL de acoplamiento que haga referencia a una imagen de Docker.

**Formato API**

```https
POST /engines
```

**Solicitud**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker. El valor se puede establecer en Spark o PySpark. |
| `algorithm` | El algoritmo que se está utilizando, establezca este valor en `fp` (canalización de funciones). |
| `name` | Nombre deseado para el motor de canalización de funciones. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como la descripción de la fórmula. Esta es una propiedad obligatoria. Si no desea proporcionar una descripción, establezca su valor en una cadena vacía. |
| `mlLibrary` | Campo que se requiere al crear motores para las fórmulas de PySpark y Scala. Este campo debe establecerse en `databricks-spark`. |
| `artifacts.default.image.location` | Ubicación de la imagen del Docker. Solo se admite Azure ACR o Public (no autenticado) Dockerhub. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker. Puede ser &quot;Spark&quot; o &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Tipo de embalaje del motor. Este valor debe establecerse en `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Los parámetros del archivo de configuración `pipeline.json`. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del nuevo motor de canalización de funciones creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor de canalización de funciones PySpark.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Recuperar una lista de motores

Puede recuperar una lista de motores realizando una sola solicitud de GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

**Formato de API**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de motores y sus detalles.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Recuperar un motor específico {#retrieve-specific}

Puede recuperar los detalles de un motor específico realizando una solicitud de GET que incluya el ID del motor deseado en la ruta de solicitud.

**Formato de API**

```https
GET /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor deseado.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Actualizar un motor

Puede modificar y actualizar un motor existente sobrescribiendo sus propiedades mediante una solicitud de PUT que incluya el ID del motor de destinatario en la ruta de la solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!NOTE]
>
>Para garantizar el éxito de esta solicitud de PUT, se sugiere que primero realice una solicitud de GET para [recuperar el motor por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud de PUT.

La siguiente llamada de API de ejemplo actualizará el nombre y la descripción de un motor al tener estas propiedades inicialmente:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**Formato de API**

```https
PUT /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles actualizados del motor.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Eliminar un motor

Puede eliminar un motor realizando una solicitud de DELETE mientras especifica el ID del motor de destinatario en la ruta de la solicitud. Al eliminar un motor, se eliminarán en cascada todas las instancias de MLI que hagan referencia a dicho motor, incluidas las ejecuciones de experimentos y experimentos que pertenezcan a dichas instancias de MLI.

**Formato de API**

```https
DELETE /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
