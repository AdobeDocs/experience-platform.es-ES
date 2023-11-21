---
title: Esquemas en Real-time Customer Data Platform B2B Edition
description: Descripción general de la función de los esquemas XDM (Experience Data Model) en Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Esquemas en Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition proporciona varios [Clases del modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md#class) que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas y mucho más. Además, Real-Time CDP B2B Edition permite definir relaciones varios a uno entre estos esquemas para que puedan participar en casos de uso de segmentación avanzada.

>[!IMPORTANT]
>
>Debe tener acceso a Real-Time CDP B2B Edition para que los esquemas B2B puedan participar en [Perfil del cliente en tiempo real](../../profile/home.md).

En Real-Time CDP B2B Edition se proporcionan las siguientes clases estándar:

* [Cuenta empresarial de XDM](../../xdm/classes/b2b/business-account.md)
* [Relación de persona de la cuenta XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign.md)
* [Miembros de campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relación de persona de oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Miembros de lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para comprender cómo encajan los esquemas en el flujo de trabajo B2B, consulte la [tutorial de extremo a extremo](../b2b-tutorial.md).

Para ver los pasos sobre cómo crear una relación varios a uno entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Si utiliza una conexión de origen B2B, puede utilizar una herramienta para generar automáticamente los esquemas necesarios y las relaciones entre ellos. Consulte la guía de [Áreas de nombres B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) en la documentación de orígenes para obtener más información.
