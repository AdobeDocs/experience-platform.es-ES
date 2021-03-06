---
audience: user
user-guide-title: Ayuda de conectores de origen de Adobe Experience Platform
breadcrumb-title: Guía de conectores de origen
user-guide-description: Ingeste datos de una variedad de fuentes o estructuras y etiquete y mejore los datos ingestados.
feature: Sources
source-git-commit: 6f7611b120046fffc1b7c15bd657d699f4b4a588
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 14%

---


# Fuentes {#sources}

- [Resumen de fuentes](home.md)
- Conectores de origen disponibles {#connectors}
   - aplicaciones de Adobe {#adobe-applications}
      - [Fuente de clasificaciones de Analytics](connectors/adobe-applications/classifications.md)
      - [Fuente de Analytics](connectors/adobe-applications/analytics.md)
      - [origen del Audience Manager](connectors/adobe-applications/audience-manager.md)
      - [Fuente de atributos del cliente](connectors/adobe-applications/customer-attributes.md)
      - [Fuente de la recopilación de datos](connectors/adobe-applications/data-collection.md)
      - Asignaciones de campos {#mapping}
         - [Asignaciones de campos de Analytics](connectors/adobe-applications/mapping/analytics.md)
         - [asignaciones de campos de Audience Manager](connectors/adobe-applications/mapping/audience-manager.md)
         - [Asignaciones de campos de destino](connectors/adobe-applications/mapping/target.md)
         - [asignaciones de campos de Marketo Engage](connectors/adobe-applications/mapping/marketo.md)
         - [Asignaciones de campos de Microsoft Dynamics](connectors/adobe-applications/mapping/dynamics.md)
         - [Asignaciones de campos de Salesforce](connectors/adobe-applications/mapping/salesforce.md)
      - Marketo {#marketo}
         - [Conector del Marketo Engage](connectors/adobe-applications/marketo/marketo.md)
         - [Guía de autenticación del Marketo Engage](connectors/adobe-applications/marketo/marketo-auth.md)
         - [Esquemas y áreas de nombres B2B](connectors/adobe-applications/marketo/marketo-namespaces.md)
   - Advertising {#advertising}
      - [Conector de Google AdWords](connectors/advertising/ads.md)
   - Analytics {#analytics}
      - [Conector de panel mixto](connectors/analytics/mixpanel.md)
   - Almacenamiento en la nube {#cloud-storage}
      - [Conector de Amazon Kinesis](connectors/cloud-storage/kinesis.md)
      - [Conector Amazon S3](connectors/cloud-storage/s3.md)
      - [Conector HDFS de Apache](connectors/cloud-storage/hdfs.md)
      - [Conector de Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md)
      - [Conector de Azure Blob](connectors/cloud-storage/blob.md)
      - [Conector de los centros de eventos de Azure](connectors/cloud-storage/eventhub.md)
      - [Conector de almacenamiento de archivos de Azure](connectors/cloud-storage/azure-file-storage.md)
      - [Zona de aterrizaje de datos](connectors/cloud-storage/data-landing-zone.md)
      - [Conector FTP](connectors/cloud-storage/ftp.md)
      - [Conector de almacenamiento de Google Cloud](connectors/cloud-storage/google-cloud-storage.md)
      - [Google PubSub](connectors/cloud-storage/google-pubsub.md)
      - [Almacenamiento de objetos de oracle](connectors/cloud-storage/oracle-object-storage.md)
      - [Conector SFTP](connectors/cloud-storage/sftp.md)
      - [Conector de Amazon S3 y Azure Blob](connectors/cloud-storage/blob-s3.md)
   - Consentimiento y preferencias {#consent}
      - [Integración de OneTrust](connectors/consent-and-preferences/onetrust.md)
   - CRM {#crm}
      - [Conector de Microsoft Dynamics](connectors/crm/ms-dynamics.md)
      - [Conector de Salesforce](connectors/crm/salesforce.md)
      - [Conector de Veeva CRM](connectors/crm/veeva.md)
      - [Conector Zoho CRM](connectors/crm/zoho.md)
   - Éxito del cliente {#customer-success}
      - [Conector de Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
      - [Conector ServiceNow](connectors/customer-success/servicenow.md)
      - [Conector de Zendesk](connectors/customer-success/zendesk.md)
   - Bases de datos {#databases}
      - [Conector Amazon Redshift](connectors/databases/redshift.md)
      - [Apache Hive en el conector de Azure HDInsights](connectors/databases/hive.md)
      - [Apache Spark en el conector de Azure HDInsights](connectors/databases/spark.md)
      - [Conector de Data Explorer de Azure](connectors/databases/data-explorer.md)
      - [Conector de azure synapse Analytics](connectors/databases/synapse-analytics.md)
      - [Conector de almacenamiento de tablas de Azure](connectors/databases/ats.md)
      - [Conector de la Couchbase](connectors/databases/couchbase.md)
      - [Conector BigQuery de Google](connectors/databases/bigquery.md)
      - [Conector GreenPlum](connectors/databases/greenplum.md)
      - [Conector HP Vertica](connectors/databases/hp-vertica.md)
      - [Conector DB2 de IBM](connectors/databases/ibm-db2.md)
      - [Conector MariaDB](connectors/databases/mariadb.md)
      - [Conector de Microsoft SQL Server](connectors/databases/sql-server.md)
      - [Conector MySQL](connectors/databases/mysql.md)
      - [Conector de oracle](connectors/databases/oracle.md)
      - [Conector Phoenix](connectors/databases/phoenix.md)
      - [Conector PostgreSQL](connectors/databases/postgres.md)
      - [Conector del Snowflake](connectors/databases/snowflake.md)
   - eCommerce {#ecommerce}
      - [Conector Shopify](connectors/ecommerce/shopify.md)
   - Sistema local {#local-system}
      - [Conector de carga de archivos locales](connectors/local-system/local-file-upload.md)
   - Automatización de marketing {#marketing-automation}
      - [Conector HubSpot](connectors/marketing-automation/hubspot.md)
      - [Conector Mailchimp](connectors/marketing-automation/mailchimp.md)
      - [Conector Eloqua del oracle](connectors/marketing-automation/oracle-eloqua.md)
      - [Marketing Cloud de Salesforce](connectors/marketing-automation/salesforce-marketing-cloud.md)
   - Pagos {#payments}
      - [Conector PayPal](connectors/payments/paypal.md)
      - [Conector cuadrado](connectors/payments/square.md)
   - Protocolos {#protocols}
      - [Conector OData genérico](connectors/protocols/odata.md)
      - [Conector de API de REST genérico](connectors/protocols/generic-rest.md)
   - Transmisión {#streaming}
      - [Conector de API HTTP](connectors/streaming/http.md)
- Tutoriales de API {#api-tutorials}
   - Creación de una conexión base {#create}
      - Publicidad {#advertising}
         - [Google AdWords](tutorials/api/create/advertising/ads.md)
      - Analytics {#analytics}
         - [Panel de mezcla](tutorials/api/create/analytics/mixpanel.md)
      - Almacenamiento en la nube {#cloud-storage}
         - [Amazon Kinesis](tutorials/api/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/api/create/cloud-storage/s3.md)
         - [HDFS de Apache](tutorials/api/create/cloud-storage/hdfs.md)
         - [Azure Blob](tutorials/api/create/cloud-storage/blob.md)
         - [Almacenamiento de Azure Data Lake Gen2](tutorials/api/create/cloud-storage/adls-gen2.md)
         - [Centros de eventos de Azure](tutorials/api/create/cloud-storage/eventhub.md)
         - [Almacenamiento de archivos de Azure](tutorials/api/create/cloud-storage/azure-file-storage.md)
         - [Zona de aterrizaje de datos](tutorials/api/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/api/create/cloud-storage/ftp.md)
         - [Almacenamiento en la nube de Google](tutorials/api/create/cloud-storage/google.md)
         - [Google PubSub](tutorials/api/create/cloud-storage/google-pubsub.md)
         - [Almacenamiento de objetos de oracle](tutorials/api/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/api/create/cloud-storage/sftp.md)
      - Consentimiento y preferencias {#consent}
         - [Integración de OneTrust](tutorials/api/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/api/create/crm/ms-dynamics.md)
         - [Salesforce](tutorials/api/create/crm/salesforce.md)
         - [Véeva CRM](tutorials/api/create/crm/veeva.md)
         - [Zoho CRM](tutorials/api/create/crm/zoho.md)
      - Éxito del cliente {#customer-success}
         - [Nube de servicio de Salesforce](tutorials/api/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/api/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/api/create/customer-success/zendesk.md)
      - Bases de datos {#databases}
         - [Amazon Redshift](tutorials/api/create/databases/redshift.md)
         - [Apache Hive en Azure HDInsights](tutorials/api/create/databases/hive.md)
         - [Apache Spark en Azure HDInsights](tutorials/api/create/databases/spark.md)
         - [Data Explorer de Azure](tutorials/api/create/databases/data-explorer.md)
         - [Azure Synapse Analytics](tutorials/api/create/databases/synapse-analytics.md)
         - [Almacenamiento de tablas de Azure](tutorials/api/create/databases/ats.md)
         - [Couchbase](tutorials/api/create/databases/couchbase.md)
         - [Google BigQuery](tutorials/api/create/databases/bigquery.md)
         - [GreenPlum](tutorials/api/create/databases/greenplum.md)
         - [HP Vertica](tutorials/api/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/api/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/api/create/databases/mariadb.md)
         - [MySQL](tutorials/api/create/databases/mysql.md)
         - [Oracle](tutorials/api/create/databases/oracle.md)
         - [Phoenix](tutorials/api/create/databases/phoenix.md)
         - [PostgreSQL](tutorials/api/create/databases/postgres.md)
         - [Snowflake](tutorials/api/create/databases/snowflake.md)
         - [SQL Server](tutorials/api/create/databases/sql-server.md)
      - comercio electrónico {#ecommerce}
         - [Shopify](tutorials/api/create/ecommerce/shopify.md)
      - Automatización de marketing {#marketing-automation}
         - [HubSpot](tutorials/api/create/marketing-automation/hubspot.md)
         - [Campaña MailChimp](tutorials/api/create/marketing-automation/mailchimp-campaign.md)
         - [Miembros de MailChimp](tutorials/api/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/api/create/marketing-automation/oracle-eloqua.md)
         - [Marketing Cloud de Salesforce](tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
      - Pagos {#payments}
         - [PayPal](tutorials/api/create/payments/paypal.md)
         - [Cuadrado](tutorials/api/create/payments/square.md)
      - Protocolos {#protocols}
         - [OData genérico](tutorials/api/create/protocols/odata.md)
         - [API de REST genérica](tutorials/api/create/protocols/generic-rest.md)
      - Transmisión {#streaming}
         - [API HTTP](tutorials/api/create/streaming/http.md)
   - Explorar datos {#explore}
      - [Explorar datos publicitarios](tutorials/api/explore/advertising.md)
      - [Explorar datos de almacenamiento en la nube](tutorials/api/explore/cloud-storage.md)
      - [Explorar datos CRM](tutorials/api/explore/crm.md)
      - [Explorar los datos de éxito de los clientes](tutorials/api/explore/customer-success.md)
      - [Explorar datos de base de datos](tutorials/api/explore/database-nosql.md)
      - [Explorar datos de comercio electrónico](tutorials/api/explore/ecommerce.md)
      - [Explorar datos de automatización de marketing](tutorials/api/explore/marketing-automation.md)
      - [Explorar datos de pago](tutorials/api/explore/payments.md)
      - [Explorar datos de protocolo](tutorials/api/explore/protocols.md)
      - [Explorar tablas de datos](tutorials/api/explore/tabular.md)
   - Recopilación de datos {#collect}
      - [Recopilación de datos publicitarios](tutorials/api/collect/advertising.md)
      - [Recopilar datos de almacenamiento en la nube](tutorials/api/collect/cloud-storage.md)
      - [Recopilar datos CRM](tutorials/api/collect/crm.md)
      - [Recopilar datos de éxito de clientes](tutorials/api/collect/customer-success.md)
      - [Recopilar datos de base de datos](tutorials/api/collect/database-nosql.md)
      - [Recopilar datos de comercio electrónico](tutorials/api/collect/ecommerce.md)
      - [Recopilación de datos de automatización de mercadotecnia](tutorials/api/collect/marketing-automation.md)
      - [Recopilar datos de pago](tutorials/api/collect/payments.md)
      - [Recopilación de datos de protocolo](tutorials/api/collect/protocols.md)
      - [Recopilación de datos de flujo continuo](tutorials/api/collect/streaming.md)
   - [Monitorizar flujos de datos](tutorials/api/monitor.md)
   - [Actualizar cuentas](tutorials/api/update.md)
   - [Actualizar flujos de datos](tutorials/api/update-dataflows.md)
   - [Eliminar cuentas](tutorials/api/delete.md)
   - [Eliminar flujos de datos](tutorials/api/delete-dataflows.md)
- Tutoriales de la interfaz de usuario {#ui-tutorials}
   - Crear una conexión de origen {#create}
      - aplicaciones de Adobe {#adobe-applications}
         - [Adobe Analytics (datos de grupos de informes)](tutorials/ui/create/adobe-applications/analytics.md)
         - [Adobe Analytics (datos de clasificaciones)](tutorials/ui/create/adobe-applications/classifications.md)
         - [Adobe Audience Manager](tutorials/ui/create/adobe-applications/audience-manager.md)
         - [Adobe Campaign Managed Services](tutorials/ui/create/adobe-applications/campaign.md)
         - [Atributos del cliente](tutorials/ui/create/adobe-applications/customer-attributes.md)
         - [Marketo Engage](tutorials/ui/create/adobe-applications/marketo.md)
      - Publicidad {#advertising}
         - [Google AdWords](tutorials/ui/create/advertising/ads.md)
      - Analytics {#analytics}
         - [Panel de mezcla](tutorials/ui/create/analytics/mixpanel.md)
      - Almacenamiento en la nube {#cloud-storage}
         - [Amazon Kinesis](tutorials/ui/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/ui/create/cloud-storage/s3.md)
         - [HDFS de Apache](tutorials/ui/create/cloud-storage/hdfs.md)
         - [Almacenamiento de Azure Data Lake Gen2](tutorials/ui/create/cloud-storage/adls-gen2.md)
         - [Azure Blob](tutorials/ui/create/cloud-storage/blob.md)
         - [Centros de eventos de Azure](tutorials/ui/create/cloud-storage/eventhub.md)
         - [Almacenamiento de archivos de Azure](tutorials/ui/create/cloud-storage/azure-file-storage.md)
         - [Zona de aterrizaje de datos](tutorials/ui/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/ui/create/cloud-storage/ftp.md)
         - [Almacenamiento en la nube de Google](tutorials/ui/create/cloud-storage/google-cloud-storage.md)
         - [Google PubSub](tutorials/ui/create/cloud-storage/google-pubsub.md)
         - [Almacenamiento de objetos de oracle](tutorials/ui/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/ui/create/cloud-storage/sftp.md)
         - [Amazon S3 y Blob](tutorials/ui/create/cloud-storage/blob-s3.md)
      - Consentimiento y preferencias {#consent}
         - [Integración de OneTrust](tutorials/ui/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/ui/create/crm/dynamics.md)
         - [Salesforce](tutorials/ui/create/crm/salesforce.md)
         - [Véeva CRM](tutorials/ui/create/crm/veeva.md)
         - [Zoho CRM](tutorials/ui/create/crm/zoho.md)
      - Éxito del cliente {#customer-success}
         - [Nube de servicio de Salesforce](tutorials/ui/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/ui/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/ui/create/customer-success/zendesk.md)
      - Bases de datos {#databases}
         - [Amazon Redshift](tutorials/ui/create/databases/redshift.md)
         - [Apache Hive en Azure HDInsights](tutorials/ui/create/databases/hive.md)
         - [Apache Spark en Azure HDInsights](tutorials/ui/create/databases/spark.md)
         - [Data Explorer de Azure](tutorials/ui/create/databases/data-explorer.md)
         - [azure synapse Analytics](tutorials/ui/create/databases/synapse-analytics.md)
         - [Almacenamiento de tablas de Azure](tutorials/ui/create/databases/ats.md)
         - [Couchbase](tutorials/ui/create/databases/couchbase.md)
         - [Google Big Query](tutorials/ui/create/databases/bigquery.md)
         - [GreenPlum](tutorials/ui/create/databases/greenplum.md)
         - [HP Vertica](tutorials/ui/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/ui/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/ui/create/databases/mariadb.md)
         - [Microsoft SQL Server](tutorials/ui/create/databases/sql-server.md)
         - [MySQL](tutorials/ui/create/databases/mysql.md)
         - [Oracle](tutorials/ui/create/databases/oracle.md)
         - [Phoenix](tutorials/ui/create/databases/phoenix.md)
         - [PostgreSQL](tutorials/ui/create/databases/postgres.md)
         - [Snowflake](tutorials/ui/create/databases/snowflake.md)
      - comercio electrónico {#ecommerce}
         - [Shopify](tutorials/ui/create/ecommerce/shopify.md)
      - Sistema local {#local-system}
         - [Carga de archivo local](tutorials/ui/create/local-system/local-file-upload.md)
      - Automatización de marketing {#marketing-automation}
         - [HubSpot](tutorials/ui/create/marketing-automation/hubspot.md)
         - [Campañas Mailchimp](tutorials/ui/create/marketing-automation/mailchimp-campaigns.md)
         - [Miembros de Mailchimp](tutorials/ui/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/ui/create/marketing-automation/oracle-eloqua.md)
         - [Marketing Cloud de Salesforce](tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
      - Pagos {#payments}
         - [PayPal](tutorials/ui/create/payments/paypal.md)
         - [Cuadrado](tutorials/ui/create/payments/square.md)
      - Protocolos {#protocols}
         - [OData genérico](tutorials/ui/create/protocols/odata.md)
      - Transmisión {#streaming}
         - [API HTTP](tutorials/ui/create/streaming/http.md)
   - Configuración de un flujo de datos {#dataflow}
      - [Flujo de datos de conexión publicitaria](tutorials/ui/dataflow/advertising.md)
      - [Flujo de datos de conexión de Analytics](tutorials/ui/dataflow/analytics.md)
      - [Flujo de datos de conexión de almacenamiento en la nube por lotes](tutorials/ui/dataflow/batch/cloud-storage.md)
      - [Flujo de datos de conexión de almacenamiento en la nube de transmisión](tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
      - [Flujo de datos de conexión de consentimiento y preferencias](tutorials/ui/dataflow/consent-and-preferences.md)
      - [Flujo de datos de conexión CRM](tutorials/ui/dataflow/crm.md)
      - [Flujo de datos de conexión de éxito del cliente](tutorials/ui/dataflow/customer-success.md)
      - [Flujo de datos de conexión de base de datos](tutorials/ui/dataflow/databases.md)
      - [Flujo de datos de conexión de comercio electrónico](tutorials/ui/dataflow/ecommerce.md)
      - [Flujo de datos de conexión de automatización de marketing](tutorials/ui/dataflow/marketing-automation.md)
      - [Flujo de datos de conexión de pago](tutorials/ui/dataflow/payments.md)
      - [Flujo de datos de conexión de protocolo](tutorials/ui/dataflow/protocols.md)
   - [Activar datos entrantes para rellenar perfiles de clientes](tutorials/ui/profile.md)
   - [Monitorizar flujos de datos por lotes](tutorials/ui/monitor.md)
   - [Monitorización de flujos de datos de flujo de transmisión](tutorials/ui/monitor-streaming.md)
   - [Actualizar cuentas](tutorials/ui/update.md)
   - [Actualizar flujos de datos](tutorials/ui/update-dataflows.md)
   - [Eliminar cuentas](tutorials/ui/delete-accounts.md)
   - [Eliminar flujos de datos](tutorials/ui/delete.md)
   - [Suscripción a las alertas de fuentes](tutorials/ui/alerts.md)
- SDK de fuentes {#sdk}
   - [Información general](sources-sdk/overview.md)
   - [Opciones de Configuration](sources-sdk/config/config.md)
   - [Configurar la especificación de autenticación](sources-sdk/config/authspec.md)
   - [Configuración de la especificación de origen](sources-sdk/config/sourcespec.md)
   - [Configuración de la especificación de exploración](sources-sdk/config/explorespec.md)
   - [Información general sobre la API del SDK de fuentes](sources-sdk/api/api-overview.md)
   - [Primeros pasos](sources-sdk/api/getting-started.md)
   - [Crear una especificación de conexión](sources-sdk/api/create.md)
   - [Actualizar una especificación de conexión](sources-sdk/api/update-connection-specs.md)
   - [Actualización de una especificación de flujo](sources-sdk/api/update-flow-specs.md)
   - [Enviar el origen](sources-sdk/api/submit.md)
   - [Documentar el origen en Adobe Experience Platform](sources-sdk/documentation/doc-overview.md)
   - [Utilice la interfaz web de GitHub para crear una página de documentación de fuentes](sources-sdk/documentation/github.md)
   - [Utilice un editor de texto en el entorno local para crear una página de documentación de fuentes](sources-sdk/documentation/text-editor.md)
   - [Plantilla de API de autoservicio de documentación](sources-sdk/documentation/template.md)
   - [Plantilla de interfaz de usuario de autoservicio de documentación](sources-sdk/documentation/ui-template.md)
- [Notificaciones de ejecución de flujo](notifications.md)
- [LISTA DE PERMITIDOS de direcciones IP](ip-address-allow-list.md)
- [Preguntas frecuentes](./troubleshooting.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/flow-service/)
- [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)
