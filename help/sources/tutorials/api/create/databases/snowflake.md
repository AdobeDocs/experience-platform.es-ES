---
title: Conexión de Snowflake a Experience Platform mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Snowflake mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 4%

---

# Conectar [!DNL Snowflake] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Snowflake] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea esta guía para saber cómo conectar su cuenta de origen de [!DNL Snowflake] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Snowflake] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL Snowflake] descripción general](../../../../connectors/databases/snowflake.md#prerequisites) para obtener información sobre la autenticación.

## Conectar [!DNL Snowflake] a Experience Platform en Azure {#azure}

>[!WARNING]
>
>La autenticación básica (o autenticación de clave de cuenta) para el origen [!DNL Snowflake] quedará obsoleta en noviembre de 2025. Debe pasar a la autenticación basada en pares de claves para seguir utilizando el origen e introduciendo datos de la base de datos en Experience Platform. Para obtener más información sobre la obsolescencia, lea la [[!DNL Snowflake] guía de prácticas recomendadas sobre cómo mitigar los riesgos de compromiso de credenciales](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL Snowflake] a Experience Platform en Azure.

>[!NOTE]
>
>Debe establecer el indicador `PREVENT_UNLOAD_TO_INLINE_URL` en `FALSE` para permitir la descarga de datos de la base de datos [!DNL Snowflake] en Experience Platform.

### Crear una conexión base para [!DNL Snowflake] en Experience Platform en Azure {#azure-base}

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Snowflake] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB CadenaDeConexión]

+++Solicitud

La siguiente solicitud crea una conexión base para [!DNL Snowflake]:

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
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | Cadena de conexión utilizada para conectarse a la instancia [!DNL Snowflake]. El patrón de cadena de conexión de [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Respuesta

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Autenticación de par de claves con clave privada cifrada]

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.account` | El nombre de su cuenta de [!DNL Snowflake]. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Snowflake]. |
| `auth.params.database` | Base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.privateKey` | La clave privada cifrada [!DNL Base64-] de su cuenta [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | La frase de contraseña que corresponde con su clave privada. |
| `auth.params.warehouse` | El almacén de [!DNL Snowflake] que está utilizando. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Autenticación de par de claves con clave privada no cifrada]

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.account` | El nombre de su cuenta de [!DNL Snowflake]. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Snowflake]. |
| `auth.params.database` | Base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.privateKey` | La clave privada no cifrada [!DNL Base64-] de su cuenta [!DNL Snowflake]. |
| `auth.params.warehouse` | El almacén de [!DNL Snowflake] que está utilizando. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Conectar [!DNL Snowflake] a Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL Snowflake] a Experience Platform en AWS.

### Crear una conexión base para [!DNL Snowflake] en Experience Platform en AWS {#aws-base}

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación básica]

La siguiente solicitud crea una conexión base para que [!DNL Snowflake] ingrese datos en Experience Platform en AWS:

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.host` | La URL de host a la que se conecta su cuenta de [!DNL Snowflake]. |
| `auth.params.port` | Número de puerto que usa [!DNL Snowflake] al conectarse a un servidor a través de Internet. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Snowflake]. |
| `auth.params.database` | Base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.password` | La contraseña asociada a su cuenta de [!DNL Snowflake]. |
| `auth.params.warehouse` | El almacén de [!DNL Snowflake] que está utilizando. |
| `auth.params.schema` | Nombre del esquema asociado con la base de datos [!DNL Snowflake]. Debe asegurarse de que el usuario al que desea otorgar acceso a la base de datos también tenga acceso a este esquema. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!TAB Autenticación de par de claves con clave privada no cifrada]

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.account` | El nombre de su cuenta de [!DNL Snowflake]. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Snowflake]. |
| `auth.params.database` | Base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.privateKey` | La clave privada no cifrada [!DNL Base64-] de su cuenta [!DNL Snowflake]. |
| `auth.params.warehouse` | El almacén de [!DNL Snowflake] que está utilizando. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++


+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

Siguiendo este tutorial, ha creado una conexión base [!DNL Snowflake] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
