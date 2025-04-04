---
title: Notas de la versión para etiquetas y reenvío de eventos
description: Las notas de la versión más recientes para etiquetas y reenvío de eventos de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 93%

---

# Notas de la versión para etiquetas y reenvío de eventos

>[!IMPORTANT]
>
>En adelante, las notas de la versión para etiquetas y reenvío de eventos ya no se proporcionarán en esta página. Consulte las [notas de la versión de Adobe Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/release-notes/latest#data-collection) más recientes para obtener información detallada sobre las actualizaciones de etiquetas y reenvío de eventos.

## 26 de abril de 2023

* **Secreto JWT de OAuth**: el [Secreto JWT de OAuth](https://experienceleague.adobe.com/es/docs/experience-platform/tags/event-forwarding/secrets) permite a los clientes utilizar tokens de servicio de Adobe y de Google para admitir interacciones de servidor a servidor en el reenvío de eventos.

Se ha publicado la siguiente extensión nueva:

* Extensión **[!DNL Pinterest Conversions API]**: la extensión de reenvío de eventos [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=es) permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor que utilizan [!DNL Pinterest Conversions API].

## 29 de marzo de 2023

**Flujos de trabajo de inicio rápido (Beta)**

Acceda a los nuevos flujos de trabajo de inicio rápido en “Introducción” desde la pantalla de inicio de la recopilación de datos. Los siguientes flujos de trabajo ya están disponibles para los clientes como versión Beta pública.
* **[API de Conversiones de Meta](https://experienceleague.adobe.com/es/docs/experience-platform/tags/extensions/server/meta/overview#quick-start)**: los clientes de envío de eventos pueden recopilar y reenviar rápidamente datos de evento desde el lado del servidor a Meta para las conversiones de anuncios en solo unos sencillos pasos.
* **[SDK móvil](https://developer.adobe.com/client-sdks/documentation/)**: los clientes pueden implementar rápidamente el SDK móvil y validar eventos móviles básicos en solo unos sencillos pasos.

Se han publicado nuevas extensiones:

* Extensión de reenvío de eventos **[!DNL Braze]**: la extensión de reenvío de eventos [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor con las API de seguimiento de usuarios de [!DNL Braze].
* **[Extensión de reenvío de eventos de la API de eventos Epsilon]**: la extensión [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a [!DNL Epsilon] con la API de eventos [!DNL Epsilon].
* Extensión de reenvío de eventos **[!DNL Mixpanel]**: la extensión [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) le permite aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a [!DNL Mixpanel] con la API de eventos de seguimiento.

## 25 de enero de 2023

* **Nueva pantalla de inicio**: la página de inicio de la IU de recopilación de datos se ha actualizado para incluir información útil de incorporación y vínculos para optimizar la productividad. Esto incluye lo siguiente:
   1. Documentación y flujos de trabajo recomendados para empezar
   1. Propiedades, reglas y elementos de datos recientes
   1. Extensiones populares
   1. Nuevas actualizaciones de la extensión con una función de instalación rápida
* **Enviar datos a [!DNL Google Ads] con el reenvío de eventos**: ahora puede utilizar la extensión de la API [[!DNL Google Ads Enhanced Conversions] ](../extensions/server/google-ads-enhanced-conversions/overview.md) para el reenvío de eventos, junto con [Secretos de Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar de forma segura los datos del lado del servidor a [!DNL Google Ads] en tiempo real.

## 23 de noviembre de 2022

* Extensión **[!DNL AWS]para el reenvío de eventos**: ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL AWS] información general sobre las extensiones](../../tags/extensions/server/aws/overview.md) para obtener más detalles.
* Extensión **[!DNL Google Ads Enhanced Conversions]para el reenvío de eventos**: ahora puede enviar datos de conversión a [!DNL Google Ads] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Google Ads Enhanced Conversions] información general sobre las extensiones](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más detalles.
* Extensión **[!DNL Microsoft Azure]para el reenvío de eventos**: ahora puede enviar datos a [!DNL Microsoft Azure] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Microsoft Azure] información general sobre las extensiones](../../tags/extensions/server/azure/overview.md) para obtener más detalles.

## 26 de octubre de 2022

* **Administración de datos confidenciales para flujos de datos**: Los flujos de datos ahora aprovechan varias tecnologías de Experience Platform para administrar correctamente los datos confidenciales, tal como se exige en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [administración de datos confidenciales en las secuencias de datos](../../datastreams/overview.md#sensitive) para obtener más información.
* Extensión **[!DNL Splunk]para el reenvío de eventos**: ahora puede enviar datos a [!DNL Splunk] mediante una extensión de [reenvío de eventos](../ui/event-forwarding/overview.md). Consulte la [[!DNL Splunk] información general sobre las extensiones](../extensions/server/splunk/overview.md) para obtener más detalles.
* Extensión **[!DNL Zendesk]para el reenvío de eventos**: ahora puede enviar datos a [!DNL Zendesk] mediante una extensión de [reenvío de eventos](../ui/event-forwarding/overview.md). Consulte la [[!DNL Zendesk] información general sobre las extensiones](../extensions/server/zendesk/overview.md) para obtener más detalles.

## 28 de septiembre de 2022

* **Integración de navegación izquierda de Adobe Experience Platform**: todas las capacidades que anteriormente eran exclusivas de la IU de recopilación de datos (incluidas las etiquetas y el reenvío de eventos) ahora también están disponibles a través del panel de navegación izquierdo en la IU del Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre IU al trabajar con funciones de recopilación de datos en Experience Platform.
* **Atribución de usuario en etiquetas y reenvío de eventos**: al enumerar propiedades disponibles en las etiquetas y el reenvío de eventos, cada propiedad enumerada ahora muestra cuándo se actualizó por última vez y quién lo hizo.
* Extensión **[[!DNL Snap Conversions API] ](https://exchange.adobe.com/apps/ec/108550) para el reenvío de eventos**: ahora puede enviar datos a [!DNL Snapchat Conversions API] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Para obtener más información sobre cómo autenticar y utilizar la API, consulte la [[!DNL Snapchat Marketing API] documentación](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julio de 2022

* El acceso a las capacidades de etiquetas y reenvío de eventos ahora se administra mediante Adobe Admin Console en la tarjeta para la recopilación de datos de Adobe Experience Platform. Para obtener más información, consulte la guía de [Permisos de recopilación de datps](../../collection/permissions.md).
* La compatibilidad con Internet Explorer 10 y 11 ha quedado [obsoleta](../ie-deprecation.md).

## 22 de junio de 2022

Se han publicado nuevas extensiones:

* [Extensión de etiquetas de la capa de datos de Google](../extensions/client/google-data-layer/overview.md): permite usar una capa de datos de Google en la implementación de etiquetas.
* [Extensión de reenvío de eventos de conversiones mejoradas de Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): permite mejorar las conversiones de Google Ads en tiempo real.
* [Extensión de reenvío de eventos de Mailchimp](../extensions/server/mailchimp/overview.md): envía eventos a la API de marketing de Mailchimp, que puede activar los correos electrónicos para campañas de marketing, recorridos o transacciones de marketing de Mailchimp.