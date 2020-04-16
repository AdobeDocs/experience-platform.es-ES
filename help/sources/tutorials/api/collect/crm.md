---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recopilación de datos CRM mediante conectores de origen y API
topic: overview
translation-type: tm+mt
source-git-commit: 88376a67e064208ab62dd339e820adb8e47d3c4e

---


# Recopilación de datos CRM mediante conectores de origen y API

Este tutorial trata los pasos para recuperar datos de un sistema CRM y llevarlos a la plataforma a través de conectores de origen y API.

## Primeros pasos

Este tutorial requiere que tenga acceso a un sistema CRM a través de una conexión base válida e información sobre la tabla que desea incluir en Platform, incluyendo la ruta y la estructura de la tabla. Si no tiene esta información, consulte el tutorial sobre [explorar sistemas CRM mediante la API](../explore/crm.md) de servicio de flujo antes de intentar este tutorial.

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Guía](../../../../xdm/api/getting-started.md)para desarrolladores de Esquema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de Esquema. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
* [Servicio](../../../../catalog/home.md)de catálogo: Catalog es el sistema de registros para la ubicación y el linaje de los datos dentro de la plataforma de experiencia.
* [Ingesta](../../../../ingestion/batch-ingestion/overview.md)por lotes: La API de inserción de lotes permite ingestar datos en la plataforma de experiencias como archivos por lotes.
* [Simuladores](../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema CRM mediante la API de servicio de flujo.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Creación de una clase y un esquema XDM ad-hoc

Para poder introducir datos externos en la plataforma mediante conectores de origen, se debe crear una clase y un esquema XDM ad-hoc para los datos de origen sin procesar.

Para crear una clase ad-hoc y un esquema, siga los pasos descritos en el tutorial [de esquema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Al crear una clase ad-hoc, todos los campos encontrados en los datos de origen deben describirse dentro del cuerpo de la solicitud.

Siga los pasos descritos en la guía para desarrolladores hasta que haya creado un esquema ad-hoc. Obtenga y almacene el identificador único (`$id`) del esquema ad-hoc y, a continuación, continúe con el paso siguiente de este tutorial.

## Creación de una conexión de origen {#source}

Con la creación de un esquema XDM ad-hoc, ahora se puede crear una conexión de origen mediante una solicitud POST a la API de servicio de flujo. Una conexión de origen consiste en una conexión base, un archivo de datos de origen y una referencia al esquema que describe los datos de origen.

**Formato API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for a CRM system",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Source Connection for a CRM system",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/140c03de81b959db95879033945cfd4c",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "tableName": "{TABLE_PATH}",
            "columns": [
                {
                    "name": "first_name",
                    "type": "string",
                    "meta": {
                        "originalType": "String"
                    }
                },
                {
                    "name": "last_name",
                    "type": "string",
                    "meta": {
                        "originalType": "String"
                    }
                },
                {
                    "name": "email",
                    "type": "string",
                    "meta": {
                        "originalType": "String"
                    }
                }
            ]
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | ID de una conexión base para un sistema CRM. |
| `data.schema.id` | ID del esquema XDM ad-hoc. |
| `params.path` | Ruta del archivo de origen. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Almacene este valor tal como se requiere en pasos posteriores para crear una conexión de destinatario.

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
}
```

## Creación de un esquema destinatario XDM {#target}

En pasos anteriores, se creó un esquema XDM ad-hoc para estructurar los datos de origen. Para que los datos de origen se utilicen en Platform, también se debe crear un esquema de destinatario para estructurar los datos de origen según sus necesidades. El esquema de destinatario se utiliza para crear un conjunto de datos de la plataforma en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destinatario realizando una solicitud POST a la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquema. Si prefiere utilizar la interfaz de usuario en la plataforma de experiencias, el tutorial [Editor de](../../../../xdm/tutorials/create-schema-ui.md) Esquemas proporciona instrucciones paso a paso para realizar acciones similares en el Editor de Esquemas.

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitud**

La siguiente solicitud de ejemplo crea un esquema XDM que extiende la clase de Perfil individual XDM.

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
        "title": "Target schema for CRM source connector",
        "description": "",
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

Una respuesta correcta devuelve detalles del esquema recién creado, incluido su identificador único (`$id`). Almacene este ID como sea necesario en pasos posteriores para crear un conjunto de datos, una asignación y un flujo de datos de destinatario.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
    "meta:altId": "{TENANT_ID}.schemas.417a33eg81a221bd10495920574gfa2d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for CRM source connector",
    "description": "",
    "type": "object",
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
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "meta:registryMetadata": {
        "eTag": "6m/FrIlXYU2+yH6idbcmQhKSlMo="
    }
}
```

## Creación de un conjunto de datos de destinatario

Se puede crear un conjunto de datos de destinatario realizando una solicitud POST a la API de servicio de catálogo, proporcionando el ID del esquema de destinatario dentro de la carga útil.

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
        "name": "Target Dataset for CRM data",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `schemaRef.id` | ID del esquema XDM de destinatario. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado en el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API. Almacene el ID del conjunto de datos de destinatario como se requiere en pasos posteriores para crear una conexión de destinatario y un flujo de datos.

```json
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Creación de una conexión base de datos

Para crear una conexión de destinatario e ingerir datos externos en la plataforma, primero se debe adquirir una conexión de base de datos.

Para crear una conexión de base de datos, siga los pasos descritos en el tutorial [de conexión de base de](../create-dataset-base-connection.md)datos.

Siga los pasos descritos en la guía para desarrolladores hasta que haya creado una conexión base de datos. Obtenga y almacene el identificador único (`$id`) de la conexión base y continúe con el siguiente paso de este tutorial.

## Creación de una conexión de destinatario

Ahora tiene los identificadores únicos para una conexión base de datos, un esquema de destinatario y un conjunto de datos de destinatario. Con estos identificadores, puede crear una conexión de destinatario mediante la API de servicio de flujo para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato API**

```http
POST /targetConnections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection",
        "description": "Target Connection for CRM data",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `baseConnectionId` | ID de la conexión base de datos. |
| `data.schema.id` | El `$id` del esquema XDM de destinatario. |
| `params.dataSetId` | ID del conjunto de datos de destinatario. |
| `connectionSpec.id` | ID de especificación de conexión para su CRM. |

>[!NOTE] Al crear una conexión de destinatario, asegúrese de utilizar el valor de conexión base del conjunto de datos para la conexión base `id` en lugar de la conexión base del conector de origen de terceros.

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## Crear una asignación {#mapping}

Para que los datos de origen se puedan ingerir en un conjunto de datos de destinatario, primero deben asignarse al esquema de destinatario al que se adhiere el conjunto de datos de destinatario. Esto se consigue realizando una solicitud POST a la API de servicio de conversión con asignaciones de datos definidas en la carga útil de la solicitud.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `xdmSchema` | ID del esquema XDM de destinatario. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Almacene este valor como se requiere en un paso posterior para crear un flujo de datos.

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## Buscar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de las fuentes y de traerlos a la Plataforma. Para crear un flujo de datos, primero debe obtener las especificaciones de flujo de datos responsables de recopilar datos CRM.

**Formato API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos que es responsable de llevar los datos del sistema CRM a la plataforma. Almacene el valor del `id` campo como se requiere en el paso siguiente para crear un nuevo flujo de datos.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## Crear un flujo de datos

El último paso para recopilar datos CRM es crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores obligatorios:

* [ID de conexión de origen](#source)
* [ID de conexión de Destinatario](#target)
* [ID de asignación](#mapping)
* [Id. de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud POST mientras proporciona los valores mencionados anteriormente en la carga útil.

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
        "name": "Dataflow between a CRM system and Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "mode": "append"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | Id. de especificación de flujo de datos |
| `sourceConnectionIds` | ID de conexión de origen |
| `targetConnectionIds` | ID de conexión de Destinatario |
| `transformations.params.mappingId` | ID de asignación |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de origen para recopilar datos de un sistema CRM de forma programada. Los datos entrantes ahora se pueden utilizar en los servicios de plataforma descendente, como Perfil del cliente en tiempo real y Área de trabajo de ciencias de datos. Consulte los siguientes documentos para obtener más información:

* [Información general sobre el Perfil del cliente en tiempo real](../../../../profile/home.md)
* [Información general sobre el área de trabajo de ciencias de datos](../../../../data-science-workspace/home.md)