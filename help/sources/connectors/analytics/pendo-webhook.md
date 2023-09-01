---
title: Resumen de origen de Pendo
description: Aprenda a conectar Pendo a Adobe Experience Platform mediante API o la interfaz de usuario aprovechando los webhooks
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>El [!DNL Pendo] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde aplicaciones de análisis de terceros. La compatibilidad con proveedores de análisis incluye [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) es una aplicación de análisis de productos diseñada para ayudar a las empresas de software a desarrollar productos que interesen a los clientes. La aplicación permite a los creadores de software integrar sus productos con una amplia gama de herramientas que pueden conducir tanto a una mejor experiencia del producto para los usuarios como a nuevas perspectivas para el equipo de productos.

El [!DNL Pendo] La fuente de permite introducir esquemas de eventos de webhook admitidos y sus datos de evento asociados de [!DNL Pendo.io] uso del [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). El [!DNL Pendo] La fuente funciona con [!DNL Pendo] Webhooks de URL.

Los webhooks admitidos son:

* [Guía](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Mostrado
* [Encuesta](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Mostrado/Enviado
* [Puntuación de Net Promoter](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Mostrado/Enviado

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Pendo] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

A [!DNL Pendo] cuenta. Si todavía no dispone de uno, consulte la [[!DNL Pendo] registrar](https://app.pendo.io/register) página para registrarse y crear su cuenta.

### Configuración de [!DNL Pendo] Webhook {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un webhook para informar a Platform sobre [!DNL Pendo] eventos. [!DNL Pendo] Los webhooks pueden enviar notificaciones en tiempo real a otros servicios cuando ocurren ciertos eventos y enviar esta información a su [!DNL Pendo] origen. Para obtener más información, lea los tutoriales sobre [obteniendo la URL de extremo de flujo continuo](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) y [configuración de un [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conectando [!DNL Pendo] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo crear un [!DNL Pendo] conector de flujo continuo con el que conectarse [!DNL Platform] mediante las API de o la interfaz de usuario de:

### Connect [!DNL Pendo] a Platform mediante API {#connect-to-platform-using-api}

* [Cree una conexión de origen para traer [!DNL Pendo] datos a Platform mediante API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connect [!DNL Pendo] a Platform mediante la IU {#connect-to-platform-using-ui}

* [Cree una conexión de origen para traer [!DNL Pendo] datos a Platform mediante la interfaz de usuario de](../../tutorials/ui/create/analytics/pendo-webhook.md)
