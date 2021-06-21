---
keywords: control de datos rtcdp;control de datos rtcdp;control de datos del perfil de datos del cliente en tiempo real;privacidad rtcdp;rtcdp privacidad
title: Privacidad en la plataforma de datos del cliente en tiempo real
seo-title: Privacidad en la plataforma de datos del cliente en tiempo real
description: La plataforma de datos del cliente en tiempo real permite optimizar el proceso de cumplimiento de las normas de privacidad de sus operaciones de datos.
seo-description: La plataforma de datos del cliente en tiempo real permite optimizar el proceso de cumplimiento de las normas de privacidad de sus operaciones de datos.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Privacidad en la plataforma de datos del cliente en tiempo real

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) ayuda a los especialistas en marketing a reunir los datos de varios sistemas empresariales, lo que les permite identificar, comprender y captar mejor a sus clientes. Adobe mantiene la privacidad de datos de los consumidores como un principio de diseño fundamental y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de datos de sus clientes.

La mayoría de las [!DNL Real-time CDP] capacidades son ofrecidas por Adobe Experience Platform. Este documento proporciona información sobre las diversas tecnologías de mejora de la privacidad admitidas por [!DNL Real-time CDP], con vínculos a la documentación [!DNL Experience Platform] para obtener más información.

## Respeto de las solicitudes de acceso y eliminación de los clientes

Las regulaciones legales de privacidad como [!DNL General Data Protection Regulation] (RGPD) y [!DNL California Consumer Privacy Act] (CCPA) otorgan a los clientes el derecho de solicitar acceso a los datos personales que recopila de ellos o su eliminación. Dado que [!DNL Real-time CDP] aprovecha las capacidades de [!DNL Experience Platform] para la recopilación y almacenamiento de datos, las solicitudes de los clientes para acceder y eliminar sus datos personales deben administrarse dentro de [!DNL Platform]. Consulte la descripción general de [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obtener más información.

## Funciones de exclusión

[!DNL Real-time CDP] permite a los clientes excluir la inclusión de sus datos personales en los casos de uso de segmentación. Las preferencias de exclusión de los clientes se capturan y almacenan en [!DNL Real-time Customer Profile] y se pueden aplicar excluyendo a los usuarios que han optado por excluirse de un segmento utilizando lógica booleana (&quot;AND NOT&quot;) en el predicado de segmentos.

Para obtener más información, consulte el documento [cumplimiento de las solicitudes de exclusión](../../segmentation/consents.md) en la documentación del servicio de segmentación de Adobe Experience Platform .

## Compatibilidad con IAB TCF 2.0

[!DNL Real-time CDP] se basa en Adobe Experience Platform, que forma parte de la lista de  [proveedores registrados ](https://iabeurope.eu/vendor-list-tcf-v2-0/) para  [!DNL Transparency & Consent Framework (TCF)], tal como lo describe  [!DNL Interactive Advertising Bureau (IAB)]. De conformidad con los requisitos de TCF 2.0, Platform le permite recopilar datos detallados de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta si determinados perfiles se incluyen en segmentos de audiencia exportados, según su caso de uso.

Para obtener más información, consulte la información general sobre la compatibilidad con [IAB TCF 2.0 en Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Pasos siguientes

Este documento proporciona una breve introducción a las capacidades de privacidad de [!DNL Real-time CDP]. Consulte la documentación vinculada a través de esta guía para obtener más información sobre cada función.
