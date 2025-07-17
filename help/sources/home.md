---
keywords: Experience Platform;inicio;temas populares;conectores de origen;conector de origen;fuentes;fuentes de datos;fuente de datos;conexión de fuente de datos
solution: Experience Platform
title: Información general sobre conectores Source
description: Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 952fc2fac819c545304aca4505208fe59841097f
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 8%

---

# Información general sobre conectores Source

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se usa para recopilar y centralizar datos de clientes de distintos orígenes dentro de Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen a varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas de él para hacer más.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Fuentes creadas por Adobe y por socios {#adobe-and-partner-built-sources}

Algunos de los conectores del catálogo de fuentes de Experience Platform los crea y mantiene Adobe, mientras que otros los crean y mantienen empresas asociadas con [Sources SDK](/help/sources/sources-sdk/overview.md). Una nota en la parte superior de la página de documentación para cada conector creado por el socio indica si el socio crea y mantiene una fuente. Por ejemplo, el [conector Amazon S3](/help/sources/connectors/cloud-storage/s3.md) lo crea Adobe, mientras que el [conector RainFocus](/help/sources/connectors/analytics/rainfocus.md) lo crea y mantiene el equipo RainFocus.

En el caso de los conectores creados y mantenidos por el socio, esto significa que es posible que el equipo del socio tenga que resolver los problemas con el conector (método de contacto proporcionado en la nota de la página de documentación). Para problemas con los conectores creados y mantenidos por Adobe, póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente.

>[!ENDSHADEBOX]

## Catálogo de fuentes

Lea las secciones siguientes para obtener una lista de todas las fuentes disponibles en el catálogo de fuentes.

### Aplicaciones de Adobe {#adobe-applications}

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluidas Adobe Analytics y Adobe Audience Manager. Lea los siguientes documentos relacionados para obtener más información:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Datos de clasificaciones de Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/classifications.md)
- [Datos del grupo de informes de Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Crear una conexión de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Crear una conexión de origen de Adobe Campaign Managed Cloud Services en la interfaz de usuario](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Recopilación de datos de Adobe](connectors/adobe-applications/data-collection.md)
   - [Crear una conexión de origen de Atributos del cliente en la IU](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Crear una  [!DNL Marketo Engage] conexión de origen en la interfaz de usuario](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Crear una conexión de origen y un flujo de datos de  [!DNL Marketo Engage] para los datos de actividad personalizados](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Fuentes empresariales avanzadas {#advanced-enterprise-sources}

Las siguientes fuentes están disponibles solo para los clientes de [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

| Fuente | Categoría | Tipo de ingesta | Nube |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Almacenamiento en la nube | Streaming | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Base de datos | Lote | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Base de datos | Lote | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Almacenamiento en la nube | Streaming | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Base de datos | Lote | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Base de datos | Lote | Azure |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Almacenamiento en la nube | Streaming | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Base de datos | Streaming | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Base de datos | Lote | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

Puede utilizar las siguientes fuentes para introducir datos publicitarios en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [Google Ads](connectors/advertising/ads.md) | Lote | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

Puede utilizar las siguientes fuentes para introducir datos de análisis en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Lote | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Streaming | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Streaming | Azure |

{style="table-layout:auto"}

### Almacenamiento en la nube {#cloud-storage}

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Experience Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes mediante la interfaz de usuario de. Consulte los siguientes documentos relacionados para obtener más información:

Puede utilizar las siguientes fuentes para introducir datos de almacenamiento en la nube en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Lote | Azure |
| [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) | Lote | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Lote | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Lote | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Lote | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Lote | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Lote | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Lote | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Lote | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Lote | Azure |

{style="table-layout:auto"}

### Consentimiento y preferencias {#consent}

Puede utilizar las siguientes fuentes para introducir datos de consentimiento y preferencias en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Lote | Azure |

{style="table-layout:auto"}

### Administración de la relación con los clientes (CRM) {#customer-relationship-management}

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de clientes. Experience Platform proporciona soporte para la ingesta de datos CRM desde [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

Puede utilizar las siguientes fuentes para introducir datos CRM en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Lote | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Lote | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Lote | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Lote | Azure |

{style="table-layout:auto"}

### Éxito del cliente {#customer-success}

Puede utilizar las siguientes fuentes para introducir datos de éxito de los clientes en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Lote | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Lote | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Lote | Azure |

{style="table-layout:auto"}

### Base de datos {#database}

Experience Platform es compatible con la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

Puede utilizar las siguientes fuentes para introducir datos de la base de datos en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Lote | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Lote | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Lote | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Lote | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Lote | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Lote | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Lote | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Lote | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Lote | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Lote | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Lote | Azure |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Lote | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Lote | Azure |

{style="table-layout:auto"}

### Partners de datos e identidad {#data-partner}

Puede utilizar las siguientes fuentes para introducir datos y datos de socios de identidad en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Lote | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Lote | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Lote | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Lote | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Lote | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Lote | Azure |

{style="table-layout:auto"}

### comercio electrónico {#ecommerce}

Puede utilizar las siguientes fuentes para introducir datos de comercio electrónico en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Lote | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Lote | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Streaming | Azure |

{style="table-layout:auto"}

### Sistema local {#local-system}

Puede utilizar las siguientes fuentes para introducir datos del sistema local en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [Carga de archivo local](connectors/local-system/local-file-upload.md) | Lote | Azure |

{style="table-layout:auto"}

### Automatización de marketing {#marketing-automation}

Puede utilizar las siguientes fuentes para introducir datos de automatización de marketing en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Streaming | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Streaming | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Streaming | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Lote | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Lote | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Lote | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Lote | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Lote | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Lote | Azure, AWS |

{style="table-layout:auto"}

### Pagos {#payments}

Puede utilizar las siguientes fuentes para introducir datos de pagos en Experience Platform.

| Fuente | Tipo de ingesta | Nube |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Lote | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Lote | Azure |

{style="table-layout:auto"}

### Streaming {#streaming}

Puede utilizar las siguientes fuentes para transmitir datos a Experience Platform.

| Fuente | Tipo de ingesta | Compatibilidad con Cloud |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Streaming | Azure, AWS |

{style="table-layout:auto"}

### Protocolos {#protocols}

Puede utilizar las siguientes fuentes para introducir datos de protocolo en Experience Platform.

| Fuente | Tipo de ingesta | Compatibilidad con Cloud |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Lote | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Lote | Azure |

{style="table-layout:auto"}

## Control de acceso para orígenes en ingesta de datos

Los permisos para las fuentes en la ingesta de datos se pueden administrar dentro de Adobe Admin Console. Puede obtener acceso a los permisos a través de la ficha **[!UICONTROL Permisos]** en un perfil de producto concreto. Desde el panel **[!UICONTROL Editar permisos]**, puede acceder a los permisos que pertenecen a las fuentes a través de la entrada de menú **[!UICONTROL ingesta de datos]**. El permiso **[!UICONTROL Ver fuentes]** concede acceso de solo lectura a las fuentes disponibles en la ficha **[!UICONTROL Catálogo]** y a las fuentes autenticadas en la ficha **[!UICONTROL Examinar]**, mientras que el permiso **[!UICONTROL Administrar fuentes]** concede acceso completo para leer, crear, editar y deshabilitar fuentes.

En la tabla siguiente se describe cómo se comporta la interfaz de usuario en función de diferentes combinaciones de estos permisos:

| Nivel de permisos | Descripción |
| ---- | ----|
| **[!UICONTROL Ver orígenes]** En | Conceda acceso de sólo lectura a los orígenes de cada tipo de origen en la ficha Catálogo, así como a las fichas Examinar, Cuentas y Flujo de datos. |
| **[!UICONTROL Administrar Fuentes]** En | Además de las funciones incluidas en **[!UICONTROL Ver fuentes]**, concede acceso a la opción **[!UICONTROL Conectar Source]** en el **[!UICONTROL catálogo]** y a la opción **[!UICONTROL Seleccionar datos]** en **[!UICONTROL Examinar]**. **[!UICONTROL Administrar fuentes]** también le permite habilitar o deshabilitar **[!UICONTROL Flujos de datos]** y editar sus programaciones. |
| **[!UICONTROL Ver fuentes]** desactivadas y **[!UICONTROL Administrar fuentes]** desactivadas | Revocar todo acceso a orígenes. |

Para obtener más información acerca de los permisos disponibles otorgados mediante Permisos de Adobe, lea la [descripción general del control de acceso](../access-control/home.md).

### Control de acceso basado en atributos

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos.

Con el control de acceso basado en atributos, puede aplicar configuraciones de asignación a campos para los que tiene permisos. Además, no puede introducir datos en un conjunto de datos si no tiene acceso a todos los campos del conjunto de datos.

#### Compatibilidad con el control de acceso basado en atributos en las fuentes

>[!TIP]
>
>El control de acceso basado en atributos funciona de la siguiente manera: **roles** se crean para categorizar los tipos de usuarios que interactúan con la instancia de Experience Platform. **Las etiquetas** se han aplicado a **roles** para designar el acceso a ese rol dado. **Las etiquetas** también se aplican a recursos como campos de esquema y segmentos. Para que un usuario tenga acceso a ciertos campos y segmentos de esquema, debe agregarlos a *un rol con la misma etiqueta asignada al recurso consultado*. Para obtener más información, lea la [guía completa de control de acceso basado en atributos](../access-control/abac/end-to-end-guide.md).

- Aplique etiquetas a los campos de esquema para definir el acceso a campos de esquema específicos de su organización. Una vez establecido el acceso a campos de esquema específicos, los usuarios solo podrán crear asignaciones para los campos a los que tengan acceso.
- Los usuarios sin las funciones adecuadas no podrán crear ni actualizar flujos de datos con asignaciones que impliquen campos de esquema inaccesibles. Además, los usuarios no autorizados no pueden actualizar, eliminar, habilitar ni deshabilitar flujos de datos existentes con campos de esquema inaccesibles.
- Además, un flujo de datos debe tener exactamente el mismo ID y versión de esquema en su asignación, conjunto de datos de destino y conexión de destino.

Para obtener más información sobre el control de acceso basado en atributos, lea la [descripción general del control de acceso basado en atributos](../access-control/abac/overview.md).

## Términos y condiciones {#terms-and-conditions}

Al usar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), el Cliente reconoce por la presente que Beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Beta. Se le aconseja utilizar Informativo y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dicho Beta y/o materiales de acompañamiento. Beta se considera información confidencial de Adobe.

Cualquier &quot;comentario&quot; (información sobre Beta, incluidos, entre otros, problemas o defectos que encuentre al utilizar Beta, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia para compartir sus sugerencias o informar de un error, y busque una mejora de las funciones.
