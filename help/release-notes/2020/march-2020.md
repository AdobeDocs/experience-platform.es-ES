---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2020'
description: Las notas de la versión de marzo de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notas de la versión;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 17%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 11 de marzo de 2020**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

* [Control de datos](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Control de datos {#governance}

[!DNL Experience Platform] permite que las empresas reúnan datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capten clientes. [!DNL Experience Platform] incluye una infraestructura de administración de datos de extremo a extremo para garantizar el uso correcto de los datos dentro de [!DNL Platform] y cuando se comparten entre sistemas.

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluidos la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para las acciones de marketing.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes funciones nuevas están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones de Beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de las directivas de uso de datos para [!DNL Real-Time Customer Data Platform] | Las políticas de uso de datos ahora se aplican en el flujo de trabajo de activación de datos a los destinos. El control de datos también se incrusta y aplica cuando se realizan cambios que afectan a activaciones existentes (como cambios en etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Linaje de datos para aplicación | Cuando se infringe una directiva de uso de datos en Real-Time CDP, la interfaz de usuario muestra una notificación que contiene información sobre el linaje de datos para ayudar al usuario a comprender por qué se violaron las directivas y qué puede hacer para resolver la infracción. |


**Problemas conocidos**

* Ninguna

Para obtener más información sobre la administración de datos, consulte la [descripción general de la administración de datos](../../data-governance/home.md).

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para introducir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de streaming, los conectores de Adobe nativos, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingesta parcial por lotes | La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral. Con esta capacidad, los usuarios pueden introducir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se agrupan por separado. Se añaden detalles a los lotes que no han superado la validación para explicar por qué no lo han hecho. Encontrará más información sobre la ingesta parcial por lotes en la [documentación sobre la ingesta parcial por lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* Ninguna

Para obtener más información acerca de la ingesta de datos en Platform, visite la [documentación de ingesta de datos](../../ingestion/home.md).


## Destinos {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera perfecta.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación para obtener más información:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento en nube | Real-Time CDP ahora puede entregar los segmentos como archivos de datos en las ubicaciones de almacenamiento en la nube de [!DNL Amazon S3] o SFTP. Esto permite enviar audiencias y sus atributos de perfil a los sistemas internos mediante archivos CSV o delimitados por tabuladores. |
| Destinos de Advertising | La tarjeta de destino [!DNL Google] ahora está dividida en tres tarjetas de destino, para las tres plataformas diferentes [!DNL Google] admitidas actualmente en Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Para obtener más información, visite la [descripción general de destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente individual parezca tener varias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de gráficos privados se ha mejorado para reducir la latencia de generación de gráficos de un proceso por lotes semanal a un gráfico diario actualizado, lo que permite a los clientes de [!DNL Identity Service] acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* Ninguna

Para obtener más información acerca de [!DNL Identity Service], consulte la [descripción general del servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector Adobe Audience Manager | Ya no se enviarán los datos de nivel de señal de Audience Manager. Tenga en cuenta que se seguirá incluyendo la pertenencia de segmentos a rasgos y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos renombrados | Los conjuntos de datos generados por el conector de Audience Manager tendrán nombres y descripciones actualizados. |
| Habilitar la opción [!DNL Profile] en Audience Manager | Se puede habilitar o deshabilitar [!DNL Profile] para promocionar el conjunto de datos a [!DNL Real-Time Customer Profile]. La opción de alternancia está habilitada de forma predeterminada. |
| Compatibilidad con IU para sistemas de almacenamiento en la nube | Nuevo conector de origen para [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario. |
| Compatibilidad con IU para sistemas CRM | Nuevo conector de origen para [!DNL HubSpot], [!DNL Salesforce Service Cloud] y [!DNL ServiceNow] en la interfaz de usuario. |
| Compatibilidad con IU para sistemas de base de datos | Nuevo conector de origen para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] y [!DNL MySQL] en la interfaz de usuario. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
