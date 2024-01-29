---
title: Creación de una conexión base de Snowflake mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Snowflake mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# Crear un [!DNL Snowflake] conexión base mediante el [!DNL Flow Service] API

>[!IMPORTANT]
>
>El [!DNL Snowflake] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Utilice el siguiente tutorial para aprender a crear una conexión base para [!DNL Snowflake] uso del [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Snowflake] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes propiedades de credenciales para autenticar su [!DNL Snowflake] origen.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

| Credencial | Descripción |
| ---------- | ----------- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes [!DNL Snowflake] organizaciones. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la [!DNL Snowflake] documentación sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |
| `database` | El [!DNL Snowflake] La base de datos de contiene los datos que desea traer a Platform. |
| `username` | El nombre de usuario de [!DNL Snowflake] cuenta. |
| `password` | La contraseña para el [!DNL Snowflake] cuenta de usuario. |
| `role` | La función de control de acceso predeterminada que se utilizará en [!DNL Snowflake] sesión. La función debe ser una función existente que ya se haya asignado al usuario especificado. La función predeterminada es `PUBLIC`. |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] ejemplo. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticación de par de claves]

Para utilizar la autenticación de par clave, debe generar un par clave RSA de 2048 bits y, a continuación, proporcionar los siguientes valores al crear una cuenta para su [!DNL Snowflake] origen.

| Credencial | Descripción |
| --- | --- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes [!DNL Snowflake] organizaciones. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la [!DNL Snowflake] documentación sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | El nombre de usuario de su [!DNL Snowflake] cuenta. |
| `privateKey` | El [!DNL Base64-]clave privada codificada de su [!DNL Snowflake] cuenta. Puede generar claves privadas cifradas o no cifradas. Si utiliza una clave privada cifrada, también debe proporcionar una frase de contraseña de clave privada al autenticarse con el Experience Platform. |
| `privateKeyPassphrase` | La frase de contraseña de clave privada es una capa adicional de seguridad que debe utilizar al autenticarse con una clave privada cifrada. No es necesario que proporcione la frase de contraseña si utiliza una clave privada no cifrada. |
| `database` | El [!DNL Snowflake] base de datos que contiene los datos que desea introducir en Experience Platform. |
| `warehouse` | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] el almacén es independiente entre sí y se debe acceder a él de forma individual al llevar los datos al Experience Platform. |

Para obtener más información sobre estos valores, consulte la [[!DNL Snowflake] guía de autenticación de par de claves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Debe configurar la variable `PREVENT_UNLOAD_TO_INLINE_URL` marcar como `FALSE` para permitir la descarga de datos desde [!DNL Snowflake] base de datos a Experience Platform.

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Snowflake] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

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
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] ejemplo. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | El [!DNL Snowflake] identificador de especificación de conexión: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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
| `auth.params.account` | El nombre de su [!DNL Snowflake] cuenta. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Snowflake] cuenta. |
| `auth.params.database` | El [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.privateKey` | El [!DNL Base64-]clave privada cifrada codificada de su [!DNL Snowflake] cuenta. |
| `auth.params.privateKeyPassphrase` | La frase de contraseña que corresponde con su clave privada. |
| `auth.params.warehouse` | El [!DNL Snowflake] almacén que está utilizando. |
| `connectionSpec.id` | El [!DNL Snowflake] identificador de especificación de conexión: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
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
| `auth.params.account` | El nombre de su [!DNL Snowflake] cuenta. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Snowflake] cuenta. |
| `auth.params.database` | El [!DNL Snowflake] de la que se extraerán los datos. |
| `auth.params.privateKey` | El [!DNL Base64-]clave privada no cifrada codificada de su [!DNL Snowflake] cuenta. |
| `auth.params.warehouse` | El [!DNL Snowflake] almacén que está utilizando. |
| `connectionSpec.id` | El [!DNL Snowflake] identificador de especificación de conexión: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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

>[!ENDTABS]

Al seguir este tutorial, ha creado un [!DNL Snowflake] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
