---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introducción a Conectores de origen de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---


# Información general sobre los conectores de origen

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen a varios proveedores de datos. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

Con Experience Platform, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas a partir de ellas para hacer más.

## Tipos de fuentes

Las fuentes del Experience Platform se agrupan en las siguientes categorías:

### Aplicaciones de Adobe

Experience Platform permite la ingesta de datos desde otras aplicaciones de Adobe, incluidos Adobe Analytics, Adobe Audience Manager y Experience Platform Launch. Consulte los siguientes documentos relacionados para obtener más información:

- [Descripción general del conector del Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creación de un conector de origen de Adobe Audience Manager en la interfaz de usuario](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Descripción general del conector de datos de Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creación de un conector de origen de Adobe Analytics en la interfaz de usuario](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creación de un conector de origen de Atributos del cliente en la interfaz de usuario](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidad

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de publicidad de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Conector de Google AdWords](connectors/advertising/ads.md)

### Almacenamiento de nube

Las fuentes de almacenamiento de nube pueden llevar sus propios datos a Platform sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes mediante la interfaz de usuario. Consulte los siguientes documentos relacionados para obtener más información:

- [Conector Gen2 de Azure Data Lake Almacenamiento](connectors/cloud-storage/adls-gen2.md)
- [Conector Azure Blob y Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Conector de Amazon Kinesis](connectors/cloud-storage/kinesis.md)
- [Conector HDFS de Apache](connectors/cloud-storage/hdfs.md)
- [Conector de los centros de Evento de Azure](connectors/cloud-storage/eventhub.md)
- [Conector de Almacenamiento de archivos de Azure](connectors/cloud-storage/azure-file-storage.md)
- [Conector FTP y SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Conector de Almacenamiento de Google Cloud](connectors/cloud-storage/google-cloud-storage.md)

### Administración de la relación con los clientes (CRM)

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. Experience Platform proporciona asistencia para la ingesta de datos CRM desde Microsoft Dynamics 365 y Salesforce. Consulte los siguientes documentos relacionados para obtener más información:

- [Conector de Microsoft Dynamics](connectors/crm/ms-dynamics.md)
- [Conector de Salesforce](connectors/crm/salesforce.md)

### Éxito del cliente

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de cliente de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [Conector de Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Conector ServiceNow](connectors/customer-success/servicenow.md)

### Database

Experience Platform proporciona soporte para la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Conector Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive en el conector Azure HDInsights](connectors/databases/hive.md)
- [Apache Spark en el conector HDInsights de Azure](connectors/databases/spark.md)
- [Conector del Explorador de datos de Azure](connectors/databases/data-explorer.md)
- [Conector de Analytics de sincronización de Azure](connectors/databases/synapse-analytics.md)
- [Conector de Almacenamiento de tabla de Azure](connectors/databases/ats.md)
- [Conector de la base de acoplamiento](connectors/databases/couchbase.md)
- [Conector Google BigQuery](connectors/databases/bigquery.md)
- [Conector GreenPlum](connectors/databases/greenplum.md)
- [Conector HP Vertica](connectors/databases/hp-vertica.md)
- [Conector IBM DB2](connectors/databases/ibm-db2.md)
- [Conector MariaDB](connectors/databases/mariadb.md)
- [Conector de Microsoft SQL Server](connectors/databases/sql-server.md)
- [Conector MySQL](connectors/databases/mysql.md)
- [Conector Oracle](connectors/databases/oracle.md)
- [Conector Phoenix](connectors/databases/phoenix.md)
- [Conector PostgreSQL](connectors/databases/postgres.md)

### Automatización de mercadotecnia

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Conector HubSpot](connectors/marketing-automation/hubspot.md)

### Pagos

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de pagos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Conector PayPal](connectors/payments/paypal.md)

### Protocolos

Experience Platform proporciona soporte para la ingesta de datos desde un sistema de protocolos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Conector OData genérico](connectors/protocols/odata.md)

## Control de acceso para fuentes en la ingestión de datos

Los permisos para fuentes en la ingestión de datos se pueden administrar en Adobe Admin Console. Puede acceder a los permisos a través de la ficha *Permisos* de un perfil de producto determinado. Desde el panel **Editar permisos** , puede acceder a los permisos correspondientes a los orígenes a través de la entrada del menú de ingesta *de* datos. El permiso Fuentes **de** Vista concede acceso de solo lectura a los orígenes disponibles en la ficha *Catálogo* y a los orígenes autenticados en la ficha *Examinar* , mientras que el permiso **Administrar fuentes** concede acceso total a los orígenes de lectura, creación, edición y desactivación.

La tabla siguiente describe cómo se comporta la interfaz de usuario en función de las distintas combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **Fuentes** de Vista activadas | Conceda acceso de solo lectura a los orígenes de cada tipo de origen en la ficha *Catálogo* , así como a las fichas *Examinar*, *Cuentas* y *FlujoDeDatos* . |
| **Administrar fuentes** en | Además de las funciones incluidas en las fuentes **de** Vista, concede acceso a la opción Origen *de* Connect en el *catálogo* y a la opción *Seleccionar datos* en la *exploración*. **Administrar fuentes** también permite habilitar o deshabilitar *flujos* de datos y editar sus programaciones. |
| **Fuentes** de Vista desactivadas y **administradas** desactivadas | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles concedidos a través de Admin Console, incluidas estas cuatro fuentes, consulte la descripción general [del](../access-control/home.md)control de acceso.

## Términos y condiciones {#terms-and-conditions}

Al utilizar cualquiera de las fuentes etiquetadas como beta (&quot;Beta&quot;), reconoce que la versión beta se proporciona ***&quot;tal cual&quot; sin garantía de ningún tipo***.

Adobe no tendrá la obligación de mantener, corregir, actualizar, cambiar, modificar o de otro modo admitir la versión beta. Se le aconseja que tenga precaución y no dependa en modo alguno del funcionamiento o el rendimiento correctos de dicha versión beta o de los materiales que la acompañen. La versión beta se considera información confidencial de Adobe.

Se asigna a Adobe cualquier &quot;Comentario&quot; (información sobre la versión beta, incluidos, entre otros, los problemas o defectos que se produzcan al usar la versión beta, sugerencias, mejoras y recomendaciones) que proporcione a Adobe, incluidos todos los derechos, el título y el interés en dichos comentarios.

Envíe comentarios abiertos o cree un ticket de asistencia técnica para compartir sus sugerencias o informe de un error, busque una mejora de la función.
