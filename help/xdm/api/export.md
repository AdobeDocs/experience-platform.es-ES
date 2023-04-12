---
title: Exportar extremo de API
description: El extremo /export de la API del Registro de esquemas permite compartir recursos XDM entre entornos limitados.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Exportar extremo

Todos los recursos de [!DNL Schema Library] se encuentran en un entorno limitado específico de Adobe Experience Platform. En algunos casos, es posible que desee compartir recursos del Modelo de datos de experiencia (XDM) entre entornos limitados y organizaciones. La variable `/rpc/export` en la variable [!DNL Schema Registry] La API permite generar una carga útil de exportación para cualquier esquema, grupo de campos de esquema o tipo de datos en la variable [!DNL Schema Library]y, a continuación, utilice esa carga útil para importar ese recurso (y todos los recursos dependientes) en un entorno limitado de destino y en una organización a través del [`/rpc/import` extremo](./import.md).

## Primeros pasos

La variable `/rpc/export` es parte de la variable [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

La variable `/rpc/export` el extremo es parte de las llamadas a procedimientos remotos (RPC) que son compatibles con la variable [!DNL Schema Registry]. A diferencia de otros extremos en la variable [!DNL Schema Registry] Los extremos de API y RPC no requieren encabezados adicionales como `Accept` o `Content-Type`y no use un `CONTAINER_ID`. En su lugar, deben usar la variable `/rpc` como se muestra en las llamadas de API a continuación.

## Generar una carga útil de exportación para un recurso {#export}

Para cualquier esquema, grupo de campos o tipo de datos existente en la variable [!DNL Schema Library], puede generar una carga útil de exportación realizando una solicitud de GET al `/export` , proporcionando el ID del recurso en la ruta.

**Formato de API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_ID}` | La variable `meta:altId` o con codificación de URL `$id` del recurso XDM que desea exportar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una carga útil de exportación para un `Restaurant` grupo de campos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de objetos, que representan el recurso XDM de destino y todos sus recursos dependientes. En este ejemplo, el primer objeto de la matriz es un `Property` tipo de datos que el `Restaurant` el grupo de campos emplea, mientras que el segundo objeto es el `Restaurant` grupo de campos. Esta carga útil se puede utilizar para [importar el recurso](#import) en un entorno limitado u organización diferente.

Tenga en cuenta que todas las instancias del ID de inquilino del recurso se sustituyen por `<XDM_TENANTID_PLACEHOLDER>`. Esto permite que el Registro de esquemas aplique automáticamente el ID de inquilino correcto a los recursos en función de dónde se envíen en la llamada de importación posterior.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Importación del recurso {#import}

Después de generar la carga útil de exportación desde el archivo CSV, puede enviar esa carga útil a la variable `/rpc/import` para generar el esquema.

Consulte la [guía de extremo de importación](./import.md) para obtener más información sobre cómo generar esquemas a partir de cargas de exportación.
