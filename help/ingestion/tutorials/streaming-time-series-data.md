---
keywords: Experience Platform;home;popular topics;streaming ingestion;ingestion;time series data;stream time series data;
solution: Experience Platform
title: Transmisión de datos de series temporales
topic: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las API de servicio de inserción de datos de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: fce215edb99cccc8be0109f8743c9e56cace2be0
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 2%

---


# Transmitir datos de series temporales a Adobe Experience Platform

Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las [!DNL Data Ingestion Service] API de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!Modelo de datos de experiencia DNL (XDM)]](../../xdm/home.md): Marco normalizado por el cual [!DNL Platform] se organizan los datos de experiencia.
- [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [Guía](../../xdm/api/getting-started.md)para desarrolladores de esquema Registry: Una guía completa que cubre cada uno de los extremos disponibles de la [!DNL Schema Registry] API y cómo realizar llamadas a ellos. Esto incluye saber cuál es su `{TENANT_ID}`función, que aparece en las llamadas a lo largo de este tutorial, así como también saber cómo crear esquemas, que se utiliza para crear un conjunto de datos para la ingestión.

Además, este tutorial requiere que ya haya creado una conexión de flujo. Para obtener más información sobre la creación de una conexión de flujo continuo, lea el tutorial [](./create-streaming-connection.md)Crear una conexión de flujo continuo.

Las siguientes secciones proporcionan información adicional que debe conocer para realizar llamadas a las API de inserción de flujo continuo.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Redactar un esquema basado en la clase XDM ExperienceEvent

Para crear un conjunto de datos, primero deberá crear un nuevo esquema que implemente la [!DNL XDM ExperienceEvent] clase. Para obtener más información sobre cómo crear esquemas, consulte la guía [para desarrolladores de la API de registro de](../../xdm/api/getting-started.md)Esquema.

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
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
| `meta:immutableTags` | En este ejemplo, la `union` etiqueta se utiliza para mantener los datos en [[!DNL Perfil del cliente en tiempo real]](../../profile/home.md). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles del esquema recién creado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "{SCHEMA_VERSION}",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que cree tengan el espacio de nombres correcto y estén contenidos en la organización de IMS. Para obtener más información sobre el Id. del inquilino, lea la guía [del registro de](../../xdm/api/getting-started.md#know-your-tenant-id)esquemas. |

Tenga en cuenta tanto los atributos `$id` como los `version` atributos, ya que ambos se utilizarán al crear el conjunto de datos.

## Definir un descriptor de identidad principal para el esquema

A continuación, agregue un descriptor [de](../../xdm/api/descriptors.md) identidad al esquema creado anteriormente, utilizando el atributo de dirección de correo electrónico de trabajo como identificador principal. Si lo hace, se producirán dos cambios:

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
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
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
>Códigos **de Área de nombres de identidad &#x200B;**
>
> Asegúrese de que los códigos sean válidos; el ejemplo anterior utiliza &quot;correo electrónico&quot;, que es una Área de nombres de identidad estándar. Otras Áreas de nombres de identidad estándar de uso común se encuentran en las preguntas más frecuentes [de](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)Identity Service.
>
> Si desea crear una Área de nombres personalizada, siga los pasos descritos en la descripción general [de la Área de nombres de](../../identity-service/home.md)identidad.

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con información sobre la Área de nombres de identidad principal recién creada para el esquema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Crear un conjunto de datos para datos de series temporales

Una vez que haya creado el esquema, deberá crear un conjunto de datos para ingestar los datos del registro.

>[!NOTE]
>
>Este conjunto de datos se habilitará para **[!DNL Real-time Customer Profile]** y **[!DNL Identity]** configurando las etiquetas correspondientes.

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Ingesta de datos de series temporales a la conexión de flujo continuo

Con el conjunto de datos y la conexión de flujo en su lugar, puede ingestar registros JSON con formato XDM para ingestar datos de series temporales dentro de [!DNL Platform].

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El `id` valor de la conexión de flujo recién creada. |
| `synchronousValidation` | Parámetro de consulta opcional para fines de desarrollo. Si se establece en `true`, se puede utilizar para recibir comentarios inmediatos a fin de determinar si la solicitud se ha enviado correctamente. De forma predeterminada, este valor se establece en `false`. |

**Solicitud**

>[!NOTE]
>
>Tendrá que generar sus propios `xdmEntity._id` y `xdmEntity.timestamp`. Una buena manera de generar un ID es utilizar un UUID. Además, la siguiente llamada de API **no requiere** encabezados de autenticación.


```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
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
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
            }
        }
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la nueva transmisión [!DNL Profile].

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
| `receivedTimeMs`:: Marca de tiempo (epoch en milisegundos) que muestra la hora a la que se recibió la solicitud. |
| `synchronousValidation.status` | Desde que se agregó el parámetro de consulta `synchronousValidation=true` , aparecerá este valor. Si la validación se ha realizado correctamente, el estado será `pass`. |

## Recuperar los datos de serie temporal recién ingestados

Para validar los registros ingestados anteriormente, puede utilizar la [[!DNL API de acceso a Perfil]](../../profile/api/entities.md) para recuperar los datos de la serie temporal. Esto se puede realizar mediante una solicitud de GET al extremo y utilizando parámetros de consulta opcionales `/access/entities` . Se pueden utilizar varios parámetros, separados por signos ampersands (&amp;).&quot;

>[!NOTE]
>
>Si el ID de directiva de combinación no está definido y el `schema.name` valor o `relatedSchema.name` está `_xdm.context.profile`, [!DNL Profile Access] buscará **todas** las identidades relacionadas.

**Formato API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parámetro | Descripción |
| --------- | ----------- |
| `schema.name` | **Requerido.** Nombre del esquema al que está accediendo. |
| `relatedSchema.name` | **Requerido.** Dado que está accediendo a un `_xdm.context.experienceevent`, este valor especifica el esquema de la entidad de perfil a la que están relacionados los eventos de series temporales. |
| `relatedEntityId` | ID de la entidad relacionada. Si se proporciona, también debe proporcionar la Área de nombres de entidad. |
| `relatedEntityIdNS` | Área de nombres del ID que intenta recuperar. |

**Solicitud**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de las entidades solicitadas. Como puede ver, se trata de los mismos datos de series temporales que antes se ingirieron.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Pasos siguientes

Al leer este documento, ahora puede comprender cómo ingerir datos de registro en [!DNL Platform] conexiones de flujo continuo. Puede intentar realizar más llamadas con diferentes valores y recuperar los valores actualizados. Además, puede supervisar en inicio los datos que ingrese mediante la [!DNL Platform] interfaz de usuario. Para obtener más información, lea la guía de [monitorización de la ingestión](../quality/monitor-data-flows.md) de datos.

Para obtener más información sobre la transmisión por secuencias de ingestión en general, lea la información general sobre la [transmisión por secuencias](../streaming-ingestion/overview.md).
