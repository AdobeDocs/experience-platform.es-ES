---
keywords: control de datos rtcdp;control de datos rtcdp;control de datos del perfil de datos del cliente en tiempo real;privacidad rtcdp;rtcdp privacidad
title: Privacidad en Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform le permite optimizar el proceso de cumplimiento de las normas de privacidad de sus operaciones de datos.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Privacidad en Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) ayuda a los especialistas en marketing a unir los datos de varios sistemas empresariales, lo que les permite identificar, comprender y captar mejor a sus clientes. Adobe mantiene la privacidad de datos de los consumidores como un principio de diseño fundamental y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de datos de sus clientes.

La mayoría de [!DNL Real-Time CDP] son compatibles con Adobe Experience Platform. Este documento proporciona información sobre las diversas tecnologías de mejora de la privacidad compatibles con [!DNL Real-Time CDP], con vínculos a [!DNL Experience Platform] documentación para obtener más información.

## Respeto de las solicitudes de acceso y eliminación de los clientes

Las regulaciones legales de privacidad, como la [!DNL General Data Protection Regulation] (RGPD) y [!DNL California Consumer Privacy Act] (CCPA) otorga a los clientes el derecho de solicitar el acceso a los datos personales que recopile de ellos o su eliminación. Since [!DNL Real-Time CDP] aprovecha [!DNL Experience Platform] funciones para la recopilación y el almacenamiento de datos, las solicitudes de los clientes de acceso y eliminación de sus datos personales deben administrarse en [!DNL Platform]. Consulte la descripción general sobre [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obtener más información.

>[!IMPORTANT]
>
> Las solicitudes de privacidad enviadas a través de Adobe Experience Platform Privacy Service para Adobe Marketo Engage solo se aplican a los clientes de Real-Time CDP B2B.

## Funciones de exclusión

[!DNL Real-Time CDP] permite a los clientes excluir la inclusión de sus datos personales en los casos de uso de segmentación. Las preferencias de exclusión de los clientes las captura y almacena [!DNL Real-Time Customer Profile], y se pueden aplicar excluyendo los usuarios que han optado por no participar en un segmento utilizando lógica booleana (&quot;Y NO&quot;) en el predicado de segmentos.

Consulte el documento en [cumplimiento de las solicitudes de exclusión](../../segmentation/consents.md) en la documentación del servicio de segmentación de Adobe Experience Platform para obtener más información.

## Compatibilidad con IAB TCF 2.0

[!DNL Real-Time CDP] se crea en Adobe Experience Platform, que forma parte del [lista de proveedores](https://iabeurope.eu/vendor-list-tcf-v2-0/) para el [!DNL Transparency & Consent Framework (TCF)], tal y como describe el [!DNL Interactive Advertising Bureau (IAB)]. De conformidad con los requisitos de TCF 2.0, Platform le permite recopilar datos detallados de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta si determinados perfiles se incluyen en segmentos de audiencia exportados, según su caso de uso.

Consulte la descripción general sobre [Compatibilidad con IAB TCF 2.0 en Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información.

## Pasos siguientes

Este documento ofrece una breve introducción a las capacidades de privacidad de [!DNL Real-Time CDP]. Consulte la documentación vinculada a través de esta guía para obtener más información sobre cada función.
