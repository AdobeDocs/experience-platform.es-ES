---
title: Esquemas en la plataforma de datos del cliente en tiempo real B2B Edition
description: Una descripción general de la función de los esquemas del Modelo de datos de Experience (XDM) en la Plataforma de datos del cliente en tiempo real B2B Edition.
source-git-commit: a8c322cfe02c7a005275ec33e5dac92d2f76667a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Esquemas en la plataforma de datos del cliente en tiempo real B2B Edition

La plataforma de datos del cliente en tiempo real B2B Edition proporciona varias [clases estándar del Modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md#class) que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas y mucho más. Además, CDP B2B Edition en tiempo real le permite definir relaciones &quot;varios a uno&quot; entre estos esquemas para que puedan participar en casos de uso de segmentación avanzada.

En CDP B2B Edition en tiempo real se proporcionan las siguientes clases estándar:

* [Cuenta comercial XDM](../../xdm/classes/b2b/business-account.md)
* [Relación de persona de cuenta comercial XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campaña empresarial XDM](../../xdm/classes/b2b/business-campaign.md)
* [Miembros de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidad comercial XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relación de persona de oportunidad comercial XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing empresarial XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Miembros de la lista de marketing empresarial XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para ver los pasos sobre cómo crear una relación &quot;varios a uno&quot; entre dos esquemas, consulte el tutorial sobre la [definición de relaciones de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Si utiliza una conexión de origen B2B, puede utilizar una herramienta para generar automáticamente los esquemas necesarios y las relaciones entre ellos. Consulte la guía sobre [B2B namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) en la documentación de fuentes para obtener más información.
