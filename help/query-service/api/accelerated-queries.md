---
title: Punto final de consultas aceleradas
description: Obtenga información sobre cómo acceder al almacén acelerado de consultas sin estado para devolver rápidamente resultados según los datos agregados. Este documento proporciona un ejemplo de solicitud HTTP y respuesta para el extremo de consultas aceleradas del servicio de consulta.
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# Extremo de consultas aceleradas

Como parte del SKU de Distiller de datos, la variable [API del servicio de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/) permite realizar consultas sin estado en el almacén acelerado. Los resultados devueltos se basan en datos agregados. La disminución de la latencia de los resultados permite un intercambio de información más interactivo. Las API de consultas aceleradas también se utilizan para activar [tableros definidos por el usuario](../../dashboards/user-defined-dashboards.md).

Antes de continuar con esta guía, asegúrese de haber leído y entendido el [Guía de API del servicio de consulta](./getting-started.md) para utilizar correctamente la API del servicio de consulta.

## Primeros pasos

El SKU de Distiller de datos es necesario para utilizar el almacén acelerado de consultas. Consulte la [embalaje](../packages.md) y [guardrails](../guardrails.md#query-accelerated-store) documentación relacionada con el SKU de Distiller de datos. Si no tiene el SKU de Distiller de datos, póngase en contacto con su representante del servicio al cliente de Adobe para obtener más información.

<!-- Document is hidden temporarily
Please see the [packaging](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), and [licensing](../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

Las siguientes secciones detallan las llamadas de API necesarias para acceder al almacén acelerado de consultas de forma apátrida a través de la API del servicio de consultas. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

## Ejecutar una consulta acelerada {#run-accelerated-query}

Realice una solicitud de POST al `/accelerated-queries` para ejecutar una consulta acelerada. La consulta se encuentra directamente en la carga útil de la solicitud o se hace referencia a ella con un ID de plantilla.

**Formato de API**

```shell
POST /accelerated-queries
```

### Solicitud

>[!IMPORTANT]
>
>Solicitudes al `/accelerated-queries` El extremo requiere una instrucción SQL O un ID de plantilla, pero no ambos. El envío de ambos en una solicitud causa un error.

La siguiente solicitud envía una consulta SQL en el cuerpo de la solicitud al almacén acelerado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Esta solicitud alternativa envía un ID de plantilla en el cuerpo de la solicitud al almacén acelerado. El SQL de la plantilla correspondiente se utiliza para consultar el almacén acelerado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Propiedad | Descripción |
|---|---|
| `dbName` | Nombre de la base de datos a la que está realizando una consulta acelerada. El valor de `dbName` debe adoptar el formato de `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. La base de datos proporcionada debe existir en el almacén acelerado; de lo contrario, la solicitud generará un error. También debe asegurarse de que la variable `x-sandbox-name` encabezado y nombre del simulador de pruebas en `dbName` consulte el mismo simulador de pruebas. |
| `sql` | Una cadena de instrucción SQL. El tamaño máximo permitido es de 100000 caracteres. |
| `templateId` | El identificador único de una consulta creada y guardada como plantilla cuando se realiza una solicitud de POST al `/templates` punto final. |
| `name` | Un nombre descriptivo y reconocible opcional para la consulta acelerada. |
| `description` | Un comentario opcional sobre la intención de la consulta para ayudar a otros usuarios a comprender su propósito. El tamaño máximo permitido es de 1000 bytes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el esquema ad hoc creado por la consulta.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para su brevedad.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Propiedad | Descripción |
|---|---|
| `queryId` | El valor de ID de la consulta creada. |
| `resultsMeta` | Este objeto contiene los metadatos de cada columna devuelta en los resultados para que los usuarios conozcan el nombre y el tipo de cada columna. |
| `resultsMeta._adhoc` | Un esquema del Modelo de datos de experiencia (XDM) ad-hoc con campos a los que solo se asigna un nombre para su uso mediante un único conjunto de datos. |
| `resultsMeta._adhoc.type` | Tipo de datos del esquema ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | Se trata de un valor generado por el sistema para el tipo de campo XDM. Para obtener más información sobre los tipos disponibles, consulte la documentación sobre [tipos XDM disponibles](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | Son los nombres de columna del conjunto de datos consultado. |
| `resultsMeta._adhoc.results` | Son los nombres de fila del conjunto de datos consultado. Reflejan cada una de las columnas devueltas. |
