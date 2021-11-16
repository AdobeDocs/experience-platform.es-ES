---
title: Esquemas en Real-time Customer Data Platform B2B Edition
description: Una descripción general de la función de los esquemas del Modelo de datos de experiencia (XDM) en Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Esquemas en Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition ofrece varias [Clases del Modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md#class) que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas, etc. Además, CDP B2B Edition en tiempo real le permite definir relaciones &quot;varios a uno&quot; entre estos esquemas para que puedan participar en casos de uso de segmentación avanzada.

>[!IMPORTANT]
>
>Debe tener acceso a CDP B2B Edition en tiempo real para que los esquemas B2B participen en [Perfil del cliente en tiempo real](../../profile/home.md).

En CDP B2B Edition en tiempo real se proporcionan las siguientes clases estándar:

* [Cuenta comercial XDM](../../xdm/classes/b2b/business-account.md)
* [Relación de persona de cuenta comercial XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campaña empresarial XDM](../../xdm/classes/b2b/business-campaign.md)
* [Miembros de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidad comercial XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relación de persona de oportunidad comercial XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing empresarial XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Miembros de la lista de marketing empresarial XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para ver los pasos sobre cómo crear una relación &quot;varios a uno&quot; entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Si utiliza una conexión de origen B2B, puede utilizar una herramienta para generar automáticamente los esquemas necesarios y las relaciones entre ellos. Consulte la guía de [Espacios de nombres B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) en la documentación de fuentes para obtener más información.
