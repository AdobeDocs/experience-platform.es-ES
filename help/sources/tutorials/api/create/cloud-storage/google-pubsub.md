---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Create a Google PubSub Source Connection Using the Flow Service API
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Google PubSub mediante la API de servicio de flujo.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# Create a [!DNL Google PubSub] Source Connection Using the Flow Service API

Este tutorial le guía por los pasos para conectarse [!DNL Google PubSub] (en lo sucesivo, &quot;el[!DNL PubSub]&quot;) al Experience Platform, usando el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL PubSub] a Platform que utiliza la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

In order for [!DNL Flow Service] to connect to [!DNL PubSub], you must provide values for the following connection properties:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | ID del proyecto necesario para la autenticación [!DNL PubSub]. |
| `credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | The connection specification returns a source’s connector properties, including authentication specifications related to creating the base and source target connections. La variable [!DNL PubSub] el ID de especificación de conexión es: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Para obtener más información sobre estos valores, consulte esta [[!DNL PubSub] autenticación](https://cloud.google.com/pubsub/docs/authentication) documento. Para utilizar la autenticación basada en cuentas de servicio, consulte esta [[!DNL PubSub] guía sobre la creación de cuentas de servicio](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

El primer paso para crear una conexión de origen es autenticar su [!DNL PubSub] y genere un ID de conexión base. A base connection ID allows you to explore and navigate files from within your source and identify specific items that you want to ingest, including information regarding their data types and formats.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL PubSub] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.projectId` | The project ID required to authenticate [!DNL PubSub]. |
| `auth.params.credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | La variable [!DNL PubSub] id. de especificación de conexión: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID de conexión base es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Crear una conexión de origen {#source}

Una conexión de origen crea y administra la conexión con el origen externo desde el que se introducen los datos. Una conexión de origen consiste en información como el origen de datos, el formato de datos y un ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica para un inquilino y una organización IMS.

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
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede proporcionar para incluir más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión base de su [!DNL PubSub] fuente que se generó en el paso anterior. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL PubSub]. This ID is: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | The format of the [!DNL PubSub] data that you want to ingest. Currently, the only supported data format is `json`. |
| `params.topicId` | El ID del tema define el recurso con nombre específico que los editores envían a los mensajes |
| `params.subscriptionId` | El ID de suscripción define el recurso con nombre específico que representa el flujo de mensajes de un solo tema específico que se enviarán a la aplicación de suscripción. |
| `params.dataType` | Este parámetro define el tipo de datos que se están incorporando. Supported data types include: `raw` and `xdm`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL PubSub] conexión de origen utilizando la variable [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo mediante el [!DNL Flow Service] API](../../collect/streaming.md).
