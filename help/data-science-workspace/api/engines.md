---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Motores
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Motores

Los motores son la base de los modelos de aprendizaje automático en el área de trabajo de ciencias de datos. Contienen algoritmos de aprendizaje automático que resuelven problemas específicos, conductos de funciones para realizar ingeniería de funciones o ambos.

## Buscar el registro del Docker

>[!TIP]
>Si no tiene una URL de Docker, visite los archivos de origen del [paquete en un tutorial de fórmula](../models-recipes/package-source-files-recipe.md) para obtener un tutorial paso a paso sobre la creación de una URL de host de Docker.

Se requieren las credenciales del Registro de Docker para cargar un archivo de fórmula empaquetado, incluyendo la dirección URL del host de Docker, el nombre de usuario y la contraseña. Puede buscar esta información realizando la siguiente solicitud GET:

**Formato de API**

```http
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
>La contraseña del Docker cambia cada vez que `{ACCESS_TOKEN}` se actualiza.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Creación de un motor mediante URL de acoplamiento {#docker-image}

Puede crear un motor realizando una solicitud POST mientras proporciona sus metadatos y una URL de Docker que haga referencia a una imagen de Docker en formularios de varias partes.

**Formato de API**

```http
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
                    "location": "{DOCKER_URL}",
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

Cuando se realiza una solicitud de las fórmulas de PySpark, el `executionType` y `type` es &quot;PySpark&quot;. Cuando se realiza una solicitud para las fórmulas de Scala, `executionType` y `type` es &quot;Spark&quot;. En el siguiente ejemplo de fórmula Scala se utiliza Spark:

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
| `mlLibrary` | Campo que se requiere al crear motores para las fórmulas de PySpark y Scala. Este campo debe definirse como `databricks-spark`. |
| `artifacts.default.image.location` | Ubicación de la imagen del Docker. Solo se admite Azure ACR o el Dockerhub público (no autenticado). |
| `artifacts.default.image.executionType` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crea la imagen del Docker. Puede ser &quot;Spark&quot; o &quot;PySpark&quot;. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`). La siguiente respuesta de ejemplo es para un motor Python. Todas las respuestas del motor siguen este formato:

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

## Recuperar una lista de motores

Puede recuperar una lista de motores realizando una sola solicitud GET. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](./appendix.md#query)de recursos.

**Formato de API**

```http
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

Puede recuperar los detalles de un motor específico realizando una solicitud GET que incluya el ID del motor deseado en la ruta de solicitud.

**Formato de API**

```http
GET /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor deseado.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Actualizar un motor

Puede modificar y actualizar un motor existente sobrescribiendo sus propiedades mediante una solicitud PUT que incluya el ID del motor de destinatario en la ruta de la solicitud y proporcionando una carga útil JSON que contenga propiedades actualizadas.

>[!NOTE] Para garantizar el éxito de esta solicitud PUT, se sugiere que primero realice una solicitud GET para [recuperar el motor por ID](#retrieve-specific). A continuación, modifique y actualice el objeto JSON devuelto y aplique la totalidad del objeto JSON modificado como carga útil para la solicitud PUT.

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

```http
PUT /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "id": "{ENGINE_ID}",
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

Puede eliminar un motor realizando una solicitud DELETE mientras especifica el ID del motor de destinatario en la ruta de la solicitud. Al eliminar un motor, se eliminarán en cascada todas las instancias de MLI que hagan referencia a dicho motor, incluidas las ejecuciones de experimentos y experimentos que pertenezcan a dichas instancias de MLI.

**Formato de API**

```http
DELETE /engines/{ENGINE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ENGINE_ID}` | ID de un motor existente. |

**Solicitud**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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

## Solicitudes obsoletas

>[!IMPORTANT]
>Los artefactos binarios ya no son compatibles y se definen para eliminarlos posteriormente. Las nuevas fórmulas de PySpark y Scala deberían seguir los ejemplos de imágenes [del](#docker-image) acoplador para crear un motor.

## Crear un motor con artefactos binarios: obsoleto

Puede crear un motor con artefactos locales `.jar` o `.egg` binarios realizando una solicitud POST mientras proporciona sus metadatos y la ruta del artefacto en formularios de varias partes.

**Formato de API**

```http
POST /engines
```

**Solicitud**

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
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como la descripción de la fórmula. Esta es una propiedad obligatoria. Si no desea proporcionar una descripción, establezca su valor en una cadena vacía. |
| `algorithm` | Una cadena que especifica el tipo de algoritmo de aprendizaje automático. Los tipos de algoritmo admitidos son &quot;Clasificación&quot;, &quot;Regresión&quot; o &quot;Personalizado&quot;. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al lenguaje en el que se crea el artefacto binario y puede ser &quot;PySpark&quot; o &quot;Spark&quot;. |


**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`).

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Creación de un motor de canalización de funciones mediante artefactos binarios (obsoleto) {#create-a-feature-pipeline-engine-using-binary-artifacts}

>[!IMPORTANT]
>Los artefactos binarios ya no son compatibles y se definen para eliminarlos posteriormente.

Puede crear una canalización de funciones Motor utilizando artefactos locales `.jar` o `.egg` binarios realizando una solicitud POST mientras proporciona sus metadatos y las rutas del artefacto en formularios de varias partes. Un motor PySpark o Spark tiene la capacidad de especificar recursos de cálculo, como el número de núcleos o la cantidad de memoria. Consulte la sección del apéndice sobre las configuraciones [de recursos de](./appendix.md#resource-config) PySpark y Spark para obtener más información.

**Formato de API**

```http
POST /engines
```

**Solicitud**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre deseado para el motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como nombre de la fórmula. |
| `description` | Una descripción opcional del motor. La fórmula correspondiente a este motor heredará este valor para que se muestre en la interfaz de usuario como la descripción de la fórmula. Esta es una propiedad obligatoria. Si no desea proporcionar una descripción, establezca su valor en una cadena vacía. |
| `algorithm` | Una cadena que especifica el tipo de algoritmo de aprendizaje automático. Establezca este valor como &quot;fp&quot; para especificar que esta creación sea un motor de canalización de funciones. |
| `type` | El tipo de ejecución del motor. Este valor corresponde al idioma en el que se crean los artefactos binarios y puede ser &quot;PySpark&quot; o &quot;Spark&quot;. |

**Respuesta**

Una respuesta correcta devuelve una carga útil que contiene los detalles del motor recién creado, incluido su identificador único (`id`).

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```
