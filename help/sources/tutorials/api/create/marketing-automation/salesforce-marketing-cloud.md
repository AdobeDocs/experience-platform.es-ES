---
title: Conexión de Salesforce Marketing Cloud a Experience Platform mediante la API de Flow Service
description: Obtenga información sobre cómo conectar su cuenta de Salesforce Marketing Cloud a Experience Platform mediante API.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---

# Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la API [!DNL Flow Service]

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto en enero de 2026. Una nueva fuente se publicará a finales de este año como alternativa. Una vez lanzada la nueva fuente, debe planificar la migración a la nueva fuente creando nuevas conexiones de cuenta y flujos de datos antes de finales de enero de 2026.

Lea esta guía para aprender a conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Azure Synapse Analytics] mediante la API [!DNL Flow Service].


### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Salesforce Marketing Cloud] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL Salesforce Marketing Cloud] descripción general de la autenticación](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md) para obtener información sobre la autenticación.

### Uso de API de Experience Platform

Lea la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas a las API de Experience Platform correctamente.

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform en [!DNL Azure]

Lea lo siguiente para aprender a crear una conexión base y conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Experience Platform en [!DNL Azure].

### Crear una conexión base {#azure-base}

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

Una **conexión base** almacena información clave que vincula el sistema de origen con Adobe Experience Platform. Esto incluye lo siguiente:

* Credenciales de autenticación de origen
* El estado actual de la conexión
* Un **identificador de conexión base** único

El **identificador de conexión base** le permite examinar y explorar archivos de su origen, lo que le ayuda a identificar qué elementos introducir, junto con sus tipos de datos y formatos.

Para crear un identificador de conexión base, envíe una petición POST al extremo `/connections`, incluidas sus credenciales de autenticación [!DNL Salesforce Marketing Cloud] en los parámetros de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce Marketing Cloud].

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
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | Identificador de cliente asociado con la aplicación [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Ver respuesta de ejemplo

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Experience Platform en AWS.

### Crear una conexión base {#aws-base}

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para que [!DNL Salesforce Service Cloud] se conecte a Experience Platform en AWS.

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
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver ejemplo de respuesta

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Crear un flujo de datos para [!DNL Salesforce Marketing Cloud] datos

Ahora que ha conectado correctamente su cuenta de [!DNL Salesforce Marketing Cloud], puede [crear un flujo de datos e introducir datos de su proveedor de automatización de marketing en Experience Platform](../../collect/marketing-automation.md).