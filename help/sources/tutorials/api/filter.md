---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API de servicio de flujo;fuentes;orígenes
title: Filtrado de datos de nivel de fila para una fuente mediante la API de Flow Service
description: Este tutorial trata los pasos sobre cómo filtrar datos en el nivel de origen mediante la API de Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 3%

---

# Filtrado de datos de nivel de fila para un origen mediante [!DNL Flow Service] API

>[!IMPORTANT]
>
>Actualmente, la compatibilidad con el filtrado de datos de nivel de fila para un origen solo está disponible para [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md) y [[!DNL Snowflake]](../../connectors/databases/snowflake.md) fuentes.

Este tutorial proporciona pasos sobre cómo filtrar datos de nivel de fila para un origen mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Filtrar datos de origen

A continuación se describen los pasos que se deben seguir para filtrar los datos de nivel de fila para el origen.

### Búsqueda de especificaciones de conexión

Antes de poder utilizar la API para filtrar datos de nivel de fila para un origen, primero debe recuperar los detalles de especificación de conexión del origen para determinar los operadores y el idioma que admite un origen específico.

Para recuperar la especificación de conexión de un origen determinado, realice una solicitud de GET al `/connectionSpecs` punto final del [!DNL Flow Service] al proporcionar el nombre de la propiedad de su origen como parte de los parámetros de consulta.

**Formato de API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Puede recuperar la variable [!DNL Google BigQuery] especificación de conexión mediante la aplicación de `name` y especificar `"google-big-query"` en la búsqueda. |

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión para [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las especificaciones de conexión para [!DNL Google BigQuery], incluida información sobre el idioma de consulta admitido y los operadores lógicos.

>[!NOTE]
>
>La respuesta de la API siguiente se trunca por brevedad.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Propiedad | Descripción |
| --- | --- |
| `attributes.filterAtSource.enabled` | Determina si el origen consultado admite el filtrado de datos de nivel de fila. |
| `attributes.filterAtSource.queryLanguage` | Determina el lenguaje de consulta que admite el origen de la consulta. |
| `attributes.filterAtSource.logicalOperators` | Determina los operadores lógicos que se pueden utilizar para filtrar los datos de nivel de fila para el origen. |
| `attributes.filterAtSource.comparisonOperators` | Determina los operadores de comparación que se pueden utilizar para filtrar los datos de nivel de fila para el origen. Consulte la tabla siguiente para obtener más información sobre los operadores de comparación. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina el carácter que se utilizará para aplicar secuencias de escape a las columnas. |
| `attributes.filterAtSource.valueEscapeChar` | Determina cómo se rodearán los valores al escribir una consulta SQL. |

{style="table-layout:auto"}

#### Operadores de comparación

| Operador | Descripción |
| --- | --- |
| `==` | Filtra por si la propiedad es igual al valor proporcionado. |
| `!=` | Filtra por si la propiedad no es igual al valor proporcionado. |
| `<` | Filtra por si la propiedad es menor que el valor proporcionado. |
| `>` | Filtra por si la propiedad es buena que el valor proporcionado. |
| `<=` | Filtra por si la propiedad es menor o igual que el valor proporcionado. |
| `>=` | Filtra por si la propiedad es buena o igual que el valor proporcionado. |
| `like` | Filtros al utilizarse en una `WHERE` para buscar un patrón especificado. |
| `in` | Filtra por si la propiedad se encuentra dentro de un intervalo especificado. |

{style="table-layout:auto"}

### Especificar condiciones de filtrado para la ingesta

Una vez identificados los operadores lógicos y el lenguaje de consulta que admite el origen, puede utilizar el lenguaje de consulta de perfil (PQL) para especificar las condiciones de filtrado que desea aplicar a los datos de origen.

En el ejemplo siguiente, las condiciones se aplican solo a los datos de selección que son iguales a los valores proporcionados para los tipos de nodo enumerados como parámetros.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Previsualización de los datos

Puede obtener una vista previa de los datos realizando una solicitud de GET a `/explore` punto final del [!DNL Flow Service] API al proporcionar `filters` como parte de los parámetros de consulta y especificación de las condiciones de entrada PQL en [!DNL Base64].

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de su origen. |
| `{TABLE_PATH}` | La propiedad path de la tabla que desea inspeccionar. |
| `{FILTERS}` | Sus condiciones de filtrado PQL codificadas en [!DNL Base64]. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una solicitud correcta devuelve la siguiente respuesta.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Crear una conexión de origen para los datos filtrados

Para crear una conexión de origen e introducir datos filtrados, realice una solicitud de POST al `/sourceConnections` al tiempo que proporciona las condiciones de filtrado como parte de los parámetros del cuerpo.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen desde la que se pueden introducir datos `test1.fasTestTable` donde `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Apéndice

Esta sección proporciona más ejemplos de diferentes cargas útiles para el filtrado.

### Condiciones singulares

Puede omitir el `fnApply` para escenarios que solo requieren una condición.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Uso del `in` operador

Consulte la carga útil de ejemplo siguiente para ver un ejemplo del operador `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Uso del `isNull` operador

Consulte la carga útil de ejemplo siguiente para ver un ejemplo del operador `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Uso del `NOT` operador

Consulte la carga útil de ejemplo siguiente para ver un ejemplo del operador `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Ejemplo con condiciones anidadas

Consulte la carga útil de ejemplo siguiente para ver un ejemplo de condiciones anidadas complejas.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
