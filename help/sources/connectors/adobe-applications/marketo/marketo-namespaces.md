---
title: Espacios de nombres y esquemas B2B
description: Este documento proporciona información general sobre las áreas de nombres personalizadas necesarias al crear un conector de origen B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5eeb0397ddc96a224919a776f94058ae3a539b69
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 6%

---

# Espacios de nombres y esquemas B2B

>[!AVAILABILITY]
>
>- Debe tener acceso a [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) para que sus esquemas B2B califiquen en [Perfil del cliente en tiempo real](../../../../profile/home.md).
>
>- A partir de enero de 2026, Real-Time CDP B2B edition dejará de admitir **relaciones no estándar** entre entidades B2B. Por lo tanto, se recomienda actualizar las entidades B2B para que utilicen las relaciones estándar descritas en la [guía de esquemas y áreas de nombres B2B](../../../../rtcdp/schemas/b2b.md).

>[!NOTE]
>
>Puede utilizar plantillas en la interfaz de usuario de Adobe Experience Platform para acelerar la creación de recursos para los datos B2B y B2C. Para obtener más información, lea la guía de [uso de plantillas en la interfaz de usuario de Experience Platform](../../../tutorials/ui/templates.md).

Lea este documento para obtener información sobre la configuración subyacente de los espacios de nombres y esquemas que se van a utilizar con orígenes B2B. Este documento también proporciona detalles sobre la configuración de la utilidad de automatización de Postman necesaria para generar espacios de nombres y esquemas B2B.

## Configurar áreas de nombres B2B y la utilidad de generación automática de esquemas

>[!IMPORTANT]
>
>Las credenciales de la cuenta de servicio (JWT) han quedado obsoletas. Debe asegurarse de migrar la aplicación o integración a la nueva credencial de servidor a servidor de OAuth antes del 27 de enero de 2025. Lea la siguiente documentación para ver los pasos detallados sobre [cómo migrar su credencial JWT a la credencial de servidor a servidor OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Consulte la siguiente documentación para obtener información sobre los requisitos previos de cómo configurar su entorno [!DNL Postman] para que sea compatible con el espacio de nombres B2B y la utilidad de generación automática de esquemas.

- Puede descargar la colección de utilidades de generación automática de esquemas y áreas de nombres desde este [repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obtener información sobre el uso de las API de Experience Platform, incluidos detalles sobre cómo recopilar valores para los encabezados necesarios y leer llamadas de API de ejemplo, consulte la guía sobre [introducción a las API de Experience Platform](../../../../landing/api-guide.md).
- Para obtener información sobre cómo generar tus credenciales para las API de Experience Platform, consulta el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md).
- Para obtener información sobre cómo configurar [!DNL Postman] para las API de Experience Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../../landing/postman.md).

Con una consola de desarrollador de Experience Platform y [!DNL Postman] configuradas, ahora puede empezar a aplicar los valores de entorno apropiados a su entorno [!DNL Postman].

La siguiente tabla contiene valores de ejemplo, así como información adicional sobre cómo rellenar el entorno [!DNL Postman]:

| Variable | Descripción | Ejemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificador único usado para generar su `{ACCESS_TOKEN}`. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `API_KEY` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | El contenedor `global` contiene todas las clases, los grupos de campos de esquema, los tipos de datos y los esquemas proporcionados por los socios estándar de Adobe y Experience Platform. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en `global`. | `global` |
| `TECHNICAL_ACCOUNT_ID` | Credencial utilizada para integrarse en Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | El sistema de Identity Management (IMS) proporciona el marco para la autenticación en los servicios de Adobe. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar la información de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nombre de la partición de zona protegida virtual que está utilizando. | `prod` |
| `TENANT_ID` | ID que se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | El extremo URL al que realiza llamadas de API. Este valor es fijo y siempre se establece en: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Ejecución de scripts

Con la colección y el entorno [!DNL Postman] configurados, ahora puede ejecutar el script a través de la interfaz [!DNL Postman].

En la interfaz [!DNL Postman], seleccione la carpeta raíz de la utilidad autogenerador y, a continuación, seleccione **[!DNL Run]** en el encabezado superior.

![Carpeta raíz del generador de espacios de nombres y esquemas en la interfaz de usuario de Postman. &quot;Ejecuciones&quot; aparece resaltado en la barra de menús superior.](../images/marketo/root_folder.png)

Aparecerá la interfaz [!DNL Runner]. Aquí, asegúrese de que todas las casillas de verificación estén seleccionadas y luego seleccione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![Se comprobó la interfaz Runner de la interfaz de usuario de Postman con varias solicitudes en la colección Namespaces and Schemas y se resaltó el botón &quot;Run Namespaces and Schemas&quot; a la derecha.](../images/marketo/run_generator.png)

Una solicitud correcta crea los espacios de nombres y esquemas necesarios para B2B.

## Áreas de nombres B2B

Las áreas de nombres de identidad son un componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que sirve para distinguir el contexto de una identidad. Una identidad completa incluye un valor de identidad y un área de nombres. Lea la [descripción general de áreas de nombres](../../../../identity-service/features/namespaces.md) para obtener más información.

Las áreas de nombres B2B se utilizan en la identidad principal de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente de las áreas de nombres B2B.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad |
| --- | --- | --- |
| Persona B2B | `b2b_person` | `CROSS_DEVICE` |
| Cuenta B2B | `b2b_account` | `B2B_ACCOUNT` |
| Oportunidad B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relación de persona de oportunidad B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campaña B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Miembro de la campaña B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Lista de marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Miembro de lista de marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relación de persona de la cuenta B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Esquemas B2B

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Experience Platform, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase base y cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, vea los [conceptos básicos de la composición de esquema](../../../../xdm/schema/composition.md).

