---
keywords: Experience Platform;inicio;temas populares;datos de almacenamiento en la nube;datos de flujo continuo;flujo continuo
solution: Experience Platform
title: Recopilación de datos de flujo continuo mediante conectores de origen y API
topic-legacy: overview
type: Tutorial
description: Este tutorial trata los pasos para recuperar datos de flujo continuo y llevarlos a Platform mediante conectores de origen y API.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 2%

---

# Recopilación de datos de flujo continuo mediante conectores de origen y API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial trata los pasos para recuperar datos de un conector de origen de flujo continuo y llevarlos a [!DNL Experience Platform] mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Este tutorial requiere que tenga un ID de conexión válido para un conector de flujo continuo. Si no tiene esta información, consulte los siguientes tutoriales sobre la creación de una conexión de origen de flujo continuo antes de intentar este tutorial:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../create/streaming/http.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Guía](../../../../xdm/api/getting-started.md) para desarrolladores de Schema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de esquemas. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo es el sistema de registro para la ubicación y linaje de datos dentro de  [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): La introducción por transmisión para  [!DNL Platform] proporciona a los usuarios un método para enviar datos desde dispositivos de cliente y del lado del servidor a  [!DNL Experience Platform] en tiempo real.
- [Simuladores para pruebas](../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para recopilar datos de flujo continuo correctamente mediante la API [!DNL Flow Service].

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

- `Content-Type: application/json`

## Crear una conexión de origen {#source}

Puede crear una conexión de origen realizando una solicitud de POST a la API [!DNL Flow Service]. Una conexión de origen consiste en un ID de conexión, una ruta al archivo de datos de origen y un ID de especificación de conexión.

Para crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para conectores basados en archivos:

| Formato de datos | Valor de enumeración |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parqué | `parquet` |

Para todos los conectores basados en tablas, establezca el valor en `tabular`.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `providerId` | El ID del proveedor del conector de flujo continuo. |
| `connectionId` | El ID de conexión único de su conector de flujo continuo. |
| `connectionSpec.id` | El ID de especificación de conexión asociado al conector de flujo continuo específico. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Obtener URL de extremo de flujo continuo {#get-endpoint}

Con la conexión de origen creada, ahora puede recuperar la URL del extremo de flujo continuo.

**Formato de API**

```http
GET /flowservice/sourceConnections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de sourceConnections que creó anteriormente. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/sourceConnections/e96d6135-4b50-446e-922c-6dd66672b6b2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la conexión solicitada. La URL del extremo de flujo continuo se crea automáticamente con la conexión y se puede recuperar utilizando el valor `inletUrl`.

```json
{
    "items": [
        {
            "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
            "createdAt": 1617743929826,
            "updatedAt": 1617743930363,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG}",
            "name": "Test source connector for streaming data",
            "description": "Test source connector for streaming data",
            "baseConnectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
            "state": "enabled",
            "data": {
                "format": "delimited",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "params": {
                "sourceId": "Streaming raw data",
                "inletUrl": "https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "inletId": "2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "dataType": "raw",
                "name": "hgtest"
            },
            "version": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "etag": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
                    "connectionSpec": {
                        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                        "version": "1.0"
                    }
                }
            }
        }
    ]
}
```


## Crear un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en [!DNL Platform], se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos [!DNL Platform] en el que se incluyen los datos de origen. Este esquema XDM de destino también amplía la clase XDM [!DNL Individual Profile].

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la [API del Registro de Esquemas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**Formato de API**

```http
POST /tenant/schemas
```

**Solicitud**

La siguiente solicitud de ejemplo crea un esquema XDM que amplía la clase XDM [!DNL Individual Profile].

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**Respuesta**

Una respuesta correcta devuelve detalles del esquema recién creado, incluido su identificador único (`$id`). Este ID es necesario en pasos posteriores para crear un conjunto de datos de destinatario, una asignación y un flujo de datos.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creación de un conjunto de datos de destino

Se puede crear un conjunto de datos de destino realizando una solicitud de POST a la [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), proporcionando el ID del esquema de destino dentro de la carga útil.

**Formato de API**

```http
POST /catalog/dataSets
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        },
        "name": "Test streaming dataset"
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `schemaRef.id` | El ID del esquema XDM de destino. |
| `schemaRef.contentType` | Versión del esquema. Este valor debe establecerse `application/vnd.adobe.xed-full-notext+json;version=1`, que devuelve la última versión secundaria del esquema. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de solo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas API. El ID del conjunto de datos de destino es necesario en pasos posteriores para crear una conexión de destino y un flujo de datos.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Crear una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que llegan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos, un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión a un lago de datos. Con estos identificadores, se puede crear una conexión de destino mediante la API [!DNL Flow Service] para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `params.dataSetId` | El ID del conjunto de datos de destino. |
| `connectionSpec.id` | El ID de especificación de conexión utilizado para conectarse al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único de la nueva conexión de destino (`id`). Este ID se requiere en pasos posteriores.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Crear una asignación {#mapping}

Para que los datos de origen se introduzcan en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino. Esto se logra realizando una solicitud de POST al servicio de conversión con asignaciones de datos definidas dentro de la carga útil de la solicitud.

**Formato de API**

```http
POST /conversion/mappingSets
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `xdmSchema` | El `$id` del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Buscar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de los orígenes y traerlos a [!DNL Platform]. Para crear un flujo de datos, primero debe obtener las especificaciones del flujo de datos realizando una solicitud de GET a la API [!DNL Flow Service]. Las especificaciones de flujo de datos son responsables de recopilar datos de un conector de flujo continuo.
**Formato de API**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos que es responsable de traer datos de su conector de flujo continuo a [!DNL Platform]. Este ID es necesario en el siguiente paso para crear un nuevo flujo de datos.

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Crear un flujo de datos

El último paso para recopilar datos de flujo continuo es crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores obligatorios:

- [ID de conexión de origen](#source)
- [ID de conexión de Target](#target)
- [ID de asignación](#mapping)
- [ID de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | El [Id. de especificación de flujo](#specs) recuperado en el paso anterior. |
| `sourceConnectionIds` | El [ID de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | El [ID de conexión de destino](#target-connection) recuperado en un paso anterior. |
| `transformations.params.mappingId` | El [ID de asignación](#mapping) recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Registro de datos sin procesar que se van a ingerir {#ingest-data}

Ahora que ha creado su flujo, puede enviar su mensaje JSON al extremo de flujo que creó anteriormente.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión de flujo continuo recién creada. |

**Solicitud**

La solicitud de ejemplo ingesta datos sin procesar en el extremo de flujo que se creó anteriormente.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
          "day": 9
      }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la información recién ingerida.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | El ID de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado en el servidor para el registro que acaba de enviar. Este ID ayuda a los Adobes a rastrear el ciclo vital de este registro a través de varios sistemas y con depuración. |
| `receivedTimeMs`: Marca de tiempo (época en milisegundos) que muestra la hora a la que se recibió la solicitud. |

## Pasos siguientes

Al seguir este tutorial, ha creado un flujo de datos para recopilar datos de flujo continuo del conector de flujo continuo. Los datos entrantes ahora se pueden usar en servicios descendentes [!DNL Platform] como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Resumen del perfil del cliente en tiempo real](../../../../profile/home.md)
- [Información general de Data Science Workspace](../../../../data-science-workspace/home.md)
