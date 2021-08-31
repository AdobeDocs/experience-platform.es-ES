---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Crear una conexión de Google PubSub Source mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Google PubSub mediante la API de servicio de flujo.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Google PubSub] mediante la API del servicio de flujo

>[!NOTE]
>
>El conector [!DNL Google PubSub] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial le guía por los pasos para conectar [!DNL Google PubSub] (en adelante denominado &quot;[!DNL PubSub]&quot;) con el Experience Platform, utilizando la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectar correctamente [!DNL PubSub] a Platform mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL PubSub], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | El ID de proyecto necesario para autenticarse [!DNL PubSub]. |
| `credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones de destino de origen y base. El ID de especificación de conexión [!DNL PubSub] es: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Para obtener más información sobre estos valores, consulte este documento [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication). Para utilizar la autenticación basada en cuentas de servicio, consulte esta [[!DNL PubSub] guía sobre la creación de cuentas de servicio](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar las credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

El primer paso para crear una conexión de origen es autenticar el origen [!DNL PubSub] y generar un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL PubSub] como parte de los parámetros de solicitud.

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
| `auth.params.projectId` | El ID de proyecto necesario para autenticarse [!DNL PubSub]. |
| `auth.params.credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

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

Para crear una conexión de origen, realice una solicitud de POST al extremo `/sourceConnections` de la API [!DNL Flow Service].

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
| `baseConnectionId` | El ID de conexión base del origen [!DNL PubSub] que se generó en el paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión fija para [!DNL PubSub]. Este ID es : `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | El formato de los datos [!DNL PubSub] que desea introducir. Actualmente, el único formato de datos admitido es `json`. |
| `params.topicId` | El ID del tema define el recurso con nombre específico que los editores envían a los mensajes |
| `params.subscriptionId` | El ID de suscripción define el recurso con nombre específico que representa el flujo de mensajes de un solo tema específico que se enviarán a la aplicación de suscripción. |
| `params.dataType` | Este parámetro define el tipo de datos que se están incorporando. Los tipos de datos admitidos son: `raw` y `xdm`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de origen [!DNL PubSub] utilizando la API [!DNL Flow Service]. Puede utilizar este ID de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo mediante la [!DNL Flow Service] API](../../collect/streaming.md).
