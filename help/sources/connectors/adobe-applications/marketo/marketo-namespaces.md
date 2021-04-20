---
keywords: Experience Platform;inicio;temas populares;conector de origen de Marketo;áreas de nombres;esquemas
solution: Experience Platform
title: 'Espacios de nombres de Marketo '
topic: sobre validación
description: Este documento proporciona información general sobre las áreas de nombres personalizadas necesarias al crear un conector de origen de Marketo Engage.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 6%

---


# (Beta) [!DNL Marketo Engage] áreas de nombres y esquemas

>[!IMPORTANT]
>
>El origen [!DNL Marketo Engage] está actualmente en versión beta. La función y la documentación están sujetas a cambios.

Este documento proporciona información sobre la configuración subyacente para los espacios de nombres B2B y esquemas utilizados con [!DNL Marketo Engage] (en adelante denominados &quot;[!DNL Marketo]&quot;). Este documento también proporciona detalles sobre la configuración de la utilidad de automatización de Postman necesaria para generar esquemas y áreas de nombres [!DNL Marketo] B2B.

## Requisitos previos

Para poder generar los esquemas y espacios de nombres B2B, primero debe configurar la consola del desarrollador de Platform y el entorno [!DNL Postman] . Para obtener más información, consulte el tutorial sobre [configuración de la consola del desarrollador y [!DNL Postman]](../../../../landing/postman.md).

Con una consola de desarrollador de Platform y una [!DNL Postman] configuración, aplique las siguientes variables a su entorno [!DNL Marketo]:

| Variable de entorno | Valor de ejemplo | Notas |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Consulte el tutorial sobre [la autenticación de la instancia [!DNL Marketo] ](./marketo-auth.md) para obtener más información. |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Consulte la siguiente [[!DNL Salesforce] guía](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obtener más información sobre la adquisición de su ID de organización. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Consulte la siguiente [[!DNL Microsoft Dynamics] guía](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) para obtener más información sobre la adquisición de su ID de organización. |
| `has_abm` | `false` | Este valor se establece en `true` si está suscrito a Marketing basado en cuentas. |
| `has_msi` | `false` | Este valor se establece en `true` si está suscrito a [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] áreas de nombres

Las áreas de nombres de identidad son un componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que sirve como indicadores del contexto al que se relaciona una identidad.

Una identidad completa incluye un valor de ID y un área de nombres. Se requiere un nuevo espacio de nombres personalizado para cada nueva combinación de [!DNL Marketo] instancia y conjunto de datos. Por ejemplo, un conector de origen [!DNL Marketo] que incorpora el conjunto de datos `programs` requiere su propio espacio de nombres personalizado, y otro conector de origen de Marketo que incorpora el mismo conjunto de datos también requiere su propio nuevo espacio de nombres personalizado. Consulte la [descripción general de los espacios de nombres](../../../../identity-service/namespaces.md) para obtener más información.

El espacio de nombres [!DNL Marketo] se utiliza en la identidad principal de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres [!DNL Marketo].

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Tipo de emisor | Tipo de entidad emisora | Ejemplo de ID de Munchkin |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | generado automáticamente | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | generado automáticamente | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | generado automáticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | generado automáticamente | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | generado automáticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | generado automáticamente | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | generado automáticamente | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] áreas de nombres

Si está suscrito a la integración [!DNL Salesforce] , el espacio de nombres [!DNL Salesforce] se utiliza en la identidad secundaria de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres [!DNL Salesforce].

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Tipo de emisor | Tipo de entidad emisora | [!DNL Salesforce] ejemplo de ID de organización de suscripción |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] áreas de nombres

Si está suscrito a la integración [!DNL Dynamics] , el espacio de nombres [!DNL Dynamics] se utiliza como identidad secundaria de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres [!DNL Dynamics].

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Tipo de emisor | Tipo de entidad emisora | [!DNL Salesforce] ejemplo de ID de organización de suscripción |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | generado automáticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | generado automáticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | generado automáticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | generado automáticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | generado automáticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] esquemas

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas consisten en una clase base y cero o más mezclas.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquema](../../../../xdm/schema/composition.md).

