---
keywords: administración de datos rtcdp;administración de datos rtcdp;administración de datos del perfil de datos del cliente en tiempo real;privacidad rtcdp;rtcdp privacidad
title: Privacidad en el Perfil de datos del cliente en tiempo real
seo-title: Privacidad en el Perfil de datos del cliente en tiempo real
description: El Perfil de datos de clientes en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
seo-description: El Perfil de datos de clientes en tiempo real le permite optimizar el proceso para mantener las operaciones de datos conformes con las normativas de privacidad.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Privacidad en [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ayuda a los especialistas en mercadotecnia a reunir los datos de varios sistemas empresariales, permitiéndoles identificar, comprender y captar mejor a sus clientes. Adobe mantiene la privacidad de los datos del consumidor como un principio fundamental de diseño y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de los datos de sus clientes.

La mayoría de las [!DNL Real-time CDP] capacidades son ofrecidas por Adobe Experience Platform. Este documento proporciona información sobre las distintas tecnologías de mejora de la privacidad admitidas por [!DNL Real-time CDP], con vínculos a [!DNL Experience Platform] documentación para obtener más información.

## Cumplimiento de las solicitudes de eliminación y acceso de los clientes

Las regulaciones legales de privacidad como [!DNL General Data Protection Regulation] (GDPR) y [!DNL California Consumer Privacy Act] (CCPA) otorgan a los clientes el derecho de solicitar acceso o la eliminación de los datos personales que recopila de ellos. Debido a que [!DNL Real-time CDP] aprovecha [!DNL Experience Platform] las capacidades de recopilación y almacenamiento de datos, las solicitudes de los clientes para acceder y eliminar sus datos personales deben ser administradas dentro de [!DNL Platform]. Consulte la información general en [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obtener más información.

## Capacidades de exclusión

[!DNL Real-time CDP] permite a los clientes exclusión que sus datos personales se incluyan en casos de uso de segmentación. Las preferencias de exclusión de los clientes son capturadas y almacenadas por [!DNL Real-time Customer Profile] y se pueden aplicar excluyendo a los usuarios que hayan exclusión de un segmento mediante lógica booleana (&quot;Y NO&quot;) en el predicado de segmentos.

Consulte el documento sobre [cumplimiento de las solicitudes de exclusión](../../segmentation/honoring-opt-outs.md) en la documentación del servicio de segmentación de Adobe Experience Platform para obtener más información.

## Compatibilidad con IAB TCF 2.0

[!DNL Real-time CDP] está compilado en Adobe Experience Platform, que forma parte de la lista de  [proveedores registrados ](https://iabeurope.eu/vendor-list-tcf-v2-0/) para la  [!DNL Transparency & Consent Framework (TCF)], tal como lo describe el  [!DNL Interactive Advertising Bureau (IAB)]. De conformidad con los requisitos de TCF 2.0, Platform le permite recopilar datos detallados de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta si determinados perfiles se incluyen en segmentos de audiencia exportados, según el caso de uso.

Consulte la información general sobre la compatibilidad con [IAB TCF 2.0 en Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información.

## Pasos siguientes

Este documento proporcionó una breve introducción a las capacidades de privacidad de [!DNL Real-time CDP]. Consulte la documentación vinculada a esta guía para obtener más información sobre cada función.