---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API de servicio de flujo;fuentes;fuentes
title: Filtrado De Datos De Nivel De Fila Para Una Fuente Mediante La API De Servicio De Flujo
description: Este tutorial trata los pasos sobre cómo filtrar datos en el nivel de origen mediante la API de servicio de flujo
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: da6f5a79b1ee16fb0d44a5c2990ed1b8be1f99e2
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 3%

---

# Filtrado de datos de nivel de fila para un origen mediante la variable [!DNL Flow Service] API

>[!IMPORTANT]
>
>Actualmente, la compatibilidad con el filtrado de datos de nivel de fila solo está disponible para las siguientes fuentes:
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics ](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Marketing Cloud de Salesforce](../../connectors/marketing-automation/salesforce-marketing-cloud.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


Este tutorial proporciona pasos sobre cómo filtrar datos de nivel de fila para un origen mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Filtrar datos de origen

A continuación se describen los pasos a seguir para filtrar los datos de nivel de fila del origen.

### Buscar especificaciones de conexión

Antes de poder utilizar la API para filtrar datos de nivel de fila para un origen, debe recuperar los detalles de especificación de conexión de la fuente para determinar los operadores y el idioma que admite un origen específico.

Para recuperar una especificación de conexión de un origen determinado, realice una solicitud de GET al `/connectionSpecs` punto final del [!DNL Flow Service] al proporcionar el nombre de propiedad de su origen como parte de sus parámetros de consulta.

**Formato de API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Los parámetros de consulta opcionales por los que filtrar los resultados. Puede recuperar el [!DNL Google BigQuery] especificación de conexión aplicando la `name` propiedad y especificar `"google-big-query"` en la búsqueda. |

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
>La siguiente respuesta de API se trunca para su brevedad.

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
| `attributes.filterAtSource.enabled` | Determina si el origen consultado admite el filtrado para datos de nivel de fila. |
| `attributes.filterAtSource.queryLanguage` | Determina el idioma de consulta que admite el origen consultado. |
| `attributes.filterAtSource.logicalOperators` | Determina los operadores lógicos que se pueden usar para filtrar datos de nivel de fila para el origen. |
| `attributes.filterAtSource.comparisonOperators` | Determina los operadores de comparación que se pueden usar para filtrar datos de nivel de fila para el origen. Consulte la siguiente tabla para obtener más información sobre los operadores de comparación. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina el carácter que se utiliza para aplicar secuencias de escape a las columnas. |
| `attributes.filterAtSource.valueEscapeChar` | Determina cómo se rodearán los valores al escribir una consulta SQL. |

{style="table-layout:auto"}

#### Operadores de comparación

| Operador | Descripción |
| --- | --- |
| `==` | Filtra si la propiedad es igual al valor proporcionado. |
| `!=` | Filtra si la propiedad no es igual al valor proporcionado. |
| `<` | Filtra si la propiedad es menor que el valor proporcionado. |
| `>` | Filtra si la propiedad es buena que el valor proporcionado. |
| `<=` | Filtra si la propiedad es menor o igual que el valor proporcionado. |
| `>=` | Filtra por si la propiedad es buena o igual al valor proporcionado. |
| `like` | Filtros que se utilizan en una `WHERE` para buscar un patrón especificado. |
| `in` | Filtra si la propiedad se encuentra dentro de un intervalo especificado. |

{style="table-layout:auto"}

### Especificación de las condiciones de filtrado para la ingesta

Una vez identificados los operadores lógicos y el lenguaje de consulta que admite el origen, puede utilizar el lenguaje de consulta de perfil (PQL) para especificar las condiciones de filtrado que desea aplicar a los datos de origen.

En el ejemplo siguiente, las condiciones se aplican solo a los datos seleccionados que coinciden con los valores proporcionados para los tipos de nodo enumerados como parámetros.

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

### Previsualizar los datos

Puede obtener una vista previa de los datos realizando una solicitud de GET al `/explore` punto final del [!DNL Flow Service] API mientras proporciona `filters` como parte de los parámetros de consulta y especificación de las condiciones de entrada de PQL en [!DNL Base64].

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base del origen. |
| `{TABLE_PATH}` | La propiedad path de la tabla que desea inspeccionar. |
| `{FILTERS}` | Las condiciones de filtrado de PQL están codificadas en [!DNL Base64]. |

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

### Creación de una conexión de origen para datos filtrados

Para crear una conexión de origen e ingerir datos filtrados, realice una solicitud de POST al `/sourceConnections` al proporcionar las condiciones de filtrado como parte de los parámetros de su cuerpo.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para introducir datos de `test1.fasTestTable` donde `city` = `DDN`.

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

Puede omitir la `fnApply` para escenarios que solo requieren una condición.

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

### Al usar la variable `in` operador

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

### Al usar la variable `isNull` operador

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

### Al usar la variable `NOT` operador

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
