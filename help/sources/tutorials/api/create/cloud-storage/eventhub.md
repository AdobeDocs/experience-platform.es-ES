---
title: Crear una conexión de Azure Event Hubs con Source mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Azure Event Hubs mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Azure Event Hubs] mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Azure Event Hubs] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea este tutorial para aprender a conectar [!DNL Azure Event Hubs] (denominado en adelante &quot;[!DNL Event Hubs]&quot;) a Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
- [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectar correctamente [!DNL Event Hubs] a Experience Platform mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta de [!DNL Event Hubs], debe proporcionar valores para las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación estándar]

| Credencial | Descripción |
| --- | --- |
| `sasKeyName` | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal del espacio de nombres [!DNL Event Hubs]. El `sasPolicy` al que corresponde el `sasKey` debe tener `manage` derechos configurados para que se rellene la lista [!DNL Event Hubs]. |
| `namespace` | El área de nombres de [!DNL Event Hub] al que está accediendo. Un espacio de nombres [!DNL Event Hub] proporciona un contenedor de ámbito único, en el que puede crear uno o varios [!DNL Event Hubs]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB Autenticación SAS]

| Credencial | Descripción |
| --- | --- |
| `sasKeyName` | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal del espacio de nombres [!DNL Event Hubs]. El `sasPolicy` al que corresponde el `sasKey` debe tener `manage` derechos configurados para que se rellene la lista [!DNL Event Hubs]. |
| `namespace` | El área de nombres de [!DNL Event Hub] al que está accediendo. Un espacio de nombres [!DNL Event Hub] proporciona un contenedor de ámbito único, en el que puede crear uno o varios [!DNL Event Hubs]. |
| `eventHubName` | Rellene su nombre de [!DNL Azure Event Hub]. Lea la [documentación de Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) para obtener más información sobre [!DNL Event Hub] nombres. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obtener más información sobre la autenticación de firmas de acceso compartido (SAS) para [!DNL Event Hubs], lea la [[!DNL Azure] guía sobre el uso de SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Autenticación de Active Directory de Azure del centro de eventos]

| Credencial | Descripción |
| --- | --- |
| `tenantId` | El ID de inquilino desde el que desea solicitar permiso. Su ID de inquilino puede tener el formato de GUID o de nombre descriptivo. **Nota**: El identificador de inquilino se conoce como &quot;Id. de directorio&quot; en la interfaz [!DNL Microsoft Azure]. |
| `clientId` | El ID de aplicación asignado a su aplicación. Puede recuperar este identificador del portal [!DNL Microsoft Entra ID] donde registró su [!DNL Azure Active Directory]. |
| `clientSecretValue` | El secreto de cliente que se utiliza junto con el ID de cliente para autenticar la aplicación. Puede recuperar el secreto de cliente del portal [!DNL Microsoft Entra ID] en el que registró su [!DNL Azure Active Directory]. |
| `namespace` | El área de nombres de [!DNL Event Hub] al que está accediendo. Un espacio de nombres [!DNL Event Hub] proporciona un contenedor de ámbito único, en el que puede crear uno o varios [!DNL Event Hubs]. |

Para obtener más información sobre [!DNL Azure Active Directory], lea la guía de [Azure sobre el uso del Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Autenticación de Azure Active Directory con ámbito de concentrador de eventos]

| Credencial | Descripción |
| --- | --- |
| `tenantId` | El ID de inquilino desde el que desea solicitar permiso. Su ID de inquilino puede tener el formato de GUID o de nombre descriptivo. **Nota**: El identificador de inquilino se conoce como &quot;Id. de directorio&quot; en la interfaz [!DNL Microsoft Azure]. |
| `clientId` | El ID de aplicación asignado a su aplicación. Puede recuperar este identificador del portal [!DNL Microsoft Entra ID] donde registró su [!DNL Azure Active Directory]. |
| `clientSecretValue` | El secreto de cliente que se utiliza junto con el ID de cliente para autenticar la aplicación. Puede recuperar el secreto de cliente del portal [!DNL Microsoft Entra ID] en el que registró su [!DNL Azure Active Directory]. |
| `namespace` | El área de nombres de [!DNL Event Hub] al que está accediendo. Un espacio de nombres [!DNL Event Hub] proporciona un contenedor de ámbito único, en el que puede crear uno o varios [!DNL Event Hubs]. |
| `eventHubName` | Rellene su nombre de [!DNL Azure Event Hub]. Lea la [documentación de Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) para obtener más información sobre [!DNL Event Hub] nombres. |

