---
keywords: Experience Platform;inicio;temas populares;conectores de origen;conector de origen;fuentes;fuentes de datos;fuente de datos;conexión de fuente de datos
solution: Experience Platform
title: Información general sobre conectores Source
description: Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 8541af0e2c0a2f5709f1621877ca204b0d3d64bd
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 2%

---

# Información general sobre conectores Source

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se usa para recopilar y centralizar datos de clientes de distintos orígenes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen a varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas de él para hacer más.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Fuentes empresariales avanzadas {#advanced-enterprise-sources}

Las siguientes fuentes están disponibles solo para los clientes de [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Lote]{type=Informative}

## Fuentes creadas por Adobes y socios {#adobe-and-partner-built-sources}

Algunos de los conectores del catálogo de fuentes de Experience Platform se crean y mantienen mediante Adobe, mientras que otros se crean y mantienen mediante compañías asociadas con [Sources SDK](/help/sources/sources-sdk/overview.md). Una nota en la parte superior de la página de documentación para cada conector creado por el socio indica si el socio crea y mantiene una fuente. Por ejemplo, el [conector Amazon S3](/help/sources/connectors/cloud-storage/s3.md) se crea por Adobe, mientras que el [conector RainFocus](/help/sources/connectors/analytics/rainfocus.md) lo crea y mantiene el equipo RainFocus.

En el caso de los conectores creados y mantenidos por el socio, esto significa que es posible que el equipo del socio tenga que resolver los problemas con el conector (método de contacto proporcionado en la nota de la página de documentación). Para problemas con los conectores creados y mantenidos por el Adobe, póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente.

## Categorías de orígenes

Los orígenes de un Experience Platform se agrupan en las siguientes categorías:

### Aplicaciones de Adobe {#adobe-applications}

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluidas Adobe Analytics y Adobe Audience Manager. Consulte los siguientes documentos relacionados para obtener más información:

- [Resumen de origen de Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Resumen de fuentes de datos de clasificaciones Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/classifications.md)
- [Resumen de fuentes de datos del grupo de informes Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Crear una conexión de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Resumen de origen de Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Crear una conexión de origen de Adobe Campaign Managed Cloud Services en la interfaz de usuario](./tutorials/ui/create/adobe-applications/campaign.md)
- [Resumen de origen de Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Resumen de fuente de recopilación de datos de Adobe](connectors/adobe-applications/data-collection.md)
   - [Crear una conexión de origen de Atributos del cliente en la IU](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] información general de origen](connectors/adobe-applications/marketo/marketo.md)
   - [Crear una  [!DNL Marketo Engage] conexión de origen en la interfaz de usuario](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Crear una conexión de origen y un flujo de datos de  [!DNL Marketo Engage] para los datos de actividad personalizados](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [Google Ads](connectors/advertising/ads.md) [!BADGE Lote]{type=Informative}

### Analytics {#analytics}

Experience Platform es compatible con la ingesta de datos desde una plataforma de análisis de terceros. Lea los siguientes documentos relacionados para obtener más información:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Lote]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Transmisión]{type=Positive}

### Almacenamiento en la nube {#cloud-storage}

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes mediante la interfaz de usuario de. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Lote]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Lote]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Lote]{type=Informative}

### Consentimiento y preferencias {#consent}

El Experience Platform de proporciona asistencia para la ingesta de datos desde una plataforma de administración de preferencias y consentimiento de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Lote]{type=Informative}

### Administración de la relación con los clientes (CRM) {#customer-relationship-management}

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de clientes. El Experience Platform proporciona soporte para la ingesta de datos CRM de [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Lote]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Lote]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Lote]{type=Informative}

### Éxito del cliente {#customer-success}

El Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de clientes de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Lote]{type=Informative}

### Base de datos {#database}

El Experience Platform proporciona asistencia para la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Lote]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Lote]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Lote]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Lote]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Lote]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Lote]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Lote]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Lote]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Lote]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Lote]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Lote]{type=Informative}

### Partners de datos e identidad {#data-partner}

El Experience Platform proporciona asistencia para la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE Lote]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE Lote]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Lote]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de comercio electrónico de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Transmisión]{type=Positive}

### Sistema local {#local-system}

El Experience Platform proporciona asistencia para la ingesta de datos desde el sistema local. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [Carga de archivo local](connectors/local-system/local-file-upload.md)

### Automatización de marketing {#marketing-automation}

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Transmisión]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Lote]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Lote]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Lote]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Pagos {#payments}

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Lote]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Lote]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE Lote]{type=Informative}

### Streaming {#streaming}

El Experience Platform de proporciona asistencia para la ingesta de datos de fuentes de flujo continuo. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Transmisión]{type=Positive}

