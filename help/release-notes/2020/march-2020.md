---
title: Notas de la versión de Adobe Experience Platform, marzo de 2020
description: Notas de la versión de marzo de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notas de la versión;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de marzo de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [Control de datos](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Control de datos {#governance}

[!DNL Experience Platform] permite a las empresas unir datos de varios sistemas empresariales para permitir a los especialistas en marketing identificar, comprender y captar mejor a los clientes. [!DNL Experience Platform] incluye una infraestructura de administración de datos end-to-end para garantizar el uso adecuado de los datos dentro de [!DNL Platform] y cuando se comparten entre sistemas.

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para las acciones de marketing.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes nuevas funciones están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de políticas de uso de datos para [!DNL Real-Time Customer Data Platform] | Las políticas de uso de datos ahora se refuerzan en el flujo de trabajo de activación de datos en los destinos. La administración de datos también se incrusta y se aplica cuando se realizan cambios que afectan a las activaciones existentes (como cambios en las etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Línea de datos para la aplicación | Cuando se infringe una política de uso de datos en Real-Time CDP, la interfaz de usuario muestra una notificación que contiene información sobre el linaje de datos para ayudar al usuario a comprender por qué se violaron las políticas y qué puede hacer para resolver la infracción. |


**Problemas conocidos**

* Ninguna

Para obtener más información sobre la administración de datos, consulte la [Información general sobre la administración de datos](../../data-governance/home.md).

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de transmisión, los conectores de Adobe nativos, los socios de integración de datos o la IU de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingesta parcial por lotes | La ingesta parcial de lotes es la capacidad de ingerir datos que contengan errores, hasta un umbral determinado. Con esta capacidad, los usuarios pueden ingerir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se procesan por lotes por separado. Los detalles se agregan a los lotes en los que se ha producido un error para explicar por qué no pasaron la validación. Puede encontrar más información sobre la ingesta parcial de lotes en la [documentación de ingesta parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre la ingesta de datos en Platform, visite [Documentación de ingesta de datos](../../ingestion/home.md).


## Destinos {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento en la nube | Real-Time CDP ahora puede entregar sus segmentos como archivos de datos a su [!DNL Amazon S3] o ubicaciones de almacenamiento en la nube SFTP. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | La variable [!DNL Google] la tarjeta de destino ahora se divide en tres tarjetas de destino, para las tres [!DNL Google] plataformas compatibles actualmente con Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Pantalla y vídeo 360. |

Para obtener más información, visite [información general sobre destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de Private Graph se ha mejorado para reducir la latencia de generación de gráficos desde un proceso semanal por lotes a un gráfico diario actualizado, lo que permite [!DNL Identity Service] para acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* Ninguna

Para obtener más información, consulte [!DNL Identity Service], consulte la [Información general del servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector Adobe Audience Manager | Ya no se enviarán datos de nivel de señal de Audience Manager. Tenga en cuenta que se seguirá incluyendo la pertenencia a segmentos para características y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos con nombre cambiado | Los conjuntos de datos generados por el conector de Audience Manager tendrán nombres y descripciones actualizados. |
| Habilitar [!DNL Profile] alternar en Audience Manager | [!DNL Profile] alternar puede habilitarse o deshabilitarse para promocionar el conjunto de datos a [!DNL Real-Time Customer Profile]. La opción de alternancia está activada de forma predeterminada. |
| Compatibilidad con la interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario de . |
| Compatibilidad con la interfaz de usuario para sistemas CRM | Nuevo conector de origen para [!DNL HubSpot], [!DNL Salesforce Service Cloud]y [!DNL ServiceNow] en la interfaz de usuario de . |
| Compatibilidad con la interfaz de usuario para sistemas de bases de datos | Nuevo conector de origen para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]y [!DNL MySQL] en la interfaz de usuario de . |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
