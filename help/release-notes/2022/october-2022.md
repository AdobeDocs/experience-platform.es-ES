---
title: Notas de la versión de Adobe Experience Platform, octubre de 2022
description: Notas de la versión de octubre de 2022 para Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: cd99ccb7b026565814dd6f268b2a92dda34bc7f0
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 3%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de octubre de 2022**

- [Claves gestionadas por el cliente](#cmk)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Notas de la versión de Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Claves gestionadas por el cliente {#cmk}](#customer-managed-keys-cmk)
   - [Recopilación de datos {#data-collection}](#data-collection-data-collection)
   - [\[!DNL Destinations\] {#destinations}](#dnl-destinations-destinations)
   - [Modelo de datos de experiencia (XDM) {#xdm}](#experience-data-model-xdm-xdm)
   - [Servicio de consultas {#query-service}](#query-service-query-service)
   - [Fuentes {#sources}](#sources-sources)

## Claves gestionadas por el cliente {#cmk}

Todos los datos almacenados en Adobe Experience Platform se cifran en reposo utilizando claves a nivel de sistema. Si utiliza una aplicación creada sobre Platform, ahora puede optar por utilizar sus propias claves de cifrado, lo que le otorga un bueno control sobre la seguridad de los datos.

Consulte la descripción general sobre [claves administradas por el cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obtener más información sobre la función.

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de datos confidenciales para conjuntos de datos | Los conjuntos de datos ahora aprovechan varias tecnologías de plataforma para manejar adecuadamente los datos confidenciales según se aplican en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Porability and Accounability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../edge/datastreams/overview.md#sensitive) para obtener más información. |
| [!DNL Splunk] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Splunk] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Splunk] información general de la extensión](../../tags/extensions/server/splunk/overview.md) para obtener más información. |
| [!DNL Zendesk] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Zendesk] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Zendesk] información general de la extensión](../../tags/extensions/server/zendesk/overview.md) para obtener más información. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Exportaciones de conjuntos de datos (Beta) | La variable [Exportación de conjuntos de datos: funcionalidad beta](/help/destinations/ui/export-datasets.md) permite exportar datos de primera generación (tal y como se define en la variable [Descripción del producto de Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) desde Adobe Experience Platform a sus propios sistemas de cliente externos, a través de la interfaz de usuario de destinos. Esto le permite sacar datos del Experience Platform con un flujo de trabajo sin código/de bajo código a seis destinos de almacenamiento en la nube (enumerados en la tabla siguiente) para casos de uso analíticos y de cumplimiento. |
| (Beta) Funciones mejoradas de exportación de archivos | Ahora puede beneficiarse de la funcionalidad de personalización mejorada al exportar archivos fuera del Experience Platform: <br><ul><li>Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados mediante la variable [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Posibilidad de personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Esta funcionalidad es compatible con las seis nuevas tarjetas de almacenamiento de nube beta que se enumeran en la siguiente tabla. |

{style="table-layout:auto"}

**Destinos nuevos o actualizados** {#new-or-updated-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line es una popular plataforma de comunicación que conecta personas, servicios e información y que ha pasado de ser una aplicación de chat a ser un centro de actividades de entretenimiento, sociales y diarias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 es una plataforma de aplicaciones empresariales basada en la nube que combina Enterprise Resource Planning (ERP) y Customer Relationship Management (CRM) junto con aplicaciones de productividad y herramientas de IA para ofrecer operaciones integrales más fluidas y controladas, un mejor potencial de crecimiento y costos reducidos. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | La variable [!DNL (Beta) Adobe Commerce] el conector de destino le permite seleccionar uno o varios segmentos de Real-Time CDP para activarlos en su [!DNL Adobe Commerce] para ofrecer una experiencia personalizada dinámica para sus compradores. Within [!DNL Adobe Commerce], puede seleccionar los segmentos de Real-Time CDP para personalizar las ofertas únicas del carro de compras, como &quot;comprar 2 obtener 1 gratis&quot;. También puede mostrar banners a pantalla completa y modificar los precios de los productos mediante ofertas promocionales, todas ellas personalizadas para segmentos de Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Cree una conexión de salida activa a [!DNL Azure Data Lake Storage Gen2] para exportar periódicamente archivos de datos de Adobe Experience Platform a su propia ubicación de almacenamiento. Este nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento de información aprovisionada por Adobe Experience Platform, lo que le otorga acceso a una instalación de almacenamiento de archivos segura y basada en la nube para exportar archivos desde Platform. Este nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Cree una conexión de salida activa a [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios bloques. Este nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Los participantes de la beta ahora ven dos [!DNL Amazon S3] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Los participantes de la beta ahora ven dos [!DNL Azure Blob] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Los participantes de la beta ahora ven dos [!DNL SFTP] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |

{style="table-layout:auto"}

**Documentación nueva o actualizada**

| Documentación | Descripción |
| ----------- | ----------- |
| [Barreras de destino](../../destinations/guardrails.md) | Esta página proporciona uso predeterminado y límites de velocidad con respecto al comportamiento de activación. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información detallada de la sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se ha actualizado el `authorized` de un tipo booleano a una cadena. `season` y `episode` se han cambiado de enteros a cadenas. |
| Tipo de datos | [[!UICONTROL Información sobre los detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` se ha cambiado el nombre a `friendlyName`y `ID` se ha cambiado el nombre a `name`. |
| Tipo de datos | [[!UICONTROL Información de detalles de error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` se ha cambiado a `name`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y captura los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Supervisión de consultas a través de la interfaz de usuario de Platform | El servicio de consultas [!UICONTROL Consultas programadas] proporciona una visibilidad mejorada para el estado de todos los trabajos de consulta a través de la interfaz de usuario. Ahora puede encontrar información importante sobre el estado de las ejecuciones de consultas, incluidos los mensajes de error y los códigos en caso de error, desde [!UICONTROL Consultas programadas] pestaña . También puede suscribirse a las alertas a través de la interfaz de usuario para cualquiera de estas consultas en función de su estado. Consulte la [Monitorizar documento de consultas](../../query-service/ui/monitor-queries.md) para obtener más información sobre esta función. |
| Modelo de datos de perspectivas de informes acelerados de consulta | Como parte del SKU de Distiller de datos, el almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Con el almacén acelerado de consultas, puede crear un modelo de datos personalizado o ampliar los modelos de datos de Adobe Real-time Customer Data Platform existentes para mejorar sus perspectivas de informes y sus visualizaciones. Consulte la [documento de perspectivas de informes de almacén acelerado de consultas](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) para obtener más información sobre esta función. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md).
Nuevas funciones de Adobe Experience Platform:

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- | 
| Disponibilidad beta del origen de Adobe Workfront | Utilice la variable [Fuente de Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para llevar los datos de Workfront al Experience Platform y realizar casos de uso, como combinar los registros de trabajo con datos de terceros, aplicar análisis históricos y de series temporales en registros de trabajo y consultar datos de trabajo mediante SQL estándar. Para obtener más información, consulte la guía de [creación de una conexión de origen de Workfront en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
