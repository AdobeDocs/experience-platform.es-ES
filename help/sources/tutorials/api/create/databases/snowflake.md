---
keywords: Experience Platform;inicio;temas populares;Snowflake;snowflake
solution: Experience Platform
title: Creación de una conexión base de Snowflake mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Snowflake mediante la API de Flow Service.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Crear un [!DNL Snowflake] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Snowflake] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Snowflake] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Snowflake], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `account` | El nombre completo de la cuenta asociado con su [!DNL Snowflake] cuenta. Un completo [!DNL Snowflake] nombre de cuenta incluye su nombre de cuenta, región y cloud platform. Por ejemplo, `cj12345.east-us-2.azure`. Para obtener más información sobre los nombres de cuenta, consulte esta sección [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén de datos es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |
| `database` | El [!DNL Snowflake] La base de datos de contiene los datos que desea traer a Platform. |
| `username` | El nombre de usuario de [!DNL Snowflake] cuenta. |
| `password` | La contraseña para el [!DNL Snowflake] cuenta de usuario. |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] ejemplo. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Snowflake] es `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Snowflake] documento](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Snowflake] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

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
          "specName": "ConnectionString,
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

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Al seguir este tutorial, ha creado un [!DNL Snowflake] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
