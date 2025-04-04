---
title: Conecte su cuenta de flujo continuo de Snowflake a Adobe Experience Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Snowflake Streaming mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 5%

---

# Transmitir datos de [!DNL Snowflake] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>
> El origen de flujo continuo [!DNL Snowflake] está disponible en la API para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Este tutorial proporciona pasos sobre cómo conectar y transmitir datos desde su cuenta de [!DNL Snowflake] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Para obtener información y configuración previas sobre el origen de flujo de [!DNL Snowflake]. Lea la [[!DNL Snowflake] descripción general del origen de transmisión](../../../../connectors/databases/snowflake-streaming.md).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base {#create-a-base-connection}

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Snowflake] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Snowflake]:

>[!TIP]
>
>El valor `auth.specName` debe escribirse exactamente como en el ejemplo siguiente, incluidos los espacios en blanco.

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
| `auth.params.account` | El nombre de su cuenta de streaming [!DNL Snowflake]. |
| `auth.params.database` | Nombre de la base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.warehouse` | Nombre de su almacén de [!DNL Snowflake]. El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén es independiente entre sí y se debe acceder a él de forma individual al llevar los datos a Experience Platform. |
| `auth.params.username` | El nombre de usuario de su cuenta de streaming [!DNL Snowflake]. |
| `auth.params.schema` | (Opcional) El esquema de base de datos asociado con su cuenta de flujo continuo [!DNL Snowflake]. |
| `auth.params.password` | Contraseña de su cuenta de streaming [!DNL Snowflake]. |
| `auth.params.role` | (Opcional) El rol del usuario para esta conexión de [!DNL Snowflake]. Si no se proporciona, el valor predeterminado es `public`. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Snowflake]: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada y su etiqueta correspondiente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Exploración de las tablas de datos {#explore-your-data-tables}

A continuación, use el id. de conexión base para explorar y navegar por las tablas de datos de origen realizando una petición GET al extremo `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` y proporcionando al mismo tiempo el id. de conexión base como parámetro.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identificador de conexión base de su origen de flujo continuo [!DNL Snowflake]. |


**Solicitud**

La siguiente solicitud recupera la estructura y el contenido de su cuenta de flujo continuo [!DNL Snowflake].

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

Para crear una conexión de origen, realice una petición POST al extremo `/sourceConnections` de la API [!DNL Flow Service].

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
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `baseConnectionId` | Identificador de conexión base autenticada para el origen de flujo continuo [!DNL Snowflake]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | Id. de especificación de conexión para el origen de flujo continuo [!DNL Snowflake]. |
| `params.tableName` | Nombre de la tabla de la base de datos [!DNL Snowflake] que desea llevar a Experience Platform. |
| `params.timestampColumn` | Nombre de la columna de marca de tiempo que se utilizará para recuperar los valores incrementales. |
| `params.backfill` | Un indicador booleano que determina si los datos se recuperan desde el principio (hora de la época 0) o desde el momento en que se inicia el origen. Para obtener más información sobre este valor, lea la [[!DNL Snowflake] descripción general de la fuente de transmisión](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | El valor de zona horaria indica la hora actual de la zona horaria que debe recuperarse al consultar la base de datos [!DNL Snowflake]. Se debe proporcionar este parámetro si la columna de marca de tiempo de la configuración está establecida en `TIMESTAMP_NTZ`. Si no se proporciona `timezoneValue`, el valor predeterminado es UTC. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de origen y su etiqueta correspondiente. El ID de conexión de origen se utilizará en un paso posterior para crear un flujo de datos.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Creación de un flujo de datos

Para crear un flujo de datos para transmitir datos de la cuenta del recorrido [!DNL Snowflake] a Experience Platform, debe realizar una petición POST al extremo `/flows` y, al mismo tiempo, proporcionar los siguientes valores:

>[!TIP]
>
>Siga los vínculos a continuación para obtener guías paso a paso sobre cómo recuperar los siguientes ID.

* [ID de conexión de Source](#create-a-source-connection)
* [ID de conexión de destino](../../collect/database-nosql.md#create-a-target-connection)
* [ID de especificación de flujo](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID de asignación](../../collect/database-nosql.md#create-a-mapping)

**Formato de API**

```http
POST /flows
```

**Solicitud**

La siguiente solicitud crea un flujo de datos de flujo continuo para su cuenta de [!DNL Snowflake].

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
| `sourceConnectionIds` | Identificador de conexión de origen del origen de flujo continuo [!DNL Snowflake]. |
| `targetConnectionIds` | Identificador de conexión de destino del origen de flujo continuo [!DNL Snowflake]. |
| `flowSpec.id` | Id. de especificación de flujo para crear un flujo de datos para un origen de flujo continuo [!DNL Snowflake]. Este ID de especificación de flujo le permite crear un flujo de datos de flujo continuo con transformaciones de asignación. Este identificador se corrigió y es: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
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

Al seguir este tutorial, ha creado un flujo de datos de flujo continuo para los datos de [!DNL Snowflake] mediante la API [!DNL Flow Service]. Visite la siguiente documentación para obtener más información sobre las fuentes de Adobe Experience Platform:

* [Información general de fuentes](../../../../home.md)
* [Monitorización del flujo de datos mediante API](../../monitor.md)
