---
keywords: Experience Platform;inicio;temas populares;preparación de datos;guía de api;esquemas;
solution: Experience Platform
title: Punto final de API de Esquemas
topic: esquemas
description: 'Puede utilizar el extremo `/functions` en la API de Adobe Experience Platform para validar las expresiones de asignación y las funciones del conjunto de asignaciones de lista disponibles. '
translation-type: tm+mt
source-git-commit: 60c80a73deb8c77f19d5963cc3319d46143fb4c3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---


# Puntos finales de funciones

Las funciones de conjunto de asignaciones permiten transformar los datos entre esquemas de origen y destino. Puede utilizar el extremo `/languages/el` para validar sus expresiones, así como obtener una lista de todas las funciones de conjuntos de asignaciones disponibles.

## Validar expresiones

Puede validar si la expresión actual es válida realizando una solicitud de POST al extremo `/languages/el/validate` .

**Formato de API**

```
POST /languages/el/validate
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el estado de validación de la expresión.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Funciones del conjunto de asignaciones de lista

Puede recuperar una lista de todas las funciones de conjunto de asignaciones disponibles realizando una solicitud de GET al extremo `/languages/el/functions` .

**Formato de API**

```
GET /languages/el/functions
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todas las funciones de conjuntos de asignaciones disponibles.

>[!NOTE]
>
>Esta respuesta se ha truncado para el espacio.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Enumerar operadores de conjuntos de asignaciones

Puede recuperar una lista de todos los operadores de conjuntos de asignaciones disponibles realizando una solicitud de GET al extremo `/languages/el/operators` .

**Formato de API**

```
GET /languages/el/operators
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todos los operadores de conjuntos de asignaciones disponibles.

>[!NOTE]
>
>Esta respuesta se ha truncado para el espacio.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
