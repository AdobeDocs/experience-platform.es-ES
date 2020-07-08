---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 11 de marzo de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 5%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de marzo de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [Gobierno de datos](#governance)
* [Ingesta de datos](#ingestion)
* [Destinos](#destinations)
* [Servicio de identidad](#identity)
* [Fuentes](#sources)

## Gobierno de datos {#governance}

Experience Platform permite a las compañías reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capten mejor a los clientes. Experience Platform incluye una infraestructura de administración de datos end-to-end, que incluye el etiquetado y cumplimiento del uso de datos (DULE), para garantizar el uso adecuado de los datos dentro de Platform y cuando se comparten entre sistemas.

La Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro del Experience Platform en varios niveles, incluyendo la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso en los datos para las acciones de mercadotecnia.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes funciones nuevas están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de políticas de uso de datos para datos de clientes en tiempo real Platform | Las políticas de uso de datos ahora se aplican en el flujo de trabajo de activación de datos a destinos. La Administración de datos también se incrusta y se aplica cuando se realizan cambios que afectan a activaciones existentes (como cambios en etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Lineamiento de datos para la aplicación | Cuando se infringe una directiva de uso de datos en CDP en tiempo real, la interfaz de usuario muestra una notificación que contiene información de linaje de datos para ayudar al usuario a comprender por qué se violaron las políticas y qué pueden hacer para resolver la infracción. |


**Problemas conocidos**

* None

Para obtener más información acerca de la Administración de datos, consulte la información general [de la Administración de](../../data-governance/home.md)datos.

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Adobe Experience Platform Data Ingestion proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de flujo, los conectores nativos de Adobe, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingestión parcial por lotes | La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos sus datos correctos a Adobe Experience Platform mientras todos sus datos incorrectos se agrupan por lotes por separado. Se agregan detalles a los lotes que no han tenido éxito para explicar por qué no han superado la validación. Puede encontrar más información sobre la ingestión parcial de lotes en la documentación sobre la ingestión [parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* None

Para obtener más información sobre la ingesta de datos en Platform, visite la documentación [de la ingestión de](../../ingestion/home.md)datos.


## Destinos {#destinations}

En [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para dichos socios de una manera transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento de nube | Ahora, CDP en tiempo real de Adobe puede entregar sus segmentos como archivos de datos en sus ubicaciones de almacenamiento de nube de Amazon S3 o SFTP. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | La tarjeta de destino de Google ahora se divide en tres tarjetas de destino, para las tres plataformas de Google admitidas actualmente en el CDP en tiempo real de Adobe: Google Ads, Google Ad Manager, Google Display &amp; Video 360. |

Para obtener más información, visite la descripción general de [destinos](../../rtcdp/destinations/destinations-overview.md)

## Servicio de identidad {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de los clientes se fragmentan en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de su cliente y de su comportamiento al enlazar identidades entre dispositivos y sistemas, permitiéndole ofrecer experiencias digitales personales y impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de Private Graph se ha mejorado para reducir la latencia de generación de gráficos de un proceso semanal por lotes a un gráfico diario actualizado, lo que permite a los clientes de Identity Service acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* None

Para obtener más información acerca de Identity Service, consulte la información general [de](../../identity-service/home.md)Identity Service.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas del conector de Adobe Audience Manager | Ya no se enviarán datos de nivel de señal del Administrador de Audiencias. Tenga en cuenta que se seguirá incluyendo la pertenencia a segmentos para características y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos con nombre cambiado | Los conjuntos de datos generados por el conector Administrador de Audiencias tendrán nombres y descripciones actualizados. |
| Habilitar la alternancia de Perfiles en el Administrador de Audiencias | Se puede habilitar o deshabilitar la alternancia de Perfiles para promocionar conjuntos de datos al Perfil del cliente en tiempo real. El alternador se activará de forma predeterminada. |
| Compatibilidad con la interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas CRM | Nuevo conector de origen para HubSpot, Salesforce Service Cloud y ServiceNow en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas de bases de datos | Nuevo conector de origen para AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server y MySQL en la interfaz de usuario. |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.