---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recopilación de datos de almacenamiento en la nube mediante las API y los conectores de origen
topic: overview
translation-type: tm+mt
source-git-commit: 2a8e8f2deffca06782f0ad9b8154ee763c05f06d
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 1%

---


# Recopilación de datos de almacenamiento en la nube mediante las API y los conectores de origen

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

En este tutorial se explican los pasos para recuperar datos de un almacenamiento de nube de terceros y llevarlos a la plataforma mediante conectores de origen y API.

## Primeros pasos

Este tutorial requiere que tenga acceso a un almacenamiento de nube de terceros a través de una conexión válida e información sobre el archivo que desea introducir en Platform, incluida la ruta y la estructura del archivo. Si no dispone de esta información, consulte el tutorial sobre la [exploración de un almacenamiento de nube de terceros mediante la API](../explore/cloud-storage.md) de servicio de flujo antes de intentar este tutorial.

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Guía](../../../../xdm/api/getting-started.md)para desarrolladores de Esquema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de Esquema. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
- [Servicio](../../../../catalog/home.md)de catálogo: Catalog es el sistema de registros para la ubicación y el linaje de los datos dentro de la plataforma de experiencia.
- [Ingesta](../../../../ingestion/batch-ingestion/overview.md)por lotes: La API de inserción de lotes permite ingestar datos en la plataforma de experiencias como archivos por lotes.
- [Simuladores](../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un almacenamiento de nube mediante la API de servicio de flujo.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

- Content-Type: `application/json`

## Creación de una clase y un esquema XDM ad-hoc

Para poder introducir datos externos en la plataforma mediante conectores de origen, se debe crear una clase y un esquema XDM ad-hoc para los datos de origen sin procesar.

Para crear una clase ad-hoc y un esquema, siga los pasos descritos en el tutorial [de esquema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Al crear una clase ad-hoc, todos los campos encontrados en los datos de origen deben describirse dentro del cuerpo de la solicitud.

Siga los pasos descritos en la guía para desarrolladores hasta que haya creado un esquema ad-hoc. El identificador único (`$id`) del esquema ad-hoc es necesario para continuar con el siguiente paso de este tutorial.

## Creación de una conexión de origen {#source}

Con la creación de un esquema XDM ad-hoc, ahora se puede crear una conexión de origen mediante una solicitud POST a la API de servicio de flujo. Una conexión de origen consiste en un ID de conexión, un archivo de datos de origen y una referencia al esquema que describe los datos de origen.

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
        "name": "Test source connection for a Cloud Storage connector",
        "baseConnectionId": "ac33bd66-1565-4915-b3bd-6615657915c4",
        "description": "Test source connection for a Cloud Storage connector",
        "data": {
            "format": "delimited",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/22a4ab59462a64de551d42dd10ec1f19d8d7246e3f90072a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/backfil/data8.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | ID de conexión única del sistema de almacenamiento en la nube de terceros al que está accediendo. |
| `data.schema.id` | ID del esquema XDM ad-hoc. |
| `params.path` | Ruta del archivo de origen al que está accediendo. |
| `connectionSpec.id` | El ID de especificación de conexión asociado a su sistema de almacenamiento en la nube de terceros específico. Consulte el [apéndice](#appendix) para obtener una lista de los ID de especificaciones de conexión. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "8bae595c-8548-4716-ae59-5c85480716e9",
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Creación de un esquema destinatario XDM {#target}

En pasos anteriores, se creó un esquema XDM ad-hoc para estructurar los datos de origen. Para que los datos de origen se utilicen en Platform, también se debe crear un esquema de destinatario para estructurar los datos de origen según sus necesidades. El esquema de destinatario se utiliza para crear un conjunto de datos de la plataforma en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destinatario realizando una solicitud POST a la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquema.

Si prefiere utilizar la interfaz de usuario en la plataforma de experiencias, el tutorial [Editor de](../../../../xdm/tutorials/create-schema-ui.md) Esquemas proporciona instrucciones paso a paso para realizar acciones similares en el Editor de Esquemas.

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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:altId": "_{TENANT_ID}.schemas.e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Cloud Storage connector",
    "type": "object",
    "description": "Target schema for Cloud Storage",
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
        "repo:createdDate": 1589398474190,
        "repo:lastModifiedDate": 1589398474190,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "f07723475e933dc30ed411d97986a36f13aa20c820463dd8cf7b74e63f4e7801",
        "meta:globalLibVersion": "1.10.1.1"
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
        "name": "Target dataset for a Cloud Storage connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `schemaRef.id` | ID del esquema XDM de destinatario. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado en el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API. El ID del conjunto de datos de destinatario es necesario en pasos posteriores para crear una conexión de destinatario y un flujo de datos.

```json
[
    "@/dataSets/5ebc4be8590b1b191a8dc4ca"
]
```

## Creación de una conexión de destinatario

Una conexión de destinatario representa la conexión al destino en el que aterrizan los datos ingestados. Para crear una conexión de destinatario, debe proporcionar el ID de especificación de conexión fijo asociado con el lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos un esquema de destinatario un conjunto de datos de destinatario y el ID de especificación de conexión con el lago de datos. Con estos identificadores, puede crear una conexión de destinatario mediante la API de servicio de flujo para especificar el conjunto de datos que contendrá los datos de origen entrantes.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ebc4be8590b1b191a8dc4ca"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
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

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destinatario. Este ID se requiere en pasos posteriores.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Crear una asignación {#mapping}

Para que los datos de origen se puedan ingerir en un conjunto de datos de destinatario, primero deben asignarse al esquema de destinatario al que se adhiere el conjunto de datos de destinatario. Esto se logra realizando una solicitud POST al servicio de conversión con asignaciones de datos definidas dentro de la carga útil de la solicitud.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
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
                "destinationXdmPath": "_id",
                "sourceAttribute": "id",
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

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "febec6a6785e45ea9ed594422cc483d7",
    "version": 0,
    "createdDate": 1589398562232,
    "modifiedDate": 1589398562232,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Recuperar especificaciones de flujo de datos {#specs}

Un flujo de datos es responsable de recopilar datos de las fuentes y de traerlos a la Plataforma. Para crear un flujo de datos, primero debe obtener las especificaciones de flujo de datos responsables de recopilar datos de almacenamiento en la nube.

**Formato API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la especificación de flujo de datos que es responsable de traer datos de su almacenamiento de nube a la plataforma. La respuesta incluye un ID de especificación de flujo único. Este ID es necesario en el paso siguiente para crear un nuevo flujo de datos.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
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
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
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

El último paso para recopilar datos de almacenamiento en la nube es crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores necesarios:

- [ID de conexión de origen](#source)
- [ID de conexión de Destinatario](#target)
- [ID de asignación](#mapping)
- [Id. de especificación de flujo de datos](#specs)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud POST mientras proporciona los valores mencionados anteriormente en la carga útil.

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
        "name": "Cloud Storage flow to AEP",
        "description": "Cloud Storage flow to AEP",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8bae595c-8548-4716-ae59-5c85480716e9"
        ],
        "targetConnectionIds": [
            "1f5af99c-f1ef-4076-9af9-9cf1ef507678"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "febec6a6785e45ea9ed594422cc483d7",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1589398646",
            "frequency":"minute",
            "interval":"30"
        }
    }'
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

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de origen para recopilar datos de su almacenamiento de nube de forma programada. Los datos entrantes ahora se pueden utilizar en los servicios de plataforma descendente, como Perfil del cliente en tiempo real y Área de trabajo de ciencias de datos. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../../data-science-workspace/home.md)

## Apéndice {#appendix}

La sección siguiente lista los diferentes conectores de origen de almacenamiento de nube y sus especificaciones de conexiones.

### Especificación de conexión

| Nombre del conector | Especificación de conexión |
| -------------- | --------------- |
| Amazon S3 (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Blob de Azure (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Azure Data Lake Almacenamiento Gen2 (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Centros de Evento de Azure (centros de Evento) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Almacenamiento de archivos de Azure | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| Almacenamiento de Google Cloud | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| HDFS | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |