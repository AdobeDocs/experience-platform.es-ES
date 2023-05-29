---
title: Información general de origen de Customer.io
description: Aprenda a conectar Customer.io a Adobe Experience Platform mediante API o la interfaz de usuario de aprovechando los webhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>El [!DNL Customer.io] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de flujo continuo. Los proveedores de streaming admiten [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) es una plataforma de mensajería automatizada para especialistas en marketing que desean obtener más control y flexibilidad para crear y enviar correos electrónicos impulsados por datos, notificaciones push, mensajes en la aplicación y SMS.

El [!DNL Customer.io] La fuente de permite introducir esquemas de eventos de webhook admitidos y sus datos de evento asociados de [!DNL Customer.io] uso del [[!DNL Customer.io] Webhooks de informes](https://customer.io/docs/api/webhooks/).

Los esquemas de eventos de gancho web admitidos son:

* Eventos de cliente
* Eventos de correo electrónico
* Eventos de SMS
* Eventos de notificaciones push
* Eventos de mensajes en la aplicación
* Eventos de Slack
* Eventos de webhook

Para obtener una lista de los eventos disponibles a través de los webhooks, consulte la [[!DNL Customer.io] Informes de eventos de webhook](https://customer.io/docs/webhooks/#events) documentación.

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Customer.io] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL Customer.io] cuenta. Si no tiene uno, lea el [[!DNL Customer.io] página de suscripción](https://fly.customer.io/signup) para registrarse y crear su cuenta.
* Después de crear su cuenta, también deberá tener su cuenta validada. Siga los pasos documentados en la [[!DNL Customer.io] Verificación de cuenta](https://customer.io/docs/account-verification/) para completar el proceso.

### Configuración de [!DNL Customer.io] Webhook {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un webhook de creación de informes para informar a Platform sobre [!DNL Customer.io] eventos. Los webhooks pueden notificarle inmediatamente cuando cambian los atributos del cliente o cuando las personas abren sus mensajes, y enviar esta información a su [!DNL Customer.io] origen. Para obtener más información, lea los tutoriales sobre [obteniendo la URL de extremo de flujo continuo](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) y [configuración de un [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Conectando [!DNL Customer.io] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo crear un [!DNL Customer.io] conexión de flujo continuo para conectarse a [!DNL Platform] mediante las API de o la interfaz de usuario de:

### Connect [!DNL Customer.io] a Platform mediante API {#connect-to-platform-using-api}

* [Crear una conexión de origen y un flujo de datos para traer [!DNL Customer.io] datos a Platform mediante API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] a Platform mediante la IU {#connect-to-platform-using-ui}

* [Crear una conexión de origen y un flujo de datos para traer [!DNL Customer.io] datos a Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
