---
keywords: Experience Platform;inicio;temas populares;conector de origen de Marketo;áreas de nombres;esquemas
solution: Experience Platform
title: Espacios de nombres de Marketo
topic-legacy: overview
description: Este documento proporciona información general sobre las áreas de nombres personalizadas necesarias al crear un conector de origen de Marketo Engage.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: af728fb508c514db3d5871114f9a406c1ed428f2
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 5%

---

# (Beta) [!DNL Marketo Engage] áreas de nombres y esquemas

>[!IMPORTANT]
>
>El origen [!DNL Marketo Engage] está actualmente en versión beta. La función y la documentación están sujetas a cambios.

Este documento proporciona información sobre la configuración subyacente para los espacios de nombres B2B y esquemas utilizados con [!DNL Marketo Engage] (en adelante denominados &quot;[!DNL Marketo]&quot;). Este documento también proporciona detalles sobre la configuración de la utilidad de automatización de Postman necesaria para generar esquemas y áreas de nombres [!DNL Marketo] B2B.

## Configure el espacio de nombres [!DNL Marketo] y la utilidad de generación automática de esquemas

El primer paso para utilizar el espacio de nombres [!DNL Marketo] y la utilidad de generación automática de esquemas es configurar la consola del desarrollador de Platform y el entorno [!DNL Postman].

- Puede descargar el entorno y la colección de utilidades de generación automática de esquemas y espacios de nombres desde este [repositorio de GitHub](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- Para obtener información sobre el uso de las API de plataforma, incluidos detalles sobre cómo recopilar valores para los encabezados necesarios y leer llamadas de API de ejemplo, consulte la guía de [introducción a las API de plataforma](../../../../landing/api-guide.md).
- Para obtener información sobre cómo generar las credenciales para las API de plataforma, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../../landing/api-authentication.md).
- Para obtener información sobre cómo configurar [!DNL Postman] para las API de plataforma, consulte el tutorial sobre la [configuración de la consola del desarrollador y [!DNL Postman]](../../../../landing/postman.md).

Con una consola de desarrollador de Platform y [!DNL Postman] configurada, ahora puede empezar a aplicar los valores de entorno adecuados a su entorno [!DNL Postman].

La siguiente tabla contiene valores de ejemplo, así como información adicional sobre cómo rellenar el entorno [!DNL Postman]:

