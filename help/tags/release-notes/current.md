---
title: Notas de la versión para etiquetas y reenvío de eventos
description: Las notas de la versión más recientes para etiquetas y reenvío de eventos de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# Notas de la versión para etiquetas y reenvío de eventos

>[!IMPORTANT]
>
>Al avanzar, las etiquetas y las notas de la versión del reenvío de eventos ya no se proporcionarán en esta página. Consulte las [notas de la versión de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) más recientes para obtener información detallada sobre las etiquetas y las actualizaciones del reenvío de eventos.

## 26 de abril de 2023

* **Secreto JWT de OAuth**: El [Secreto JWT de OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) permite que los clientes usen tokens de Adobe y del servicio Google para admitir interacciones de servidor a servidor en el reenvío de eventos.

Se ha lanzado la siguiente extensión nueva:

* Extensión **[!DNL Pinterest Conversions API]**: La extensión de reenvío de eventos [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=es) permite aprovechar los datos capturados en el Edge Network de Adobe Experience Platform y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor mediante [!DNL Pinterest Conversions API].

## 29 de marzo de 2023

**Flujos de trabajo de inicio rápido (Beta)**

Acceda a los nuevos flujos de trabajo de inicio rápido en “Introducción” desde la pantalla de inicio de la recopilación de datos. Los siguientes flujos de trabajo ya están disponibles para los clientes como Beta público.
* **[API de conversiones de metadatos](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: los clientes del reenvío de eventos pueden recopilar y reenviar rápidamente datos de eventos del lado del servidor a Meta para las conversiones de anuncios en solo unos sencillos pasos.
* **[SDK móvil](https://developer.adobe.com/client-sdks/documentation/)**: Los clientes pueden implementar rápidamente el SDK móvil y validar eventos móviles básicos en tan solo unos sencillos pasos.

Se han lanzado nuevas extensiones:

* **[!DNL Braze]extensión de reenvío de eventos**: La extensión de reenvío de eventos [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar los datos capturados en el Edge Network de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor mediante las API de seguimiento de usuarios de [!DNL Braze].
* Extensión de reenvío de eventos **[Epsilon Events API]**: La extensión [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar el reenvío de eventos para capturar información de eventos en el Edge Network de Adobe Experience Platform y enviarla a [!DNL Epsilon] mediante la API de eventos [!DNL Epsilon].
* **[!DNL Mixpanel]extensión de reenvío de eventos**: La extensión [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar el reenvío de eventos para capturar información de eventos en el Edge Network de Adobe Experience Platform y enviarla a [!DNL Mixpanel] mediante la API de seguimiento de eventos.

## 25 de enero de 2023

* **Nueva pantalla de inicio**: La página de inicio de la IU de recopilación de datos se ha actualizado para incluir información útil sobre la incorporación y vínculos para optimizar la productividad. Esto incluye lo siguiente:
   1. Documentación y flujos de trabajo recomendados para empezar
   1. Propiedades, reglas y elementos de datos recientes
   1. Extensiones populares
   1. Nuevas actualizaciones de la extensión con una función de instalación rápida
* **Enviar datos a [!DNL Google Ads] mediante el reenvío de eventos**: Ahora puede usar la [[!DNL Google Ads Enhanced Conversions] extensión de la API](../extensions/server/google-ads-enhanced-conversions/overview.md) para reenvío de eventos, combinada con los secretos de [Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar datos de forma segura del lado del servidor a [!DNL Google Ads] en tiempo real.

## jueves, 23 de noviembre de 2022

* Extensión **[!DNL AWS]para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL AWS] descripción general de la extensión](../../tags/extensions/server/aws/overview.md) para obtener más información.
* Extensión **[!DNL Google Ads Enhanced Conversions]para el reenvío de eventos**: Ahora puede enviar datos de conversión a [!DNL Google Ads] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Google Ads Enhanced Conversions] descripción general de la extensión](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más información.
* Extensión **[!DNL Microsoft Azure]para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Microsoft Azure] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Microsoft Azure] descripción general de la extensión](../../tags/extensions/server/azure/overview.md) para obtener más información.

## 26 de octubre de 2022

* **Administración de datos confidenciales para flujos de datos**: Los flujos de datos ahora aprovechan varias tecnologías de Platform para administrar correctamente los datos confidenciales, tal como se exige en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [administración de datos confidenciales en flujos de datos](../../datastreams/overview.md#sensitive) para obtener más información.
* Extensión **[!DNL Splunk]para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Splunk] mediante una extensión de [reenvío de eventos](../ui/event-forwarding/overview.md). Consulte la [[!DNL Splunk] descripción general de la extensión](../extensions/server/splunk/overview.md) para obtener más información.
* Extensión **[!DNL Zendesk]para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Zendesk] mediante una extensión de [reenvío de eventos](../ui/event-forwarding/overview.md). Consulte la [[!DNL Zendesk] descripción general de la extensión](../extensions/server/zendesk/overview.md) para obtener más información.

## 28 de septiembre de 2022

* **Integración de navegación izquierda de Adobe Experience Platform**: todas las funcionalidades que anteriormente eran exclusivas de la IU de recopilación de datos (incluidas las etiquetas y el reenvío de eventos) ahora también están disponibles a través de la navegación izquierda en la IU del Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre interfaces al trabajar con las capacidades de recopilación de datos en Platform.
* **Atribución de usuario en etiquetas y reenvío de eventos**: al enumerar propiedades disponibles en etiquetas y reenvío de eventos, cada propiedad enumerada ahora muestra cuándo se actualizó por última vez y quién lo hizo.
* **[[!DNL Snap Conversions API] extensión](https://exchange.adobe.com/apps/ec/108550) para el reenvío de eventos**: ahora puede enviar datos a [!DNL Snapchat Conversions API] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Para obtener más información sobre cómo autenticar y usar la API, consulte la [[!DNL Snapchat Marketing API] documentación](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julio de 2022

* El acceso a las funciones de etiquetas y reenvío de eventos ahora se administra mediante Adobe Admin Console en la tarjeta para la recopilación de datos de Adobe Experience Platform. Consulte la guía de [permisos de recopilación de datos](../../collection/permissions.md) para obtener más información.
* La compatibilidad con Internet Explorer 10 y 11 ha quedado [obsoleta](../ie-deprecation.md).

## 22 de junio de 2022

Se han lanzado nuevas extensiones:

* [Extensión de la capa de datos de Google](../extensions/client/google-data-layer/overview.md): permite usar una capa de datos de Google en la implementación de etiquetas.
* [Extensión de reenvío de eventos de conversiones mejoradas de Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Permite mejorar las conversiones de Google Ads en tiempo real.
* [Extensión de reenvío de eventos de Mailchimp](../extensions/server/mailchimp/overview.md): envía eventos a la API de marketing de Mailchimp, que puede almacenar en déclencheur correos electrónicos para campañas, recorridos o transacciones de marketing de Mailchimp.