La siguiente tabla contiene información sobre la configuración subyacente de los esquemas B2B.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre del esquema | Clase base | Grupos de campo | [!DNL Profile] en esquema | Identidad principal | Espacio de nombres de identidad principal | Identidad secundaria | Área de nombres de identidad secundaria | Relación | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cuenta B2B | [Cuenta empresarial de XDM](../../../../xdm/classes/b2b/business-account.md) | Detalles de la cuenta empresarial de XDM | Habilitado | `accountKey.sourceKey` en la clase base | Cuenta B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Cuenta B2B | <ul><li>`accountParentKey.sourceKey` en el grupo de campos Detalles de cuenta empresarial de XDM</li><li>Propiedad de destino: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Esquema de referencia: cuenta B2B</li><li>Área de nombres: Cuenta B2B</li></ul> |  |
| Persona B2B | [Perfil individual de XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Detalles de persona de negocios de XDM</li><li>Componentes de persona empresarial de XDM</li><li>IdentityMap</li><li>Detalles de consentimiento y preferencia</li></ul> | Habilitado | `b2b.personKey.sourceKey` en el grupo de campos Detalles de persona de negocios de XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del grupo de campos Detalles de persona de negocio de XDM</li><li>`workEmail.address` del grupo de campos Detalles de persona de negocio de XDM</ol></li> | <ol><li>Persona B2B</li><li>Correo electrónico</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del grupo de campos Componentes de persona de negocio de XDM</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: accountKey.sourceKey</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Oportunidad B2B | [Oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Detalles de oportunidad empresarial de XDM | Habilitado | `opportunityKey.sourceKey` en la clase base | Oportunidad B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Oportunidad B2B | <ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul> |  |
| Relación de persona de oportunidad B2B | [Relación de persona de oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Ninguna | Habilitado | `opportunityPersonKey.sourceKey` en la clase base | Relación de persona de oportunidad B2B | | | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: b2b.personKey.sourceKey</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul>**Segunda relación**<ul><li>`opportunityKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: oportunidad B2B </li><li>Área de nombres: oportunidad B2B </li><li>Propiedad de destino: `opportunityKey.sourceKey`</li><li>Nombre de relación del esquema actual: oportunidad</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Campaña B2B | [Campaña empresarial de XDM](../../../../xdm/classes/b2b/business-campaign.md) | Detalles de la campaña empresarial de XDM | Habilitado | `campaignKey.sourceKey` en la clase base | Campaña B2B | | |  |
| Miembro de la campaña B2B | [Miembros de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) | Detalles del miembro de la campaña empresarial de XDM | Habilitado | `ccampaignMemberKey.sourceKey` en la clase base | Miembro de la campaña B2B | | | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Campaigns</li></ul>**Segunda relación**<ul><li>`campaignKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Campaña B2B</li><li>Área de nombres: Campaña B2B</li><li>Propiedad de destino: `campaignKey.sourceKey`</li><li>Nombre de relación del esquema actual: Campaign</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |
| Lista de marketing B2B | [Lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Ninguna | Habilitado | `marketingListKey.sourceKey` en la clase base | Lista de marketing B2B | Ninguna | Ninguna | Ninguna | La lista estática no se sincroniza desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Miembro de lista de marketing B2B | [Miembros de la lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Ninguna | Habilitado | `marketingListMemberKey.sourceKey` en la clase base | Miembro de lista de marketing B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`PersonKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Person</li><li>Nombre de relación del esquema de referencia: Listas de marketing</li></ul>**Segunda relación**<ul><li>`marketingListKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Lista de marketing B2B</li><li>Área de nombres: Lista de marketing B2B</li><li>Propiedad de destino: `marketingListKey.sourceKey`</li><li>Nombre de relación del esquema actual: Lista de marketing</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> | El miembro de la lista estática no se ha sincronizado desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Relación de persona de la cuenta B2B | [Relación de persona de la cuenta XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidad | Habilitado | `accountPersonKey.sourceKey` en la clase base | Relación de persona de la cuenta B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: B2B Person</li><li>Propiedad de destino: `b2b.personKey.SourceKey`</li><li>Nombre de relación del esquema actual: Personas</li><li>Nombre de relación del esquema de referencia: Cuenta</li></ul>**Segunda relación**<ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Personas</li></ul> |  |

{style="table-layout:auto"}

## Próximos pasos

Para obtener información sobre cómo conectar los datos de [!DNL Marketo] a Experience Platform, consulte el tutorial sobre [creación de un conector de origen de Marketo en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).

<!--

| B2B Activity | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visit WebPage</li><li>New Lead</li><li>Convert Lead</li><li>Add To List</li><li>Remove From List</li><li>Add To Opportunity</li><li>Remove From Opportunity</li><li>Form Filled Out</li><li>Link Clicks</li><li>Email Delivered</li><li>Email Opened</li><li>Email Clicked</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Email Unsubscribed</li><li>Score Changed</li><li>Opportunity Updated</li><li>Status in Campaign Progression Changed</li><li>Person Identifier</li><li>Marketo Web URL</li><li>Interesting Moment</li><li>Call Webhook</li><li>Change Campaign Cadence</li><li>Revenue Stage Changed</li><li>Merge Leads</li><li>Email Sent</li><li>Change Campaign Stream</li><li>Add to Campaign</li></ul> | Enabled | `personKey.sourceKey` of Person Identifier field group | B2B Person | None | None | | `ExperienceEvent` is different from entities. The identity of experience event is the person who did the activity. |

-->