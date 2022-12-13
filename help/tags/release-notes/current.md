---
title: Notas de la versión de etiquetas y reenvío de eventos
description: Las notas de la versión más recientes para etiquetas y reenvío de eventos de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 892d22a88546ff270af4f5b253a013015349898b
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 5%

---

# Notas de la versión para etiquetas y reenvío de eventos

## 23 de noviembre de 2022

* **[!DNL AWS]extensión para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL AWS] información general de la extensión](../../tags/extensions/server/aws/overview.md) para obtener más información.
* **[!DNL Google Ads Enhanced Conversions]extensión para el reenvío de eventos**: Ahora puede enviar datos de conversión a [!DNL Google Ads] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Google Ads Enhanced Conversions] información general de la extensión](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más información.
* **[!DNL Microsoft Azure]extensión para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Microsoft Azure] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Microsoft Azure] información general de la extensión](../../tags/extensions/server/azure/overview.md) para obtener más información.

## 26 de octubre de 2022

* **Administración de datos confidenciales para conjuntos de datos**: Los conjuntos de datos ahora aprovechan varias tecnologías de plataforma para manejar adecuadamente los datos confidenciales según se aplican en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Porability and Accounability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../edge/datastreams/overview.md#sensitive) para obtener más información.
* **[!DNL Splunk]extensión para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Splunk] usando un [reenvío de eventos](../ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Splunk] información general de la extensión](../extensions/server/splunk/overview.md) para obtener más información.
* **[!DNL Zendesk]extensión para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Zendesk] usando un [reenvío de eventos](../ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Zendesk] información general de la extensión](../extensions/server/zendesk/overview.md) para obtener más información.

## 28 de septiembre de 2022

* **Integración de la navegación izquierda de Adobe Experience Platform**: Todas las funciones que anteriormente eran exclusivas de la interfaz de usuario de recopilación de datos (incluidas las etiquetas y el reenvío de eventos) ahora están disponibles en la sección de navegación izquierda de la interfaz de usuario del Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre las IU al trabajar con capacidades de recopilación de datos en Platform.
* **Atribución de usuario en etiquetas y reenvío de eventos**: Al enumerar las propiedades disponibles en las etiquetas y el reenvío de eventos, cada propiedad incluida ahora muestra cuándo se actualizó por última vez y quién lo hizo.
* **[[!DNL Snap Conversions API] Extensión](https://exchange.adobe.com/apps/ec/108550) para el reenvío de eventos**: Ahora puede enviar datos a [!DNL Snapchat Conversions API] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Para obtener más información sobre cómo autenticar y utilizar la API, consulte la [[!DNL Snapchat Marketing API] documentación](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 de julio de 2022

* El acceso a las etiquetas y las funciones de reenvío de eventos ahora se administra mediante Adobe Admin Console en la tarjeta de la recopilación de datos de Adobe Experience Platform. Consulte la guía de [permisos de recopilación de datos](../../collection/permissions.md) para obtener más información.
* Se ha admitido Internet Explorer 10 y 11 [obsoleto](../ie-deprecation.md).

## 22 de junio de 2022

Se han lanzado nuevas extensiones:

* [Extensión de etiqueta de la capa de datos de Google](../extensions/client/google-data-layer/overview.md): Permite utilizar una capa de datos de Google en la implementación de etiquetas.
* [Extensión de reenvío de eventos de conversiones mejoradas de Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Permite mejorar las conversiones de Google Ads en tiempo real.
* [Extensión de reenvío de eventos Mailchimp](../extensions/server/mailchimp/overview.md): Envía eventos a la API de marketing de Mailchimp, que puede enviar correos electrónicos de déclencheur para campañas de marketing de Mailchimp, recorridos o transacciones.