---
title: Conexión de la cuenta de flujo de Snowflake a Adobe Experience Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform al flujo de Snowflake mediante la API de Flow Service.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# Transmitir [!DNL Snowflake] datos al Experience Platform mediante el [!DNL Flow Service] API

>[!IMPORTANT]
>
>* El [!DNL Snowflake] la fuente de streaming está en versión beta. Lea el [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.
>* El [!DNL Snowflake] La fuente de streaming está disponible en el catálogo de fuentes para los clientes que han adquirido Real-Time CDP Ultimate.


Este tutorial proporciona pasos sobre cómo conectar y transmitir datos desde su [!DNL Snowflake] a Adobe Experience Platform mediante el [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Para obtener información sobre la configuración de requisitos previos y la [!DNL Snowflake] fuente de flujo continuo. Lea el [[!DNL Snowflake] información general de fuente de streaming](../../../../connectors/databases/snowflake-streaming.md).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base {#create-a-base-connection}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Snowflake] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Snowflake]:

>[!TIP]
>
>El `auth.specName` El valor debe introducirse exactamente como en el ejemplo siguiente, incluidos los espacios en blanco.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.account` | El nombre de su [!DNL Snowflake] cuenta de streaming. |
| `auth.params.database` | El nombre de su [!DNL Snowflake] base de datos de la que se extraerán los datos. |
| `auth.params.warehouse` | El nombre de su [!DNL Snowflake] almacén. El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada almacén es independiente entre sí y se debe acceder a él de forma individual al llevar los datos a Platform. |
| `auth.params.username` | El nombre de usuario de su [!DNL Snowflake] cuenta de streaming. |
| `auth.params.schema` | (Opcional) El esquema de base de datos asociado con su [!DNL Snowflake] cuenta de streaming. |
| `auth.params.password` | La contraseña de su [!DNL Snowflake] cuenta de streaming. |
| `auth.params.role` | (Opcional) La función del usuario para esto [!DNL Snowflake] conexión. Si no se proporciona, el valor predeterminado es `public`. |
| `connectionSpec.id` | El [!DNL Snowflake] identificador de especificación de conexión: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada y su etiqueta correspondiente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Exploración de las tablas de datos {#explore-your-data-tables}

A continuación, utilice el ID de conexión base para explorar y navegar por las tablas de datos de origen realizando una solicitud de GET a `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` al proporcionar su ID de conexión base como parámetro.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de su [!DNL Snowflake] fuente de flujo continuo. |


**Solicitud**

La siguiente solicitud recupera la estructura y el contenido de su [!DNL Snowflake] cuenta de streaming.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura y el contenido de los datos de origen en el nivel raíz.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `items.type` | Tipo de la tabla. |
| `items.names` | Nombre de la tabla. |

## Crear una conexión de origen {#create-a-source-connection}

Una conexión de origen crea y administra la conexión con el origen externo desde el que se incorporan los datos.

Para crear una conexión de origen, realice una solicitud de POST al `/sourceConnections` punto final del [!DNL Flow Service] API.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | El ID de conexión base autenticada para su [!DNL Snowflake] fuente de flujo continuo. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | ID de especificación de conexión para [!DNL Snowflake] fuente de flujo continuo. |
| `params.tableName` | El nombre de la tabla en su [!DNL Snowflake] que desee llevar a Platform. |
| `params.timestampColumn` | Nombre de la columna de marca de tiempo que se utilizará para recuperar los valores incrementales. |
| `params.backfill` | Un indicador booleano que determina si los datos se recuperan desde el principio (hora de la época 0) o desde el momento en que se inicia el origen. Para obtener más información sobre este valor, lea [[!DNL Snowflake] información general de fuente de streaming](../../../../connectors/databases/snowflake-streaming.md). |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de origen y su etiqueta correspondiente. El ID de conexión de origen se utilizará en un paso posterior para crear un flujo de datos.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Creación de un flujo de datos

Para crear un flujo de datos para transmitir datos desde el recorrido [!DNL Snowflake] cuenta a Platform, debe realizar una solicitud de POST a `/flows` al tiempo que proporciona los siguientes valores:

>[!TIP]
>
>Siga los vínculos a continuación para obtener guías paso a paso sobre cómo recuperar los siguientes ID.

* [ID de conexión de origen](#create-a-source-connection)
* [ID de conexión de destino](../../collect/database-nosql.md#create-a-target-connection)
* [ID de especificación de flujo](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID de asignación](../../collect/database-nosql.md#create-a-mapping)

**Formato de API**

```http
POST /flows
```

**Solicitud**

La siguiente solicitud crea un flujo de datos de flujo continuo para su [!DNL Snowflake] cuenta.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `sourceConnectionIds` | El ID de conexión de origen de su [!DNL Snowflake] fuente de flujo continuo. |
| `targetConnectionIds` | El ID de conexión de destino de su [!DNL Snowflake] fuente de flujo continuo. |
| `flowSpec.id` | ID de especificación de flujo para crear un flujo de datos para una [!DNL Snowflake] fuente de flujo continuo. Este ID de especificación de flujo le permite crear un flujo de datos de flujo continuo con transformaciones de asignación. Este ID es fijo y es: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | ID de asignación para el flujo de datos. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y su etiqueta correspondiente.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un flujo de datos de flujo continuo para su [!DNL Snowflake] datos con el [!DNL Flow Service] API. Visite la siguiente documentación para obtener más información sobre las fuentes de Adobe Experience Platform:

* [Resumen de orígenes](../../../../home.md)
* [Monitorización del flujo de datos mediante API](../../monitor.md)