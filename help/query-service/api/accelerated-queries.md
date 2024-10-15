---
title: Punto final de consultas aceleradas
description: Obtenga información sobre cómo acceder al almacén acelerado de consultas de forma independiente para devolver rápidamente resultados basados en datos agregados. Este documento proporciona una solicitud y una respuesta HTTP de ejemplo para el extremo de consultas aceleradas del servicio de consultas.
role: Developer
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Extremo de consultas aceleradas

Como parte del SKU de Data Distiller, la [API de servicio de consultas](https://developer.adobe.com/experience-platform-apis/references/query-service/) le permite realizar consultas sin estado en el almacén acelerado. Los resultados devueltos se basan en los datos agregados. La disminución de la latencia de los resultados permite un intercambio de información más interactivo. Las API de consultas aceleradas también se usan para activar [paneles definidos por el usuario](../../dashboards/standard-dashboards.md).

Antes de continuar con esta guía, asegúrese de haber leído y comprendido la [guía de API del servicio de consultas](./getting-started.md) para usar correctamente la API del servicio de consultas.

## Introducción

El SKU de Data Distiller es necesario para utilizar el almacén acelerado de consultas. Consulte la documentación de [empaquetado](../packaging.md) y [protecciones](../guardrails.md#query-accelerated-store), así como la [licencia](../data-distiller/license-usage.md) relacionada con el SKU de Data Distiller. Si no tiene el SKU de Distiller de datos, póngase en contacto con el representante del servicio de atención al cliente de Adobe para obtener más información.

Las siguientes secciones detallan las llamadas de API necesarias para acceder al almacén acelerado de consultas de forma independiente a través de la API del servicio de consultas. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

## Ejecutar una consulta acelerada {#run-accelerated-query}

Realice una solicitud de POST al extremo `/accelerated-queries` para ejecutar una consulta acelerada. La consulta está contenida directamente en la carga útil de la solicitud o se hace referencia a ella con un ID de plantilla.

**Formato de API**

```shell
POST /accelerated-queries
```

### Solicitud

>[!IMPORTANT]
>
>Las solicitudes al extremo `/accelerated-queries` requieren una instrucción SQL O un identificador de plantilla, pero no ambas. Enviar ambos en una solicitud provoca un error.

La siguiente solicitud envía una consulta SQL en el cuerpo de la solicitud al almacén acelerado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
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
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
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
| `dbName` | El nombre de la base de datos a la que está realizando una consulta acelerada. El valor de `dbName` debe tener el formato de `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. La base de datos proporcionada debe existir dentro del almacén acelerado o la solicitud producirá un error. También debe asegurarse de que el encabezado `x-sandbox-name` y el nombre de la zona protegida en `dbName` hagan referencia a la misma zona protegida. |
| `sql` | Una cadena de instrucción SQL. El tamaño máximo permitido es de 1000000 caracteres. |
| `templateId` | Identificador único de una consulta creada y guardada como plantilla cuando se realiza una solicitud de POST al extremo `/templates`. |
| `name` | Un nombre descriptivo y sencillo opcional para la consulta acelerada. |
| `description` | Un comentario opcional sobre la intención de la consulta para ayudar a otros usuarios a comprender su propósito. El tamaño máximo permitido es de 1000 bytes. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el esquema ad hoc creado por la consulta.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para ser más breve.

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
| `resultsMeta._adhoc` | Esquema de modelo de datos de experiencia (XDM) ad hoc con campos de espacio de nombres para su uso exclusivo en un único conjunto de datos. |
| `resultsMeta._adhoc.type` | El tipo de datos del esquema ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | Es un valor generado por el sistema para el tipo de campo XDM. Para obtener más información sobre los tipos disponibles, consulte la documentación de [tipos XDM disponibles](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Estos son los nombres de columna del conjunto de datos consultado. |
| `resultsMeta._adhoc.results` | Estos son los nombres de fila del conjunto de datos consultado. Reflejan cada una de las columnas devueltas. |
