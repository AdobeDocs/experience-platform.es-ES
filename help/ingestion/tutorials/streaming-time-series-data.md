---
keywords: Experience Platform;inicio;temas populares;ingesta de transmisión;ingesta;datos de series temporales;datos de series temporales de transmisión;
solution: Experience Platform
title: Transmisión de datos de series temporales mediante API de ingesta de transmisión
topic-legacy: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, que forman parte de las API del servicio de ingesta de datos de Adobe Experience Platform.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: cedc53b78ea8eb8f3e93178b60ebe49b90c11650
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Transmisión de datos de series temporales mediante API de ingesta de transmisión

Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, que forman parte de Adobe Experience Platform [!DNL Data Ingestion Service] API.

## Primeros pasos

Este tutorial requiere conocimientos prácticos de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil unificado y de cliente en tiempo real basado en datos agregados de varias fuentes.
- [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md): Una guía completa que cubre cada uno de los extremos disponibles del [!DNL Schema Registry] y cómo realizar llamadas a ellos. Esto incluye conocer su `{TENANT_ID}`, que aparece en las llamadas a lo largo de este tutorial, así como saber cómo crear esquemas, que se utiliza para crear un conjunto de datos para la ingesta.

Además, este tutorial requiere que ya haya creado una conexión de flujo continuo. Para obtener más información sobre la creación de una conexión de flujo continuo, lea la [crear un tutorial de conexión de flujo continuo](./create-streaming-connection.md).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../landing/api-guide.md).

## Componer un esquema basado en la clase XDM ExperienceEvent

Para crear un conjunto de datos, primero debe crear un nuevo esquema que implemente la variable [!DNL XDM ExperienceEvent] Clase . Para obtener más información sobre cómo crear esquemas, lea la [Guía del desarrollador de API del Registro del Esquema](../../xdm/api/getting-started.md).

