---
title: Información general sobre Oracle Eloqua (V2) Source
description: Aprenda a conectar Oracle Eloqua a Adobe Experience Platform.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 1%

---

# Resumen de origen de [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>El origen [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) original quedó obsoleto en enero de 2026. No hay migraciones disponibles para este origen obsoleto y debe volver a implementar los datos usando el nuevo origen [!DNL Oracle Eloqua] (V2).

[!DNL Oracle Eloqua] es una potente plataforma de automatización de marketing de nivel empresarial diseñada para ayudar a las organizaciones, principalmente en el espacio B2B, a automatizar y personalizar el complejo proceso de administrar posibles clientes y organizar los recorridos de los compradores. Sirve como centro donde los equipos de marketing pueden definir, implementar y medir campañas sofisticadas en varios canales digitales, lo que garantiza que los clientes potenciales reciban el contenido adecuado en el momento preciso en que más participan. Los objetos admitidos para la ingesta mediante [!DNL Eloqua] son **Contactos**, **Cuentas**, **Campañas** y **Actividades**. Una vez completada la ingesta inicial, los datos modificados se importan mediante un proceso incremental programado.

Puede usar el origen [!DNL Eloqua] para conectar su cuenta de [!DNL Eloqua] a Adobe Experience Platform. Lea la documentación siguiente para aprender a empezar.

## Ejemplos de casos de uso {#use-case-examples}

A continuación se muestra una tabla en la que se describen los objetos de marketing admitidos por la integración de [!DNL Eloqua] (V2) con Adobe Experience Platform. Para cada objeto, encontrará una descripción junto con ejemplos de casos de uso para ilustrar cómo la integración de datos de [!DNL Eloqua] con Real-Time CDP puede mejorar la eficacia del marketing y los resultados de las campañas.

| Objeto | Descripción | Ejemplos de casos de uso |
| --- | --- | --- |
| Contactos | Introduzca datos de contacto (como nombre, correo electrónico, número de teléfono y cargo) en Real-Time CDP para crear perfiles de cliente detallados y unificados que consoliden todas las interacciones y compromisos con cada contacto individual. | **Optimización de la campaña:** Al integrar los datos de contacto de [!DNL Eloqua], su equipo de marketing puede identificar posibles clientes de alta prioridad en función de actividades recientes como aperturas de correo electrónico, envíos de formularios y registros de eventos. Real-Time CDP proporciona una vista de 360° del comportamiento de cada contacto en el correo electrónico, el sitio web y otros puntos de contacto de marketing, lo que permite a los equipos de marketing adaptar las campañas y optimizar la mensajería para mejorar la participación y la conversión. |
| Cuentas | Ingeste datos de nivel de cuenta (como nombre de la empresa, sector, tamaño de la empresa, ingresos y ubicación) para crear estrategias de marketing basado en cuentas (ABM) en Real-Time CDP y permitir que su equipo se dirija a las organizaciones adecuadas y participe en ellas con mensajes relevantes. | **Campañas ABM:** La integración de datos de cuenta de [!DNL Eloqua] ayuda a crear campañas ABM dirigidas. Por ejemplo, una empresa de software podría utilizar los datos de la cuenta para segmentar y enviar campañas de correo electrónico personalizadas a los responsables de la toma de decisiones en empresas del sector financiero, promoviendo nuevas soluciones adaptadas a su sector. |
| Campañas | Ingeste datos de campaña (como nombres, tipos, objetivos y métricas de rendimiento de campañas como tasas de apertura y CTR) en Real-Time CDP para rastrear y optimizar el rendimiento de la campaña en varios canales. Utilice estos datos para medir el retorno de la inversión y refinar sus estrategias. | **Atribución en canales múltiples:** Si [!DNL Eloqua] envía datos de campaña a Real-Time CDP, los equipos de marketing pueden ver el rendimiento de las campañas en varios canales (correo electrónico, medios sociales, anuncios, etc.), atribuyendo conversiones a los puntos de contacto correctos y refinando las estrategias futuras basadas en ese insight. |
| Actividades | Ingeste datos de actividad (como aperturas de correo electrónico, clics, visitas a sitios web, envíos de formularios, asistencia a seminarios web) para rastrear el comportamiento en tiempo real y los contactos en diferentes canales, lo que crea oportunidades para una participación personalizada en tiempo real. | **Nutrición en tiempo real:** Al integrar los datos de actividad de [!DNL Eloqua], Real-Time CDP puede enviar correos electrónicos personalizados o déclencheur a los equipos de ventas cuando un contacto interactúa con contenido (como descargar un documento técnico o hacer clic en un vínculo de correo electrónico), lo que permite un seguimiento oportuno y mejores oportunidades de conversión. |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Lea las secciones siguientes para conocer la configuración de requisitos previos que debe completar antes de poder conectar su origen a Experience Platform.

