---
keywords: Experience Platform;inicio;temas populares;datos de almacenamiento en la nube;datos de flujo continuo;flujo continuo
solution: Experience Platform
title: Creación de un flujo de datos de streaming para datos sin procesar mediante la API de Flow Service
type: Tutorial
description: Este tutorial trata los pasos para recuperar los datos de flujo continuo y llevarlos a Platform mediante conectores de origen y API.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 3%

---

# Crear un flujo de datos de flujo continuo para los datos sin procesar mediante la API [!DNL Flow Service]

Este tutorial cubre los pasos para recuperar datos sin procesar de un conector de origen de flujo continuo y llevarlos al Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): el marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Guía para desarrolladores de Schema Registry](../../../../xdm/api/getting-started.md): Incluye información importante que necesita conocer para realizar correctamente llamadas a la API de Schema Registry. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados necesarios para realizar solicitudes (con especial atención al encabezado Aceptar y sus posibles valores).
- [[!DNL Catalog Service]](../../../../catalog/home.md): el catálogo es el sistema de registro para la ubicación de datos y el linaje dentro del Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): la transmisión por secuencias de ingesta para Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor al Experience Platform en tiempo real.
- [Zonas protegidas](../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../landing/api-guide.md).

### Crear una conexión de origen {#source}

Este tutorial también requiere que tenga un ID de conexión de origen válido para un conector de flujo continuo. Si no tiene esta información, consulte los siguientes tutoriales sobre la creación de una conexión de origen de flujo continuo antes de intentar realizar este tutorial:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen. Este esquema XDM de destino también amplía la clase XDM [!DNL Individual Profile].

Para crear un esquema XDM de destino, realice una solicitud de POST al extremo `/schemas` de la [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve detalles del esquema recién creado, incluido su identificador único (`$id`). Este ID es necesario en pasos posteriores para crear un conjunto de datos, una asignación y un flujo de datos de destino.

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
    "imsOrg": "{ORG_ID}",
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

## Crear un conjunto de datos de destinatario

Con un esquema XDM de destino creado y su único `$id`, ahora puede crear un conjunto de datos de destino para contener los datos de origen. Para crear un conjunto de datos de destino, realice una solicitud de POST al extremo `dataSets` de la [API de servicio de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/), al tiempo que proporciona el ID del esquema de destino dentro de la carga útil.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
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
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del conjunto de datos que se va a crear. |
| `schemaRef.id` | URI `$id` para el esquema XDM en el que se basará el conjunto de datos. |
| `schemaRef.contentType` | La versión del esquema. Este valor debe establecerse en `application/vnd.adobe.xed-full-notext+json;version=1`, que devuelve la última versión secundaria del esquema. Consulte la sección sobre [versiones de esquema](../../../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena generada por el sistema de solo lectura que se utiliza para hacer referencia al conjunto de datos en las llamadas a la API. El ID del conjunto de datos de destino es necesario en pasos posteriores para crear una conexión de destino y un flujo de datos.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Creación de una conexión de destino {#target-connection}

Las conexiones de Target crean y administran una conexión de destino a Platform o a cualquier ubicación donde aterrizarán los datos transferidos. Las conexiones de destino contienen información sobre el destino de datos, el formato de datos y el ID de conexión de destino necesarios para crear un flujo de datos. Las instancias de conexión de destino son específicas de un inquilino y una organización.

Para crear una conexión de destino, realice una solicitud de POST al extremo `/targetConnections` de la API [!DNL Flow Service]. Como parte de la solicitud, debe proporcionar el formato de datos, el `dataSetId` recuperado en el paso anterior y el identificador de especificación de conexión fija vinculado a [!DNL Data Lake]. Este identificador es `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `data.format` | El formato especificado de los datos que está trayendo al lago de datos. |
| `params.dataSetId` | El ID del conjunto de datos de destinatario generado en el paso anterior. **Nota**: debe proporcionar un identificador de conjunto de datos válido al crear una conexión de destino. Si la ID del conjunto de datos no es válida, se producirá un error. |
| `connectionSpec.id` | ID de especificación de conexión utilizado para conectarse al lago de datos. Este identificador es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destino. Este ID es necesario en pasos posteriores.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino.

Para crear un conjunto de asignaciones, realice una solicitud de POST al extremo `mappingSets` de la [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) y proporcione el esquema XDM de destino `$id` y los detalles de los conjuntos de asignaciones que desee crear.

**Formato de API**

```http
POST /mappingSets
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Recuperación de una lista de especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de fuentes y llevarlos a Platform. GET Para crear un flujo de datos, primero debe obtener las especificaciones del flujo de datos realizando una solicitud a la API [!DNL Flow Service].

**Formato de API**

```http
GET /flowSpecs
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de especificaciones de flujo de datos. El id. de especificación de flujo de datos que debe recuperar para crear un flujo de datos con cualquiera de [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] o [!DNL Google PubSub] es `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
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
        },
    ]
}
```

## Creación de un flujo de datos

El último paso para recopilar datos de flujo continuo es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

- [ID de conexión de Source](#source)
- [ID de conexión de destino](#target)
- [ID de asignación](#mapping)
- [ID de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
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
| `flowSpec.id` | [ID de especificación de flujo](#specs) recuperado en el paso anterior. |
| `sourceConnectionIds` | [Id. de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | [Id. de conexión de destino](#target-connection) recuperado en un paso anterior. |
| `transformations.params.mappingId` | [ID de asignación](#mapping) recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Datos de Post para la ingesta

Consulte la carga útil de ejemplo a continuación para ver ejemplos de json sin procesar o compatible con XDM que puede enviar para su ingesta.

>[!NOTE]
>
>Debe añadir un retraso de al menos ~5 minutos entre la creación del flujo de datos y la ingesta de cualquier dato de flujo continuo. Esto permite que el flujo de datos esté completamente habilitado antes de que se incorpore cualquier dato.

Los siguientes ejemplos se aplican a todos:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB Datos sin procesar]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Datos XDM]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha creado un flujo de datos para recopilar datos de flujo continuo desde el conector de flujo continuo. Ahora, los servicios de la plataforma descendente como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace] pueden usar los datos entrantes. Consulte los siguientes documentos para obtener más información:

- [Información general del perfil del cliente en tiempo real](../../../../profile/home.md)
- [Información general del espacio de trabajo de ciencia de datos](../../../../data-science-workspace/home.md)
