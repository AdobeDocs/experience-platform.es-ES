---
keywords: Experience Platform;inicio;temas populares;flujo de ingestión;ingestión;registrar datos;datos de registro de flujo;
solution: Experience Platform
title: Datos de registro de flujo mediante API de inserción de flujo
topic: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las API de servicio de inserción de datos de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 27a7855492f2f8e7a92651cd97371c904dd1561d
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 2%

---


# Transmitir datos de registros mediante API de inserción de flujo

Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las API de Adobe Experience Platform [!DNL Data Ingestion Service].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [Guía](../../xdm/api/getting-started.md) para desarrolladores de esquema Registry: Una guía completa que cubre cada uno de los extremos disponibles de la  [!DNL Schema Registry] API y cómo realizar llamadas a ellos. Esto incluye conocer su `{TENANT_ID}`, que aparece en las llamadas a través de este tutorial, así como saber cómo crear esquemas, que se utiliza para crear un conjunto de datos para la ingestión.

Además, este tutorial requiere que ya haya creado una conexión de flujo. Para obtener más información sobre la creación de una conexión de flujo continuo, lea el [tutorial de creación de una conexión de flujo](./create-streaming-connection.md).

Las siguientes secciones proporcionan información adicional que debe conocer para realizar llamadas a las API de inserción de flujo continuo.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Redactar un esquema basado en la clase [!DNL XDM Individual Profile]

Para crear un conjunto de datos, primero deberá crear un nuevo esquema que implemente la clase [!DNL XDM Individual Profile]. Para obtener más información sobre cómo crear esquemas, lea la [guía para desarrolladores de la API de registro de Esquema](../../xdm/api/getting-started.md).

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `title` | El nombre que desea usar para su esquema. Este nombre debe ser único. |
| `description` | Una descripción significativa del esquema que está creando. |
| `meta:immutableTags` | En este ejemplo, la etiqueta `union` se utiliza para mantener los datos en [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles del esquema recién creado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que cree tengan el espacio de nombres correcto y estén contenidos en la organización de IMS. Para obtener más información sobre el Id. del inquilino, lea la [guía del registro de esquemas](../../xdm/api/getting-started.md#know-your-tenant-id). |

Tenga en cuenta los atributos `$id` y `version`, ya que ambos se utilizarán al crear el conjunto de datos.

## Definir un descriptor de identidad principal para el esquema

A continuación, agregue un [descriptor de identidad](../../xdm/api/descriptors.md) al esquema creado anteriormente, utilizando el atributo de dirección de correo electrónico de trabajo como identificador principal. Si lo hace, se producirán dos cambios:

1. La dirección de correo electrónico del trabajo se convertirá en un campo obligatorio. Esto significa que los mensajes enviados sin este campo no se validarán correctamente y no se ingerirán.

2. [!DNL Real-time Customer Profile] utilizará la dirección de correo electrónico de trabajo como identificador para ayudar a reunir más información sobre esa persona.

### Solicitud

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | El `$id` que recibió anteriormente cuando compuso el esquema. Debería tener este aspecto: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Códigos de Área de nombres de identidad**
>
> Asegúrese de que los códigos sean válidos; el ejemplo anterior utiliza &quot;correo electrónico&quot;, que es una Área de nombres de identidad estándar. Otras Áreas de nombres de identidad estándar de uso común se pueden encontrar en las [preguntas frecuentes del servicio de identidad](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Si desea crear una Área de nombres personalizada, siga los pasos descritos en la [información general de la Área de nombres de identidad](../../identity-service/home.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con información sobre el descriptor de identidad principal recién creado para el esquema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Crear un conjunto de datos para los datos de registro

Una vez que haya creado el esquema, deberá crear un conjunto de datos para ingestar los datos del registro.

>[!NOTE]
>
>Este conjunto de datos se habilitará para **[!DNL Real-time Customer Profile]** y **[!DNL Identity Service]**.

**Formato API**

```http
POST /catalog/dataSets
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 y una matriz que contiene el ID del conjunto de datos recién creado con el formato `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Ingesta de datos de registro en la conexión de flujo {#ingest-data}

Con el conjunto de datos y la conexión de transmisión en su lugar, puede ingestar registros JSON con formato XDM para ingestar datos de registro en [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión de flujo creada anteriormente. |
| `synchronousValidation` | Parámetro de consulta opcional para fines de desarrollo. Si se establece en `true`, se puede utilizar para recibir comentarios inmediatos a fin de determinar si la solicitud se ha enviado correctamente. De forma predeterminada, este valor se establece en `false`. |

**Solicitud**

La ingesta de datos de registro en una conexión de flujo puede realizarse con o sin el nombre del origen.

La solicitud de ejemplo siguiente ingesta un registro con un nombre de origen que falta en Platform. Si a un registro le falta el nombre del origen, agregará el ID de origen de la definición de conexión de flujo.

>[!NOTE]
>
>La siguiente llamada de API **no** requiere encabezados de autenticación.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

Si desea incluir un nombre de origen, en el siguiente ejemplo se muestra cómo incluirlo.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la [!DNL Profile] recién transmitida.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de la conexión de flujo creada anteriormente. |
| `xactionId` | Identificador único generado por el servidor para el registro que acaba de enviar. Este ID ayuda a Adobe a rastrear el ciclo vital de este registro a través de varios sistemas y con la depuración. |
| `receivedTimeMs` | Marca de tiempo (epoch en milisegundos) que muestra la hora a la que se recibió la solicitud. |
| `synchronousValidation.status` | Dado que se agregó el parámetro de consulta `synchronousValidation=true`, aparecerá este valor. Si la validación se ha realizado correctamente, el estado será `pass`. |

## Recuperar los datos de registro recién ingestados

Para validar los registros ingestados anteriormente, puede utilizar [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar los datos del registro.

>[!NOTE]
>
>Si no se define la ID de directiva de combinación y `schema.name` o `relatedSchema.name` es `_xdm.context.profile`, [!DNL Profile Access] obtendrá **todas las identidades relacionadas**.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parámetro | Descripción |
| --------- | ----------- |
| `schema.name` | **Requerido.** Nombre del esquema al que está accediendo. |
| `entityId` | ID de la entidad. Si se proporciona, también debe proporcionar la Área de nombres de entidad. |
| `entityIdNS` | Área de nombres del ID que intenta recuperar. |

**Solicitud**

Puede revisar los datos del registro ingestados anteriormente con la siguiente solicitud de GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de las entidades solicitadas. Como puede ver, este es el mismo registro que se ingirió correctamente anteriormente.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Pasos siguientes

Al leer este documento, ahora puede comprender cómo ingerir datos de registro en [!DNL Platform] mediante conexiones de flujo continuo. Puede intentar realizar más llamadas con diferentes valores y recuperar los valores actualizados. Además, puede realizar inicios para monitorear los datos ingestados mediante la [!DNL Platform] interfaz de usuario. Para obtener más información, lea la guía [de ingestión de datos de monitoreo](../quality/monitor-data-ingestion.md).

Para obtener más información sobre la transmisión por secuencias de ingestión en general, lea la [información general sobre la transmisión por secuencias de ingestión](../streaming-ingestion/overview.md).


