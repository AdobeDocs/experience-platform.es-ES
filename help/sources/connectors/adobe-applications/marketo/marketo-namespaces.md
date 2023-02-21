---
title: Esquemas y áreas de nombres B2B
description: Este documento proporciona información general sobre los espacios de nombres personalizados necesarios al crear un conector de origen B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fa3f937862dd8b6078f73b2a172b3fb5db652dc7
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 4%

---

# Esquemas y áreas de nombres B2B

>[!NOTE]
>
>Puede utilizar plantillas en la interfaz de usuario de Adobe Experience Platform para acelerar la creación de recursos para datos B2B y B2C. Para obtener más información, consulte la guía de [uso de plantillas en la interfaz de usuario de Platform](../../../tutorials/ui/templates.md).

Este documento proporciona información sobre la configuración subyacente para los espacios de nombres y esquemas que se van a utilizar con orígenes B2B. Este documento también proporciona detalles sobre la configuración de la utilidad de automatización de Postman necesaria para generar esquemas y áreas de nombres B2B.

>[!IMPORTANT]
>
>Debe tener acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para que los esquemas B2B participen en [Perfil del cliente en tiempo real](../../../../profile/home.md).

## Configuración de espacios de nombres B2B y utilidad de generación automática de esquemas

El primer paso para utilizar el espacio de nombres B2B y la utilidad de generación automática de esquemas es configurar la consola del desarrollador de Platform y [!DNL Postman] entorno.

- Puede descargar el entorno y la colección de utilidades de generación automática de esquemas y espacios de nombres desde esta [Repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obtener información sobre el uso de las API de plataforma, incluidos detalles sobre cómo recopilar valores para los encabezados necesarios y leer llamadas de API de ejemplo, consulte la guía de [introducción a las API de Platform](../../../../landing/api-guide.md).
- Para obtener información sobre cómo generar sus credenciales para las API de plataforma, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md).
- Para obtener información sobre cómo configurar [!DNL Postman] para las API de plataforma, consulte el tutorial en [configuración de la consola de desarrollador y [!DNL Postman]](../../../../landing/postman.md).

Con una consola de desarrollador de Platform y [!DNL Postman] configure, ahora puede empezar a aplicar los valores de entorno adecuados a su [!DNL Postman] entorno.

La siguiente tabla contiene valores de ejemplo, así como información adicional sobre cómo rellenar el [!DNL Postman] entorno:

| Variable | Descripción | Ejemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificador único que se usa para generar el informe `{ACCESS_TOKEN}`. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | El token web JSON (JWT) es una credencial de autenticación que se utiliza para generar su {ACCESS_TOKEN}. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo generar su `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Token de autorización necesario para completar llamadas a las API de Experience Platform. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Por lo que se refiere a [!DNL Marketo], este valor es fijo y siempre se establece en: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | La variable `global` contenedor contiene todas las clases proporcionadas por el socio de Experience Platform y Adobe estándar, los grupos de campos de esquema, los tipos de datos y los esquemas. Por lo que se refiere a [!DNL Marketo], este valor es fijo y siempre está establecido en `global`. | `global` |
| `PRIVATE_KEY` | Una credencial utilizada para autenticar su [!DNL Postman] a las API de Experience Platform. Consulte el tutorial sobre la configuración de la consola de desarrollador y [configuración de la consola de desarrollador y [!DNL Postman]](../../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Una credencial utilizada para integrarse en el Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | El sistema Identity Management (IMS) proporciona el marco para la autenticación en los servicios de Adobe. Por lo que se refiere a [!DNL Marketo], este valor es fijo y siempre se establece en: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Una entidad corporativa que puede ser propietaria o titular de licencias de productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial en [configuración de la consola de desarrollador y [!DNL Postman]](../../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su `{ORG_ID}` información. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nombre de la partición de entorno limitado virtual que está utilizando. | `prod` |
| `TENANT_ID` | Un ID utilizado para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos en su organización de IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Punto final de URL al que está realizando llamadas de API. Este valor es fijo y siempre se establece en: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### Ejecución de las secuencias de comandos

Con [!DNL Postman] configuración de entorno y recopilación, ahora puede ejecutar el script a través del [!DNL Postman] interfaz.

En el [!DNL Postman] , seleccione la carpeta raíz de la utilidad del generador automático y, a continuación, seleccione **[!DNL Run]** en el encabezado superior.

![carpeta raíz](../images/marketo/root-folder.png)

La variable [!DNL Runner] se abre. Desde aquí, asegúrese de que todas las casillas de verificación estén seleccionadas y, a continuación, seleccione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

Una solicitud correcta crea los espacios de nombres y esquemas necesarios para B2B.

## Espacios de nombres B2B

Las áreas de nombres de identidad son un componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que sirven para distinguir el contexto o el tipo de una identidad. Una identidad completa incluye un valor de ID y un área de nombres. Consulte la [información general sobre áreas de nombres](../../../../identity-service/namespaces.md) para obtener más información.

Las áreas de nombres B2B se utilizan en la identidad principal de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres B2B.

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad |
| --- | --- | --- |
| Persona B2B | `b2b_person` | `CROSS_DEVICE` |
| Cuenta B2B | `b2b_account` | `B2B_ACCOUNT` |
| Oportunidad B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relación de persona de oportunidad B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campaña B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Miembro de la campaña B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Lista de marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Miembro de la Lista de Marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relación de persona de cuenta B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## Esquemas B2B

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase base y de cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición del esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte la [conceptos básicos de la composición del esquema](../../../../xdm/schema/composition.md).

La siguiente tabla contiene información sobre la configuración subyacente de los esquemas B2B.

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre del esquema | Clase base | Grupos de campo | [!DNL Profile] en Esquema | Identidad primaria | Área de nombres de identidad principal | Identidad secundaria | Área de nombres de identidad secundaria | Relación | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cuenta B2B | [Cuenta comercial XDM](../../../../xdm/classes/b2b/business-account.md) | Detalles de la cuenta comercial de XDM | Habilitado | `accountKey.sourceKey` en la clase base | Cuenta B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Cuenta B2B | <ul><li>`accountParentKey.sourceKey` en el grupo de campos Detalles de cuenta comercial XDM</li><li>Propiedad de destino: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li></ul> |
| Persona B2B | [Perfil individual XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Detalles de persona comercial XDM</li><li>Componentes de persona empresarial XDM</li><li>Mapa de identidades</li><li>Detalles de consentimiento y preferencia</li></ul> | Habilitado | `b2b.personKey.sourceKey` en el grupo de campos Detalles de persona empresarial XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del grupo de campos Detalles de persona comercial XDM</li><li>`workEmail.address` del grupo de campos Detalles de persona comercial XDM</ol></li> | <ol><li>Persona B2B</li><li>Correo electrónico</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del grupo de campos Componentes de persona empresarial XDM</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: accountKey.sourceKey</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| Oportunidad B2B | [Oportunidad comercial XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Detalles de oportunidades comerciales de XDM | Habilitado | `opportunityKey.sourceKey` en la clase base | Oportunidad B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Oportunidad B2B | <ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul> |
| Relación de persona de oportunidad B2B | [Relación de persona de oportunidad comercial XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Ninguna | Habilitado | `opportunityPersonKey.sourceKey` en la clase base | Relación de persona de oportunidad B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Relación de persona de oportunidad B2B | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: Persona B2B</li><li>Propiedad de destino: b2b.personKey.sourceKey</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul>**Segunda relación**<ul><li>`opportunityKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Oportunidad B2B </li><li>Área de nombres: Oportunidad B2B </li><li>Propiedad de destino: `opportunityKey.sourceKey`</li><li>Nombre de relación del esquema actual: Oportunidad</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| Campaña B2B | [Campaña empresarial XDM](../../../../xdm/classes/b2b/business-campaign.md) | Detalles de la campaña empresarial XDM | Habilitado | `campaignKey.sourceKey` en la clase base | Campaña B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Campaña B2B |
| Miembro de la campaña B2B | [Miembros de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) | Detalles del miembro de la campaña empresarial XDM | Habilitado | `ccampaignMemberKey.sourceKey` en la clase base | Miembro de la campaña B2B | `extSourceSystemAudit.externalKey.sourceKey` en la clase base | Miembro de la campaña B2B | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: Persona B2B</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Campañas</li></ul>**Segunda relación**<ul><li>`campaignKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Campaña B2B</li><li>Área de nombres: Campaña B2B</li><li>Propiedad de destino: `campaignKey.sourceKey`</li><li>Nombre de relación del esquema actual: Campaign</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| Lista de marketing B2B | [Lista de marketing empresarial XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Ninguna | Habilitado | `marketingListKey.sourceKey` en la clase base | Lista de marketing B2B | Ninguna | Ninguna | Ninguna | La lista estática no está sincronizada desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Miembro de la Lista de Marketing B2B | [Miembros de la lista de marketing empresarial XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Ninguna | Habilitado | `marketingListMemberKey.sourceKey` en la clase base | Miembro de la Lista de Marketing B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`PersonKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: Persona B2B</li><li>Propiedad de destino: `b2b.personKey.sourceKey`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Listas de marketing</li></ul>**Segunda relación**<ul><li>`marketingListKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Lista de marketing B2B</li><li>Área de nombres: Lista de marketing B2B</li><li>Propiedad de destino: `marketingListKey.sourceKey`</li><li>Nombre de relación del esquema actual: Lista de marketing</li><li>Nombre de relación del esquema de referencia: People</li></ul> | El miembro de lista estática no está sincronizado desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| Actividad B2B | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visite WebPage</li><li>Nuevo posible cliente</li><li>Convertir posible cliente</li><li>Agregar a lista</li><li>Quitar de la lista</li><li>Agregar a oportunidad</li><li>Eliminar de oportunidad</li><li>Formulario rellenado</li><li>Clics en vínculos</li><li>Correo electrónico enviado</li><li>Correo electrónico abierto</li><li>Correo electrónico en el que se hizo clic</li><li>Correo electrónico rechazado</li><li>Correo electrónico rechazado leve</li><li>Cancelación de suscripción de correo electrónico</li><li>Puntuación cambiada</li><li>Oportunidad actualizada</li><li>Cambio del estado en la progresión de la campaña</li><li>Identificador de persona</li><li>URL web de Marketo</li><li>Momento interesante</li><li>Llamar a Weblock</li><li>Cambiar la cadencia de una campaña</li><li>Etapa de ingresos cambiada</li><li>Combinar posibles clientes</li><li>Correo electrónico enviado</li><li>Cambiar flujo de campaña</li><li>Añadir a Campaign</li></ul> | Habilitado | `personKey.sourceKey` del grupo de campos Identificador de persona | Persona B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`listOperations.listKey.sourceKey` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Lista de marketing B2B</li><li>Área de nombres: Lista de marketing B2B</li></ul>**Segunda relación**<ul><li>`opportunityEvent.opportunityKey.sourceKey` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Oportunidad B2B</li><li>Área de nombres: Oportunidad B2B</li></ul>**Tercera relación**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: Campaña B2B</li><li>Área de nombres: Campaña B2B</li></ul> | `ExperienceEvent` es diferente a las entidades. La identidad del evento de experiencia es la persona que realizó la actividad. |
| Relación de persona de cuenta B2B | [Relación de persona de cuenta comercial XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidad | Habilitado | `accountPersonKey.sourceKey` en la clase base | Relación de persona de cuenta B2B | Ninguna | Ninguna | **Primera relación**<ul><li>`personKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona B2B</li><li>Área de nombres: Persona B2B</li><li>Propiedad de destino: `b2b.personKey.SourceKey`</li><li>Nombre de relación del esquema actual: People</li><li>Nombre de relación del esquema de referencia: Cuenta</li></ul>**Segunda relación**<ul><li>`accountKey.sourceKey` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Cuenta B2B</li><li>Área de nombres: Cuenta B2B</li><li>Propiedad de destino: `accountKey.sourceKey`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: People</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Para aprender a conectar su [!DNL Marketo] datos para Platform, consulte el tutorial en [creación de un conector de origen de Marketo en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).