**Formato de API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `title` | El nombre que desea utilizar para el esquema. Este nombre debe ser único. |
| `description` | Una descripción significativa del esquema que está creando. |
| `meta:immutableTags` | En este ejemplo, la variable `union` se usa para mantener los datos en [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles del esquema recién creado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
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
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. Para obtener más información sobre el ID del inquilino, lea la [guía de registro de esquema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Tome nota de la `$id` , así como el `version` , ya que ambos se utilizarán al crear su conjunto de datos.

## Definir un descriptor de identidad principal para el esquema

A continuación, añada un [descriptor de identidad](../../xdm/api/descriptors.md) al esquema creado anteriormente, utilizando el atributo de dirección de correo electrónico de trabajo como identificador principal. Al hacerlo, se producirán dos cambios:

1. La dirección de correo electrónico de trabajo se convertirá en un campo obligatorio. Esto significa que los mensajes enviados sin este campo no se validan correctamente y no se incorporan.

2. [!DNL Real-time Customer Profile] utilizará la dirección de correo electrónico de trabajo como identificador para ayudar a unir más información sobre ese individuo.

### Solicitud

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | La variable `$id` que recibió anteriormente al componer el esquema. Debería tener un aspecto similar al siguiente: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Códigos de área de nombres de identidad**
>
> Asegúrese de que los códigos sean válidos: el ejemplo anterior utiliza &quot;correo electrónico&quot;, que es un área de nombres de identidad estándar. Otras áreas de nombres de identidad estándar usadas con frecuencia se pueden encontrar dentro de la variable [Preguntas frecuentes sobre el servicio de identidad](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Si desea crear un área de nombres personalizada, siga los pasos descritos en la sección [información general del área de nombres de identidad](../../identity-service/home.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con información sobre el área de nombres de identidad principal recién creada para el esquema.

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
    "imsOrg": "{ORG_ID}"
}
```

## Crear un conjunto de datos para datos de series temporales

Una vez que haya creado el esquema, deberá crear un conjunto de datos para introducir los datos de registro.

>[!NOTE]
>
>Este conjunto de datos estará habilitado para **[!DNL Real-time Customer Profile]** y **[!DNL Identity]** estableciendo las etiquetas adecuadas.

**Formato de API**

```http
POST /catalog/dataSets
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
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


## Creación de una conexión de flujo continuo

Después de crear el esquema y el conjunto de datos, debe crear una conexión de flujo continuo para introducir los datos.

Para obtener más información sobre la creación de una conexión de flujo continuo, lea la [crear un tutorial de conexión de flujo continuo](./create-streaming-connection.md).

## Ingesta de datos de series temporales en la conexión de flujo continuo

Con el conjunto de datos, la conexión de flujo continuo y el flujo de datos creado, puede ingerir registros JSON con formato XDM para introducir datos de series temporales en [!DNL Platform].

**Formato de API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | La variable `id` de la conexión de flujo continuo recién creada. |
| `syncValidation` | Un parámetro de consulta opcional diseñado para fines de desarrollo. Si está configurado como `true`, se puede utilizar para comentarios inmediatos a fin de determinar si la solicitud se ha enviado correctamente. De forma predeterminada, este valor se establece en `false`. Tenga en cuenta que si establece este parámetro de consulta en `true` que la tarifa de la solicitud estará limitada a 60 veces por minuto `CONNECTION_ID`. |

**Solicitud**

La ingesta de datos de series temporales en una conexión de flujo continuo se puede realizar con o sin el nombre de origen.

La solicitud de ejemplo siguiente incorpora datos de series temporales con un nombre de origen ausente en Platform. Si en los datos falta el nombre del origen, se agregará el ID de origen de la definición de conexión de flujo continuo.

Ambas `xdmEntity._id` y `xdmEntity.timestamp` son campos obligatorios para los datos de series temporales. La variable `xdmEntity._id` representa un identificador único para el propio registro, **not** un ID exclusivo de la persona o dispositivo cuyo registro es.

Deberá generar su propio `xdmEntity._id` y `xdmEntity.timestamp` para el registro de una manera que se mantenga consistente si alguna vez se necesita volver a introducir el registro. Lo ideal es que el sistema de origen contenga estos valores. Si no hay un ID disponible, considere la posibilidad de concatenar valores de otros campos del registro para crear un valor único que se pueda regenerar de forma coherente a partir del registro cuando se vuelva a introducir.

>[!NOTE]
>
>La siguiente llamada de API hace lo siguiente **not** requieren encabezados de autenticación.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
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

Si desea incluir un nombre de origen, el siguiente ejemplo muestra cómo lo incluiría.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | La variable `inletId` de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado en el servidor para el registro que acaba de enviar. Este ID ayuda a los Adobes a rastrear el ciclo vital de este registro a través de varios sistemas y con depuración. |
| `receivedTimeMs`: Marca de tiempo (época en milisegundos) que muestra la hora a la que se recibió la solicitud. |
| `syncValidation.status` | Desde el parámetro de consulta `syncValidation=true` se ha añadido, este valor aparecerá. Si la validación se ha realizado correctamente, el estado será `pass`. |

## Recuperar los datos de series temporales recién introducidos

Para validar los registros ingestados anteriormente, puede utilizar la variable [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar los datos de la serie temporal. Esto se puede hacer mediante una solicitud de GET al `/access/entities` y utilizando parámetros de consulta opcionales. Se pueden usar varios parámetros, separados por el símbolo &amp;.&quot;

>[!NOTE]
>
>Si el ID de la directiva de combinación no está definido y la variable `schema.name` o `relatedSchema.name` es `_xdm.context.profile`, [!DNL Profile Access] recuperará **all** identidades relacionadas.

**Formato de API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parámetro | Descripción |
| --------- | ----------- |
| `schema.name` | **Requerido.** Nombre del esquema al que se accede. |
| `relatedSchema.name` | **Requerido.** Como está accediendo a un `_xdm.context.experienceevent`, este valor especifica el esquema de la entidad de perfil a la que están relacionados los eventos de series temporales. |
| `relatedEntityId` | El ID de la entidad relacionada. Si se proporciona, también debe proporcionar el área de nombres de la entidad. |
| `relatedEntityIdNS` | El espacio de nombres del ID que está intentando recuperar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de las entidades solicitadas. Como puede ver, estos son los mismos datos de series temporales que se incorporaron anteriormente.

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

Al leer este documento, ahora puede comprender cómo introducir datos de registro en [!DNL Platform] uso de conexiones de flujo continuo. Puede intentar realizar más llamadas con valores diferentes y recuperar los valores actualizados. Además, puede empezar a supervisar los datos introducidos mediante [!DNL Platform] IU. Para obtener más información, lea la [monitorización de la ingesta de datos](../quality/monitor-data-ingestion.md) guía.

Para obtener más información sobre la transmisión por secuencias en general, lea la [información general sobre la ingesta de transmisión](../streaming-ingestion/overview.md).