| Variable | Descripción | Ejemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificador único utilizado para generar su `{ACCESS_TOKEN}`. Consulte el tutorial sobre [autenticación y acceso a las API del Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | El token web JSON (JWT) es una credencial de autenticación que se utiliza para generar su {ACCESS_TOKEN}. Consulte el tutorial sobre [autenticación y acceso a las API del Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo generar su `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API del Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Token de autorización necesario para completar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API del Experience Platform](../../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | El contenedor `global` contiene todas las clases, grupos de campos de esquema, tipos de datos y esquemas proporcionados por el socio de Experience Platform y Adobe estándar. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en `global`. | `global` |
| `PRIVATE_KEY` | Una credencial utilizada para autenticar la instancia [!DNL Postman] en las API de Experience Platform. Consulte el tutorial sobre la configuración de la consola de desarrollador y [la configuración de la consola de desarrollador y [!DNL Postman]](../../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Una credencial utilizada para integrarse en el Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | El sistema Identity Management (IMS) proporciona el marco para la autenticación en los servicios de Adobe. Con respecto a [!DNL Marketo], este valor es fijo y siempre se configura como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Una entidad corporativa que puede ser propietaria o titular de licencias de productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre la [configuración de la consola del desarrollador y [!DNL Postman]](../../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar la información de `{IMS_ORG}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nombre de la partición de entorno limitado virtual que está utilizando. | `prod` |
| `TENANT_ID` | Un ID utilizado para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos en su organización de IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Punto final de URL al que está realizando llamadas de API. Este valor es fijo y siempre se establece en: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | El ID exclusivo de su cuenta [!DNL Marketo]. Consulte el tutorial sobre [la autenticación de su [!DNL Marketo] instancia](./marketo-auth.md) para obtener información sobre cómo recuperar su `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | El ID de organización de su cuenta [!DNL Salesforce]. Consulte la siguiente [[!DNL Salesforce] guía](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obtener más información sobre cómo adquirir su ID de organización [!DNL Salesforce]. | `00D4W000000FgYJUA0` |
| `msd_org_id` | El ID de organización de su cuenta [!DNL Dynamics]. Consulte la siguiente [[!DNL Microsoft Dynamics] guía](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) para obtener más información sobre cómo adquirir su ID de organización [!DNL Dynamics]. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Un valor booleano que indica si está suscrito a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Un valor booleano que indica si está suscrito a [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Ejecución de las secuencias de comandos

Con la colección [!DNL Postman] y el entorno configurados, ahora puede ejecutar el script a través de la interfaz [!DNL Postman].

En la interfaz [!DNL Postman], seleccione la carpeta raíz de la utilidad del generador automático y, a continuación, seleccione **[!DNL Run]** en el encabezado superior.

![carpeta raíz](../images/marketo/root-folder.png)

Aparece la interfaz [!DNL Runner]. Desde aquí, asegúrese de que todas las casillas de verificación estén seleccionadas y, a continuación, seleccione **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**.

![run-generator](../images/marketo/run-generator.png)

Una solicitud correcta crea los espacios de nombres B2B y esquemas según las especificaciones beta.

## [!DNL Marketo] áreas de nombres

Las áreas de nombres de identidad son un componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que sirve como indicadores del contexto al que se relaciona una identidad.

Una identidad completa incluye un valor de ID y un área de nombres. Se requiere un nuevo espacio de nombres personalizado para cada nueva combinación de [!DNL Marketo] instancia y conjunto de datos. Por ejemplo, un conector de origen [!DNL Marketo] que incorpora el conjunto de datos `programs` requiere su propio espacio de nombres personalizado, y otro conector de origen de Marketo que incorpora el mismo conjunto de datos también requiere su propio nuevo espacio de nombres personalizado. Consulte la [descripción general de los espacios de nombres](../../../../identity-service/namespaces.md) para obtener más información.

El espacio de nombres [!DNL Marketo] se utiliza en la identidad principal de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres [!DNL Marketo].

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

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

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Tipo de emisor | Tipo de entidad emisora | [!DNL Salesforce] ejemplo de ID de organización de suscripción |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | generado automáticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] áreas de nombres

Si está suscrito a la integración [!DNL Dynamics] , el espacio de nombres [!DNL Dynamics] se utiliza como identidad secundaria de la entidad.

La siguiente tabla contiene información sobre la configuración subyacente para los espacios de nombres [!DNL Dynamics].

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Tipo de emisor | Tipo de entidad emisora | [!DNL Dynamics] ejemplo de ID de organización de suscripción |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | generado automáticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | generado automáticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | generado automáticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | generado automáticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | generado automáticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | generado automáticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] esquemas

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase base y de cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquema](../../../../xdm/schema/composition.md).

La siguiente tabla contiene información sobre la configuración subyacente de los esquemas [!DNL Marketo].

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Nombre del esquema | Clase base | Grupos de campo | [!DNL Profile] en Esquema | Identidad primaria | Área de nombres de identidad principal | Identidad secundaria | Área de nombres de identidad secundaria | Relación | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | Cuenta comercial XDM | Detalles de la cuenta comercial de XDM | Habilitado | `accountID` en la clase base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` en el grupo de campos Detalles de cuenta comercial XDM</li><li>Tipo: uno a uno</li><li>Esquema de referencia: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | Perfil individual XDM | <ul><li>Detalles de persona comercial XDM</li><li>Componentes de persona empresarial XDM</li><li>Mapa de identidades</li></ul> | Habilitado | `personID` en la clase base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` del grupo de campos Detalles de persona comercial XDM</li><li>`workEmail.address` del grupo de campos Detalles de persona comercial XDM</li><li>`identityMap` del grupo de campos de mapa de identidad</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>Correo electrónico</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` del grupo de campos Componentes de persona empresarial XDM</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `accountID`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | Oportunidad comercial XDM | Detalles de oportunidades comerciales de XDM | Habilitado | `opportunityID` en la clase base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_company_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `accountID`</li><li>Nombre de relación del esquema actual: Cuenta</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | Relación de persona de oportunidad comercial XDM | Ninguna | Habilitado | `opportunityPersonID` en la clase base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Oportunidades</li></ul>Segunda relación<ul><li>`opportunityID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `opportunityID`</li><li>Nombre de relación del esquema actual: Oportunidad</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | Campaña empresarial XDM | Detalles de la campaña empresarial XDM | Habilitado | `campaignID` en la clase base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | Miembro de XDM Business Campaign | Detalles del miembro de la campaña empresarial XDM | Habilitado | `campaignMemberID` en la clase base | `marketo_program_member_{MUNCHKIN_ID}` | Ninguna | Ninguna | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: Persona de Marketo {MUNCHKIN_ID}</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Programas</li></ul>Segunda relación<ul><li>`campaignID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_program_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `campaignID`</li><li>Nombre de relación del esquema actual: Programa</li><li>Nombre de relación del esquema de referencia: People</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | Lista de marketing empresarial XDM | Ninguna | Habilitado | `marketingListID` en la clase base | `marketo_static_list_{MUNCHKIN_ID}` | Ninguna | Ninguna | Ninguna | La lista estática no está sincronizada desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | Miembros de la lista de marketing empresarial XDM | Ninguna | Habilitado | `marketingListMemberID` en la clase base | `marketo_static_list_member_{MUNCHKIN_ID}` | Ninguna | Ninguna | Primera relación<ul><li>`personID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_person_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `personID`</li><li>Nombre de relación del esquema actual: Persona</li><li>Nombre de relación del esquema de referencia: Listas</li></ul>Segunda relación<ul><li>`marketingListID` en la clase base</li><li>Tipo: Varios a uno</li><li>Esquema de referencia: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propiedad de destino: `marketingListID`</li><li>Nombre de relación del esquema actual: Lista</li><li>Nombre de relación del esquema de referencia: People</li></ul> | El miembro de la lista estática no está sincronizado desde [!DNL Salesforce] y, por lo tanto, no tiene una identidad secundaria. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | Cuenta comercial XDM | Detalles de la cuenta comercial de XDM | Habilitado | `accountID` en la clase base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` en la clase base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` en el grupo de campos Detalles de cuenta comercial XDM</li><li>Tipo: uno a uno</li><li>Esquema de referencia: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Actividad `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>Visite WebPage</li><li>Nuevo posible cliente</li><li>Convertir posible cliente</li><li>Agregar a lista</li><li>Quitar de la lista</li><li>Agregar a oportunidad</li><li>Eliminar de oportunidad</li><li>Formulario rellenado</li><li>Clics en vínculos</li><li>Correo electrónico enviado</li><li>Correo electrónico abierto</li><li>Correo electrónico en el que se hizo clic</li><li>Correo electrónico rechazado</li><li>Correo electrónico rechazado leve</li><li>Cancelación de suscripción de correo electrónico</li><li>Puntuación cambiada</li><li>Oportunidad actualizada</li><li>Cambio del estado en la progresión de la campaña</li><li>Identificador de persona</li><li>URL web de Marketo | Habilitado | `personID` del grupo de campos Identificador de persona | `marketo_person_{MUNCHKIN_ID}` | Ninguna | Ninguna | Primera relación<ul><li>`listOperations.listID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Segunda relación<ul><li>`opportunityEvent.opportunityID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Tercera relación<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Tipo: uno a uno</li><li>Esquema de referencia: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Área de nombres: `marketo_program_{MUNCHKIN_ID}`</li></ul> | La identidad principal del esquema `[!DNL Marketo] Activity {MUNCHKIN_ID}` es `personID`, que es la misma que la identidad principal del esquema `[!DNL Marketo] Person {MUNCHKIN_ID}`. |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Para aprender a conectar los datos [!DNL Marketo] a Platform, consulte el tutorial sobre la [creación de un conector de origen de Marketo en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).
