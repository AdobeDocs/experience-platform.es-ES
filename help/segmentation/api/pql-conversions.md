---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conversiones de PQL
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Conversiones de PQL

intro

- Conversión de formato desde pql/text y pql/json

## Primeros pasos

Los extremos de API que se utilizan en esta guía forman parte de la API de segmentación. Antes de continuar, consulte la guía para desarrolladores [de Segmentación](./getting-started.md).

En particular, la sección [de](./getting-started.md#getting-started) introducción de la guía para desarrolladores de Segmentación incluye vínculos a temas relacionados, una guía para leer las llamadas de la API de muestra en el documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas exitosas a cualquier API de la plataforma de experiencia.

## Conversión de formato desde pql/text y pql/json

**Formato API**

```http
POST /segment/conversion
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre único para la definición del segmento. |
| `expression.type` | El tipo de expresión. Puede ser `PQL` o `ARL`. |
| `expression.format` | Formato de expresión. Puede ser `pql/text` o `pql/json`. |
| `expression.value` | La cadena de consulta de la expresión que desea convertir. |
| `schema.name` | ID de clase del esquema al que hace referencia. |
| `ttlInDays` | Un entero que representa el tiempo de vida (TTL). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del segmento convertido.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Pasos siguientes