### Configurar la aplicación para la autenticación

Siga los pasos a continuación para aprender a configurar su cuenta de [!DNL Eloqua] y conectarse a Experience Platform mediante autenticación básica.

Para empezar, inicie sesión en su instancia de [!DNL Eloqua] como administrador (o como usuario que tenga acceso para crear usuarios, grupos de seguridad y aplicaciones).

![El tablero de My Eloqua.](../../images/tutorials/create/eloqua/admin.png)

Vaya a **Configuración** > **Extensiones de plataforma** > **Desarrollador de App Cloud** > **Crear aplicación**. Proporcione detalles para la aplicación, como nombre, descripción, icono y la URL de devolución de llamada de OAuth. Seleccione **Guardar** cuando haya terminado.

![El panel Desarrollador de aplicaciones y el botón Crear aplicación en el panel de Eloqua.](../../images/tutorials/create/eloqua/create-app.png)

| Propiedad | Descripción |
| --- | --- |
| Nombre | Nombre de la aplicación. |
| Descripción | Breve descripción de la aplicación. |
| Icono | La URL del icono. |
| URL de devolución de llamada OAuth | Dirección URL a la cual se debe redirigir a los usuarios después de instalar la aplicación y autenticarse con [!DNL Eloqua]. |

![La ventana Crear aplicación en Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Con la aplicación creada, ve a [!DNL Authentication to Eloqua] y recupera **el ID de cliente** y **el secreto de cliente** de la aplicación recién creada. Estos valores se utilizarán más adelante al conectarse a Experience Platform.

![El ID de cliente y el secreto de cliente en Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

Los grupos de seguridad permiten a los administradores controlar qué niveles de acceso tienen los usuarios a los recursos, las funciones, las interfaces, etc. Para crear un grupo de seguridad, vaya a **Configuración** > **Usuarios**. A continuación, seleccione la ficha **Grupo** en el panel izquierdo y, a continuación, seleccione **Crear nuevo grupo de seguridad**.

![Panel de administración de usuarios en Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Utilice la ventana **[!DNL Security Group Overview]** para proporcionar un nombre y un acrónimo para el grupo de seguridad. Una vez creado, vaya a [!DNL Action Permissions], agregue el permiso de API [!DNL Consume] de la lista y seleccione **Guardar**.

![Ventana de información general del grupo de seguridad en Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![Ventana de selección para la API de consumo](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>La API [!DNL Consume] es un permiso obligatorio, pero puede agregar más permisos según el uso que haga de la aplicación.

Para introducir datos de campaña, vaya a la interfaz **Editar usuario** y agregue [!DNL Guided Campaigns] al grupo de seguridad seleccionado.

![Grupo de seguridad con campañas guiadas agregadas.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Si lo desea, puede crear un usuario adicional y agregarlo a un grupo de seguridad. Para ver los pasos detallados, lea la documentación de [!DNL Eloqua] sobre [crear un usuario](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) y [asignar un usuario a un grupo de seguridad](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes credenciales a fin de conectar [!DNL Eloqua] a Experience Platform.

| Credencial | Descripción |
| --- | --- |
| ID de cliente | El identificador expuesto públicamente que [!DNL Eloqua] usó para identificar su cuenta al autorizar a Experience Platform. |
| Secreto del cliente | La clave confidencial conocida sólo por la aplicación cliente y el servidor de autorización. Esta clave es necesaria junto con el ID de cliente para autenticar la cuenta. |
| Nombre de usuario | El nombre de usuario asociado con su cuenta de [!DNL Eloqua]. Se utiliza para verificar y autorizar su acceso. El nombre de usuario sigue el formato de `CompanyName\Username`. |
| Contraseña | La contraseña asociada a su cuenta de [!DNL Eloqua]. Junto con su nombre de usuario, otorga acceso a su entorno Eloqua. |
| Extremo base | El prefijo del URI base de autenticación de [!DNL Eloqua]. El extremo base no debe incluir `http://` ni `https://` al autenticarse. |

## Guía de asignación de [!DNL Eloqua]

>[!NOTE]
>
>Los siguientes son los campos delta que se utilizan internamente para la carga de datos incrementales:
>
>- **Contactos:** `C_DateModified`
>- **Cuentas:** `M_DateModified`
>- **Actividad:** `CreatedAt`
>- **Objetos personalizados:** `UpdatedAt`
>- **Campaña:** `updatedAt`

En las tablas siguientes se proporcionan asignaciones detalladas entre [!DNL Eloqua] campos de origen y sus campos de destino correspondientes del modelo de datos de experiencia (XDM) en Experience Platform. Cada fila describe la lógica de transformación, ya sea que el campo sea inmutable, y proporciona notas adicionales para ayudarle a comprender cómo se incorporarán y estructurarán los datos de [!DNL Eloqua] en Experience Platform.

### Cuentas

| Columna Source Eloqua | Ruta de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Este campo siempre se configura con el valor fijo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | El conector no puede detectar automáticamente su ID de instancia de CRM. Debe reemplazar manualmente `${CRM_INSTANCE_ID}` con su ID de instancia de CRM real, ya sea su ID de instancia de Salesforce o Dynamics. Durante la ingesta, si `M_SFDCAccountID` está presente, el conector generará la clave externa utilizando ese valor y anexará `\@CRM_INSTANCE_ID.Salesforce`. Si ese campo está vacío, el conector usará `M_MSCRMAccountID` y anexará `\@CRM_INSTANCE_ID.Dynamics` en su lugar. Si ambos campos están vacíos, este campo se establecerá en null. |

{style="table-layout:auto"}

### Actividades

| Columna Source Eloqua | Ruta de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Este campo siempre se configura con el valor fijo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | En función de ActivityType, se rellenará el valor de eventType de Experience Platform correspondiente. Para las actividades externas, no hay ningún eventType en Experience Platform. Puede modificar esta asignación para controlar más tipos. |
| `ActivityDate` | timestamp | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Campañas

| Columna Source Eloqua | Ruta de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Este campo siempre se configura con el valor fijo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Contactos

| Columna Source Eloqua | Ruta de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Este campo siempre se configura con el valor fijo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID` se reemplazará automáticamente por el conector. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Si la instancia [!DNL Eloqua] está sincronizada con Salesforce, mantenga esta asignación. De lo contrario, elimínelo. El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de Salesforce sincronizado. Esta misma asignación se aplica a personComponents y extSourceSystemAudit, por lo que mantenga ambos. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Si la instancia [!DNL Eloqua] está sincronizada con Dynamics, mantenga esta asignación. De lo contrario, elimínelo. El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de Dynamics sincronizado. Esta misma asignación se aplica a personComponents y extSourceSystemAudit, por lo que mantenga ambos. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Si la instancia [!DNL Eloqua] está sincronizada con Salesforce, mantenga esta asignación. De lo contrario, elimínelo. El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de Salesforce sincronizado. Esta misma asignación se aplica a personComponents y extSourceSystemAudit, por lo que mantenga ambos. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Si la instancia [!DNL Eloqua] está sincronizada con Dynamics, mantenga esta asignación. De lo contrario, elimínelo. El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de Dynamics sincronizado. Esta misma asignación se aplica a personComponents y extSourceSystemAudit, por lo que mantenga ambos. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de CRM sincronizado, ya sea el ID de instancia de Salesforce o el ID de instancia de Dynamics. Esta misma asignación se aplica tanto a b2b.accountKey como a personComponents.sourceAccountKey, por lo que debe mantener ambas. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | El conector no tiene una forma de determinar el CRM_INSTANCE_ID, por lo que debe reemplazar ${CRM_INSTANCE_ID} con su ID de instancia de CRM sincronizado, ya sea el ID de instancia de Salesforce o el ID de instancia de Dynamics. Esta misma asignación se aplica tanto a b2b.accountKey como a personComponents.sourceAccountKey, por lo que debe mantener ambas. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Referencia de asignación del tipo de actividad

| Tipo de actividad Eloqua | eventType de XDM |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | pasar tal cual |

{style="table-layout:auto"}

### Marcadores de posición variables

Las plantillas de asignación utilizan los siguientes marcadores de posición de variables que se sustituyen una vez que se ejecuta un flujo de datos:

| Marcador | Descripción | Uso |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | ID único de la instancia de origen de Eloqua | Se utiliza en claves de origen |
| `${CRM_INSTANCE_ID}` | ID único para el sistema CRM (Salesforce/Dynamics) | Se utiliza en claves externas |

## Conectar [!DNL Eloqua] a Experience Platform

Continúe configurando la conexión de origen de [!DNL Eloqua] en Experience Platform. Para obtener una guía paso a paso sobre cómo configurar la conexión a través de la interfaz de usuario, consulte el [tutorial aquí](../../tutorials/ui/create/marketing-automation/eloqua.md). Lea este tutorial para obtener información sobre cómo conectar su cuenta de [!DNL Eloqua], seleccionar datos, asignar campos, programar ingestas y supervisar flujos de datos.