La siguiente tabla contiene información sobre la configuración subyacente de los esquemas [!DNL Marketo].

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre del esquema | Clase base | Mezclas | Identidad primaria | Área de nombres de identidad principal | Identidad secundaria | Área de nombres de identidad secundaria | Relación | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Empresa {MUNCHKIN_ID} | Cuenta comercial XDM | Detalles de la cuenta comercial de XDM | `accountID` en la clase base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` en la mezcla de detalles de cuentas comerciales XDM</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Empresa de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Persona {MUNCHKIN_ID} | Perfil individual XDM | <ul><li>Detalles de persona comercial XDM</li><li>Componentes de persona empresarial XDM</li></ul> | `personID` en la clase base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` de la mezcla de detalles de XDM Business Person</li><li>`workEmail.address` de la mezcla de detalles de XDM Business Person</li><li>`identityMap` de la mezcla de mapa de identidad</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>Correo electrónico</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` de la mezcla de componentes XDM Business Person</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Empresa de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `accountID`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| [!DNL Marketo] Oportunidad {MUNCHKIN_ID} | Oportunidad comercial XDM | Detalles de oportunidades comerciales de XDM | `opportunityID` en la clase base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Empresa de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `accountID`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul> |
| [!DNL Marketo] Función de contacto de oportunidad {MUNCHKIN_ID} | Relación de persona de oportunidad comercial XDM | Ninguna | `opportunityPersonID` en la clase base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul>Segunda relación<ul><li>`opportunityID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Oportunidad de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `opportunityID`</li><li>Nombre de relación del esquema actual: Oportunidad</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| [!DNL Marketo] Programa {MUNCHKIN_ID} | Campaña empresarial XDM | Detalles de la campaña empresarial XDM | `campaignID` en la clase base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Miembro del programa {MUNCHKIN_ID} | Miembro de XDM Business Campaign | Detalles del miembro de la campaña empresarial XDM | `campaignMemberID` en la clase base | `marketo_program_member_{MUNCHKIN_ID}` | Ninguna | Ninguna | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Programas</li></ul>Segunda relación<ul><li>`campaignID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Programa Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_program_{MUNCHKIN_ID}`</li><li>Propiedad de destino: campaignID</li><li>Nombre de relación del esquema actual: Programa</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| [!DNL Marketo] Lista estática {MUNCHKIN_ID} | Lista de marketing empresarial XDM | Ninguna | `marketingListID` en la clase base | `marketo_static_list_{MUNCHKIN_ID}` | Ninguna | Ninguna | Ninguna | La lista estática no está sincronizada desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria |
| [!DNL Marketo] Miembro de lista estática {MUNCHKIN_ID} | Miembros de la lista de marketing empresarial XDM | Ninguna | `marketingListMemberID` en la clase base | `marketo_static_list_member_{MUNCHKIN_ID}` | Ninguna | Ninguna | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Listas</li></ul>Segunda relación<ul><li>`marketingListID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Lista estática de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `marketingListID`</li><li>Nombre de relación del esquema actual: Lista</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| [!DNL Marketo] Cuenta con nombre {MUNCHKIN_ID} | Cuenta comercial XDM | Detalles de la cuenta comercial de XDM | `accountID` en la clase base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` en la mezcla de detalles de cuentas comerciales XDM</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Cuenta con nombre de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Actividad {MUNCHKIN ID} | Evento de experiencia XDM | <ul><li>Visite WebPage</li><li>Nuevo posible cliente</li><li>Convertir posible cliente</li><li>Agregar a lista</li><li>Quitar de la lista</li><li>Agregar a oportunidad</li><li>Eliminar de oportunidad</li><li>Formulario rellenado</li><li>Clics en vínculos</li><li>Correo electrónico enviado</li><li>Correo electrónico abierto</li><li>Correo electrónico en el que se hizo clic</li><li>Correo electrónico rechazado</li><li>Correo electrónico rechazado leve</li><li>Cancelación de suscripción de correo electrónico</li><li>Puntuación cambiada</li><li>Oportunidad actualizada</li><li>Cambio del estado en la progresión de la campaña</li><li>Identificador de persona</li><li>URL web de Marketo | `personID` de la mezcla de Identificador de persona | marketo_person_{MUNCHKIN_ID} | Ninguna | Ninguna | Primera relación<ul><li>`listOperations.listID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Lista estática de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Segunda relación<ul><li>`opportunityEvent.opportunityID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Oportunidad de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Tercera relación<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Programa Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Todos los esquemas están habilitados para [!DNL Real-time Customer Profile]

## Pasos siguientes

Para aprender a conectar los datos [!DNL Marketo] a Platform, consulte el tutorial sobre la [creación de un conector de origen de Marketo en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).