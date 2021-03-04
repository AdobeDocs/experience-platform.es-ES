---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de Experience Platform 11 de marzo de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notas de la versión;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de marzo de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permite a las empresas unir datos de varios sistemas empresariales para permitir a los especialistas en marketing identificar, comprender y captar mejor a los clientes. [!DNL Experience Platform] incluye una infraestructura de administración de datos end-to-end para garantizar el uso adecuado de los datos dentro de  [!DNL Platform] y cuando se comparten entre sistemas.

Adobe Experience Platform [!DNL Data Governance] es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso a los datos para las acciones de marketing.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes nuevas funciones están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de políticas de uso de datos para [!DNL Real-time Customer Data Platform] | Las políticas de uso de datos ahora se refuerzan en el flujo de trabajo de activación de datos en los destinos. [!DNL Data Governance] también se incrusta y se aplica cuando se realizan cambios que afectan a las activaciones existentes (como cambios en las etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos y otros). |
| Línea de datos para la aplicación | Cuando se infringe una política de uso de datos en tiempo real de CDP, la interfaz de usuario muestra una notificación que contiene información sobre el linaje de datos para ayudar al usuario a comprender por qué se violaron las políticas y qué puede hacer para resolver la infracción. |


**Problemas conocidos**

* Ninguna

Para obtener más información sobre [!DNL Data Governance], consulte la [Información general sobre el control de datos](../../data-governance/home.md).

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para introducir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de transmisión, los conectores nativos de Adobe, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingesta parcial por lotes | La ingesta parcial de lotes es la capacidad de ingerir datos que contengan errores, hasta un umbral determinado. Con esta capacidad, los usuarios pueden introducir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se procesan por lotes por separado. Los detalles se agregan a los lotes en los que se ha producido un error para explicar por qué no pasaron la validación. Puede encontrar más información sobre la ingesta parcial de lotes en la [documentación de ingesta parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre la ingesta de datos en Platform, visite la [Documentación sobre la ingesta de datos](../../ingestion/home.md).


## Destinos {#destinations}

En la [Plataforma de datos del cliente en tiempo real](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a esos socios de una manera transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento en la nube | CDP en tiempo real ahora puede entregar sus segmentos como archivos de datos a sus [!DNL Amazon S3] ubicaciones de almacenamiento en la nube de SFTP o . Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | La tarjeta de destino [!DNL Google] ahora se divide en tres tarjetas de destino, para las tres plataformas [!DNL Google] diferentes que se admiten actualmente en CDP en tiempo real: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Pantalla y video 360. |

Para obtener más información, visite [información general sobre destinos](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de Private Graph se ha mejorado para reducir la latencia de generación de gráficos desde un proceso semanal por lotes a un gráfico diario actualizado, lo que permite a los clientes [!DNL Identity Service] acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre [!DNL Identity Service], consulte la [información general del servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurar, etiquetar y mejorar esos datos mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector de Adobe Audience Manager | Ya no se enviarán datos de nivel de señal de Audience Manager. Tenga en cuenta que se seguirá incluyendo la pertenencia a segmentos para características y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos con nombre cambiado | Los conjuntos de datos generados por el conector de Audience Manager tendrán nombres y descripciones actualizados. |
| Habilitar el conmutador [!DNL Profile] en Audience Manager | [!DNL Profile] se puede habilitar o deshabilitar la opción para promocionar el conjunto de datos a  [!DNL Real-time Customer Profile]. La opción de alternancia está activada de forma predeterminada. |
| Compatibilidad con la interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas CRM | Nuevo conector de origen para [!DNL HubSpot], [!DNL Salesforce Service Cloud] y [!DNL ServiceNow] en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas de bases de datos | Nuevo conector de origen para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] y [!DNL MySQL] en la interfaz de usuario. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).