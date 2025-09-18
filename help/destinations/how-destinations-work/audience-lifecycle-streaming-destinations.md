---
title: Ciclo de vida de la audiencia en Experience Platform y destinos de flujo
description: Descubra cómo se reflejan los nombres de audiencia y las asignaciones de Experience Platform en las plataformas de destino de streaming.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# Ciclo de vida de audiencia en destinos de flujo

En esta página se describe cómo se sincronizan las actualizaciones de nombres de audiencia y las asignaciones en Experience Platform con las plataformas de destino de flujo continuo. Al modificar los nombres de las audiencias o eliminar asignaciones de audiencias en Experience Platform, el comportamiento varía según las capacidades de la plataforma de destino.

Comprender estas diferencias es importante para administrar las operaciones del ciclo vital de la audiencia y garantizar que las plataformas de destino reflejen el estado actual de las audiencias en Experience Platform.

## Comportamiento de propagación del nombre de audiencia {#audience-name-propagation}

Cuando activa una audiencia a un destino de flujo continuo, el nombre de la audiencia se envía al destino durante la activación inicial. Sin embargo, el comportamiento de actualización de los nombres de audiencia varía según el destino:

* **[Destinos que admiten actualizaciones de nombres de audiencias](#name-update-supported)**: Si cambia un nombre de audiencia en Experience Platform, el nombre actualizado se propagará automáticamente a estos destinos.
* **[Destinos que no admiten actualizaciones de nombres de audiencias](#name-update-not-supported)**: Si cambia un nombre de audiencia en Experience Platform, el destino seguirá utilizando el nombre original de la activación inicial.

### Destinos que admiten actualizaciones de nombres de audiencia {#name-update-supported}

Los siguientes destinos de flujo continuo admiten actualizaciones automáticas de los nombres de las audiencias al modificar los nombres de las audiencias en Experience Platform:

* [Conexión de Audiencia Acxiom](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase People](../catalog/advertising/demandbase-people.md)
* [Públicos de Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Audiencia personalizada de Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(Compañías) Audiencia coincidente de LinkedIn](../catalog/social/linkedin-b2b.md)
* [Audiencia coincidente de LinkedIn](../catalog/social/linkedin.md)
* [(Heredado) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Audiencias personalizadas de Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinos que no admiten actualizaciones de nombres de audiencia {#name-update-not-supported}

Para los destinos no enumerados anteriormente, los nombres de audiencia permanecen estáticos después de la activación inicial. Si necesita actualizar un nombre de audiencia para estos destinos, debe:

1. Cree una nueva audiencia en Experience Platform con el nombre deseado
2. Activar la nueva audiencia en el destino

>[!TIP]
>
>Para evitar confusiones, utilice nombres de audiencia descriptivos desde la primera activación, especialmente cuando se activa en destinos que no admiten actualizaciones de nombres de audiencia.

## Destinos que admiten la eliminación de audiencias {#support-removal}

Al eliminar (desasignar) una audiencia de un destino de flujo continuo, Experience Platform intenta eliminar la audiencia correspondiente de la plataforma de destino. Sin embargo, no todos los destinos admiten esta funcionalidad.

Los siguientes destinos de flujo continuo admiten la eliminación automática de audiencias cuando se desasigna una audiencia del destino:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Compañías) Audiencia coincidente de LinkedIn](../catalog/social/linkedin-b2b.md)
* [(Heredado) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Audiencias de la cuenta Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Públicos de Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [Audiencias coincidentes de LinkedIn](../catalog/social/linkedin.md)
* [LiveRamp - Distribución](../catalog/advertising/liveramp-distribution.md)
* [Categorías de interés en Mailchimp](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Compromiso de cuenta de Salesforce Marketing Cloud](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Audiencias personalizadas de Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinos que no admiten la eliminación de audiencias

Para destinos no enumerados anteriormente, al desasignar una audiencia del destino, Experience Platform solo elimina la asignación. La audiencia en la plataforma de destino permanece activa hasta que se elimina manualmente en la plataforma de socio.
