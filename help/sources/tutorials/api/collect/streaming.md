---
keywords: Experience Platform;home;popular topics;cloud storage data;streaming data;streaming
solution: Experience Platform
title: Recopilación de datos de flujo continuo a través de las API y los conectores de origen
topic: overview
type: Tutorial
description: En este tutorial se explican los pasos para recuperar datos de flujo continuo y llevarlos a la plataforma a través de las API y los conectores de origen.
translation-type: tm+mt
source-git-commit: a9d6c6dda560ec401bdf41319994153e7f2c0572
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 2%

---


# Recopilación de datos de flujo continuo a través de las API y los conectores de origen

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial trata los pasos para recuperar datos de un conector de origen de flujo continuo y llevarlos a [!DNL Experience Platform] utilizar la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Este tutorial requiere que tenga un ID de conexión válido para un conector de flujo continuo. Si no dispone de esta información, consulte los siguientes tutoriales sobre la creación de una conexión de origen de flujo continuo antes de intentar este tutorial:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../../../../ingestion/tutorials/create-streaming-connection.md)

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):: El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Guía](../../../../xdm/api/getting-started.md)para desarrolladores de esquema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de Esquema. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
- [[!DNL Catalog Service]](../../../../catalog/home.md):: Catalog es el sistema de registro para la ubicación y linaje de datos dentro de [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md):: La ingestión de flujo continuo para [!DNL Platform] proporciona a los usuarios un método para enviar datos desde dispositivos cliente y servidor a [!DNL Experience Platform] en tiempo real.
- [Simuladores](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para recopilar datos de flujo de forma satisfactoria mediante la [!DNL Flow Service] API.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

- `Content-Type: application/json`

## Creación de una conexión de origen {#source}

Puede crear una conexión de origen realizando una solicitud de POST a la [!DNL Flow Service] API. Una conexión de origen consiste en un ID de conexión, una ruta al archivo de datos de origen y un ID de especificación de conexión.

Para crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para los conectores basados en archivos:

| Formato de datos | Valor de enumeración |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todos los conectores basados en tablas, establezca el valor en `tabular`.

**Formato API**

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
| `providerId` | ID del proveedor del conector de flujo continuo. |
| `connectionId` | ID de conexión única de su conector de flujo continuo. |
| `connectionSpec.id` | El ID de especificación de conexión asociado a su conector de flujo específico. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "2abd97c4-91bb-4c93-bd97-c491bbfc933d",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Creación de un esquema destinatario XDM {#target-schema}

Para que los datos de origen se utilicen en [!DNL Platform], se debe crear un esquema de destinatario para estructurar los datos de origen según sus necesidades. El esquema de destinatario se utiliza para crear un [!DNL Platform] conjunto de datos en el que se incluyen los datos de origen. Este esquema destinatario XDM también amplía la clase XDM [!DNL Individual Profile] .

Se puede crear un esquema XDM de destinatario realizando una solicitud de POST a la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquema.

**Formato API**

```http
POST /tenant/schemas
```

**Solicitud**

La siguiente solicitud de ejemplo crea un esquema XDM que extiende la clase XDM [!DNL Individual Profile] .

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

Una respuesta correcta devuelve detalles del esquema recién creado, incluido su identificador único (`$id`). Este ID es necesario en pasos posteriores para crear un conjunto de datos, una asignación y un flujo de datos de destinatario.

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

## Creación de un conjunto de datos de destinatario

Se puede crear un conjunto de datos de destinatario realizando una solicitud de POST a la API [de servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo, proporcionando el ID del esquema de destinatario dentro de la carga útil.

**Formato API**

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
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.1"
        },
        "fileDescription": {
            "format": "parquet"
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
| `schemaRef.id` | ID del esquema XDM de destinatario. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado en el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API. El ID del conjunto de datos de destinatario es necesario en pasos posteriores para crear una conexión de destinatario y un flujo de datos.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Creación de una conexión de destinatario {#target-connection}

Una conexión de destinatario representa la conexión al destino en el que aterrizan los datos ingestados. Para crear una conexión de destinatario, debe proporcionar el ID de especificación de conexión fijo asociado con el lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos un esquema de destinatario un conjunto de datos de destinatario y el ID de especificación de conexión con el lago de datos. Con estos identificadores, puede crear una conexión de destinatario utilizando la [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen de entrada.

**Formato API**

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
| `params.dataSetId` | ID del conjunto de datos de destinatario. |
| `connectionSpec.id` | ID de especificación de conexión utilizado para conectarse al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destinatario. Este ID se requiere en pasos posteriores.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Crear una asignación {#mapping}

Para que los datos de origen se puedan ingerir en un conjunto de datos de destinatario, primero deben asignarse al esquema de destinatario al que se adhiere el conjunto de datos de destinatario. Esto se logra realizando una solicitud de POST al servicio de conversión con asignaciones de datos definidas en la carga útil de la solicitud.

**Formato API**

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
| `xdmSchema` | El `$id` del esquema XDM de destinatario. |

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

Un flujo de datos es responsable de recopilar datos de las fuentes y de traerlos a [!DNL Platform]. Para crear un flujo de datos, primero debe obtener las especificaciones de flujo de datos mediante una solicitud de GET a la [!DNL Flow Service] API. Las especificaciones de flujo de datos son responsables de recopilar datos de un conector de flujo continuo.
**Formato API**

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

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos que es responsable de traer datos del conector de flujo de datos a [!DNL Platform]. Este ID es necesario en el paso siguiente para crear un nuevo flujo de datos.

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

El último paso para recopilar datos de flujo continuo es crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores necesarios:

- [ID de conexión de origen](#source)
- [ID de conexión de destinatario](#target)
- [ID de asignación](#mapping)
- [Id. de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores anteriormente mencionados dentro de la carga útil.

**Formato API**

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
            "2abd97c4-91bb-4c93-bd97-c491bbfc933d"
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
| `flowSpec.id` | ID [de especificación de](#specs) flujo recuperado en el paso anterior. |
| `sourceConnectionIds` | El ID [de conexión de](#source) origen recuperado en un paso anterior. |
| `targetConnectionIds` | El ID [de conexión de](#target-connection) destinatario recuperado en un paso anterior. |
| `transformations.params.mappingId` | ID [de](#mapping) asignación recuperada en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado un flujo de datos para recopilar datos de flujo continuo de su conector de flujo continuo. Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../../data-science-workspace/home.md)