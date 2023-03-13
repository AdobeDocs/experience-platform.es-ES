---
title: Requisitos previos para utilizar el SDK web de Adobe Experience Platform
description: Obtenga información acerca de los requisitos previos para utilizar el SDK web de Adobe Experience Platform.
keywords: dominio de origen;CNAME;esquema;crear esquema;launch;extensión de sdk web de aep;extensión;id de configuración;herramienta de configuración;elemento de datos;crear elemento de datos;objeto XDM;sendEvent;enviar evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Requisitos previos para utilizar el SDK web de Adobe Experience Platform

Para utilizar el SDK web de Adobe Experience Platform, primero debe:

- Tener los permisos adecuados configurados para los usuarios de su organización. Todos los clientes de Experience Cloud tienen acceso a las herramientas de recopilación de datos. Cada usuario de su organización solo necesitará permisos para Esquemas, Identidades y Flujos de datos. Para obtener más información sobre cómo configurar estos permisos, consulte nuestra documentación sobre [administración de permisos de recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- Se recomienda tener habilitado el dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, debe utilizarlo. Las pruebas en desarrollo funcionan sin un CNAME, pero Adobe recomienda tenerlas antes de ir a producción. Aunque la implementación de CNAME no proporciona ningún beneficio en cuanto a la duración de las cookies, puede evitar que ciertos bloqueadores de anuncios y exploradores menos comunes bloqueen las solicitudes del SDK. En estos casos, el uso de un CNAME puede impedir que la recopilación de datos se interrumpa para los usuarios que utilizan estas herramientas.

>[!IMPORTANT]
>
>**Tenga en cuenta que, a partir del 10/11/20, las implementaciones de CNAME de origen tienen una caducidad de 7 días en todos los exploradores Safari y dispositivos móviles iOS.**

- Si su sitio web ya está utilizando [Servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) en el sitio web, ya sea a través de la API de visitante o de la extensión del servicio de ID de Experience Cloud en Adobe Experience Platform Launch, y si desea seguir utilizándolo durante la migración al SDK web de Adobe Experience Platform, debe utilizar la versión más reciente de la API de visitante o la extensión del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obtener más información.
