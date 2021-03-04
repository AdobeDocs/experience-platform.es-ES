---
keywords: Experience Platform;inicio;temas populares;ingesta de flujo;ingesta;registrar datos;datos de registro de flujo;
solution: Experience Platform
title: Registrar datos mediante las API de ingesta de flujos
topic: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, que forman parte de las API del servicio de ingesta de datos de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 2%

---


# Transmisión de datos de registro mediante las API de ingesta de transmisión

Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, que forman parte de las API [!DNL Data Ingestion Service] de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere conocimientos prácticos de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil unificado y de cliente en tiempo real basado en datos agregados de varias fuentes.
- [Guía](../../xdm/api/getting-started.md) para desarrolladores de Schema Registry: Una guía completa que cubre cada uno de los extremos disponibles de la  [!DNL Schema Registry] API y cómo realizar llamadas a ellos. Esto incluye conocer su `{TENANT_ID}`, que aparece en las llamadas a lo largo de este tutorial, así como saber cómo crear esquemas, que se utilizan para crear un conjunto de datos para la ingesta.

Además, este tutorial requiere que ya haya creado una conexión de flujo continuo. Para obtener más información sobre la creación de una conexión de flujo continuo, lea el [tutorial de creación de una conexión de flujo continuo](./create-streaming-connection.md).

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas correctamente a las API de ingesta de transmisión.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Componer un esquema basado en la clase [!DNL XDM Individual Profile]

Para crear un conjunto de datos, primero debe crear un nuevo esquema que implemente la clase [!DNL XDM Individual Profile]. Para obtener más información sobre cómo crear esquemas, lea la [guía para desarrolladores de la API del Registro de Esquemas](../../xdm/api/getting-started.md).

**Formato de API**

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
| `title` | El nombre que desea utilizar para el esquema. Este nombre debe ser único. |
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
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. Para obtener más información sobre el ID del inquilino, lea la [guía del registro de esquema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Tenga en cuenta los atributos `$id`, así como los `version`, ya que ambos se utilizarán al crear su conjunto de datos.

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
| `{SCHEMA_REF_ID}` | El `$id` que recibió anteriormente al componer el esquema. Debería tener un aspecto similar al siguiente: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Códigos de área de nombres de identidad**
>
> Asegúrese de que los códigos sean válidos: el ejemplo anterior utiliza &quot;correo electrónico&quot;, que es un área de nombres de identidad estándar. En las [preguntas frecuentes sobre el servicio de identidad](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform) se pueden encontrar otros espacios de nombres de identidad estándar utilizados con más frecuencia.
>
> Si desea crear un área de nombres personalizada, siga los pasos descritos en la [descripción general del área de nombres de identidad](../../identity-service/home.md).

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

## Crear un conjunto de datos para registrar datos

Una vez que haya creado el esquema, deberá crear un conjunto de datos para introducir los datos de registro.

>[!NOTE]
>
>Este conjunto de datos estará habilitado para **[!DNL Real-time Customer Profile]** y **[!DNL Identity Service]**.

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

## Ingesta de datos de registro en la conexión de flujo continuo {#ingest-data}

Con el conjunto de datos y la conexión de flujo continuo en su lugar, puede ingerir registros JSON con formato XDM para introducir datos de registro en [!DNL Platform].

**Formato de API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión de flujo continuo creada anteriormente. |
| `synchronousValidation` | Un parámetro de consulta opcional diseñado para fines de desarrollo. Si se establece en `true`, se puede utilizar para comentarios inmediatos a fin de determinar si la solicitud se ha enviado correctamente. De forma predeterminada, este valor se establece en `false`. |

**Solicitud**

La ingesta de datos de registro en una conexión de flujo continuo se puede realizar con o sin el nombre de origen.

La solicitud de ejemplo siguiente ingesta un registro con un nombre de origen que falta en Platform. Si a un registro le falta el nombre de origen, agregará el ID de origen de la definición de conexión de flujo continuo.

>[!NOTE]
>
>La siguiente llamada de API **not** requiere encabezados de autenticación.

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

Si desea incluir un nombre de origen, el siguiente ejemplo muestra cómo lo incluiría.

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

Una respuesta correcta devuelve el estado HTTP 200 con detalles del [!DNL Profile] recién transmitido.

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
| `{CONNECTION_ID}` | El ID de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado en el servidor para el registro que acaba de enviar. Este ID ayuda a Adobe a rastrear el ciclo vital de este registro a través de varios sistemas y con depuración. |
| `receivedTimeMs` | Marca de tiempo (época en milisegundos) que muestra la hora a la que se recibió la solicitud. |
| `synchronousValidation.status` | Dado que se ha agregado el parámetro de consulta `synchronousValidation=true`, este valor aparecerá. Si la validación se ha realizado correctamente, el estado será `pass`. |

## Recuperar los datos de registro recién introducidos

Para validar los registros ingestados anteriormente, puede utilizar [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar los datos del registro.

>[!NOTE]
>
>Si el ID de la directiva de combinación no está definido y `schema.name` o `relatedSchema.name` es `_xdm.context.profile`, [!DNL Profile Access] recuperará **todas** las identidades relacionadas.

**Formato de API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parámetro | Descripción |
| --------- | ----------- |
| `schema.name` | **Requerido.** Nombre del esquema al que se accede. |
| `entityId` | El ID de la entidad. Si se proporciona, también debe proporcionar el área de nombres de la entidad. |
| `entityIdNS` | El espacio de nombres del ID que está intentando recuperar. |

**Solicitud**

Puede revisar los datos de registro ingestados anteriormente con la siguiente solicitud GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de las entidades solicitadas. Como puede ver, este es el mismo registro que se incorporó correctamente anteriormente.

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

Al leer este documento, ahora puede comprender cómo introducir datos de registro en [!DNL Platform] mediante conexiones de flujo continuo. Puede intentar realizar más llamadas con valores diferentes y recuperar los valores actualizados. Además, puede empezar a monitorizar los datos introducidos a través de la interfaz de usuario [!DNL Platform]. Para obtener más información, consulte la guía [monitorización de la ingesta de datos](../quality/monitor-data-ingestion.md).

Para obtener más información sobre la ingesta de transmisión en general, lea la [descripción general de la ingesta de transmisión](../streaming-ingestion/overview.md).


