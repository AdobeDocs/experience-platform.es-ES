---
title: Información general sobre fuentes Chatlio
description: Aprenda a conectar Chatlio a Adobe Experience Platform mediante API o la interfaz de usuario aprovechando los enlaces web
badge: "Beta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>La variable [!DNL Chatlio] el origen está en versión beta. Lea el [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde aplicaciones de transmisión. La compatibilidad con los proveedores de flujo continuo incluye [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) es una aplicación de chat en directo totalmente integrada con [!DNL Slack] y facilita múltiples agentes de soporte para ayudar simultáneamente a un visitante individual del sitio. [!DNL Chatlio] utiliza la variable [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] con más de 2000 aplicaciones y servicios diferentes.

La variable [!DNL Chatlio] source le permite ingerir esquemas de eventos de enlace web admitidos y sus datos de evento asociados desde [!DNL Chatlio.com] usando la variable [[!DNL Chatlio] Enlaces web](https://chatlio.com/docs/webhooks/).

Los vínculos web admitidos son:

* Exportación de transcripciones de chat
* Exportación de mensajes sin conexión
* Se ha iniciado una nueva conversación
* El visitante no obtuvo una respuesta a tiempo
* El visitante dejó comentarios después de una conversación

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Chatlio] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL Chatlio] cuenta. Si todavía no tiene una, visite [[!DNL Chatlio] página de suscripción](https://chatlio.com/app/#/signup) para registrar y crear su cuenta.
* Una vez que haya registrado correctamente una cuenta, siga la [[!DNL Chatlio] documentación de configuración](https://chatlio.com/docs/setup/) para completar la configuración de la cuenta.

### Configuración [!DNL Chatlio] weblock {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un enlace web para informar a Platform sobre [!DNL Chatlio] eventos. Los Webhooks pueden notificarle inmediatamente cuando cambian los atributos del cliente o cuando las personas abren los mensajes y envían esta información a su [!DNL Chatlio] fuente.

Para obtener más información, consulte los tutoriales sobre [obtener la URL del extremo de flujo continuo](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) y [configuración de [!DNL Chatlio] Weblock](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] a Platform {#connect-to-platform}

La documentación siguiente proporciona información sobre cómo crear una [!DNL Chatlio] conector de flujo continuo con el que conectarse [!DNL Platform] mediante API o la interfaz de usuario:

### Connect [!DNL Chatlio] a Platform mediante API {#connect-to-platform-using-api}

* [Crear una conexión de origen para traer [!DNL Chatlio] datos a Platform mediante API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen para traer [!DNL Chatlio] datos a Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

