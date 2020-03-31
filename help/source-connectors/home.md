---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre los conectores de origen de la plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# Información general sobre los conectores de origen

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen a varios proveedores de datos. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

Con la plataforma de experiencia, puede centralizar los datos que recopila de fuentes diferentes y utilizar las perspectivas obtenidas con ella para hacer más.

## Tipos de fuentes

Las fuentes de la plataforma de experiencia se agrupan en las siguientes categorías:

### Aplicaciones de Adobe

La plataforma de experiencia permite la ingesta de datos desde otras aplicaciones de Adobe, incluidos Adobe Analytics, Adobe Audiencia Manager y Experience Platform Launch. Consulte los siguientes documentos relacionados para obtener más información:

- [Descripción general del conector del Administrador de Audiencias de Adobe](./ui/adobe-applications/audience-manager.md)
- [Creación de un conector de origen de Adobe Audiencia Manager en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Descripción general del conector de datos de Adobe Analytics](./ui/adobe-applications/analytics.md)
- [Creación de un conector de origen de Adobe Analytics en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### Almacenamiento de nube

Las fuentes de almacenamiento de nube pueden llevar sus propios datos a la plataforma sin necesidad de descargar, formatear o cargar. Cada paso del proceso se integra en el flujo de trabajo de fuentes mediante la interfaz de usuario. La compatibilidad con los proveedores de almacenamiento en la nube incluye Amazon S3, Azure Blob, servidores FTP y servidores SFTP. Consulte los siguientes documentos relacionados para obtener más información:

- [Creación de un conector de origen de Azure Blob o Amazon S3 en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [Creación de un conector de origen de Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [Creación de un conector de origen FTP o SFTP en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [Creación de un conector de origen de Almacenamiento de Google Cloud en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### Administración de la relación con los clientes (CRM)

Los sistemas CRM proporcionan datos que pueden ayudar a crear relaciones con los clientes, lo que a su vez crea lealtad e impulsa la retención de los clientes. La plataforma de experiencia ofrece compatibilidad con la ingesta de datos CRM desde Microsoft Dynamics 365 y Salesforce. Consulte los siguientes documentos relacionados para obtener más información:

- [Creación de un conector de origen de Microsoft Dynamics 365 o Salesforce en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [Creación de un conector de origen de PayPal en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### Éxito del cliente (CS)

La plataforma de experiencias ofrece compatibilidad para la ingesta de datos desde una aplicación de éxito de clientes de terceros. Consulte los siguientes documentos relacionados para obtener más información:

- [Creación de un conector de origen de Salesforce Service Cloud en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [Creación de un conector de origen ServiceNow en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### Database

La plataforma de experiencias ofrece compatibilidad para la ingesta de datos desde una base de datos de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Creación de un conector de origen AWS Redshift en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [Creación de un conector de origen de Azure Synapse Analytics en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [Creación de un conector de origen Google BigQuery en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [Creación de un conector de origen MariaDB en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [Creación de un conector de origen de Microsoft SQL Server en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [Creación de un conector de origen MySQL en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [Creación de un conector de origen PostgreSQL en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### Automatización de mercadotecnia

La plataforma de experiencia ofrece compatibilidad para la ingesta de datos desde un sistema de automatización de marketing de terceros. Consulte los siguientes documentos relacionados para obtener más información sobre los conectores de origen específicos:

- [Creación de un conector de origen HubSpot en la interfaz de usuario](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## Tutoriales de API

Puede crear conectores de origen mediante la API de servicio de flujo. Para obtener más información, consulte el documento [del tutorial API de](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)fuentes.

## Control de acceso para fuentes en la ingestión de datos

Los permisos para fuentes en la ingestión de datos se pueden administrar en Adobe Admin Console. Puede acceder a los permisos a través de la ficha *Permisos* de un perfil de producto determinado. Desde el panel **Editar permisos** , puede acceder a los permisos correspondientes a los orígenes a través de la entrada del menú de ingesta *de* datos. El permiso Fuentes **de** Vista concede acceso de solo lectura a los orígenes disponibles en la ficha *Catálogo* y a los orígenes autenticados en la ficha *Examinar* , mientras que el permiso **Administrar fuentes** concede acceso total a los orígenes de lectura, creación, edición y desactivación.

La tabla siguiente describe cómo se comporta la interfaz de usuario en función de las distintas combinaciones de estos permisos:

| Nivel de permiso | Descripción |
| ---- | ----|
| **Fuentes** de Vista activadas | Conceda acceso de solo lectura a los orígenes de cada tipo de origen en la ficha *Catálogo* , así como a las fichas *Examinar*, *Cuentas* y *FlujoDeDatos* . |
| **Administrar fuentes** en | Además de las funciones incluidas en las fuentes **de** Vista, concede acceso a la opción Origen *de* Connect en el *catálogo* y a la opción *Seleccionar datos* en la *exploración*. **Administrar fuentes** también permite habilitar o deshabilitar *flujos* de datos y editar sus programaciones. |
| **Fuentes** de Vista desactivadas y **administradas** desactivadas | Revocar todo el acceso a las fuentes. |

Para obtener más información sobre los permisos disponibles concedidos a través de la Consola de administración, incluidas estas cuatro fuentes, consulte la información general [del](../access-control/home.md)control de acceso.
