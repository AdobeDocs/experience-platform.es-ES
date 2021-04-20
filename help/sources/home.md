---
keywords: Experience Platform;inicio;temas populares;conectores de origen;conector de origen;fuentes;fuentes de datos;fuente de datos;conexión de origen de datos
solution: Experience Platform
title: Información general sobre conectores de origen
topic-legacy: overview
description: Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Información general sobre conectores de origen

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen con varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas de ellas para hacer más.

## Tipos de fuentes

Las fuentes en Experience Platform se agrupan en las siguientes categorías:

### aplicaciones de Adobe

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluidas Adobe Analytics, Adobe Audience Manager y [!DNL Experience Platform Launch]. Consulte los siguientes documentos relacionados para obtener más información:

- [Información general sobre el conector de Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Resumen del conector de datos de las clasificaciones de Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Crear una conexión de fuente de datos de clasificaciones de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/classifications.md)
- [Información general del conector de datos de Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Crear una conexión de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creación de una conexión de origen de Atributos del cliente en la interfaz de usuario](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] información general del conector](connectors/adobe-applications/marketo/marketo.md)
- [Creación de una conexión de  [!DNL Marketo Engage] recursos en la interfaz de usuario](./tutorials/ui/create/adobe-applications/marketo.md)

### Publicidad

Experience Platform permite la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connector

### Almacenamiento en la nube

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a Platform sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes mediante la interfaz de usuario. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Azure Data Lake Storage Gen2] connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] connector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] connector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] connector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] connector](connectors/cloud-storage/sftp.md)

### Administración de la relación con los clientes (CRM)

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. Experience Platform proporciona soporte para la ingesta de datos CRM desde [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Microsoft Dynamics] connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connector](connectors/crm/salesforce.md)

### Éxito del cliente

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de cliente de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Salesforce Service Cloud] connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connector](connectors/customer-success/servicenow.md)

### Database

Experience Platform permite la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Amazon Redshift] connector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connector](connectors/databases/ats.md)
- [[!DNL Couchbase] connector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connector](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] connector](connectors/databases/mysql.md)
- [[!DNL Oracle] connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connector](connectors/databases/postgres.md)

### eCommerce

Experience Platform permite la ingesta de datos desde un sistema de comercio electrónico de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Automatización de la mercadotecnia

Experience Platform permite la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL HubSpot] connector](connectors/marketing-automation/hubspot.md)

### Pagos

Experience Platform permite la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL PayPal] connector](connectors/payments/paypal.md)

### Protocolos

Experience Platform permite la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre conectores de origen específicos:

- [[!DNL Generic OData] connector](connectors/protocols/odata.md)

## Control de acceso para fuentes en la ingesta de datos

Los permisos para los orígenes en la ingesta de datos se pueden administrar en Adobe Admin Console. Puede acceder a los permisos a través de la pestaña **[!UICONTROL Permissions]** en un perfil de producto determinado. Desde el panel **[!UICONTROL Edit Permissions]**, puede acceder a los permisos pertenecientes a los orígenes a través de la entrada de menú **[!UICONTROL data ingestion]**. El permiso **[!UICONTROL View Sources]** concede acceso de solo lectura a los orígenes disponibles en la pestaña **[!UICONTROL Catalog]** y a los orígenes autenticados en la pestaña **[!UICONTROL Browse]**, mientras que el permiso **[!UICONTROL Manage Sources]** concede acceso completo a los orígenes de lectura, creación, edición y desactivación.

La siguiente tabla describe cómo se comporta la interfaz de usuario en función de diferentes combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **[!UICONTROL View Sources]** Activado | Conceda acceso de solo lectura a los orígenes de cada tipo de origen en la pestaña Catálogo, así como a las pestañas Examinar, Cuentas y Flujo de datos. |
| **[!UICONTROL Manage Sources]** Activado | Además de las funciones incluidas en **[!UICONTROL View Sources]**, concede acceso a la opción **[!UICONTROL Connect Source]** en **[!UICONTROL Catalog]** y a la opción **[!UICONTROL Select Data]** en **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** también le permite activar o desactivar  **[!UICONTROL DataFlows]** y editar sus programaciones. |
| **[!UICONTROL View Sources]** Desactivado y  **[!UICONTROL Manage Sources]** desactivado | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles otorgados a través del Admin Console, incluidas las cuatro fuentes, consulte la [descripción general del control de acceso](../access-control/home.md).

## Términos y condiciones {#terms-and-conditions}

Al utilizar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), reconoce que la versión beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tendrá obligación de mantener, corregir, actualizar, cambiar, modificar o de otro modo admitir la versión beta. Se le aconseja que tenga precaución y no dependa en modo alguno del funcionamiento o rendimiento correctos de la versión Beta y/o de los materiales que la acompañen. La versión beta se considera información confidencial del Adobe.

Cualquier &quot;Comentario&quot; (información sobre la versión beta que incluya, entre otros, los problemas o defectos que encuentre al usar la versión beta, sugerencias, mejoras y recomendaciones) que Usted proporcione a su Adobe, se asigna al Adobe, incluidos todos los derechos, el título y el interés en estos Comentarios.

Envíe Comentarios abiertos o cree un ticket de asistencia para compartir sus sugerencias o informar de un error, busque una mejora de las funciones.
