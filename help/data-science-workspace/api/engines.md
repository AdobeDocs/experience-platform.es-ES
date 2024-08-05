---
keywords: Experience Platform; guía de desarrolladores; Extremo; Data Science Espacio de trabajo; temas populares; motores; API de aprendizaje automático de Sensei
solution: Experience Platform
title: Punto final de la API de motores
description: Los motores son la base de los modelos de aprendizaje automático en Data Science Espacio de trabajo. Contienen algoritmos de aprendizaje automático que resuelven problemas específicos, canalizaciones de características para realizar ingeniería de características, o ambos.
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 2%

---

# Punto final de los motores

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

Los motores son la base de los modelos de aprendizaje automático en Data Science Espacio de trabajo. Contienen algoritmos de aprendizaje automático que resuelven problemas específicos, canalizaciones de características para realizar ingeniería de características, o ambos.

## Look el registro de Docker

>[!TIP]
>
>Si no tiene un URL de Docker, visita los archivos de origen del [paquete en una tutorial de fórmula](../models-recipes/package-source-files-recipe.md) para obtener un tutorial paso a paso sobre la creación de un host URL de Docker.

Se requieren sus credenciales de registro de Docker para cargar un archivo de receta empaquetado, incluidos su host URL, nombre de usuario y contraseña de Docker. Puede buscar esta información realizando los siguientes petición GET:

**Formato API**

```https
GET /engines/dockerRegistry
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del registro de Docker, incluidos el URL de Docker (`host`), nombre de usuario (`username`) y contraseña (`password`).

>[!NOTE]
>
>Su contraseña de Docker cambia cada vez que `{ACCESS_TOKEN}` se actualiza.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Crear un motor que usa URL de Docker {#docker-image}

Puede crear un motor realizando un petición POST mientras proporciona su metadatos y un URL de Docker que hace referencia a una imagen de Docker en formularios de varias partes.

**Formato API**

```https
POST /engines
```

**Solicitar Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | El nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para mostrarlo en la interfaz de usuario como el nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para mostrarlo en la interfaz de usuario como la descripción de la fórmula. Esta propiedad es obligatoria. Si no desea proporcionar una descripción, establezca su valor como una cadena vacía. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen Docker y puede ser &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |
| `algorithm` | Cadena que especifica el tipo de algoritmo de aprendizaje automático. Los tipos de algoritmo admitidos son &quot;Clasificación&quot;, &quot;Regresión&quot; o &quot;Personalizado&quot;. |
| `artifacts.default.image.location` | La ubicación de la imagen de Docker a la que está vinculado una URL de Docker. |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen Docker y puede ser &quot;Python&quot;, &quot;R&quot; o &quot;Tensorflow&quot;. |

**Solicitar PySpark/Scala**

Al hacer un solicitud para recetas de PySpark, el `executionType` y `type` es &quot;PySpark&quot;. Al hacer un solicitud para recetas de Scala, el `executionType` y `type` es &quot;Spark&quot;. El siguiente ejemplo de fórmula de Scala utiliza Spark:

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
| `name` | El nombre deseado para el motor. La Fórmula correspondiente a este Motor heredará este valor para mostrarse en la IU como el nombre de la Fórmula. |
| `description` | Una descripción opcional del motor. La Fórmula correspondiente a este Motor heredará este valor para ser mostrada en IU como la descripción de la Fórmula. Esta Propiedad es obligatoria. Si no desea proporcionar una descripción, defina su valor para que sea una cadena vacía. |
| `type` | Tipo de ejecución del motor. Este valor corresponde al idioma en el que se basa la imagen de Docker. El valor se puede establecer en Spark o PySpark. |
| `mlLibrary` | Campo necesario al crear motores para recetas de PySpark y Scala. Este campo debe establecerse en `databricks-spark`. |
| `artifacts.default.image.location` | La ubicación de la imagen de Docker. Solo se admite Azure ACR o Dockerhub público (no autenticado). |
| `artifacts.default.image.executionType` | Tipo de ejecución del motor. Este valor corresponde al idioma en el que se basa la imagen de Docker. Puede ser &quot;Spark&quot; o &quot;PySpark&quot;. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor de Python. Todas las respuestas del motor seguir esta formato:

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

## Crear motor de canalización de características que utilice URL de Docker {#feature-pipeline-docker}

Puede crear un motor de canalización de características realizando un petición POST y proporcionando su metadatos y un URL de Docker que haga referencia a una imagen de Docker.

**Formato de API**

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
| `type` | Tipo de ejecución del motor. Este valor corresponde al idioma en el que se basa la imagen de Docker. El valor se puede establecer en Spark o PySpark. |
| `algorithm` | El algoritmo que se está utilizando, establezca este valor en `fp` (canalización de características). |
| `name` | Nombre deseado para el motor de canalización de características. La Fórmula correspondiente a este Motor heredará este valor para mostrarse en la IU como el nombre de la Fórmula. |
| `description` | Una descripción opcional del motor. La Fórmula correspondiente a este Motor heredará este valor para ser mostrada en IU como la descripción de la Fórmula. Esta Propiedad es obligatoria. Si no desea proporcionar una descripción, defina su valor para que sea una cadena vacía. |
| `mlLibrary` | Campo necesario al crear motores para recetas de PySpark y Scala. Este campo debe establecerse en `databricks-spark`. |
| `artifacts.default.image.location` | La ubicación de la imagen de Docker. Solo se admite Azure ACR o Dockerhub público (no autenticado). |
| `artifacts.default.image.executionType` | Tipo de ejecución del motor. Este valor corresponde al idioma en el que se basa la imagen de Docker. Puede ser &quot;Spark&quot; o &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Tipo de embalaje del motor. Este valor debe establecerse en `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Parámetros del `pipeline.json` archivo de configuración. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor de canalización de características recién creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor de canalización de características de PySpark.

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

## Recuperar un lista de motores

Puede recuperar un lista de motores realizando un solo petición GET. Para filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [consulta parámetros para recurso recuperación](./appendix.md#query).

**Formato API**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve un lista de motores y sus detalles.

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
| `{ENGINE_ID}` | El ID de un motor existente. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Puede modificar y actualizar un motor existente sobrescribiendo sus propiedades a través de una solicitud del PUT que incluya el ID del motor de destino en la ruta de solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!NOTE]
>
>Para garantizar el éxito de esta solicitud de PUT, se recomienda que primero realice una solicitud de GET para [recuperar el motor por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para el petición PUT.

La siguiente llamada de API de ejemplo actualizará el nombre y la descripción de un motor mientras inicialmente tiene estas propiedades:

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

**Formato API**

```https
PUT /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | El ID de un motor existente. |

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Puede eliminar un motor realizando una solicitud de DELETE mientras especifica el ID del motor de destino en la ruta de solicitud. Al eliminar un motor, se eliminarán en cascada todas las instancias de MLInstances que hagan referencia a ese motor, incluidos los experimentos y las ejecuciones de experimentos que pertenezcan a esas instancias de MLI.

**Formato de API**

```https
DELETE /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | El ID de un motor existente. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
