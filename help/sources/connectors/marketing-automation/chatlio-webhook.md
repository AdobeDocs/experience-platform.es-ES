---
title: Resumen de origen de Chatlio
description: Aprenda a conectar Chatlio a Adobe Experience Platform mediante API o la interfaz de usuario de aprovechando los webhooks
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>El [!DNL Chatlio] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de streaming. Los proveedores de streaming admiten [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) es una aplicación de chat en vivo totalmente integrada con [!DNL Slack] y facilita que varios agentes de soporte ayuden simultáneamente a un visitante individual del sitio. [!DNL Chatlio] utiliza el [!DNL Chatio Zapier App] para conectar [!DNL Chatlio] con más de 2000 aplicaciones y servicios diferentes.

El [!DNL Chatlio] La fuente de permite introducir esquemas de eventos de webhook admitidos y sus datos de evento asociados de [!DNL Chatlio.com] uso del [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Los webhooks admitidos son:

* Exportación de transcripciones de chat
* Exportación de mensajes sin conexión
* Ha comenzado una nueva conversación
* El visitante no obtuvo una respuesta a tiempo
* El visitante ha dejado comentarios tras un chat

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Chatlio] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL Chatlio] cuenta. Si todavía no dispone de una, visite la [[!DNL Chatlio] página de suscripción](https://chatlio.com/app/#/signup) para registrarse y crear su cuenta.
* Después de registrar correctamente una cuenta de, siga el [[!DNL Chatlio] documentación de configuración](https://chatlio.com/docs/setup/) para completar la configuración de su cuenta.

### Configurar [!DNL Chatlio] webhook {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un webhook para informar a Platform sobre [!DNL Chatlio] eventos. Los webhooks pueden notificarle inmediatamente cuando cambian los atributos del cliente o cuando las personas abren sus mensajes y envían esta información a su [!DNL Chatlio] origen.

Para obtener más información, lea los tutoriales sobre [obteniendo la URL de extremo de flujo continuo](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) y [configuración de un [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo crear un [!DNL Chatlio] conector de flujo continuo con el que conectarse [!DNL Platform] mediante las API de o la interfaz de usuario de:

### Connect [!DNL Chatlio] a Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen para traer [!DNL Chatlio] datos a Platform mediante API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] a Platform mediante la IU {#connect-to-platform-using-ui}

* [Cree una conexión de origen para traer [!DNL Chatlio] datos a Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
