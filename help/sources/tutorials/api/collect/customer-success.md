---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recopilar datos de un sistema de éxito de cliente mediante conectores de origen y API
topic: overview
translation-type: tm+mt
source-git-commit: 84ea3e45a3db749359f3ce4a0ea25429eee8bb66
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---


# Recopilar datos de un sistema de éxito de cliente mediante conectores de origen y API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

En este tutorial se explican los pasos para recuperar datos de un sistema de éxito de cliente y pasarlos a través de [!DNL Platform] las API y los conectores de origen.

## Primeros pasos

Este tutorial requiere que tenga acceso a un sistema de éxito de cliente de terceros a través de una conexión válida e información sobre el archivo en el que desea introducir [!DNL Platform], incluida la ruta y la estructura del archivo. Si no dispone de esta información, consulte el tutorial sobre [explorar una base de datos o sistema NoSQL con la API](../explore/customer-success.md) de servicio de flujo antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Guía](../../../../xdm/api/getting-started.md)para desarrolladores de Esquema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de Esquema. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
* [Servicio](../../../../catalog/home.md)de catálogo: Catalog es el sistema de registro para la ubicación y linaje de datos dentro de [!DNL Experience Platform].
* [Ingesta](../../../../ingestion/batch-ingestion/overview.md)por lotes: La API de inserción de lotes permite ingestar datos en [!DNL Experience Platform] archivos por lotes.
* [Simuladores](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a un sistema de éxito de cliente mediante la [!DNL Flow Service] API.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Creación de una clase y un esquema XDM ad-hoc

Para introducir datos externos [!DNL Platform] a través de conectores de origen, se debe crear una clase y un esquema XDM ad-hoc para los datos de origen sin procesar.

Para crear una clase ad-hoc y un esquema, siga los pasos descritos en el tutorial [de esquema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Al crear una clase ad-hoc, todos los campos encontrados en los datos de origen deben describirse dentro del cuerpo de la solicitud.

Siga los pasos descritos en la guía para desarrolladores hasta que haya creado un esquema ad-hoc. El identificador único (`$id`) del esquema ad-hoc es necesario para continuar con el siguiente paso de este tutorial.

## Creación de una conexión de origen {#source}

Con la creación de un esquema XDM ad-hoc, ahora se puede crear una conexión de origen mediante una solicitud POST a la [!DNL Flow Service] API. Una conexión de origen consiste en un ID de conexión, un archivo de datos de origen y una referencia al esquema que describe los datos de origen.

Para crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para los conectores **basados en** archivos:

| Data.format | Valor de enumeración |
| ----------- | ---------- |
| Archivos delimitados | `delimited` |
| Archivos JSON | `json` |
| Archivos de parquet | `parquet` |

Para todos los conectores **basados en** tablas, utilice el valor enum: `tabular`.

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
        "name": "Source connection for Customer Success",
        "baseConnectionId": "f1da3694-38a9-403d-9a36-9438a9203d42",
        "description": "Source connection for a Customer Success connector",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/classes/5d032b2230d5495aef49437d04d1c5fac4788b17ae85bf93",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Account"
        },
        "connectionSpec": {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `baseConnectionId` | ID de conexión única del sistema de éxito de clientes de terceros al que accede. |
| `data.schema.id` | El `$id` funcionamiento del esquema XDM ad-hoc. |
| `params.path` | Ruta del archivo de origen. |
| `connectionSpec.id` | ID de especificación de conexión asociada con el sistema de éxito de clientes de terceros específico. Consulte el [apéndice](#appendix) para obtener una lista de los ID de especificaciones de conexión. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en pasos posteriores para crear una conexión de destinatario.

```json
{
    "id": "17faf955-2cf8-4b15-baf9-552cf88b1540",
    "etag": "\"2900a761-0000-0200-0000-5ed18cea0000\""
}
```

## Creación de un esquema destinatario XDM {#target}

En pasos anteriores, se creó un esquema XDM ad-hoc para estructurar los datos de origen. Para que los datos de origen se utilicen en [!DNL Platform], también se debe crear un esquema de destinatario para estructurar los datos de origen según sus necesidades. El esquema de destinatario se utiliza para crear un [!DNL Platform] conjunto de datos en el que se incluyen los datos de origen. Este esquema XDM de destinatario también amplía la clase de Perfil individual XDM.

Se puede crear un esquema XDM de destinatario realizando una solicitud POST a la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquema.

Si prefiere utilizar la interfaz de usuario en [!DNL Experience Platform], el tutorial [Editor de](../../../../xdm/tutorials/create-schema-ui.md) Esquemas proporciona instrucciones paso a paso para realizar acciones similares en el Editor de Esquemas.

**Formato API**

```http
POST /tenant/schemas
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
        "title": "Target schema for a Customer Success connector",
        "description": "Target schema for Database",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:altId": "_{TENANT_ID}.schemas.b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Customer Success connector",
    "type": "object",
    "description": "Target schema for Database",
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
        "repo:createdDate": 1590791550228,
        "repo:lastModifiedDate": 1590791550228,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "d730441903b95425145d9c742647ab4426d86549159182913e5f99cc904be5b1",
        "meta:globalLibVersion": "1.10.4.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creación de un conjunto de datos de destinatario

Se puede crear un conjunto de datos de destinatario realizando una solicitud POST a la API [de servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo, proporcionando el ID del esquema de destinatario dentro de la carga útil.

**Formato API**

```http
POST catalog/dataSets
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
        "name": "Target dataset for a Customer Success connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schemaRef.id` | El `$id` del esquema XDM de destinatario. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado en el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API. Almacene el ID del conjunto de datos de destinatario como se requiere en pasos posteriores para crear una conexión de destinatario y un flujo de datos.

```json
[
    "@/dataSets/5ed18e0f4f90b719196f44a9"
]
```

## Creación de una conexión de destinatario

Una conexión de destinatario representa la conexión al destino en el que aterrizan los datos ingestados. Para crear una conexión de destinatario, debe proporcionar el ID de especificación de conexión fijo asociado con el lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos un esquema de destinatario un conjunto de datos de destinatario y el ID de especificación de conexión con el lago de datos. Con estos identificadores, puede crear una conexión de destinatario utilizando la [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen de entrada.

**Formato API**

```http
POST /targetConnections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for CS",
        "description": "Target Connection for CS",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
            "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `data.schema.id` | El `$id` del esquema XDM de destinatario. |
| `params.dataSetId` | ID del conjunto de datos de destinatario. |
| `connectionSpec.id` | ID de especificación de conexión fija al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destinatario. Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Crear una asignación {#mapping}

Para que los datos de origen se puedan ingerir en un conjunto de datos de destinatario, primero deben asignarse al esquema de destinatario al que se adhiere el conjunto de datos de destinatario. Esto se consigue realizando una solicitud POST a la [!DNL Conversion Service] API con asignaciones de datos definidas en la carga útil de la solicitud.

**Formato API**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "CreatedDate",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
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
    "id": "7c3547d3cfc14f568a51c32b4c0ed739",
    "version": 0,
    "createdDate": 1590792069173,
    "modifiedDate": 1590792069173,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Recuperar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de las fuentes y de traerlos a Platform. Para crear un flujo de datos, primero debe obtener las especificaciones de flujo de datos mediante una solicitud GET a la API de servicio de flujo. Las especificaciones de flujo de datos son responsables de recopilar datos de un sistema de éxito de clientes de terceros.

**Formato API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos que es responsable de traer datos del sistema de éxito del cliente a [!DNL Platform]. Este ID es necesario en el paso siguiente para crear un nuevo flujo de datos.

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

El último paso para recopilar datos es crear un flujo de datos. En este punto, debe tener preparados los siguientes valores obligatorios:

* [ID de conexión de origen](#source)
* [ID de conexión de Destinatario](#target)
* [ID de asignación](#mapping)
* [Id. de especificación de flujo de datos](#specs)

Para programar una ingestión, primero debe establecer el valor de tiempo de inicio en hora de generación en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day`o `week`. El valor de intervalo designa el período entre dos ingestas consecutivas y la creación de una ingestión única no requiere que se establezca un intervalo. Para todas las demás frecuencias, el valor del intervalo debe establecerse en igual o bueno que `15`.

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
        "name": "Creating a dataflow for a Customer Success connector",
        "description": "Creating a dataflow for a Customer Success connector",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "17faf955-2cf8-4b15-baf9-552cf88b1540"
        ],
        "targetConnectionIds": [
            "bc36ecd6-3b04-4067-b6ec-d63b04b0673d"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "date-time"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7c3547d3cfc14f568a51c32b4c0ed739",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590792316",
            "frequency": "minute",
            "interval": "15",
            "backfill": "true"
        }
    }'
```

**Respuesta**

Una respuesta correcta devuelve el ID `id` del flujo de datos recién creado.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | ID de especificación de flujo recuperado en el paso anterior. |
| `sourceConnectionIds` | ID de conexión de origen recuperado en un paso anterior. |
| `targetConnectionIds` | El ID de conexión de destinatario recuperado en un paso anterior. |
| `transformations.params.mappingId` | El ID de asignación recuperado en un paso anterior. |
| `scheduleParams.startTime` | La hora de inicio del flujo de datos en tiempo de generación en segundos. |
| `scheduleParams.frequency` | Los valores de frecuencia seleccionables incluyen: `once`, `minute`, `hour`, `day`o `week`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. No se requiere el intervalo cuando la frecuencia se establece como `once` y debe ser buena o igual a `15` para otros valores de frecuencia. |

## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de origen para recopilar datos de un sistema de éxito del cliente de forma programada. Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general sobre el Perfil del cliente en tiempo real](../../../../profile/home.md)
* [Información general sobre el área de trabajo de ciencias de datos](../../../../data-science-workspace/home.md)

## Apéndice

La sección siguiente lista los diferentes conectores de origen de almacenamiento de nube y sus especificaciones de conexiones.

### Especificación de conexión

| Nombre del conector | Especificación de conexión |
| -------------- | --------------- |
| [!DNL Salesforce Service Cloud] | `cb66ab34-8619-49cb-96d1-39b37ede86ea` |
| [!DNL ServiceNow] | `eb13cb25-47ab-407f-ba89-c0125281c563` |