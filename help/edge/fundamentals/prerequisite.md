---
title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
seo-title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
description: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
seo-description: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
keywords: Dominio de origen;CNAME;esquema;crear esquema;inicio;aep web sdk extension;extensión;id de configuración;herramienta de configuración;elemento de datos;crear elemento de datos;objeto XDM;enviar evento;enviar Evento;
translation-type: tm+mt
source-git-commit: a19b4384e2ea64eb9ab5f0f5443fd329ec44a2a0
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Requisitos previos para utilizar el SDK web de Adobe Experience Platform

Para utilizar el SDK web de plataforma, primero debe:

- Pida a su organización que se encargue de esta función. (El acceso al SDK web de plataforma es gratuito; si desea obtener acceso, póngase en contacto con el administrador de éxito del cliente (CSM)).
- Habilite un dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, debe utilizarlo. La prueba en desarrollo funciona sin un CNAME, pero se necesita uno antes de ir a producción.

>[!IMPORTANT]
>
>**Tenga en cuenta que a partir del 10/11/20, las implementaciones de CNAME de origen caducan durante 7 días en todos los exploradores Safari y dispositivos iOS móviles.**

- Tener derecho a Adobe Experience Platform. Si no ha adquirido Adobe Experience Platform, Adobe le proporcionará el acceso necesario para utilizarlo de forma limitada con el SDK sin coste adicional.
- Si su sitio Web ya está utilizando el [servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) en su sitio Web, ya sea a través de la API de Visitante o la extensión del servicio de ID de Experience Cloud dentro de Adobe Experience Platform Launch, y le gustaría seguir usándolo al migrar al SDK Web de Adobe Experience Platform, debe utilizar la versión más reciente de la API de Visitante o la extensión del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obtener más información.
