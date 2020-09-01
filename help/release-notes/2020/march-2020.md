---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 11 de marzo de 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de marzo de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!Gobierno de datos DNL]](#governance)
* [[!Ingesta de datos DNL]](#ingestion)
* [[!Destinos DNL]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!Fuentes DNL]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permite a las compañías reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capten mejor a los clientes. [!DNL Experience Platform] incluye una infraestructura de administración de datos end-to-end para garantizar el uso adecuado de los datos dentro [!DNL Platform] y cuando se comparten entre sistemas.

Adobe Experience Platform [!DNL Data Governance] es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] varios niveles, incluyendo catalogación, linaje de datos, etiquetado de uso de datos, políticas de acceso a datos e controles de acceso en datos para acciones de mercadotecnia.

**Nuevas funciones**

>[!NOTE]
>
>Algunas de las siguientes funciones nuevas están actualmente en fase beta y no están disponibles para todos los usuarios. Las funciones beta están sujetas a cambios.

| Función | Descripción |
| ------- | ----------- |
| Aplicación automatizada de las políticas de uso de datos para [!DNL Real-time Customer Data Platform] | Las políticas de uso de datos ahora se aplican en el flujo de trabajo de activación de datos a destinos. [!DNL Data Governance] también se incrusta y aplica cuando se realizan cambios que afectan a activaciones existentes (como cambios en etiquetas de conjuntos de datos, políticas de combinación, definiciones de segmentos, etc.). |
| Lineamiento de datos para la aplicación | Cuando se infringe una directiva de uso de datos en CDP en tiempo real, la interfaz de usuario muestra una notificación que contiene información de linaje de datos para ayudar al usuario a comprender por qué se violaron las políticas y qué pueden hacer para resolver la infracción. |


**Problemas conocidos**

* None

Para obtener más información sobre [!DNL Data Governance], consulte la información general [sobre el Gobierno](../../data-governance/home.md)de datos.

## Ingesta de datos {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de flujo, los conectores de Adobe nativos, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Ingestión parcial por lotes | La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos sus datos correctos a Adobe Experience Platform mientras que todos sus datos incorrectos se agrupan por lotes por separado. Se agregan detalles a los lotes que no han tenido éxito para explicar por qué no han superado la validación. Puede encontrar más información sobre la ingestión parcial de lotes en la documentación sobre la ingestión [parcial de lotes](../../ingestion/batch-ingestion/partial.md). |

**Problemas conocidos**

* None

Para obtener más información sobre la ingesta de datos en la plataforma, visite la documentación [de la ingestión de](../../ingestion/home.md)datos.


## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| Destinos de almacenamiento de nube | Ahora, CDP en tiempo real de Adobe puede entregar sus segmentos como archivos de datos en sus ubicaciones de almacenamiento en la nube [!DNL Amazon S3] o SFTP. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores. |
| Destinos publicitarios | La tarjeta de destino ahora se divide en tres tarjetas de destino para las tres diferentes [!DNL Google] [!DNL Google] plataformas admitidas actualmente en Adobe Real-time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Para obtener más información, visite la descripción general de [destinos](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de los clientes se fragmentan en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, permitiéndole ofrecer experiencias digitales personales y impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Gráfico privado mejorado | La funcionalidad de Private Graph se ha mejorado para reducir la latencia de generación de gráficos desde un proceso semanal por lotes a un gráfico diario actualizado, lo que permite a [!DNL Identity Service] los clientes acceder a vínculos y gráficos de identidad más actualizados. |

**Problemas conocidos**

* None

Para obtener más información sobre [!DNL Identity Service], consulte la información general [del servicio](../../identity-service/home.md)de identidad.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Señales obsoletas para el conector Adobe Audience Manager | Ya no se enviarán datos de nivel de señal del Administrador de Audiencias. Tenga en cuenta que se seguirá incluyendo la pertenencia a segmentos para características y segmentos. Como resultado de este cambio, ya no se generarán conjuntos de datos entrantes. |
| Conjuntos de datos con nombre cambiado | Los conjuntos de datos generados por el conector Administrador de Audiencias tendrán nombres y descripciones actualizados. |
| Habilitar [!DNL Profile] alternancia en Administrador de Audiencias | [!DNL Profile] se puede habilitar o deshabilitar la opción de alternar para promocionar el conjunto de datos a [!DNL Real-time Customer Profile]. El alternador se activará de forma predeterminada. |
| Compatibilidad con la interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas CRM | Nuevo conector de origen para [!DNL HubSpot], [!DNL Salesforce Service Cloud]y [!DNL ServiceNow] en la interfaz de usuario. |
| Compatibilidad con la interfaz de usuario para sistemas de bases de datos | Nuevo conector de origen para [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]y [!DNL MySQL] en la interfaz de usuario. |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.