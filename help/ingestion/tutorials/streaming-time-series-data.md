---
keywords: Experience Platform;inicio;temas populares;ingesta de transmisión;ingesta;datos de series temporales;datos de series temporales de transmisión;
solution: Experience Platform
title: Transmitir datos de series temporales mediante las API de ingesta de transmisión
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, parte de las API del servicio de ingesta de datos de Adobe Experience Platform.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 2%

---

# Transmitir datos de series temporales mediante las API de ingesta de transmisión

Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, parte de las API de Adobe Experience Platform [!DNL Data Ingestion Service].

## Introducción

Este tutorial requiere un conocimiento práctico de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real en función de los datos agregados de varios orígenes.
- [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md): Una guía completa que cubre cada uno de los extremos disponibles de la API [!DNL Schema Registry] y cómo realizar llamadas a ellos. Esto incluye conocer su `{TENANT_ID}`, que aparece en las llamadas a través de este tutorial, así como saber cómo crear esquemas, que se utiliza en la creación de un conjunto de datos para la ingesta.

Además, este tutorial requiere que ya haya creado una conexión de flujo continuo. Para obtener más información sobre cómo crear una conexión de flujo continuo, lea el [tutorial Crear una conexión de flujo continuo](./create-streaming-connection.md).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../landing/api-guide.md).

## Componga un esquema basado en la clase XDM ExperienceEvent.

