---
title: Crear una conexión de origen de Azure Event Hubs mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Azure Event Hubs mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b76bc6ddb0d49bbd089627c8df8b31703d0e50b1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# Crear un [!DNL Azure Event Hubs] conexión de origen mediante [!DNL Flow Service] API

>[!IMPORTANT]
>
>El [!DNL Azure Event Hubs] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial lo acompañará durante los pasos para conectarse [!DNL Azure Event Hubs] (en lo sucesivo, &quot;[!DNL Event Hubs]&quot;) al Experience Platform, utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Event Hubs] a Platform mediante el [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse con su [!DNL Event Hubs] En su cuenta de, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal del [!DNL Event Hubs] namespace. El `sasPolicy` que el `sasKey` corresponde a debe tener `manage` derechos configurados para el [!DNL Event Hubs] lista que se va a rellenar. |
| `namespace` | El área de nombres del [!DNL Event Hubs] está accediendo a. Un [!DNL Event Hubs] el espacio de nombres proporciona un contenedor de ámbito único, en el que puede crear uno o más [!DNL Event Hubs]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El [!DNL Event Hubs] ID de especificación de conexión: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obtener más información, consulte [este documento de Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

El primer paso para crear una conexión de origen es autenticar su [!DNL Event Hubs] y generar un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Event Hubs] credenciales de autenticación como parte de los parámetros de solicitud.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `auth.params.sasKey` | La firma de acceso compartido generada. |
| `auth.params.namespace` | El área de nombres del [!DNL Event Hubs] está accediendo a. |
| `connectionSpec.id` | El [!DNL Event Hubs] ID de especificación de conexión: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Crear una conexión de origen

>[!TIP]
>
>Un [!DNL Event Hubs] el grupo de consumidores solo se puede utilizar para un único flujo en un momento determinado.

Una conexión de origen crea y administra la conexión con el origen externo desde el que se incorporan los datos. Una conexión de origen consta de información como el origen de datos, el formato de datos y un ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica de un inquilino y una organización.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede proporcionar para incluir más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión de su [!DNL Event Hubs] origen que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL Event Hubs]. Este ID es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | El formato del [!DNL Event Hubs] datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |
| `params.eventHubName` | El nombre de su [!DNL Event Hubs] origen. |
| `params.dataType` | Este parámetro define el tipo de datos que se están introduciendo. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Uso `latest` para empezar a leer los datos más recientes, y utilice `earliest` para comenzar a leer los primeros datos disponibles en la secuencia. Este parámetro es opcional y el valor predeterminado es `earliest` si no se proporciona. |
| `params.consumerGroup` | Mecanismo de publicación o suscripción que se utilizará para [!DNL Event Hubs]. Este parámetro es opcional y el valor predeterminado es `$Default` si no se proporciona. Consulte esta sección [[!DNL Event Hubs] guía para consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obtener más información. **Nota**: Un [!DNL Event Hubs] el grupo de consumidores solo se puede utilizar para un único flujo en un momento determinado. |

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Event Hubs] conexión de origen mediante [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para lo siguiente [crear un flujo de datos de flujo continuo utilizando [!DNL Flow Service] API](../../collect/streaming.md).
