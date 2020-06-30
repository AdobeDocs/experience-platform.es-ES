---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introducción a Conectores de origen de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Información general sobre los conectores de origen

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen a varios proveedores de datos. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

Con [!DNL Experience Platform], puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas a partir de ellas para hacer más.

## Tipos de fuentes

Las fuentes de [!DNL Experience Platform] se agrupan en las siguientes categorías:

### Aplicaciones de Adobe

[!DNL Experience Platform] permite la ingesta de datos desde otras aplicaciones de Adobe, incluidos Adobe Analytics, Adobe Audience Manager y [!DNL Experience Platform Launch]. Consulte los siguientes documentos relacionados para obtener más información:

- [Descripción general del conector del Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creación de un conector de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Descripción general del conector de datos de Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creación de un conector de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creación de un conector de origen de Atributos del cliente en la interfaz de usuario](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidad

[!DNL Experience Platform] permite la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [!DNL Google AdWords](connectors/advertising/ads.md) conector

### Almacenamiento de nube

Las fuentes de almacenamiento de nube pueden incorporar sus propios datos [!DNL Platform] sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes mediante la interfaz de usuario. Consulte los siguientes documentos relacionados para obtener más información:

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) conector
- [!DNL Azure Blob and Amazon S3](connectors/cloud-storage/blob-s3.md) conector
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) conector
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) conector
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) conector
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) conector
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) conector
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) conector

### Administración de la relación con los clientes (CRM)

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. [!DNL Experience Platform] proporciona asistencia para la ingesta de datos CRM desde [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) conector
- [!DNL Salesforce](connectors/crm/salesforce.md) conector

### Éxito del cliente

[!DNL Experience Platform] proporciona soporte para la ingesta de datos desde una aplicación de éxito de cliente de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) conector
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) conector

### Database

[!DNL Experience Platform] permite la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [!DNL Amazon Redshift](connectors/databases/redshift.md) conector
- [!DNL Apache Hive on Azure HDInsights](connectors/databases/hive.md) conector
- [!DNL Apache Spark on Azure HDInsights](connectors/databases/spark.md) conector
- [!DNL Azure Data Explorer](connectors/databases/data-explorer.md) conector
- [!DNL Azure Synapse Analytics](connectors/databases/synapse-analytics.md) conector
- [!DNL Azure Table Storage](connectors/databases/ats.md) conector
- [!DNL Couchbase](connectors/databases/couchbase.md) conector
- [!DNL Google BigQuery](connectors/databases/bigquery.md) conector
- [!DNL GreenPlum](connectors/databases/greenplum.md) conector
- [!DNL HP Vertica](connectors/databases/hp-vertica.md) conector
- [!DNL IBM DB2](connectors/databases/ibm-db2.md) conector
- [!DNL MariaDB](connectors/databases/mariadb.md) conector
- [!DNL Microsoft SQL Server](connectors/databases/sql-server.md) conector
- [!DNL MySQL](connectors/databases/mysql.md) conector
- [!DNL Oracle](connectors/databases/oracle.md) conector
- [!DNL Phoenix](connectors/databases/phoenix.md) conector
- [!DNL PostgreSQL](connectors/databases/postgres.md) conector

### Automatización de mercadotecnia

[!DNL Experience Platform] proporciona asistencia para la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) conector

### Pagos

[!DNL Experience Platform] proporciona soporte para la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [!DNL PayPal](connectors/payments/paypal.md) conector

### Protocolos

[!DNL Experience Platform] proporciona soporte para la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [!DNL Generic OData](connectors/protocols/odata.md) conector

## Control de acceso para fuentes en la ingestión de datos

Los permisos para fuentes en la ingestión de datos se pueden administrar en Adobe Admin Console. Puede acceder a los permisos a través de la ficha *[!UICONTROL Permisos]* de un perfil de producto determinado. Desde el panel **[!UICONTROL Editar permisos]** , puede acceder a los permisos correspondientes a los orígenes a través de la entrada del menú de ingesta *[!UICONTROL de]* datos. El permiso Fuentes **[!UICONTROL de]** Vista concede acceso de solo lectura a los orígenes disponibles en la ficha *[!UICONTROL Catálogo]* y a los orígenes autenticados en la ficha *[!UICONTROL Examinar]* , mientras que el permiso **[!UICONTROL Administrar fuentes]** concede acceso total a los orígenes de lectura, creación, edición y desactivación.

La tabla siguiente describe cómo se comporta la interfaz de usuario en función de las distintas combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **[!UICONTROL Fuentes]** de Vista activadas | Conceda acceso de solo lectura a los orígenes de cada tipo de origen en la ficha *Catálogo* , así como a las fichas *Examinar*, *Cuentas* y *FlujoDeDatos* . |
| **[!UICONTROL Administrar fuentes]** en | Además de las funciones incluidas en las fuentes **[!UICONTROL de]** Vista, concede acceso a la opción Origen *[!UICONTROL de]* Connect en el *[!UICONTROL catálogo]* y a la opción *[!UICONTROL Seleccionar datos]* en la *[!UICONTROL exploración]*. **[!UICONTROL Administrar fuentes]** también permite habilitar o deshabilitar *[!UICONTROL flujos]* de datos y editar sus programaciones. |
| **[!UICONTROL Fuentes]** de Vista desactivadas y **[!UICONTROL administradas]** desactivadas | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles concedidos a través de Admin Console, incluidas estas cuatro fuentes, consulte la descripción general [del](../access-control/home.md)control de acceso.

## Términos y condiciones {#terms-and-conditions}

Al utilizar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), reconoce que la versión beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tendrá la obligación de mantener, corregir, actualizar, cambiar, modificar o de otro modo admitir la versión beta. Se le aconseja que tenga precaución y no dependa en modo alguno del funcionamiento o el rendimiento correctos de dicha versión beta o de los materiales que la acompañen. La versión beta se considera información confidencial de Adobe.

Se asigna a Adobe cualquier &quot;Comentario&quot; (información sobre la versión beta, incluidos, entre otros, los problemas o defectos que se produzcan al usar la versión beta, sugerencias, mejoras y recomendaciones) que proporcione a Adobe, incluidos todos los derechos, el título y el interés en dichos comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia técnica para compartir sus sugerencias o informe de un error, busque una mejora de la función.
