---
keywords: control de datos rtcdp;control de datos rtcdp;control de datos del perfil de datos del cliente en tiempo real;privacidad rtcdp;privacidad rtcdp
title: Privacidad en Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform le permite agilizar el proceso de cumplimiento de las normas de privacidad en sus operaciones de datos.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Privacidad en Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) ayuda a los especialistas en marketing a reunir datos de varios sistemas empresariales, lo que les permite identificar, comprender y captar mejor a sus clientes. Adobe considera la privacidad de los datos del consumidor como un principio de diseño fundamental y proporciona varios controles para ayudar a los especialistas en marketing a administrar la privacidad de datos de sus clientes.

La mayoría de las [!DNL Real-Time CDP] funcionalidades están impulsadas por Adobe Experience Platform. Este documento proporciona información sobre las distintas tecnologías de mejora de la privacidad admitidas por [!DNL Real-Time CDP], con vínculos a la documentación de [!DNL Experience Platform] para obtener más información.

## Respeto de las solicitudes de acceso y eliminación de clientes

Las regulaciones legales de privacidad, como el [!DNL General Data Protection Regulation] (RGPD) y el [!DNL California Consumer Privacy Act] (CCPA), otorgan a los clientes el derecho de solicitar acceso a los datos personales que recopile de ellos o de eliminarlos. Dado que [!DNL Real-Time CDP] aprovecha las capacidades de [!DNL Experience Platform] para la recopilación y el almacenamiento de datos, las solicitudes de los clientes para acceder y eliminar sus datos personales deben administrarse en [!DNL Platform]. Consulte la descripción general de [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) para obtener más información.

>[!IMPORTANT]
>
> Las solicitudes de privacidad enviadas a través de Adobe Experience Platform Privacy Service para Adobe Marketo Engage se aplican solo a los clientes B2B de Real-Time CDP.

## Funciones de exclusión

[!DNL Real-Time CDP] permite que los clientes se excluyan de la inclusión de sus datos personales en los casos de uso de segmentación. [!DNL Real-Time Customer Profile] captura y almacena las preferencias de exclusión de los clientes, y estas preferencias se pueden aplicar excluyendo a los usuarios que se han excluido de una audiencia mediante la lógica booleana (&quot;Y NO&quot;) en el predicado de segmento.

Consulte el documento [Respeto de las solicitudes de exclusión](../../segmentation/consents.md) en la documentación del servicio de segmentación de Adobe Experience Platform para obtener más información.

## Compatibilidad con IAB TCF 2.0

[!DNL Real-Time CDP] se ha creado en Adobe Experience Platform, que forma parte de la [lista de proveedores](https://iabeurope.eu/vendor-list-tcf/) registrados para [!DNL Transparency & Consent Framework (TCF)], como se describe en [!DNL Interactive Advertising Bureau (IAB)]. En cumplimiento con los requisitos de TCF 2.0, Platform le permite recopilar datos detallados del consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta en si ciertos perfiles se incluyen en las audiencias exportadas, según su caso de uso.

Consulte la descripción general de la compatibilidad con [IAB TCF 2.0 en Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información.

## Pasos siguientes

Este documento proporciona una breve introducción a las capacidades de privacidad de [!DNL Real-Time CDP]. Consulte la documentación vinculada a través de esta guía para obtener más información sobre cada función.