>[!ENDTABS]

Para obtener más información sobre estos valores, consulte [este documento de Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Event Hubs]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

El primer paso para crear una conexión de origen es autenticar el origen de [!DNL Event Hubs] y generar un identificador de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Event Hubs] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación estándar]

Para crear una cuenta con autenticación estándar, realice una petición POST al extremo `/connections` y proporcione los valores para `sasKeyName`, `sasKey` y `namespace`.

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
| `auth.params.namespace` | El área de nombres de [!DNL Event Hubs] al que está accediendo. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticación SAS]

Para crear una cuenta con autenticación SAS, realice una petición POST al extremo `/connections` y proporcione los valores para `sasKeyName`, `sasKey`, `namespace` y `eventHubName`.

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
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
| `auth.params.namespace` | El área de nombres de [!DNL Event Hubs] al que está accediendo. |
| `params.eventHubName` | Nombre del origen de [!DNL Event Hubs]. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticación de Active Directory de Azure del centro de eventos]

Para crear una cuenta mediante la autenticación de Azure Active Directory, realice una petición POST al extremo `/connections` y proporcione los valores para `tenantId`, `clientId`, `clientSecretValue` y `namespace`.

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
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
| `auth.params.tenantId` | El ID de inquilino de su aplicación. **Nota**: El identificador de inquilino se conoce como &quot;Id. de directorio&quot; en la interfaz [!DNL Microsoft Azure]. |
| `auth.params.clientId` | El ID de cliente de su organización. |
| `auth.params.clientSecretValue` | El valor secreto de cliente de su organización. |
| `auth.params.namespace` | El área de nombres de [!DNL Event Hubs] al que está accediendo. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticación de Azure Active Directory con ámbito de concentrador de eventos]

Para crear una cuenta mediante la autenticación de Azure Active Directory, realice una petición POST al extremo `/connections` y proporcione los valores para `tenantId`, `clientId`, `clientSecretValue`, `namespace` y `eventHubName`.

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
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
| `auth.params.tenantId` | El ID de inquilino de su aplicación. **Nota**: El identificador de inquilino se conoce como &quot;Id. de directorio&quot; en la interfaz [!DNL Microsoft Azure]. |
| `auth.params.clientId` | El ID de cliente de su organización. |
| `auth.params.clientSecretValue` | El valor secreto de cliente de su organización. |
| `auth.params.namespace` | El área de nombres de [!DNL Event Hubs] al que está accediendo. |
| `auth.params.eventHubName` | Nombre del origen de [!DNL Event Hubs]. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Event Hubs] es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID de conexión es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Crear una conexión de origen

>[!TIP]
>
>Un grupo de consumidores [!DNL Event Hubs] solo se puede usar para un solo flujo a la vez.

Una conexión de origen crea y administra la conexión con el origen externo desde el que se incorporan los datos. Una conexión de origen consta de información como el origen de datos, el formato de datos y un ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica de un inquilino y una organización.

Para crear una conexión de origen, realice una petición POST al extremo `/sourceConnections` de la API [!DNL Flow Service].

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
          "eventHubName": "{EVENT_HUB_NAME}",
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
| `baseConnectionId` | Identificador de conexión del origen [!DNL Event Hubs] que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL Event Hubs]. Este identificador es: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Formato de los datos de [!DNL Event Hubs] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `params.eventHubName` | Nombre del origen de [!DNL Event Hubs]. |
| `params.dataType` | Este parámetro define el tipo de datos que se están introduciendo. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Use `latest` para comenzar a leer los datos más recientes y use `earliest` para comenzar a leer los primeros datos disponibles en el flujo. Este parámetro es opcional y el valor predeterminado es `earliest` si no se proporciona. |
| `params.consumerGroup` | Mecanismo de publicación o suscripción que se utilizará para [!DNL Event Hubs]. Este parámetro es opcional y el valor predeterminado es `$Default` si no se proporciona. Consulte esta [[!DNL Event Hubs] guía sobre consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obtener más información. **Nota**: Un grupo de consumidores [!DNL Event Hubs] solo se puede usar para un solo flujo en un momento dado. |

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de origen [!DNL Event Hubs] mediante la API [!DNL Flow Service]. Puede usar este identificador de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo usando la [!DNL Flow Service] API](../../collect/streaming.md).
