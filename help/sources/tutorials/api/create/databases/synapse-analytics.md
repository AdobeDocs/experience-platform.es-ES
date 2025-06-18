---
title: Conexión de Azure Synapse Analytics a Experience Platform mediante la API de Flow Service
description: Obtenga información sobre cómo conectar su cuenta de Azure Synapse Analytics a Experience Platform mediante API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---

# Conectar [!DNL Azure Synapse Analytics] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Azure Synapse Analytics] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea esta guía para aprender a conectar su cuenta de [!DNL Azure Synapse Analytics] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Azure Synapse Analytics] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL Azure Synapse Analytics] descripción general](../../../../connectors/databases/synapse-analytics.md#prerequisites) para obtener información sobre la autenticación.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Azure Synapse Analytics] a Experience Platform

Lea lo siguiente para aprender a crear una conexión base y conectar su cuenta de [!DNL Azure Synapse Analytics] a Experience Platform.

### Crear una conexión base

Una **conexión base** almacena información clave que vincula el sistema de origen con Adobe Experience Platform. Esto incluye lo siguiente:

* Credenciales de autenticación de origen
* El estado actual de la conexión
* Un **identificador de conexión base** único

El **identificador de conexión base** le permite examinar y explorar archivos de su origen, lo que le ayuda a identificar qué elementos introducir, junto con sus tipos de datos y formatos.

Para crear un identificador de conexión base, envíe una petición POST al extremo `/connections`, incluidas sus credenciales de autenticación [!DNL Azure Synapse Analytics] en los parámetros de la solicitud.

**Formato de API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación basada en cadena de conexión]

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Azure Synapse Analytics] mediante la autenticación basada en la cadena de conexión.

+++Ver solicitud de ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | Cadena de conexión utilizada para conectarse a [!DNL Azure Synapse Analytics]. El patrón de cadena de conexión [!DNL Azure Synapse Analytics] es `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Azure Synapse Analytics] es: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver respuesta de ejemplo

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Autenticación basada en clave principal de servicio]

La siguiente solicitud crea una conexión base para [!DNL Azure Synapse Analytics] mediante la autenticación basada en clave principal de servicio.

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Credencial | Descripción |
| --- | --- |
| `auth.params.server` | El nombre de dominio completo de su extremo SQL [!DNL Azure Synapse Analytics]. |
| `auth.params.database` | Nombre de la base de datos específica en el espacio de trabajo [!DNL Azure Synapse Analytics]. |
| `auth.params.tenant` | El identificador de inquilino [!DNL Azure Active Directory] asociado con su suscripción a [!DNL Azure]. |
| `auth.params.servicePrincipalId` | Id. de cliente de una aplicación [!DNL Azure Active Directory]. |
| `auth.params.servicePrincipalKey` | El secreto de cliente o la contraseña asociados con la entidad de seguridad de servicio. |
| `connectSpec.id` | Identificador de especificación de conexión de [!DNL Azure Synapse Analytics]. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver respuesta de ejemplo

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Azure Synapse Analytics] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
