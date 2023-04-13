---
title: Información general de fuentes Pendo
description: Aprenda a conectar Pendo a Adobe Experience Platform mediante API o la interfaz de usuario aprovechando los enlaces web
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>La variable [!DNL Pendo] el origen está en versión beta. Lea el [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform permite la ingesta de datos desde aplicaciones de análisis de terceros. La compatibilidad con los proveedores de análisis incluye [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) es una aplicación de análisis de productos creada para ayudar a las empresas de software a desarrollar productos que resonen con los clientes. La aplicación permite a los fabricantes de software integrar sus productos con una amplia gama de herramientas que pueden ofrecer a los usuarios una mejor experiencia de producto y nuevas perspectivas para el equipo de productos.

La variable [!DNL Pendo] source le permite ingerir esquemas de eventos de enlace web admitidos y sus datos de evento asociados desde [!DNL Pendo.io] usando la variable [[!DNL Pendo] Enlaces web](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). La variable [!DNL Pendo] el origen funciona con [!DNL Pendo] Enlaces web de URL.

Los vínculos web admitidos son:

* [Guía](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Mostrado
* [Encuesta](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Mostrado/Enviado
* [Puntuación del promotor de red](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Mostrado/Enviado

## Requisitos previos {#prerequisites}

Antes de crear un [!DNL Pendo] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

A [!DNL Pendo] cuenta. Si todavía no tiene uno, consulte la [[!DNL Pendo] register](https://app.pendo.io/register) para registrar y crear su cuenta.

### Configuración [!DNL Pendo] Weblock {#set-up-webhook}

Una vez que haya creado correctamente el flujo de datos, debe configurar un enlace web para informar a Platform sobre [!DNL Pendo] eventos. [!DNL Pendo] Los Webhooks pueden enviar notificaciones en tiempo real a otros servicios cuando se producen determinados eventos y enviar esta información a su [!DNL Pendo] fuente. Para obtener más información, consulte los tutoriales sobre [obtener la URL del extremo de flujo continuo](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) y [configuración de [!DNL Pendo] Weblock](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Conexión [!DNL Pendo] a Platform {#connect-to-platform}

La documentación siguiente proporciona información sobre cómo crear una [!DNL Pendo] conector de flujo continuo con el que conectarse [!DNL Platform] mediante API o la interfaz de usuario:

### Connect [!DNL Pendo] a Platform mediante API {#connect-to-platform-using-api}

* [Crear una conexión de origen para traer [!DNL Pendo] datos a Platform mediante API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connect [!DNL Pendo] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen para traer [!DNL Pendo] datos a Platform mediante la interfaz de usuario](../../tutorials/ui/create/analytics/pendo-webhook.md)
