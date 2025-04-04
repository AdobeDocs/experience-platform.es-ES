---
title: Información general sobre Chatlio Source
description: Aprenda a conectar Chatlio a Adobe Experience Platform mediante API o la interfaz de usuario de aprovechando los webhooks
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>El origen [!DNL Chatlio] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de streaming. La compatibilidad con los proveedores de streaming incluye [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) es una aplicación de chat en vivo que está totalmente integrada con [!DNL Slack] y que facilita que varios agentes de soporte ayuden simultáneamente a un visitante individual del sitio. [!DNL Chatlio] usa [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] con más de 2000 aplicaciones y servicios diferentes.

El origen [!DNL Chatlio] le permite introducir esquemas de eventos de gancho web admitidos y sus datos de evento asociados de [!DNL Chatlio.com] mediante [[!DNL Chatlio] los ganchos web](https://chatlio.com/docs/webhooks/).

Los webhooks admitidos son:

* Exportación de transcripciones de chat
* Exportación de mensajes sin conexión
* Ha comenzado una nueva conversación
* El visitante no obtuvo una respuesta a tiempo
* El visitante ha dejado comentarios tras un chat

## Requisitos previos {#prerequisites}

Para poder crear una conexión de origen de [!DNL Chatlio], primero debe asegurarse de que dispone de lo siguiente:

* Una cuenta de [!DNL Chatlio]. Si todavía no tiene una, visite la [[!DNL Chatlio] página de suscripción](https://chatlio.com/app/#/signup) para registrarse y crear su cuenta.
* Una vez que haya registrado correctamente una cuenta, siga la [[!DNL Chatlio] documentación de instalación](https://chatlio.com/docs/setup/) para completar la configuración de la cuenta.

### Configurar el webhook [!DNL Chatlio] {#set-up-webhook}

Una vez que haya creado correctamente su flujo de datos, debe configurar un webhook para informar a Experience Platform sobre [!DNL Chatlio] eventos. Los webhooks pueden notificarle inmediatamente cuando cambien los atributos del cliente o cuando las personas abran sus mensajes y envíen esta información a su origen de [!DNL Chatlio].

Para obtener más información, lee los tutoriales sobre [cómo obtener la URL del extremo de streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) y [cómo configurar un  [!DNL Chatlio] webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Conectar [!DNL Chatlio] a Experience Platform {#connect-to-platform}

La documentación siguiente proporciona información sobre cómo crear un conector de flujo continuo [!DNL Chatlio] para conectarse con [!DNL Experience Platform] mediante API o la interfaz de usuario:

### Conectar [!DNL Chatlio] a Experience Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen para llevar  [!DNL Chatlio] datos a Experience Platform mediante API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Conectar [!DNL Chatlio] a Experience Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen para llevar  [!DNL Chatlio] datos a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
