---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 11 de marzo de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: c2495b463d713f85ba621a7bf687c5959ec13adb

---


# Notas de la versión de Adobe Experience Platform

## Fecha de la versión: 11 de marzo de 2020

## Gobierno de datos

La plataforma de experiencia permite a las compañías reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capten mejor a los clientes. La plataforma de experiencia incluye una infraestructura de administración de datos end-to-end, que incluye el etiquetado y cumplimiento del uso de datos (DULE), para garantizar el uso adecuado de los datos dentro de la plataforma y cuando se comparten entre sistemas.

La Administración de datos de la plataforma de experiencia de Adobe es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de la plataforma de experiencias en varios niveles, incluyendo la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso en los datos para las acciones de marketing.

### Nuevas funciones

>[!NOTE] Algunas de las siguientes funciones nuevas están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de políticas de uso de datos para la plataforma de datos del cliente en tiempo real | Las políticas de uso de datos ahora se aplican en el flujo de trabajo de activación de datos a destinos. La Administración de datos también se incrusta y se aplica cuando se realizan cambios que afectan a activaciones existentes (como cambios en etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Lineamiento de datos para la aplicación | Cuando se infringe una directiva de uso de datos en CDP en tiempo real, la interfaz de usuario muestra una notificación que contiene información de linaje de datos para ayudar al usuario a comprender por qué se violaron las políticas y qué pueden hacer para resolver la infracción. |


### Problemas conocidos

* None

Para obtener más información acerca de la Administración de datos, consulte la información general [de la Administración de](../../data-governance/home.md)datos.

## Ingesta de datos

Adobe Experience Platform proporciona un completo conjunto de funciones para ingestar cualquier tipo y latencia de datos. La integración de datos de la plataforma de experiencia de Adobe proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de flujo, los conectores nativos de Adobe, los socios de integración de datos o la interfaz de usuario de la plataforma de experiencia de Adobe.

### Nuevas funciones

| Función | Descripción |
|------- | -----------|
| Ingestión parcial por lotes | La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos los datos correctos a Adobe Experience Platform, mientras que todos los datos incorrectos se agrupan por lotes por separado. Se agregan detalles a los lotes que no han tenido éxito para explicar por qué no han superado la validación. Puede encontrar más información sobre la ingestión parcial de lotes en la documentación sobre la ingestión [parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

### Problemas conocidos

* None

Para obtener más información sobre la ingesta de datos en la plataforma, visite la documentación [de la ingestión de](../../ingestion/home.md)datos.


## Destinos

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

### Nuevos destinos

Hay disponibles nuevos destinos en los que puede activar los datos de la plataforma Adobe Experience. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento de nube | Ahora, CDP en tiempo real de Adobe puede entregar sus segmentos como archivos de datos en sus ubicaciones de almacenamiento de nube de Amazon S3 o SFTP. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | La tarjeta de destino de Google ahora se divide en tres tarjetas de destino, para las tres plataformas de Google admitidas actualmente en el CDP en tiempo real de Adobe: Google Ads, Google Ad Manager, Google Display &amp; Video 360. |

Para obtener más información, visite la descripción general de [destinos](../../rtcdp/destinations/destinations-overview.md)

## Servicio de identidad

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de los clientes se fragmentan en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform Identity Service le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

### Nuevas funciones

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de Private Graph se ha mejorado para reducir la latencia de generación de gráficos de un proceso semanal por lotes a un gráfico diario actualizado, lo que permite a los clientes de Identity Service acceder a vínculos y gráficos de identidad más actualizados. |

### Problemas conocidos

* None

Para obtener más información acerca de Identity Service, consulte la información general [de](../../identity-service/home.md)Identity Service.

## Fuentes

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

### Nuevas funciones

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector del Administrador de Audiencias de Adobe | Ya no se enviarán datos de nivel de señal del Administrador de Audiencias. Tenga en cuenta que se seguirá incluyendo la pertenencia a segmentos para características y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos con nombre cambiado | Los conjuntos de datos generados por el conector Administrador de Audiencias tendrán nombres y descripciones actualizados. |
| Habilitar la alternancia de Perfiles en el Administrador de Audiencias | Se puede habilitar o deshabilitar la alternancia de Perfiles para promocionar conjuntos de datos al Perfil del cliente en tiempo real. El alternador se activará de forma predeterminada. |
| Compatibilidad con la interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas CRM | Nuevo conector de origen para HubSpot, Salesforce Service Cloud y ServiceNow en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas de bases de datos | Nuevo conector de origen para AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server y MySQL en la interfaz de usuario. |

### Problemas conocidos

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../source-connectors/home.md)las fuentes.