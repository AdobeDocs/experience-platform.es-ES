---
keywords: Experience Platform;inicio;temas populares;conectores de origen;conector de origen;fuentes;fuentes de datos;fuente de datos;conexión de origen de datos
solution: Experience Platform
title: Información general sobre conectores de origen
topic-legacy: overview
description: Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 6ae0560607c1e5f80ddfe752e59850f438794351
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---

# Información general sobre conectores de origen

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen con varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas de ellas para hacer más.

## Tipos de fuentes

Las fuentes en Experience Platform se agrupan en las siguientes categorías:

### aplicaciones de Adobe {#adobe-applications}

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluidas Adobe Analytics y Adobe Audience Manager. Consulte los siguientes documentos relacionados para obtener más información:

- [Información general de la fuente de Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Resumen de la conexión de fuentes de datos de las clasificaciones de Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Crear una conexión de fuente de datos de clasificaciones de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/classifications.md)
- [Descripción general de la conexión de origen de datos del grupo de informes de Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Crear una conexión de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Resumen de la fuente de recopilación de datos de Adobe](connectors/adobe-applications/data-collection.md)
- [Creación de una conexión de origen de Atributos del cliente en la interfaz de usuario](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] información general de la fuente](connectors/adobe-applications/marketo/marketo.md)
- [Cree un [!DNL Marketo Engage] conexión de origen en la interfaz de usuario](./tutorials/ui/create/adobe-applications/marketo.md)

### Advertising {#advertising}

Experience Platform permite la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Google AdWords]](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform permite la ingesta de datos desde una plataforma de análisis de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)

### Almacenamiento en la nube {#cloud-storage}

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a Platform sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes mediante la interfaz de usuario. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Consentimiento y preferencias {#consent}

Experience Platform proporciona asistencia para la ingesta de datos desde una plataforma de administración de preferencias y consentimiento de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### Administración de la relación con los clientes (CRM) {#customer-relationship-management}

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. El Experience Platform es compatible con la ingesta de datos CRM desde [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Éxito del cliente {#customer-success}

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de cliente de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### Database {#database}

Experience Platform permite la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### eCommerce {#ecommerce}

Experience Platform permite la ingesta de datos desde un sistema de comercio electrónico de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Sistema local {#local-system}

Experience Platform permite la ingesta de datos desde el sistema local. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [Carga de archivo local](connectors/local-system/local-file-upload.md)

### Automatización de la mercadotecnia {#marketing-automation}

Experience Platform permite la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Pagos {#payments}

Experience Platform permite la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Transmisión {#streaming}

El Experience Platform es compatible con la ingesta de datos de fuentes de flujo continuo. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocolos {#protocols}

Experience Platform permite la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Control de acceso para fuentes en la ingesta de datos

Los permisos para los orígenes en la ingesta de datos se pueden administrar en Adobe Admin Console. Puede acceder a los permisos a través de la **[!UICONTROL Permisos]** en un perfil de producto determinado. En el **[!UICONTROL Editar permisos]** , puede acceder a los permisos pertenecientes a orígenes a través de la **[!UICONTROL ingesta de datos]** para abrir el Navegador. La variable **[!UICONTROL Ver fuentes]** el permiso concede acceso de solo lectura a las fuentes disponibles en la variable **[!UICONTROL Catálogo]** y fuentes autenticadas en la **[!UICONTROL Examinar]** mientras que la variable **[!UICONTROL Administrar fuentes]** concede acceso completo a las fuentes de lectura, creación, edición y desactivación.

La siguiente tabla describe cómo se comporta la interfaz de usuario en función de diferentes combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **[!UICONTROL Ver fuentes]** Activado | Conceda acceso de solo lectura a los orígenes de cada tipo de origen en la pestaña Catálogo, así como a las pestañas Examinar, Cuentas y Flujo de datos. |
| **[!UICONTROL Administrar fuentes]** Activado | Además de las funciones incluidas en **[!UICONTROL Ver fuentes]**, otorga acceso a **[!UICONTROL Conectar origen]** en **[!UICONTROL Catálogo]** y **[!UICONTROL Seleccionar datos]** en **[!UICONTROL Examinar]**. **[!UICONTROL Administrar fuentes]** también le permite habilitar o deshabilitar **[!UICONTROL Flujos de datos]** y editar sus programaciones. |
| **[!UICONTROL Ver fuentes]** Off y **[!UICONTROL Administrar fuentes]** Off | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles otorgados a través del Admin Console, incluidas las cuatro fuentes, consulte [información general sobre el control de acceso](../access-control/home.md).

## Términos y condiciones {#terms-and-conditions}

Al utilizar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), reconoce que se proporciona la versión beta ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tendrá obligación de mantener, corregir, actualizar, cambiar, modificar o de otro modo admitir la versión beta. Se le aconseja que tenga precaución y no dependa en modo alguno del funcionamiento o rendimiento correctos de la versión Beta y/o de los materiales que la acompañen. La versión beta se considera información confidencial del Adobe.

Cualquier &quot;Comentario&quot; (información sobre la versión beta que incluya, entre otros, los problemas o defectos que encuentre al usar la versión beta, sugerencias, mejoras y recomendaciones) que Usted proporcione a su Adobe, se asigna al Adobe, incluidos todos los derechos, el título y el interés en estos Comentarios.

Envíe Comentarios abiertos o cree un ticket de asistencia para compartir sus sugerencias o informar de un error, busque una mejora de las funciones.
