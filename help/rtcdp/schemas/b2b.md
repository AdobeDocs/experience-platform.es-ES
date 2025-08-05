---
title: Esquemas en Real-Time Customer Data Platform B2B edition
description: Una visión general de la función de los esquemas XDM (Experience Data Model) en Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 09f671af0d04251ab7b0a71528cb4b9745594b1c
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 12%

---

# Esquemas en Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition proporciona varias [clases de modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md#class) estándar que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas y más. Además, Real-Time CDP B2B edition le permite definir relaciones varios a uno entre estos esquemas para que puedan participar en casos de uso de segmentación avanzada.

>[!IMPORTANT]
>
>Los esquemas B2B están disponibles para su uso en aplicaciones de Experience Platform (por ejemplo, en [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>Sin embargo, debe tener acceso a Real-Time CDP B2B edition para que (los perfiles de) los esquemas B2B participen en [Perfil del cliente en tiempo real](../../profile/home.md).

En Real-Time CDP B2B edition se proporcionan las siguientes clases estándar:

* [Cuenta empresarial de XDM](../../xdm/classes/b2b/business-account.md)
* [Relación de persona de la cuenta de negocio de XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign.md)
* [Miembros de la campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relación de persona de la oportunidad de negocio de XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Miembros de la lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para comprender cómo se ajustan los esquemas al flujo de trabajo B2B, consulte el [tutorial completo](../b2b-tutorial.md).

Para ver los pasos sobre cómo crear una relación varios a uno entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Si utiliza una conexión de origen B2B, puede utilizar una herramienta para generar automáticamente los esquemas necesarios y las relaciones entre ellos. Consulte la guía sobre [Áreas de nombres B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) en la documentación de orígenes para obtener más información.
