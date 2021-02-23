---
keywords: Experience Platform;inicio;temas populares;conectores de origen;conector de origen;orígenes;fuentes de datos;fuente de datos;conexión de origen de datos
solution: Experience Platform
title: Información general de los conectores de origen
topic: sobre validación
description: Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.
translation-type: tm+mt
source-git-commit: 0e4fda4abf5c02df81b74f15d2fbcafb68548070
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Información general sobre los conectores de origen

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de la plataforma. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar fácilmente las conexiones de origen a varios proveedores de datos. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas a partir de ellas para hacer más.

## Tipos de fuentes

Las fuentes del Experience Platform se agrupan en las siguientes categorías:

### Aplicaciones de Adobe

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluyendo Adobe Analytics, Adobe Audience Manager y [!DNL Experience Platform Launch]. Consulte los siguientes documentos relacionados para obtener más información:

- [Descripción general del conector de Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creación de una conexión de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Descripción general del conector de datos de clasificaciones de Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Creación de una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/classifications.md)
- [Descripción general del conector de datos de Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creación de una conexión de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creación de una conexión de origen de Atributos del cliente en la interfaz de usuario](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidad

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) conector

### Almacenamiento de nube

Las fuentes de almacenamiento de nube pueden llevar sus propios datos a la plataforma sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, Parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes mediante la interfaz de usuario. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Azure Data Lake Storage Gen2] conector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] conector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] conector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] conector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] conector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] conector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] conector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] conector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] conector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] conector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] conector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] conector](connectors/cloud-storage/sftp.md)

### Administración de la relación con los clientes (CRM)

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. Experience Platform proporciona soporte para la ingesta de datos CRM desde [!DNL Microsoft Dynamics 365] y [!DNL Salesforce]. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Microsoft Dynamics] conector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] conector](connectors/crm/salesforce.md)

### Éxito del cliente

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de cliente de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [[!DNL Salesforce Service Cloud] conector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] conector](connectors/customer-success/servicenow.md)

### Database

Experience Platform proporciona soporte para la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL Amazon Redshift] conector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] conector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] conector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] conector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] conector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] conector](connectors/databases/ats.md)
- [[!DNL Couchbase] conector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] conector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] conector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] conector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] conector](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] conector](connectors/databases/sql-server.md)
- [[!DNL MySQL] conector](connectors/databases/mysql.md)
- [[!DNL Oracle] conector](connectors/databases/oracle.md)
- [[!DNL Phoenix] conector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] conector](connectors/databases/postgres.md)

### eCommerce

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de comercio electrónico de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Automatización de mercadotecnia

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL HubSpot] conector](connectors/marketing-automation/hubspot.md)

### Pagos

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL PayPal] conector](connectors/payments/paypal.md)

### Protocolos

Experience Platform proporciona soporte para la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [[!DNL Generic OData] conector](connectors/protocols/odata.md)

## Control de acceso para fuentes en la ingestión de datos

Los permisos para fuentes en la ingestión de datos se pueden administrar dentro de Adobe Admin Console. Puede acceder a los permisos a través de la ficha **[!UICONTROL Permisos]** en un perfil de producto determinado. Desde el panel **[!UICONTROL Editar permisos]**, puede acceder a los permisos correspondientes a los orígenes a través de la entrada de menú **[!UICONTROL ingestión de datos]**. El permiso **[!UICONTROL Fuentes de Vista]** otorga acceso de sólo lectura a los orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y a los orígenes autenticados en la ficha **[!UICONTROL Examinar]**, mientras que el permiso **[!UICONTROL Administrar fuentes]** otorga acceso total a las fuentes de lectura, creación, edición y desactivación.

La tabla siguiente describe cómo se comporta la interfaz de usuario en función de las distintas combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **[!UICONTROL Vista]** de fuentesActivada | Conceda acceso de solo lectura a los orígenes en cada tipo de origen en la ficha Catálogo, así como en las fichas Examinar, Cuentas y Flujo de datos. |
| **[!UICONTROL Administrar]** fuentesActivado | Además de las funciones incluidas en **[!UICONTROL Fuentes de Vista]**, concede acceso a la opción **[!UICONTROL Origen de conexión]** en **[!UICONTROL Catálogo]** y a la opción **[!UICONTROL Seleccionar datos]** en **[!UICONTROL Examinar]**. **[!UICONTROL Administrar]** fuentes también le permite habilitar o deshabilitar  **** FlujosDeDatos y editar sus programaciones. |
| **[!UICONTROL Vista]** de fuentesDesactivar y  **[!UICONTROL administrar]** fuentesDesactivar | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles otorgados a través del Admin Console, incluidas las cuatro fuentes, consulte la [información general del control de acceso](../access-control/home.md).

## Términos y condiciones {#terms-and-conditions}

Al utilizar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), reconoce que la versión beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

El Adobe no estará obligado a mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo la versión beta. Se le aconseja que tenga precaución y no dependa en modo alguno del funcionamiento o el rendimiento correctos de dicha versión beta o de los materiales que la acompañen. La versión beta se considera información confidencial del Adobe.

Cualquier &quot;Comentario&quot; (información relacionada con la versión beta, incluso, entre otros, los problemas o defectos que se produzcan al usar la versión beta, sugerencias, mejoras y recomendaciones) que proporcione el Cliente a Adobe, se asigna al Adobe, incluidos todos los derechos, títulos e intereses en y a dichos Comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia técnica para compartir sus sugerencias o informe de un error, busque una mejora de la función.
