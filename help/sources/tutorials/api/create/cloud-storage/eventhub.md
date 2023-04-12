---
keywords: Experience Platform;inicio;temas populares;centro de eventos;centro de eventos de Azure;centro de eventos
solution: Experience Platform
title: Creación de una conexión de origen de los centros de eventos de Azure mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de centros de eventos de Azure mediante la API de servicio de flujo.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---


# Cree un [!DNL Azure Event Hubs] conexión de origen utilizando la variable [!DNL Flow Service] API

Este tutorial le guía por los pasos para conectarse [!DNL Azure Event Hubs] (en lo sucesivo, &quot;el[!DNL Event Hubs]&quot;) al Experience Platform, usando el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Event Hubs] a Platform que utiliza la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con su [!DNL Event Hubs] debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | El nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal de la variable [!DNL Event Hubs] espacio de nombres. La variable `sasPolicy` que `sasKey` corresponde a debe tener `manage` derechos configurados en orden para la variable [!DNL Event Hubs] para rellenar. |
| `namespace` | El espacio de nombres de la variable [!DNL Event Hubs] está accediendo. Un [!DNL Event Hubs] namespace proporciona un contenedor de ámbitos único, en el que puede crear uno o más [!DNL Event Hubs]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. La variable [!DNL Event Hubs] el ID de especificación de conexión es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obtener más información sobre estos valores, consulte [este documento de centros de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

El primer paso para crear una conexión de origen es autenticar su [!DNL Event Hubs] y genere un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Event Hubs] credenciales de autenticación como parte de los parámetros de solicitud.

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
| `auth.params.sasKeyName` | El nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `auth.params.sasKey` | La firma de acceso compartido generada. |
| `auth.params.namespace` | El espacio de nombres de la variable [!DNL Event Hubs] está accediendo. |
| `connectionSpec.id` | La variable [!DNL Event Hubs] el ID de especificación de conexión es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Crear una conexión de origen

Una conexión de origen crea y administra la conexión con el origen externo desde el que se introducen los datos. Una conexión de origen consiste en información como el origen de datos, el formato de datos y un ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica para un inquilino y una organización.

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
| `baseConnectionId` | El ID de conexión de su [!DNL Event Hubs] fuente que se generó en el paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión fija para [!DNL Event Hubs]. Este ID es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | El formato de la variable [!DNL Event Hubs] datos que desea ingerir. Actualmente, el único formato de datos admitido es `json`. |
| `params.eventHubName` | El nombre de su [!DNL Event Hubs] fuente. |
| `params.dataType` | Este parámetro define el tipo de datos que se están incorporando. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Uso `latest` para empezar a leer los datos más recientes y usar `earliest` para empezar a leer los primeros datos disponibles del flujo. Este parámetro es opcional y el valor predeterminado es `earliest` si no se proporciona. |
| `params.consumerGroup` | El mecanismo de publicación o suscripción para el que se va a usar [!DNL Event Hubs]. Este parámetro es opcional y el valor predeterminado es `$Default` si no se proporciona. Consulte esta [[!DNL Event Hubs] guía para consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obtener más información. |

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Event Hubs] conexión de origen utilizando la variable [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo mediante el [!DNL Flow Service] API](../../collect/streaming.md).
