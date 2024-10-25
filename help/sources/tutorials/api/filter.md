---
title: Filtrado de datos de nivel de fila para una Source mediante la API de Flow Service
description: Este tutorial trata los pasos sobre cómo filtrar datos en el nivel de origen mediante la API de Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: e8e8914c41d7a083395b0bf53aaac8021fcf9e9a
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 5%

---

# Filtrar datos de nivel de fila para un origen mediante la API [!DNL Flow Service]

>[!AVAILABILITY]
>
>Actualmente, la compatibilidad con el filtrado de datos de nivel de fila solo está disponible para las siguientes fuentes:
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] actividades estándar](../../connectors/adobe-applications/marketo/marketo.md)

Lea esta guía para ver los pasos sobre cómo filtrar los datos de nivel de fila para un origen mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../landing/api-guide.md).

## Filtrar datos de origen {#filter-source-data}

A continuación se describen los pasos que se deben seguir para filtrar los datos de nivel de fila para el origen.

### Recupere las especificaciones de conexión {#retrieve-your-connection-specs}

El primer paso para filtrar los datos de nivel de fila para el origen es recuperar las especificaciones de conexión del origen y determinar los operadores y el idioma que admite el origen.

Para recuperar la especificación de conexión de un origen determinado, realice una solicitud de GET al extremo `/connectionSpecs` de la API [!DNL Flow Service] y proporcione el nombre de propiedad del origen como parte de los parámetros de consulta.

**Formato de API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Puede recuperar la especificación de conexión [!DNL Google BigQuery] aplicando la propiedad `name` y especificando `"google-big-query"` en la búsqueda. |

+++Solicitud

