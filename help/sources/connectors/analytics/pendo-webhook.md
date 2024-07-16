---
title: Información general sobre Pendo Source
description: Aprenda a conectar Pendo a Adobe Experience Platform mediante API o la interfaz de usuario aprovechando los webhooks
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>El origen [!DNL Pendo] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde aplicaciones de análisis de terceros. Los proveedores de análisis admiten [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) es una aplicación de análisis de productos creada para ayudar a las compañías de software a desarrollar productos que interesen a los clientes. La aplicación permite a los creadores de software integrar sus productos con una amplia gama de herramientas que pueden conducir tanto a una mejor experiencia del producto para los usuarios como a nuevas perspectivas para el equipo de productos.

El origen [!DNL Pendo] le permite introducir esquemas de eventos de gancho web admitidos y sus datos de evento asociados de [!DNL Pendo.io] mediante [[!DNL Pendo] los ganchos web](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). El origen [!DNL Pendo] funciona con los webhooks de URL [!DNL Pendo].

Los webhooks admitidos son:

* Se Muestra [Guía](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide)
* [Encuesta](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Mostrada/Enviada
* [Puntuación de Net Promoter](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Mostrada/Enviada

## Requisitos previos {#prerequisites}

Para poder crear una conexión de origen de [!DNL Pendo], primero debe asegurarse de que dispone de lo siguiente:

Una cuenta de [!DNL Pendo]. Si todavía no tiene una, vea la página [[!DNL Pendo] register](https://app.pendo.io/register) para registrarse y crear su cuenta.

### Configurar webhook de [!DNL Pendo] {#set-up-webhook}

Una vez que haya creado correctamente su flujo de datos, debe configurar un webhook para informar a Platform sobre [!DNL Pendo] eventos. Los webhooks de [!DNL Pendo] pueden enviar notificaciones en tiempo real a otros servicios cuando ocurren ciertos eventos y enviar esta información a tu origen de [!DNL Pendo]. Para obtener más información, lee los tutoriales sobre [cómo obtener la URL del extremo de streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) y [cómo configurar un  [!DNL Pendo] webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conectando [!DNL Pendo] a Platform {#connect-to-platform}

La documentación siguiente proporciona información sobre cómo crear un conector de flujo continuo [!DNL Pendo] para conectarse con [!DNL Platform] mediante API o la interfaz de usuario:

### Conectar [!DNL Pendo] a Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen para llevar  [!DNL Pendo] datos a Platform mediante API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Conectar [!DNL Pendo] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen para llevar  [!DNL Pendo] datos a Platform mediante la interfaz de usuario](../../tutorials/ui/create/analytics/pendo-webhook.md)
