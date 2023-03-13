---
title: Notas de la versión de Adobe Experience Platform de marzo de 2020
description: Notas de la versión de marzo de 2020 de Adobe Experience Platform.
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

[!DNL Experience Platform] permite a las empresas reunir datos de varios sistemas empresariales para permitir a los especialistas en marketing identificar, comprender y captar clientes. [!DNL Experience Platform] incluye una infraestructura de administración de datos de extremo a extremo para garantizar el uso adecuado de los datos dentro de [!DNL Platform] y cuando se comparten entre sistemas.

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para acciones de marketing.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes funciones nuevas están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de las políticas de uso de datos para [!DNL Real-Time Customer Data Platform] | Las políticas de uso de datos ahora se aplican en el flujo de trabajo de activación de datos a los destinos. El control de datos también se incrusta y aplica cuando se realizan cambios que afectan a activaciones existentes (como cambios en etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Linaje de datos para aplicación | Cuando se infringe una directiva de uso de datos en Real-Time CDP, la interfaz de usuario muestra una notificación que contiene información sobre el linaje de datos para ayudar al usuario a comprender por qué se violaron las directivas y qué puede hacer para resolver la infracción. |


**Problemas conocidos**

* Ninguna

Para obtener más información sobre la gobernanza de datos, consulte la [Resumen de gobernanza de datos](../../data-governance/home.md).

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para introducir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de streaming, los conectores de Adobe nativos, los socios de integración de datos o la IU de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingesta parcial por lotes | La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral. Con esta capacidad, los usuarios pueden introducir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se agrupan por separado. Se añaden detalles a los lotes que no han superado la validación para explicar por qué no lo han hecho. Puede encontrar más información sobre la ingesta parcial por lotes en la [documentación de ingesta parcial por lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre la ingesta de datos en Platform, visite la [Documentación de ingesta de datos](../../ingestion/home.md).


## Destinos {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma fluida.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación para obtener más información:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento en nube | Real-Time CDP ahora puede enviar los segmentos como archivos de datos a su [!DNL Amazon S3] o ubicaciones de almacenamiento en la nube SFTP. Esto permite enviar audiencias y sus atributos de perfil a los sistemas internos mediante archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | El [!DNL Google] la tarjeta de destino ahora se divide en tres tarjetas de destino, para las tres diferentes [!DNL Google] plataformas admitidas actualmente en Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Para obtener más información, visite la [información general sobre destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente individual parezca tener varias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de gráfico privado se ha mejorado para reducir la latencia de generación de gráficos de un proceso por lotes semanal a un gráfico diario actualizado, lo que permite [!DNL Identity Service] clientes de para acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* Ninguna

Para obtener más información acerca de [!DNL Identity Service], consulte la [Introducción al servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector Adobe Audience Manager | Ya no se enviarán los datos de nivel de señal de Audience Manager. Tenga en cuenta que se seguirá incluyendo la pertenencia de segmentos a rasgos y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos renombrados | Los conjuntos de datos generados por el conector de Audience Manager tendrán nombres y descripciones actualizados. |
| Activar [!DNL Profile] alternar en Audience Manager | [!DNL Profile] se puede activar o desactivar para promocionar el conjunto de datos a [!DNL Real-Time Customer Profile]. La opción de alternancia está habilitada de forma predeterminada. |
| Compatibilidad con IU para sistemas de almacenamiento en la nube | Nuevo conector de origen para [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario. |
| Compatibilidad con IU para sistemas CRM | Nuevo conector de origen para [!DNL HubSpot], [!DNL Salesforce Service Cloud], y [!DNL ServiceNow] en la interfaz de usuario. |
| Compatibilidad con IU para sistemas de base de datos | Nuevo conector de origen para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], y [!DNL MySQL] en la interfaz de usuario. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