### Protocolos {#protocols}

El Experience Platform es compatible con la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Lote]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Lote]{type=Informative}

## Control de acceso para orígenes en ingesta de datos

Los permisos para las fuentes en la ingesta de datos se pueden administrar dentro de Adobe Admin Console. Puede obtener acceso a los permisos a través de la ficha **[!UICONTROL Permisos]** en un perfil de producto concreto. Desde el panel **[!UICONTROL Editar permisos]**, puede acceder a los permisos que pertenecen a las fuentes a través de la entrada de menú **[!UICONTROL ingesta de datos]**. El permiso **[!UICONTROL Ver fuentes]** concede acceso de solo lectura a las fuentes disponibles en la ficha **[!UICONTROL Catálogo]** y a las fuentes autenticadas en la ficha **[!UICONTROL Examinar]**, mientras que el permiso **[!UICONTROL Administrar fuentes]** concede acceso completo para leer, crear, editar y deshabilitar fuentes.

En la tabla siguiente se describe cómo se comporta la interfaz de usuario en función de diferentes combinaciones de estos permisos:

| Nivel de permisos | Descripción |
| ---- | ----|
| **[!UICONTROL Ver orígenes]** En | Conceda acceso de sólo lectura a los orígenes de cada tipo de origen en la ficha Catálogo, así como a las fichas Examinar, Cuentas y Flujo de datos. |
| **[!UICONTROL Administrar Fuentes]** En | Además de las funciones incluidas en **[!UICONTROL Ver fuentes]**, concede acceso a la opción **[!UICONTROL Conectar Source]** en el **[!UICONTROL catálogo]** y a la opción **[!UICONTROL Seleccionar datos]** en **[!UICONTROL Examinar]**. **[!UICONTROL Administrar fuentes]** también le permite habilitar o deshabilitar **[!UICONTROL Flujos de datos]** y editar sus programaciones. |
| **[!UICONTROL Ver fuentes]** desactivadas y **[!UICONTROL Administrar fuentes]** desactivadas | Revocar todo acceso a orígenes. |

Para obtener más información sobre los permisos disponibles otorgados mediante Permisos de Adobe, lea la [descripción general del control de acceso](../access-control/home.md).

### Control de acceso basado en atributos

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos.

Con el control de acceso basado en atributos, puede aplicar configuraciones de asignación a campos para los que tiene permisos. Además, no puede introducir datos en un conjunto de datos si no tiene acceso a todos los campos del conjunto de datos.

#### Compatibilidad con el control de acceso basado en atributos en orígenes

>[!TIP]
>
>El control de acceso basado en atributos funciona de la siguiente manera: **roles** se crean para categorizar los tipos de usuarios que interactúan con la instancia de Platform. **Las etiquetas** se han aplicado a **roles** para designar el acceso a ese rol dado. **Las etiquetas** también se aplican a recursos como campos de esquema y segmentos. Para que un usuario tenga acceso a ciertos campos y segmentos de esquema, debe agregarlos a *un rol con la misma etiqueta asignada al recurso consultado*. Para obtener más información, lea la [guía completa de control de acceso basado en atributos](../access-control/abac/end-to-end-guide.md).

- Aplique etiquetas a los campos de esquema para definir el acceso a campos de esquema específicos de su organización. Una vez establecido el acceso a campos de esquema específicos, los usuarios solo podrán crear asignaciones para los campos a los que tengan acceso.
- Los usuarios sin las funciones adecuadas no podrán crear ni actualizar flujos de datos con asignaciones que impliquen campos de esquema inaccesibles. Además, los usuarios no autorizados no pueden actualizar, eliminar, habilitar ni deshabilitar flujos de datos existentes con campos de esquema inaccesibles.
- Además, un flujo de datos debe tener exactamente el mismo ID y versión de esquema en su asignación, conjunto de datos de destino y conexión de destino.

Para obtener más información sobre el control de acceso basado en atributos, lea la [descripción general del control de acceso basado en atributos](../access-control/abac/overview.md).

## Términos y condiciones {#terms-and-conditions}

Al usar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), el Cliente reconoce por la presente que Beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

El Adobe no tendrá ninguna obligación de mantener, corregir, actualizar, cambiar, modificar o de otro modo apoyar a Beta. Se le aconseja utilizar Informativo y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dicho Beta y/o materiales de acompañamiento. Beta se considera información confidencial de Adobe.

Cualquier &quot;comentario&quot; (información sobre Beta, incluidos, entre otros, problemas o defectos que encuentre al utilizar Beta, sugerencias, mejoras y recomendaciones) proporcionado por el cliente al Adobe se asigna por la presente al Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia para compartir sus sugerencias o informar de un error, y busque una mejora de las funciones.
