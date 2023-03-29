---
title: Información general sobre Customer.io Source
description: Obtenga información sobre cómo conectar Customer.io a Adobe Experience Platform mediante API o la interfaz de usuario mediante vínculos web.
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>La variable [!DNL Customer.io] el origen está en versión beta. Lea el [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde aplicaciones de flujo continuo. La compatibilidad con los proveedores de flujo continuo incluye [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) es una plataforma de mensajería automatizada para especialistas en marketing que desean tener más control y flexibilidad para crear y enviar correos electrónicos impulsados por datos, notificaciones push, mensajes en la aplicación y SMS.

La variable [!DNL Customer.io] source le permite ingerir esquemas de eventos de enlace web admitidos y sus datos de evento asociados desde [!DNL Customer.io] usando la variable [[!DNL Customer.io] Informes de vínculos web](https://customer.io/docs/api/webhooks/).

Los esquemas de eventos de enlace web admitidos son:

* Eventos del cliente
* Eventos de correo electrónico
* Eventos de SMS
* Eventos de notificaciones push
* Eventos de mensajes en la aplicación
* Eventos de Slack
* Eventos de vínculo web

Para obtener una lista de los eventos disponibles a través de los enlaces web, consulte la [[!DNL Customer.io] Creación de informes de los eventos de vínculo web](https://customer.io/docs/webhooks/#events) documentación.

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Customer.io] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL Customer.io] cuenta. Si no tiene uno, lea la [[!DNL Customer.io] página de suscripción](https://fly.customer.io/signup) para registrar y crear su cuenta.
* Después de crear la cuenta, también deberá validar la cuenta. Siga los pasos documentados en la [[!DNL Customer.io] Verificación de la cuenta](https://customer.io/docs/account-verification/) para completar el proceso.

### Configuración [!DNL Customer.io] Weblock {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un enlace web de informes para informar a Platform sobre [!DNL Customer.io] eventos. Los Webhooks pueden notificarle inmediatamente cuando cambian los atributos del cliente o cuando las personas abren los mensajes, y enviar esta información a su [!DNL Customer.io] fuente. Para obtener más información, consulte los tutoriales sobre [obtener la URL del extremo de flujo continuo](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) y [configuración de [!DNL Customer.io] Weblock](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Conexión [!DNL Customer.io] a Platform {#connect-to-platform}

La documentación siguiente proporciona información sobre cómo crear una [!DNL Customer.io] conexión de flujo continuo para conectarse con [!DNL Platform] mediante API o la interfaz de usuario:

### Connect [!DNL Customer.io] a Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen y un flujo de datos para traer [!DNL Customer.io] datos a Platform mediante API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Cree una conexión de origen y un flujo de datos para traer [!DNL Customer.io] datos a Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

