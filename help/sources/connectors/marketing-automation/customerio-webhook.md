---
title: Información general sobre Customer.io Source
description: Aprenda a conectar Customer.io a Adobe Experience Platform mediante API o la interfaz de usuario de aprovechando los webhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>El origen [!DNL Customer.io] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de flujo continuo. La compatibilidad con los proveedores de streaming incluye [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) es una plataforma de mensajería automatizada para especialistas en marketing que desean tener más control y flexibilidad a la hora de crear y enviar correos electrónicos impulsados por datos, notificaciones push, mensajes en la aplicación y SMS.

La fuente [!DNL Customer.io] le permite introducir esquemas de eventos de ganchos web admitidos y sus datos de evento asociados de [!DNL Customer.io] mediante [[!DNL Customer.io] Webhooks de informes](https://customer.io/docs/api/webhooks/).

Los esquemas de eventos de gancho web admitidos son:

* Eventos de cliente
* Eventos de correo electrónico
* Eventos de SMS
* Eventos de notificaciones push
* Eventos de mensajes en la aplicación
* Eventos de Slack
* Eventos de webhook

Para obtener una lista de los eventos disponibles a través de los enlaces web, consulte la documentación de [[!DNL Customer.io] Informes de eventos de enlaces web](https://customer.io/docs/webhooks/#events).

## Requisitos previos {#prerequisites}

Para poder crear una conexión de origen de [!DNL Customer.io], primero debe asegurarse de que dispone de lo siguiente:

* Una cuenta de [!DNL Customer.io]. Si no tienes una, lee la [[!DNL Customer.io] página de registro](https://fly.customer.io/signup) para registrarte y crear tu cuenta.
* Después de crear su cuenta, también deberá tener su cuenta validada. Siga los pasos documentados en la página [[!DNL Customer.io] Verificación de la cuenta](https://customer.io/docs/account-verification/) para completar el proceso.

### Configurar webhook de [!DNL Customer.io] {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un webhook de creación de informes para informar a Platform sobre [!DNL Customer.io] eventos. Los webhooks pueden notificarle inmediatamente cuando los atributos del cliente cambien o cuando las personas abran sus mensajes y enviarle esta información a su origen de [!DNL Customer.io]. Para obtener más información, lee los tutoriales sobre [cómo obtener la URL del extremo de streaming](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) y [cómo configurar un  [!DNL Customer.io] webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Conectando [!DNL Customer.io] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo crear una conexión de flujo continuo de [!DNL Customer.io] para conectarse con [!DNL Platform] mediante API o la interfaz de usuario:

### Conectar [!DNL Customer.io] a Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen y un flujo de datos para llevar  [!DNL Customer.io] datos a Platform mediante API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Conectar [!DNL Customer.io] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Cree una conexión de origen y un flujo de datos para llevar  [!DNL Customer.io] datos a Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
