---
title: Notas de la versión para etiquetas y reenvío de eventos
description: Las notas de la versión más recientes para etiquetas y reenvío de eventos de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2b11fb87523c777d5c2d855e97a4af78a8483abe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# Notas de la versión para etiquetas y reenvío de eventos

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

* **Administración de datos confidenciales para flujos de datos**: Las secuencias de datos ahora aprovechan varias tecnologías de Platform para gestionar correctamente los datos confidenciales, tal como se aplica en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../edge/datastreams/overview.md#sensitive) para obtener más información.
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