Para crear un conjunto de datos, primero deberá crear un nuevo esquema que implemente la clase [!DNL XDM ExperienceEvent]. Para obtener más información sobre cómo crear esquemas, lea la [Guía para desarrolladores de API de Registro de esquemas](../../xdm/api/getting-started.md).

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
| `title` | El nombre que desee utilizar para el esquema. Este nombre debe ser único. |
| `description` | Una descripción significativa para el esquema que está creando. |
| `meta:immutableTags` | En este ejemplo, la etiqueta `union` se usa para mantener los datos en [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

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
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización. Para obtener más información acerca del id. de inquilino, lea la [guía de registro de esquemas](../../xdm/api/getting-started.md#know-your-tenant-id). |

Tome nota de `$id`, así como de los atributos de `version`, ya que ambos se utilizarán al crear el conjunto de datos.

## Definir un descriptor de identidad principal para el esquema

A continuación, agregue un [descriptor de identidad](../../xdm/api/descriptors.md) al esquema creado anteriormente, utilizando el atributo de dirección de correo electrónico de trabajo como identificador principal. Al hacerlo, se producirán dos cambios:

1. La dirección de correo electrónico de trabajo pasará a ser un campo obligatorio. Esto significa que los mensajes enviados sin este campo no superarán la validación y no se incorporarán.

2. [!DNL Real-Time Customer Profile] usará la dirección de correo electrónico de trabajo como identificador para ayudar a unir más información sobre ese individuo.

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
| `{SCHEMA_REF_ID}` | `$id` que recibió anteriormente cuando compuso el esquema. Debe tener un aspecto similar al siguiente: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>**Códigos de área de nombres de identidad**
>
> Asegúrese de que los códigos sean válidos: el ejemplo anterior utiliza &quot;correo electrónico&quot;, que es un área de nombres de identidad estándar. Encontrará otras áreas de nombres de identidad estándar usadas con frecuencia en [Preguntas frecuentes sobre el servicio de identidad](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Si desea crear un área de nombres personalizada, siga los pasos descritos en la [descripción general del área de nombres de identidad](../../identity-service/home.md).

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

Una vez creado el esquema, deberá crear un conjunto de datos para introducir datos de registro.

>[!NOTE]
>
>Este conjunto de datos se habilitará para **[!DNL Real-Time Customer Profile]** y **[!DNL Identity]** mediante la configuración de las etiquetas adecuadas.

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

Después de crear el esquema y el conjunto de datos, deberá crear una conexión de flujo continuo para introducir los datos.

Para obtener más información sobre cómo crear una conexión de flujo continuo, lea el [tutorial Crear una conexión de flujo continuo](./create-streaming-connection.md).

## Ingesta de datos de series temporales en la conexión de flujo continuo

Con el conjunto de datos, la conexión de flujo continuo y el flujo de datos creados, puede introducir registros JSON con formato XDM para introducir datos de series temporales dentro de [!DNL Platform].

**Formato de API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de su conexión de flujo continuo recién creada. |
| `syncValidation` | Un parámetro de consulta opcional pensado para fines de desarrollo. Si se establece en `true`, se puede usar para comentarios inmediatos a fin de determinar si la solicitud se envió correctamente. De manera predeterminada, este valor está establecido en `false`. Tenga en cuenta que si establece este parámetro de consulta en `true`, la tasa de la solicitud estará limitada a 60 veces por minuto por `CONNECTION_ID`. |

**Solicitud**

La ingesta de datos de series temporales en una conexión de flujo continuo se puede realizar con o sin el nombre de origen.

La solicitud de ejemplo siguiente ingiere datos de series temporales con un nombre de origen que falta en Platform. Si a los datos les falta el nombre de origen, agregarán el ID de origen de la definición de conexión de flujo continuo.

Tanto `xdmEntity._id` como `xdmEntity.timestamp` son campos obligatorios para los datos de series temporales. El atributo `xdmEntity._id` representa un identificador único para el registro en sí, **no** un identificador único de la persona o dispositivo de cuyo registro se trate.

Necesitará generar sus propios `xdmEntity._id` y `xdmEntity.timestamp` para el registro de manera que se mantenga consistente si es necesario volver a ingerir el registro. Lo ideal es que el sistema de origen contenga estos valores. Si no hay ningún ID disponible, considere la posibilidad de concatenar valores de otros campos del registro para crear un valor único que se pueda regenerar de forma coherente desde el registro al volver a ingerirlo.

>[!NOTE]
>
>La siguiente llamada de API **no** requiere encabezados de autenticación.

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

Si desea incluir un nombre de origen, en el siguiente ejemplo se muestra cómo incluirlo.

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

Una respuesta correcta devuelve el estado HTTP 200 con detalles del [!DNL Profile] recién transmitido.

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
| `{CONNECTION_ID}` | El `inletId` de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado del lado del servidor para el registro que acaba de enviar. Este ID ayuda al Adobe a rastrear el ciclo de vida de este registro a través de varios sistemas y con la depuración. |
| `receivedTimeMs`: marca de tiempo (epoch en milisegundos) que muestra a qué hora se recibió la solicitud. |
| `syncValidation.status` | Dado que se agregó el parámetro de consulta `syncValidation=true`, este valor aparecerá. Si la validación se realizó correctamente, el estado será `pass`. |

## Recuperar los datos de series temporales recién introducidos

Para validar los registros ingeridos anteriormente, puede utilizar [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar los datos de la serie temporal. Esto se puede hacer usando una solicitud de GET al extremo `/access/entities` y usando parámetros de consulta opcionales. Se pueden utilizar varios parámetros, separados por el símbolo &amp;.&quot;

>[!NOTE]
>
>Si el id. de la política de combinación no está definido y `schema.name` o `relatedSchema.name` es `_xdm.context.profile`, [!DNL Profile Access] recuperará **todas** las identidades relacionadas.

**Formato de API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parámetro | Descripción |
| --------- | ----------- |
| `schema.name` | **Requerido.** El nombre del esquema al que está accediendo. |
| `relatedSchema.name` | **Requerido.** Dado que está accediendo a `_xdm.context.experienceevent`, este valor especifica el esquema para la entidad de perfil con la que están relacionados los eventos de series temporales. |
| `relatedEntityId` | El ID de la entidad relacionada. Si se proporciona, también debe proporcionar el área de nombres de entidad. |
| `relatedEntityIdNS` | El área de nombres del ID que está intentando recuperar. |

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

Una respuesta correcta devuelve el estado HTTP 200 con detalles de las entidades solicitadas. Como puede ver, se trata de los mismos datos de series temporales que se habían introducido anteriormente.

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

Al leer este documento, ahora comprende cómo ingerir datos de registro en [!DNL Platform] mediante conexiones de flujo continuo. Puede intentar realizar más llamadas con diferentes valores y recuperar los valores actualizados. Además, puede empezar a monitorizar los datos ingeridos a través de la interfaz de usuario de [!DNL Platform]. Para obtener más información, lea la guía [supervisión de la ingesta de datos](../quality/monitor-data-ingestion.md).

Para obtener más información sobre la ingesta de transmisión en general, lea [descripción general de la ingesta de transmisión](../streaming-ingestion/overview.md).
