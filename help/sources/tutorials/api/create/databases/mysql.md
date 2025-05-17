---
title: Conectar MySQL a Experience Platform mediante la API de Flow Service
description: Aprenda a conectar la base de datos MySQL a Experience Platform mediante API.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 659af23c6d05f184b745e13ab8545941f3892e7e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 5%

---

# Conectar [!DNL MySQL] a Experience Platform mediante la API [!DNL Flow Service]

Lea esta guía para aprender a conectar su cuenta de [!DNL MySQL] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL MySQL] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL MySQL] descripción general](../../../../connectors/databases/mysql.md#prerequisites) para obtener información sobre la autenticación.

### Uso de API de Experience Platform

Lea la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas a las API de Experience Platform correctamente.

## Conectar [!DNL MySQL] a Experience Platform en Azure {#azure}

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL MySQL] a Experience Platform en Azure.

### Crear una conexión base para [!DNL MySQL] en Experience Platform en Azure {#azure-base}

Una conexión base vincula el origen a Experience Platform y almacena los detalles de autenticación, el estado de la conexión y un ID único. Utilice este ID para examinar los archivos de origen e identificar elementos específicos que se van a introducir, incluidos sus tipos de datos y formatos.

**Formato de API**

```https
POST /connections
```

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL MySQL] como parte de los parámetros de solicitud.

>[!BEGINTABS]

>[!TAB Autenticación basada en cadena de conexión]

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL MySQL] mediante la autenticación basada en la cadena de conexión.

+++Ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.connectionString` | La cadena de conexión [!DNL MySQL] asociada a su cuenta. El patrón de cadena de conexión [!DNL MySQL] es: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver ejemplo de respuesta

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB Autenticación básica]

**Solicitud**

La siguiente solicitud crea una conexión base para un origen de [!DNL MySQL] mediante autenticación básica.

+++Ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre o IP de su base de datos [!DNL MySQL]. |
| `auth.params.database` | Nombre de la base de datos. |
| `auth.params.username` | El nombre de usuario que corresponde con su base de datos. |
| `auth.params.password` | La contraseña que corresponde a su base de datos. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL MySQL] es: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver ejemplo de respuesta

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Conectar [!DNL MySQL] a Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL MySQL] a Experience Platform en AWS.

### Crear una conexión base para [!DNL MySQL] en Experience Platform en AWS {#aws-base}

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para que [!DNL MySQL] se conecte a Experience Platform en AWS.

+++Ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre o IP de su base de datos [!DNL MySQL]. |
| `auth.params.database` | Nombre de la base de datos. |
| `auth.params.username` | El nombre de usuario que corresponde con su base de datos. |
| `auth.params.password` | La contraseña que corresponde a su base de datos. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL MySQL] es: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver ejemplo de respuesta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Crear un flujo de datos para [!DNL MySQL] datos

Ahora que ha conectado correctamente su base de datos de [!DNL MySQL], puede [crear un flujo de datos e introducir datos de su base de datos en Experience Platform](../../collect/database-nosql.md).