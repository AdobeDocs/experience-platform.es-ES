---
keywords: Experience Platform;inicio;temas populares;preparación de datos;guía de api;esquemas;
solution: Experience Platform
title: Extremo de API de esquemas
description: Puede utilizar el extremo /schemas en la API de Adobe Experience Platform para recuperar, crear y actualizar esquemas mediante programación para utilizarlos con Mapper en Platform.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---



# Extremo de esquemas

Los esquemas se pueden utilizar con Mapper para asegurarse de que los datos que ha introducido en Adobe Experience Platform coinciden con los que desea introducir. Puede usar el extremo `/schemas` para crear, enumerar y obtener esquemas personalizados mediante programación para usarlos con Mapper en Platform.

>[!NOTE]
>
>Los esquemas creados con este extremo se utilizan exclusivamente con conjuntos de asignaciones y asignadores. Para crear esquemas accesibles por otros servicios de Platform, lea la [Guía para desarrolladores de Schema Registry](../../xdm/api/schemas.md).

## Obtener todos los esquemas

Puede recuperar una lista de todos los esquemas de asignador disponibles para su organización realizando una solicitud de GET al extremo `/schemas`.

**Formato de API**

El extremo `/schemas` admite varios parámetros de consulta para ayudarle a filtrar los resultados. Aunque la mayoría de estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Sin embargo, debe incluir los parámetros `start` y `limit` como parte de la solicitud. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{LIMIT}` | **Requerido**. Especifica el número de esquemas devueltos. |
| `{START}` | **Requerido**. Especifica el desplazamiento de las páginas de resultados. Para obtener la primera página de resultados, establezca el valor en `start=0`. |
| `{NAME}` | Filtra el esquema en función del nombre. |
| `{ORDER_BY}` | Ordena el orden de los resultados. Los campos admitidos son `modifiedDate` y `createdDate`. Puede anteponer la propiedad `+` o `-` para ordenarla en orden ascendente o descendente, respectivamente. |

**Solicitud**

La siguiente solicitud recupera los dos últimos esquemas creados para su organización.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de los esquemas solicitados.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Creación de un esquema

Puede crear un esquema para validar realizando una solicitud de POST al extremo `/schemas`. Existen tres formas de crear un esquema: enviar un [esquema JSON](https://json-schema.org/), usar datos de ejemplo o hacer referencia a un esquema XDM existente.

```http
POST /schemas
```

### Uso de un esquema JSON

**Solicitud**

La siguiente solicitud le permite crear un esquema enviando un [esquema JSON](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el esquema recién creado.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Uso de datos de ejemplo

**Solicitud**

La siguiente solicitud permite crear un esquema con los datos de ejemplo que ha cargado anteriormente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sampleId` | El ID de los datos de ejemplo en los que basa el esquema. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el esquema recién creado.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Consulte un esquema XDM

**Solicitud**

La siguiente solicitud permite crear un esquema haciendo referencia a un esquema XDM existente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | El nombre del esquema que desea crear. |
| `schemaRef.id` | El ID del esquema al que hace referencia. |
| `schemaRef.contentType` | Determina el formato de respuesta del esquema referenciado. Encontrará más información sobre este campo en la [guía para desarrolladores de registros de esquemas](../../xdm/api/schemas.md#lookup) |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el esquema recién creado.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Creación de un esquema mediante la carga de archivos

Puede crear un esquema cargando un archivo JSON desde el que convertir.

**Formato de API**

```http
POST /schemas/upload
```

**Solicitud**

La siguiente solicitud permite crear un esquema a partir de un archivo JSON cargado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el esquema recién creado.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Recuperación de un esquema específico

Puede recuperar información sobre un esquema específico realizando una solicitud de GET al extremo `/schemas` y proporcionando el ID del esquema que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /schemas/{SCHEMA_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SCHEMA_ID}` | El ID del esquema que está buscando. |

**Solicitud**

La siguiente solicitud recupera información sobre el esquema especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el esquema especificado.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
