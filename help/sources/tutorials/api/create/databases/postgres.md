---
title: Conectar PostgreSQL a Experience Platform mediante la API de Flow Service
description: Aprenda a conectar su base de datos de  [!DNL PostgreSQL]  a Experience Platform mediante API.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 5348158f6de9fea1a9fe186a14409afb7e7a376e
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 3%

---

# Crear una conexión base [!DNL PostgreSQL] mediante la API [!DNL Flow Service]

Lea esta guía para aprender a conectar su base de datos de [!DNL PostgreSQL] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL PostgreSQL] mediante la API [!DNL Flow Service].

### Uso de API de Experience Platform

Lea la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas a las API de Experience Platform correctamente.

### Recopilar credenciales necesarias

Lea la [[!DNL PostgreSQL] descripción general](../../../../connectors/databases/postgres.md) para obtener más información sobre la autenticación.

### Habilitar el cifrado SSL para la cadena de conexión

Puede habilitar el cifrado SSL para la cadena de conexión [!DNL PostgreSQL] adjuntando la cadena de conexión con las siguientes propiedades:

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `EncryptionMethod` | Permite habilitar el cifrado SSL en los datos de [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(deshabilitado)</li><li>`EncryptionMethod=1`(Habilitado)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valida el certificado enviado por la base de datos [!DNL PostgreSQL] cuando se aplica `EncryptionMethod`. | <uL><li>`ValidationServerCertificate=0`(deshabilitado)</li><li>`ValidationServerCertificate=1`(Habilitado)</li></ul> |

El siguiente es un ejemplo de una cadena de conexión [!DNL PostgreSQL] anexada con cifrado SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Conectar [!DNL PostgreSQL] a Experience Platform en Azure {#azure}

Lea los pasos siguientes para aprender a conectar su cuenta de [!DNL PostgreSQL] a Experience Platform en Azure.

### Crear una conexión base {#azure-base}

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL PostgreSQL] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación basada en clave de cuenta]

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL PostgreSQL] mediante la autenticación basada en clave de cuenta:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta de [!DNL PostgreSQL]. El patrón de cadena de conexión [!DNL PostgreSQL] es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Los identificadores de especificación de conexión [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada.

+++Ver ejemplo de respuesta

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB Autenticación básica]

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL PostgreSQL] mediante autenticación básica:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| ---| --- |
| `auth.params.server` | Nombre o dirección IP de la base de datos [!DNL PostgreSQL]. |
| `auth.params.port` | Número de puerto del servidor de la base de datos. |
| `auth.params.database` | Nombre de su base de datos [!DNL PostgreSQL]. |
| `auth.params.username` | El nombre de usuario asociado con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `auth.params.password` | La contraseña asociada con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. Los valores disponibles incluyen: `Disable`, `Allow`, `Prefer`, `Verify Ca` y `Verify Full`. |
| `connectionSpec.id` | Los identificadores de especificación de conexión [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada.

+++Ver ejemplo de respuesta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Conectar [!DNL PostgreSQL] a Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos siguientes para obtener información sobre cómo conectar su base de datos de [!DNL PostgreSQL] a Experience Platform en AWS.

### Crear una conexión base {#aws-base}

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL PostgreSQL] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para que [!DNL PostgreSQL] se conecte a Experience Platform en AWS.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| ---| --- |
| `auth.params.server` | Nombre o dirección IP de la base de datos [!DNL PostgreSQL]. |
| `auth.params.port` | Número de puerto del servidor de la base de datos. |
| `auth.params.database` | Nombre de su base de datos [!DNL PostgreSQL]. |
| `auth.params.username` | El nombre de usuario asociado con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `auth.params.password` | La contraseña asociada con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `auth.params.sslMode` | Método por el que se cifran los datos durante la transferencia de datos. Los valores disponibles incluyen: `Disable`, `Allow`, `Prefer`, `Verify Ca` y `Verify Full`. |
| `connectionSpec.id` | Los identificadores de especificación de conexión [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada.

+++Ver ejemplo de respuesta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Pasos siguientes

Ahora que ha creado una conexión entre su base de datos [!DNL PostgreSQL] y Experience Platform, puede continuar con los siguientes pasos y llevar los datos de [!DNL PostgreSQL] a Experience Platform. Para obtener más información, lea la siguiente documentación:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
