---
title: Creación de una conexión de suborigen de PubSub de Google mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a una cuenta PubSub de Google mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---

# Crear un [!DNL Google PubSub] Conexión de origen mediante la API de Flow Service

>[!IMPORTANT]
>
>El [!DNL Google PubSub] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial lo acompañará durante los pasos para conectarse [!DNL Google PubSub] (en lo sucesivo, &quot;[!DNL PubSub]&quot;) al Experience Platform, utilizando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL PubSub] a Platform mediante el [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Debe proporcionar valores para las propiedades de conexión descritas a continuación para conectar su [!DNL PubSub] cuenta a [!DNL Flow Service]. Para obtener más información sobre la autenticación y la configuración de requisitos previos, lea la [[!DNL PubSub source] descripción general](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Autenticación basada en proyectos]

| Credencial | Descripción |
| --- | --- |
| `projectId` | El ID de proyecto necesario para la autenticación [!DNL PubSub]. |
| `credentials` | La credencial necesaria para autenticarse [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones de destino base y de origen. El [!DNL PubSub] ID de especificación de conexión: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Autenticación por tema y por suscripción]

| Credencial | Descripción |
| --- | --- |
| `credentials` | La credencial necesaria para autenticarse [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |
| `topicName` | El nombre del recurso que representa una fuente de mensajes. Debe especificar un nombre de tema si desea proporcionar acceso a un flujo de datos específico en su [!DNL PubSub] origen. El formato del nombre del tema es: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | El nombre de su [!DNL PubSub] suscripción. Entrada [!DNL PubSub], las suscripciones le permiten recibir mensajes, suscribiéndose al tema en el que se han publicado los mensajes. **Nota**: Un solo [!DNL PubSub] la suscripción solo se puede utilizar para un flujo de datos. Para poder crear varios flujos de datos, debe tener varias suscripciones. El formato del nombre de suscripción es: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones de destino base y de origen. El [!DNL PubSub] ID de especificación de conexión: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Para obtener más información sobre estos valores, lea esto [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication) documento. Para utilizar la autenticación basada en cuentas de servicio, lea esto [[!DNL PubSub] guía de creación de cuentas de servicio](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar las credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON al copiar y pegar las credenciales.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!TIP]
>
>Una vez creado, no se puede cambiar el tipo de autenticación de una [!DNL Google PubSub] conexión base. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

El primer paso para crear una conexión de origen es autenticar su [!DNL PubSub] y generar un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL PubSub] credenciales de autenticación como parte de los parámetros de solicitud.

El [!DNL PubSub] fuente permite especificar el tipo de acceso que desea permitir durante la autenticación. Puede configurar su cuenta para que tenga acceso raíz o restringir el acceso a un en particular [!DNL PubSub] tema y suscripción.

>[!NOTE]
>
>Principal (funciones) asignado a [!DNL PubSub] Los proyectos de se heredan en todos los temas y suscripciones creados dentro de un [!DNL PubSub] proyecto. Si desea que una entidad de seguridad (función) tenga acceso a un tema específico, dicha entidad de seguridad (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre el control de acceso](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación basada en proyectos]

Para crear una conexión base con la autenticación basada en proyectos, realice una solicitud de POST al `/connections` y proporcione su `projectId` y `credentials` en el cuerpo de la solicitud.

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
| `auth.params.projectId` | El ID de proyecto necesario para la autenticación [!DNL PubSub]. |
| `auth.params.credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | El [!DNL PubSub] ID de especificación de conexión: `70116022-a743-464a-bbfe-e226a7f8210c`. |

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

>[!TAB Autenticación por tema y por suscripción]

Para crear una conexión base con tema y autenticación basada en suscripción, realice una solicitud de POST al `/connections` y proporcione su `credentials`, `topicName`, y `subscriptionName` en el cuerpo de la solicitud.

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
| `auth.params.credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `auth.params.topicName` | El par de ID de proyecto e ID de tema para [!DNL PubSub] origen al que desea proporcionar acceso. |
| `auth.params.subscriptionName` | El par de ID de proyecto e ID de suscripción para [!DNL PubSub] origen al que desea proporcionar acceso. |
| `connectionSpec.id` | El [!DNL PubSub] ID de especificación de conexión: `70116022-a743-464a-bbfe-e226a7f8210c`. |

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
| `baseConnectionId` | El ID de conexión base de su [!DNL PubSub] origen que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL PubSub]. Este ID es: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | El formato del [!DNL PubSub] datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |
| `params.topicName` | El nombre de su [!DNL PubSub] tema. Entrada [!DNL PubSub], un tema es un recurso con nombre que representa una fuente de mensajes. |
| `params.subscriptionName` | El nombre de suscripción que corresponde a un tema determinado. Entrada [!DNL PubSub], las suscripciones permiten leer mensajes de un tema. Se pueden asignar una o varias suscripciones a un solo tema. |
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

Al seguir este tutorial, ha creado un [!DNL PubSub] conexión de origen mediante [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para lo siguiente [crear un flujo de datos de flujo continuo utilizando [!DNL Flow Service] API](../../collect/streaming.md).
