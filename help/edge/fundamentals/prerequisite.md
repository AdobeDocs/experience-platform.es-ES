---
title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
description: Obtenga información sobre los requisitos previos para utilizar el SDK web de Adobe Experience Platform.
keywords: dominio de origen;CNAME;esquema;crear esquema;launch;extensión de sdk web aep;extensión;id de configuración;herramienta de configuración;elemento de datos;crear elemento de datos;objeto XDM;sendEvent;enviar evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 9d3965be1956de754f0d2a82178bf5dcd871e239
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Requisitos previos para utilizar el SDK web de Adobe Experience Platform

Para utilizar el SDK web de Platform, primero debe:

- Aprovisione a su organización para esta función. (El acceso al SDK web de Platform es gratuito; si desea obtener acceso, póngase en contacto con el administrador de éxito de los clientes (CSM)).
- Se recomienda tener habilitado el dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, debe utilizarlo. Las pruebas en desarrollo funcionan sin un CNAME, pero Adobe recomienda tenerlo antes de ir a producción. Aunque la implementación de CNAME no proporciona ningún beneficio en términos de duración de las cookies, puede evitar que ciertos bloqueadores de anuncios y exploradores menos comunes bloqueen las solicitudes de SDK. En estos casos, el uso de un CNAME puede impedir que la recopilación de datos se interrumpa para los usuarios que utilizan estas herramientas.

>[!IMPORTANT]
>
>**Tenga en cuenta que a partir del 10/11/20, las implementaciones de CNAME de origen tienen una caducidad de 7 días en todos los navegadores Safari y dispositivos iOS móviles.**

- Tener derecho a Adobe Experience Platform. Si no ha comprado Adobe Experience Platform, Adobe le proporcionará el acceso necesario para utilizarlo de forma limitada con el SDK sin coste adicional.
- Si el sitio web ya utiliza el [servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) en el sitio web (a través de la API de visitante o la extensión del servicio de ID de Experience Cloud dentro de Adobe Experience Platform Launch) y desea seguir usándolo al migrar al SDK web de Adobe Experience Platform, debe utilizar la última versión de la API de visitante o la extensión del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obtener más información.

## Administración de permisos para el SDK web de Adobe Experience Platform

El uso de Adobe Experience Platform no requiere ningún permiso especial, pero debe tener los [permisos](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=es) adecuados para crear sus esquemas en Adobe Experience Platform. Los permisos mínimos que necesita alguien se encuentran en la categoría Modelado de datos e identidades .

![](../images/AEP-permission-categories.png)

Dentro de la categoría Modelado de datos , conceda a los usuarios los permisos Administrar esquemas y Ver esquemas .

![](../images/data-modeling-permissions.png)

Dentro de la categoría Identity Management , conceda a los usuarios los permisos Administrar espacios de nombres de identidad y Ver espacios de nombres de identidad .

![](../images/identity-management-permissions.png)
