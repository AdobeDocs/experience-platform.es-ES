---
title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
seo-title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
description: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
seo-description: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Requisitos previos para utilizar el SDK web de Adobe Experience Platform

Para utilizar este SDK, primero debe:

- Aprovisionar su organización para esta función. (Si desea entrar en la lista de espera, póngase en contacto con el administrador de éxito del cliente (CSM)).
- Habilite un dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, debe utilizarlo. La prueba en desarrollo funciona sin un CNAME, pero se necesita uno antes de ir a producción.

>[!IMPORTANT]
>
>**Tenga en cuenta que a partir del 10/11/20, las implementaciones de CNAME de origen caducan durante 7 días en todos los exploradores Safari y dispositivos iOS móviles.**

- Tener derecho a Adobe Experience Platform. Si no ha adquirido Adobe Experience Platform, Adobe le proporcionará Experience Platform Data Services Foundation para que lo utilice de forma limitada con el SDK sin cargo adicional.
- Si su sitio Web ya está utilizando el [servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) en su sitio Web, ya sea a través de la API de Visitante o la extensión del servicio de ID de Experience Cloud dentro de Adobe Experience Platform Launch, y le gustaría seguir usándolo al migrar al SDK Web de Adobe Experience Platform, debe utilizar la versión más reciente de la API de Visitante o la extensión del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obtener más información.
