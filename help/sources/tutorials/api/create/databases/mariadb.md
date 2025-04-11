---
title: Conectar MariaDB a Experience Platform mediante la API de Flow Service
description: Aprenda a conectar su cuenta de MariaDB a Experience Platform mediante API.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# Conectar [!DNL MariaDB] a Experience Platform mediante la API [!DNL Flow Service]

Lea esta guía para aprender a conectar su cuenta de [!DNL MariaDB] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL MariaDB] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL MariaDB] descripción general](../../../../connectors/databases/mariadb.md#prerequisites) para obtener información sobre la autenticación.

### Uso Experience Platform API

Lea el guía sobre [cómo empezar a usar Experience Platform API](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas con éxito a Experience Platform API.

## Conexión [!DNL MariaDB] a Experience Platform en Azure {#azure}

Lea los pasos siguientes para obtener información sobre cómo conectar su [!DNL MariaDB] cuenta a Experience Platform en Azure.

### Crear una conexión base para [!DNL MariaDB] en Experience Platform en Azure {#azure-base}

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

**Formato de API**

```https
POST /connections
```

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione las credenciales de autenticación adecuadas para su cuenta de [!DNL MariaDB].

>[!BEGINTABS]

>[!TAB Autenticación basada en cadena de conexión]

**Solicitud**

La siguiente solicitud crea una conexión base para un origen de [!DNL MariaDB] mediante la autenticación basada en la cadena de conexión.

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión asociada con su autenticación [!DNL MariaDB]. El patrón de cadena de conexión [!DNL MariaDB] es: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL MariaDB] es: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver ejemplo de respuesta

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB Autenticación básica]

**Solicitud**

La siguiente solicitud crea una conexión básica para un [!DNL MariaDB] origen mediante autenticación básica.

+++Ver solicitud ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
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
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre o IP de su base de datos [!DNL MariaDB]. |
| `auth.params.database` | Nombre de la base de datos. |
| `auth.params.username` | El nombre de usuario que corresponde con su base de datos. |
| `auth.params.password` | La contraseña que corresponde a su base de datos. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL MariaDB] es: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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

>[!ENDTABS]

## Conectar [!DNL MariaDB] a Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL MariaDB] a Experience Platform en AWS.

### Crear una conexión básica para [!DNL MariaDB] On Experience Platform en AWS {#aws-base}

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para que [!DNL MariaDB] se conecte a Experience Platform en AWS.

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
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
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
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre o IP de su base de datos [!DNL MariaDB]. |
| `auth.params.database` | Nombre de la base de datos. |
| `auth.params.username` | El nombre de usuario que corresponde con su base de datos. |
| `auth.params.password` | La contraseña que corresponde a su base de datos. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL MariaDB] es: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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


## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL MariaDB] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
