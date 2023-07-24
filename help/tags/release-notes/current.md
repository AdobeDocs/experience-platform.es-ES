---
title: Notas de la versión para etiquetas y reenvío de eventos
description: Las notas de la versión más recientes para etiquetas y reenvío de eventos de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# Notas de la versión para etiquetas y reenvío de eventos

>[!IMPORTANT]
>
>Al avanzar, las etiquetas y las notas de la versión del reenvío de eventos ya no se proporcionarán en esta página. Consulte la última versión [Notas de la versión de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=en#data-collection) para obtener etiquetas detalladas y actualizaciones del reenvío de eventos.

## 26 de abril de 2023

* **Secreto JWT de OAuth**: La [Secreto JWT de OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) permite a los clientes utilizar tokens de Adobe y servicio de Google para admitir interacciones de servidor a servidor en el reenvío de eventos.

Se ha lanzado la siguiente extensión nueva:

* **[!DNL Pinterest Conversions API]extensión**: La [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) La extensión de reenvío de eventos permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor que utilizan el [!DNL Pinterest Conversions API].

## 29 de marzo de 2023

**Flujos de trabajo de inicio rápido (beta)**

Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. Los siguientes flujos de trabajo ya están disponibles para los clientes como una versión beta pública.
* **[API de metaconversiones](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: los clientes del reenvío de eventos pueden recopilar y reenviar rápidamente datos de eventos del lado del servidor a Meta para las conversiones de anuncios en solo unos pasos sencillos.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: Los clientes pueden implementar rápidamente el SDK móvil y validar eventos móviles básicos en solo unos sencillos pasos.

Se han lanzado nuevas extensiones:

* **[!DNL Braze]extensión de reenvío de eventos**: La [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) La extensión de reenvío de eventos permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor que utilizan el [!DNL Braze] API de seguimiento de usuario.
* **[API de eventos de Epsilon] extensión de reenvío de eventos**: La [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) La extensión de le permite aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a [!DNL Epsilon] uso del [!DNL Epsilon] API de evento.
* **[!DNL Mixpanel]extensión de reenvío de eventos**: La [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) La extensión de le permite aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a [!DNL Mixpanel] uso de la API de seguimiento de eventos.

## 25 de enero de 2023

* **Nueva pantalla de inicio**: La página de inicio de la IU de recopilación de datos se ha actualizado para incluir información útil de incorporación y vínculos para optimizar la productividad. Esto incluye:
   1. Documentación y flujos de trabajo recomendados para empezar
   1. Propiedades, reglas y elementos de datos recientes
   1. Extensiones populares
   1. Nuevas actualizaciones de la extensión con una función de instalación rápida
* **Envío de datos a [!DNL Google Ads] uso del reenvío de eventos**: Ahora puede utilizar la variable [[!DNL Google Ads Enhanced Conversions] Extensión de API](../extensions/server/google-ads-enhanced-conversions/overview.md) para el reenvío de eventos, combinado con [Secretos de Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), para enviar de forma segura datos del lado del servidor a [!DNL Google Ads] en tiempo real.

## 23 de noviembre de 2022

* **[!DNL AWS]extensión para reenvío de eventos**: Ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL AWS] información general sobre extensiones](../../tags/extensions/server/aws/overview.md) para obtener más información.
* **[!DNL Google Ads Enhanced Conversions]extensión para reenvío de eventos**: Ahora puede enviar datos de conversión a [!DNL Google Ads] uso de un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Google Ads Enhanced Conversions] información general sobre extensiones](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más información.
* **[!DNL Microsoft Azure]extensión para reenvío de eventos**: Ahora puede enviar datos a [!DNL Microsoft Azure] uso de un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Microsoft Azure] información general sobre extensiones](../../tags/extensions/server/azure/overview.md) para obtener más información.

## 26 de octubre de 2022

* **Administración de datos confidenciales para flujos de datos**: Las secuencias de datos ahora aprovechan varias tecnologías de Platform para gestionar correctamente los datos confidenciales, tal como se aplica en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../datastreams/overview.md#sensitive) para obtener más información.
* **[!DNL Splunk]extensión para reenvío de eventos**: Ahora puede enviar datos a [!DNL Splunk] uso de un [reenvío de eventos](../ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Splunk] información general sobre extensiones](../extensions/server/splunk/overview.md) para obtener más información.
* **[!DNL Zendesk]extensión para reenvío de eventos**: Ahora puede enviar datos a [!DNL Zendesk] uso de un [reenvío de eventos](../ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Zendesk] información general sobre extensiones](../extensions/server/zendesk/overview.md) para obtener más información.

## 28 de septiembre de 2022

* **Integración de navegación izquierda de Adobe Experience Platform**: todas las funcionalidades que anteriormente eran exclusivas de la IU de recopilación de datos (incluidas las etiquetas y el reenvío de eventos) ahora también están disponibles a través de la navegación izquierda en la IU del Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre interfaces al trabajar con las capacidades de recopilación de datos en Platform.
* **Atribución de usuario en etiquetas y reenvío de eventos**: Al enumerar las propiedades disponibles en las etiquetas y el reenvío de eventos, cada propiedad de la lista ahora muestra cuándo se actualizó por última vez y quién lo hizo.
* **[[!DNL Snap Conversions API] extensión](https://exchange.adobe.com/apps/ec/108550) para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Snapchat Conversions API] uso de un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Para obtener más información sobre cómo autenticar y utilizar la API, consulte la [[!DNL Snapchat Marketing API] documentación](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julio de 2022

* El acceso a las funciones de etiquetas y reenvío de eventos ahora se administra mediante Adobe Admin Console en la tarjeta para la recopilación de datos de Adobe Experience Platform. Consulte la guía de [permisos de recopilación de datos](../../collection/permissions.md) para obtener más información.
* La compatibilidad con Internet Explorer 10 y 11 se ha [obsoleto](../ie-deprecation.md).

## 22 de junio de 2022

Se han lanzado nuevas extensiones:

* [Extensión de etiqueta de capa de datos Google](../extensions/client/google-data-layer/overview.md): Permite utilizar una capa de datos de Google en la implementación de etiquetas.
* [Extensión de reenvío de eventos de conversiones mejoradas de Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Permite mejorar las conversiones de Google Ads en tiempo real.
* [Extensión de reenvío de eventos de Mailchimp](../extensions/server/mailchimp/overview.md): envía eventos a la API de marketing de Mailchimp, que puede almacenar en déclencheur correos electrónicos para campañas de marketing, recorridos o transacciones de Mailchimp.