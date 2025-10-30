---
title: Esquemas en Real-Time Customer Data Platform B2B edition
description: Una visión general de la función de los esquemas XDM (Experience Data Model) en Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 8%

---

# Esquemas en Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition proporciona varias [clases de modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md#class) estándar que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas y más. Además, Real-Time CDP B2B edition le permite definir relaciones varios a uno entre estos esquemas para que puedan participar en casos de uso de segmentación avanzada.

>[!IMPORTANT]
>
>Los esquemas B2B están disponibles para su uso en aplicaciones de Experience Platform (por ejemplo, en [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>Sin embargo, debe tener acceso a Real-Time CDP B2B edition para que (los perfiles de) los esquemas B2B participen en [Perfil del cliente en tiempo real](../../profile/home.md).

En Real-Time CDP B2B edition se proporcionan las siguientes clases estándar:

* [Cuenta empresarial de XDM](../../xdm/classes/b2b/business-account.md)
* [Relación de persona de la cuenta XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign.md)
* [Miembros de campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relación de persona de oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Miembros de lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Para comprender cómo se ajustan los esquemas al flujo de trabajo B2B, consulte el [tutorial completo](../b2b-tutorial.md).

Para ver los pasos sobre cómo crear una relación varios a uno entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../../xdm/tutorials/relationship-b2b.md).

Si utiliza una conexión de origen B2B, puede utilizar una herramienta para generar automáticamente los esquemas necesarios y las relaciones entre ellos. Consulte la guía sobre [Áreas de nombres B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) en la documentación de orígenes para obtener más información.


La siguiente tabla contiene información sobre la configuración subyacente de los esquemas B2B.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre del esquema | Clase base | Grupos de campo | [!DNL Profile] en esquema | Identidad principal | Espacio de nombres de identidad principal | Identidad secundaria | Área de nombres de identidad secundaria | Relación | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cuenta B2B | [Cuenta empresarial de XDM](../../xdm/classes/b2b/business-account.md) | Detalles de la cuenta empresarial de XDM | Habilitado | `accountKey.sourceKey` en la clase base | Cuenta B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Cuenta B2B | <ul><li>`accountParentKey.sourceKey` en el grupo de campos Detalles de cuenta empresarial de XDM</li><li>Propiedad de destino: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Esquema de referencia: cuenta B2B</li><li>Área de nombres: Cuenta B2B</li></ul> |  |
| Persona B2B | [Perfil individual de XDM](../../xdm/classes/individual-profile.md) | <ul><li>Detalles de persona de negocios de XDM</li><li>Componentes de persona empresarial de XDM</li><li>IdentityMap</li><li>Detalles de consentimiento y preferencia</li></ul> | Habilitado | `b2b.personKey.sourceKey` en el grupo de campos Detalles de persona de negocios de XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del grupo de campos Detalles de persona de negocio de XDM</li><li>`workEmail.address` del grupo de campos Detalles de persona de negocio de XDM</ol></li> | <ol><li>Persona B2B</li><li>Correo electrónico</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del grupo de campos Componentes de persona de negocio de XDM</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: accountKey.sourceKey</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Oportunidad B2B | [Oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity.md) | Detalles de oportunidad empresarial de XDM | Habilitado | `opportunityKey.sourceKey` en la clase base | Oportunidad B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Oportunidad B2B | <ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul> |  |
| Relación de persona de oportunidad B2B | [Relación de persona de oportunidad empresarial de XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Ninguna | Habilitado | `opportunityPersonKey.sourceKey` en la clase base | Relación de persona de oportunidad B2B | | | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: b2b.personKey.sourceKey</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul>**Segunda relación**<ul><li>`opportunityKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: oportunidad B2B </li><li>Área de nombres: oportunidad B2B </li><li>Propiedad de destino: `opportunityKey.sourceKey`</li><li>Nombre de relación del esquema actual: oportunidad</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Campaña B2B | [Campaña empresarial de XDM](../../xdm/classes/b2b/business-campaign.md) | Detalles de la campaña empresarial de XDM | Habilitado | `campaignKey.sourceKey` en la clase base | Campaña B2B | | | | |
| Miembro de la campaña B2B | [Miembros de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md) | Detalles del miembro de la campaña empresarial de XDM | Habilitado | `ccampaignMemberKey.sourceKey` en la clase base | Miembro de la campaña B2B | | | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Campaigns</li></ul>**Segunda relación**<ul><li>`campaignKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Campaña B2B</li><li>Área de nombres: Campaña B2B</li><li>Propiedad de destino: `campaignKey.sourceKey`</li><li>Nombre de relación del esquema actual: Campaign</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Lista de marketing B2B | [Lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list.md) | Ninguna | Habilitado | `marketingListKey.sourceKey` en la clase base | Lista de marketing B2B | Ninguna | Ninguna | Ninguna | La lista estática no se sincroniza desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Miembro de lista de marketing B2B | [Miembros de la lista de marketing empresarial de XDM](../../xdm/classes/b2b/business-marketing-list-members.md) | Ninguna | Habilitado | `marketingListMemberKey.sourceKey` en la clase base | Miembro de lista de marketing B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`PersonKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Listas de marketing</li></ul>**Segunda relación**<ul><li>`marketingListKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Lista de marketing B2B</li><li>Área de nombres: Lista de marketing B2B</li><li>Propiedad de destino: `marketingListKey.sourceKey`</li><li>Nombre de relación del esquema actual: Lista de marketing</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> | El miembro de la lista estática no se ha sincronizado desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Relación de persona de la cuenta B2B | [Relación de persona de la cuenta XDM](../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidad | Habilitado | `accountPersonKey.sourceKey` en la clase base | Relación de persona de la cuenta B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.SourceKey`</li><li>Nombre de relación del esquema actual: Personas</li><li>Nombre de relación del esquema de referencia: Cuenta</li></ul>**Segunda relación**<ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |

{style="table-layout:auto"}