La siguiente solicitud recupera las especificaciones de conexión de [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve el código de estado 200 y las especificaciones de conexión de [!DNL Google BigQuery], incluida la información sobre el idioma de consulta admitido y los operadores lógicos.

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

+++

#### Operadores de comparación {#comparison-operators}

| Operador | Descripción |
| --- | --- |
| `==` | Filtra por si la propiedad es igual al valor proporcionado. |
| `!=` | Filtra por si la propiedad no es igual al valor proporcionado. |
| `<` | Filtra por si la propiedad es menor que el valor proporcionado. |
| `>` | Filtra por si la propiedad es mayor que el valor proporcionado. |
| `<=` | Filtra por si la propiedad es menor o igual que el valor proporcionado. |
| `>=` | Filtra por si la propiedad es mayor o igual que el valor proporcionado. |
| `like` | Filtra al utilizarse en una cláusula `WHERE` para buscar un patrón especificado. |
| `in` | Filtra por si la propiedad se encuentra dentro de un intervalo especificado. |

{style="table-layout:auto"}

### Especificar condiciones de filtrado para la ingesta {#specify-filtering-conditions-for-ingestion}

Una vez identificados los operadores lógicos y el lenguaje de consulta que admite el origen, puede utilizar Profile Query Language (PQL) para especificar las condiciones de filtrado que desea aplicar a los datos de origen.

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

### Previsualización de los datos {#preview-your-data}

Puede obtener una vista previa de los datos realizando una solicitud de GET al extremo `/explore` de la API [!DNL Flow Service], proporcionando `filters` como parte de los parámetros de consulta y especificando las condiciones de entrada de PQL en [!DNL Base64].

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de su origen. |
| `{TABLE_PATH}` | La propiedad path de la tabla que desea inspeccionar. |
| `{FILTERS}` | Sus condiciones de filtrado de PQL codificadas en [!DNL Base64]. |

+++Solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve el contenido y la estructura de los datos.

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

+++

### Crear una conexión de origen para los datos filtrados

Para crear una conexión de origen e introducir datos filtrados, realice una solicitud de POST al extremo `/sourceConnections` y proporcione las condiciones de filtrado en los parámetros del cuerpo de la solicitud.

**Formato de API**

```http
POST /sourceConnections
```

+++Solicitud

La siguiente solicitud crea una conexión de origen para ingerir datos de `test1.fasTestTable` donde `city` = `DDN`.

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

+++

+++Respuesta

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Filtrar entidades de actividad para [!DNL Marketo Engage] {#filter-for-marketo}

Puede usar el filtrado a nivel de fila para filtrar entidades de actividad al usar el [[!DNL Marketo Engage] conector de origen](../../connectors/adobe-applications/marketo/marketo.md). Actualmente, solo puede filtrar por entidades de actividad y tipos de actividad estándar. Las actividades personalizadas permanecen gobernadas bajo [[!DNL Marketo] asignaciones de campo](../../connectors/adobe-applications/mapping/marketo.md).

### [!DNL Marketo] tipos de actividades estándar {#marketo-standard-activity-types}

En la tabla siguiente se describen los tipos de actividades estándar de [!DNL Marketo]. Utilice esta tabla como referencia para los criterios de filtrado.

| ID de tipo de actividad | Nombre del tipo de actividad |
| --- | --- |
| 1 | Visitar página web |
| 2 | Rellenar formulario |
| 3 | Haga clic en Vínculo |
| 6 | Enviar correo electrónico |
| 7 | Correo electrónico enviado |
| 8 | Correo electrónico rechazado |
| 9 | Cancelar suscripción de correo electrónico |
| 10 | Abrir correo electrónico |
| 11 | Haga clic en Correo electrónico |
| 12 | Nuevo posible cliente |
| 21 | Convertir posible cliente |
| 22 | Cambiar puntuación |
| 24 | Añadir a lista |
| 25 | Eliminar de la lista |
| 27 | Correo electrónico rechazado |
| 32 | Combinar posibles clientes |
| 34 | Agregar a oportunidad |
| 35 | Quitar de oportunidad |
| 36 | Actualizar oportunidad |
| 46 | Momento interesante |
| 101 | Cambiar etapa de ingresos |
| 104 | Cambiar estado en progresión |
| 110 | Llamar a webhook |
| 113 | Añadir a Nutrir |
| 114 | Cambiar seguimiento de nutrición |
| 115 | Cambiar la cadencia de nutrición |

{style="table-layout:auto"}

Siga los pasos a continuación para filtrar las entidades de actividad estándar al usar el conector de origen [!DNL Marketo].

### Crear un flujo de datos de borrador

En primer lugar, cree un [[!DNL Marketo] flujo de datos](../ui/create/adobe-applications/marketo.md) y guárdelo como borrador. Consulte la siguiente documentación para ver los pasos detallados sobre cómo crear un flujo de datos de borrador:

* [Guardar un flujo de datos como borrador mediante la interfaz de usuario](../ui/draft.md)
* [Guardar un flujo de datos como borrador mediante la API](../api/draft.md)

### Recuperación del ID del flujo de datos

Una vez que tenga un flujo de datos borrador, debe recuperar su ID correspondiente.

En la interfaz de usuario, vaya al catálogo de fuentes y luego seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior. Utilice la columna de estado para identificar todos los flujos de datos guardados en modo de borrador y, a continuación, seleccione el nombre del flujo de datos. A continuación, utilice el panel **[!UICONTROL Propiedades]** de la derecha para localizar el ID de flujo de datos.

### Recuperación de detalles del flujo de datos

A continuación, debe recuperar los detalles del flujo de datos, especialmente el ID de conexión de origen asociado al flujo de datos. Para recuperar los detalles del flujo de datos, realice una solicitud de GET al extremo `/flows` y proporcione el ID del flujo de datos como parámetro de ruta.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{FLOW_ID}` | El ID del flujo de datos que desea recuperar. |

+++Solicitud

La siguiente solicitud recupera información sobre el id. de flujo de datos: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve los detalles del flujo de datos, incluida la información sobre sus conexiones de origen y destino correspondientes. Debe tomar nota de los ID de conexión de origen y destino, ya que estos valores son necesarios más adelante, para publicar el flujo de datos.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Recuperar los detalles de la conexión de origen

A continuación, use el identificador de conexión de origen y realice una solicitud de GET al extremo `/sourceConnections` para recuperar los detalles de conexión de origen.

**Formato de API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | Id. de la conexión de origen que desea recuperar. |

+++Solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve los detalles de la conexión de origen. Tome nota de la versión, ya que necesitará este valor en el siguiente paso para actualizar la conexión de origen.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Actualizar la conexión de origen con las condiciones de filtrado

Ahora que tiene el ID de conexión de origen y su versión correspondiente, puede realizar una solicitud de PATCH con las condiciones de filtrado que especifican los tipos de actividad estándar.

Para actualizar la conexión de origen, realice una solicitud de PATCH al extremo `/sourceConnections` y proporcione el identificador de conexión de origen como parámetro de consulta. Además, debe proporcionar un parámetro de encabezado `If-Match`, con la versión correspondiente de la conexión de origen.

>[!TIP]
>
>Se requiere el encabezado `If-Match` al realizar una solicitud de PATCH. El valor de este encabezado es la versión/etiqueta única del flujo de datos que desea actualizar. El valor de versión/etiqueta se actualiza con cada actualización correcta de un flujo de datos.

**Formato de API**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | El identificador de la conexión de origen que desea actualizar |

+++Solicitud

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Respuesta

Una respuesta correcta devuelve el ID de conexión de origen y la etiqueta (versión).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publish su conexión de origen

Con la conexión de origen actualizada con las condiciones de filtrado, ahora puede pasar del estado de borrador y publicar la conexión de origen. Para ello, realice una solicitud de POST al extremo `/sourceConnections` y proporcione el ID de la conexión de origen de borrador, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | El identificador de la conexión de origen que desea publicar. |
| `op` | Operación de acción que actualiza el estado de la conexión de origen consultada. Para publicar una conexión de origen de borrador, establezca `op` en `publish`. |

+++Solicitud

La siguiente solicitud publica una conexión de origen esbozada.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el ID de conexión de origen y la etiqueta (versión).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publish su conexión de destino

Al igual que en el paso anterior, también debe publicar la conexión de destino para continuar y publicar el flujo de datos de borrador. Realice una solicitud de POST al extremo `/targetConnections` y proporcione el identificador de la conexión de destino de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | El ID de la conexión de destino que desea publicar. |
| `op` | Operación de acción que actualiza el estado de la conexión de destino consultada. Para publicar una conexión de destino de borrador, establezca `op` en `publish`. |

+++Solicitud

La siguiente solicitud publica la conexión de destino con el identificador: `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el ID y la etiqueta correspondiente para la conexión de destino publicada.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publish su flujo de datos

Con las conexiones de origen y destino publicadas, ahora puede continuar con el paso final y publicar el flujo de datos. Para publicar el flujo de datos, realice una solicitud de POST al extremo `/flows` y proporcione el ID del flujo de datos y una operación de acción para la publicación.

**Formato de API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `{FLOW_ID}` | El ID del flujo de datos que desea publicar. |
| `op` | Operación de acción que actualiza el estado del flujo de datos consultado. Para publicar un flujo de datos de borrador, establezca `op` en `publish`. |

+++Solicitud

La siguiente solicitud publica el flujo de datos de borrador.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el ID y el `etag` correspondiente del flujo de datos.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Puede utilizar la interfaz de usuario del Experience Platform para comprobar que se ha publicado el flujo de datos de borrador. Vaya a la página de flujos de datos en el catálogo de fuentes y haga referencia al **[!UICONTROL estado]** del flujo de datos. Si se ejecuta correctamente, el estado debería establecerse en **Enabled**.

>[!TIP]
>
>* Un flujo de datos con el filtrado habilitado solo se rellenará una vez. Cualquier cambio en el que realice en los criterios de filtrado (ya sea una adición o una eliminación) solo surtirá efecto para los datos incrementales.
>* Si necesita introducir datos históricos para cualquier tipo de actividad nuevo, se recomienda crear un flujo de datos nuevo y definir los criterios de filtrado con los tipos de actividad adecuados en la condición de filtro.
>* No se pueden filtrar los tipos de actividades personalizadas.
>* No se pueden previsualizar los datos filtrados.

## Apéndice

Esta sección proporciona más ejemplos de diferentes cargas útiles para el filtrado.

### Condiciones singulares

Puede omitir el `fnApply` inicial en escenarios que solo requieran una condición.

+++Seleccione para ver el ejemplo

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

+++

### Uso del operador `in`

Consulte la carga útil de ejemplo siguiente para ver un ejemplo del operador `in`.

+++Seleccione para ver el ejemplo

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

+++

### Uso del operador `isNull`

+++Seleccione para ver el ejemplo

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

+++

### Uso del operador `NOT`

Consulte la carga útil de ejemplo siguiente para ver un ejemplo del operador `NOT`.


+++Seleccione para ver el ejemplo

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

+++

### Ejemplo con condiciones anidadas

Consulte la carga útil de ejemplo siguiente para ver un ejemplo de condiciones anidadas complejas.

+++Seleccione para ver el ejemplo

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

+++