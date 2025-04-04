---
title: Creación de una conexión de Google PubSub Source mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a una cuenta PubSub de Google mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 2%

---

# Crear una conexión de Source [!DNL Google PubSub] mediante la API de Flow Service

>[!IMPORTANT]
>
>El origen [!DNL Google PubSub] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Este tutorial lo guiará para conectar [!DNL Google PubSub] (denominado en adelante &quot;[!DNL PubSub]&quot;) a Experience Platform mediante la [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectar correctamente [!DNL PubSub] a Experience Platform mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Debe proporcionar valores para las propiedades de conexión que se indican a continuación para conectar su cuenta de [!DNL PubSub] a [!DNL Flow Service]. Para obtener más información sobre la autenticación y la configuración de requisitos previos, lea la [[!DNL PubSub source] descripción general](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Autenticación basada en proyecto]

| Credencial | Descripción |
| --- | --- |
| `projectId` | Identificador de proyecto necesario para autenticar [!DNL PubSub]. |
| `credentials` | Credencial necesaria para autenticar [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones de destino base y de origen. El id. de especificación de conexión [!DNL PubSub] es: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Autenticación basada en temas y suscripciones]

| Credencial | Descripción |
| --- | --- |
| `credentials` | Credencial necesaria para autenticar [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |
| `topicName` | El nombre del recurso que representa una fuente de mensajes. Debe especificar un nombre de tema si desea proporcionar acceso a un flujo de datos específico en su origen [!DNL PubSub]. El formato del nombre del tema es: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Nombre de su suscripción a [!DNL PubSub]. En [!DNL PubSub], las suscripciones le permiten recibir mensajes, mediante suscripción al tema en el que se han publicado los mensajes. **Nota**: una sola suscripción de [!DNL PubSub] solo se puede usar para un flujo de datos. Para poder crear varios flujos de datos, debe tener varias suscripciones. El formato del nombre de suscripción es: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones de destino base y de origen. El id. de especificación de conexión [!DNL PubSub] es: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Para obtener más información sobre estos valores, lea este documento [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication). Para usar la autenticación basada en cuentas de servicio, lea esta [[!DNL PubSub] guía sobre la creación de cuentas de servicio](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON al copiar y pegar las credenciales.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Google PubSub]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

El primer paso para crear una conexión de origen es autenticar el origen de [!DNL PubSub] y generar un identificador de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL PubSub] como parte de los parámetros de solicitud.

El origen [!DNL PubSub] le permite especificar el tipo de acceso que desea permitir durante la autenticación. Puede configurar su cuenta para que tenga acceso raíz o restringir el acceso a un tema y suscripción de [!DNL PubSub] en particular.

>[!NOTE]
>
>El principal (funciones) asignado a un proyecto [!DNL PubSub] se hereda en todos los temas y suscripciones creados dentro de un proyecto [!DNL PubSub]. Si desea que una entidad de seguridad (función) tenga acceso a un tema específico, dicha entidad de seguridad (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre el control de acceso](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación basada en proyecto]

Para crear una conexión base con la autenticación basada en proyectos, realice una petición POST al extremo `/connections` y proporcione sus `projectId` y `credentials` en el cuerpo de la solicitud.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `auth.params.projectId` | Identificador de proyecto necesario para autenticar [!DNL PubSub]. |
| `auth.params.credentials` | La credencial o clave necesaria para autenticar [!DNL PubSub]. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este identificador de conexión base es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Autenticación basada en temas y suscripciones]

Para crear una conexión base con tema y autenticación basada en suscripción, realice una petición POST al extremo `/connections` y proporcione sus `credentials`, `topicName` y `subscriptionName` en el cuerpo de la solicitud.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | La credencial o clave necesaria para autenticar [!DNL PubSub]. |
| `auth.params.topicName` | El par de id. de proyecto e id. de tema para el origen [!DNL PubSub] al que desea proporcionar acceso. |
| `auth.params.subscriptionName` | El par de id. de proyecto e id. de suscripción para el origen [!DNL PubSub] al que desea proporcionar acceso. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este identificador de conexión base es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Crear una conexión de origen {#source}

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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede proporcionar para incluir más información sobre la conexión de origen. |
| `baseConnectionId` | Identificador de conexión base del origen [!DNL PubSub] que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL PubSub]. Este identificador es: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Formato de los datos de [!DNL PubSub] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `params.topicName` | Nombre de su tema [!DNL PubSub]. En [!DNL PubSub], un tema es un recurso con nombre que representa una fuente de mensajes. |
| `params.subscriptionName` | El nombre de suscripción que corresponde a un tema determinado. En [!DNL PubSub], las suscripciones permiten leer mensajes de un tema. Se pueden asignar una o varias suscripciones a un solo tema. |
| `params.dataType` | Este parámetro define el tipo de datos que se están introduciendo. Los tipos de datos admitidos son: `raw` y `xdm`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de origen [!DNL PubSub] mediante la API [!DNL Flow Service]. Puede usar este identificador de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo usando la [!DNL Flow Service] API](../../collect/streaming.md).
