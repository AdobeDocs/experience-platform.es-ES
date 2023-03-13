---
title: Notas de la versión de Adobe Experience Platform de octubre de 2022
description: Notas de la versión de octubre de 2022 de Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de octubre de 2022**

- [Claves administradas por el cliente](#cmk)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

## Claves administradas por el cliente {#cmk}

Todos los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves de nivel de sistema. Si utiliza una aplicación basada en Platform, ahora puede optar por utilizar sus propias claves de cifrado, lo que le proporciona el bueno control sobre la seguridad de los datos.

Consulte la información general sobre [claves administradas por el cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obtener más información sobre la función.

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de datos confidenciales para flujos de datos | Ahora, las secuencias de datos aprovechan varias tecnologías de Platform para gestionar correctamente los datos confidenciales, tal como se exige en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../edge/datastreams/overview.md#sensitive) para obtener más información. |
| [!DNL Splunk] extensión para reenvío de eventos | Ahora puede enviar datos a [!DNL Splunk] uso de un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Splunk] información general sobre extensiones](../../tags/extensions/server/splunk/overview.md) para obtener más información. |
| [!DNL Zendesk] extensión para reenvío de eventos | Ahora puede enviar datos a [!DNL Zendesk] uso de un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Zendesk] información general sobre extensiones](../../tags/extensions/server/zendesk/overview.md) para obtener más información. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Exportaciones de conjuntos de datos (beta) | El [Funcionalidad beta de exportaciones de conjuntos de datos](/help/destinations/ui/export-datasets.md) permite exportar datos de primera generación (como se define en la [Descripción del producto de Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) desde Adobe Experience Platform a sus propios sistemas de clientes externos, a través de la interfaz de usuario de destinos. Esto le permite obtener datos de Experience Platform con un flujo de trabajo sin código o de código bajo a seis destinos de almacenamiento en la nube (enumerados en la tabla siguiente) para casos de uso analíticos y de conformidad. |
| (Beta) Funciones mejoradas de exportación de archivos | Ahora puede beneficiarse de la funcionalidad de personalización mejorada al exportar archivos fuera del Experience Platform: <br><ul><li>Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través de [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Esta funcionalidad es compatible con las seis nuevas tarjetas de almacenamiento en la nube beta que se enumeran en la tabla siguiente. |

{style="table-layout:auto"}

**Destinos nuevos o actualizados**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line es una popular plataforma de comunicación que conecta personas, servicios e información y que ha crecido desde una aplicación de chat hasta un centro para actividades de entretenimiento, sociales y diarias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 es una plataforma de aplicaciones empresariales basada en la nube que combina Planificación de recursos empresariales (ERP) y Administración de relaciones con el cliente (CRM) junto con aplicaciones de productividad y herramientas de IA, para ofrecer operaciones de extremo a extremo más suaves y controladas, un mejor potencial de crecimiento y costes reducidos. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | El [!DNL (Beta) Adobe Commerce] destination connector permite seleccionar uno o varios segmentos de Real-Time CDP para activarlos en el [!DNL Adobe Commerce] para ofrecer una experiencia dinámica y personalizada a sus compradores. En [!DNL Adobe Commerce], puede seleccionar esos segmentos de Real-Time CDP para personalizar ofertas únicas en el carro de compras como &quot;comprar 2 y obtener 1 gratis&quot;. También puede mostrar banners de pantalla completa y modificar los precios de los productos mediante ofertas promocionales, todas ellas personalizadas para segmentos de Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Cree una conexión saliente activa a [!DNL Azure Data Lake Storage Gen2] para exportar periódicamente archivos de datos de Adobe Experience Platform a su propia ubicación de almacenamiento. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento aprovisionada por Adobe Experience Platform, que le concede acceso a una función de almacenamiento de archivos segura y basada en la nube para exportar archivos fuera de Platform. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Cree una conexión saliente activa a [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios contenedores. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Los participantes beta ahora ven dos [!DNL Amazon S3] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Los participantes beta ahora ven dos [!DNL Azure Blob] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Los participantes beta ahora ven dos [!DNL SFTP] tarjetas de destino en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |

{style="table-layout:auto"}

**Documentación nueva o actualizada**

| Documentación | Descripción |
| ----------- | ----------- |
| [Protecciones de destinos](../../destinations/guardrails.md) | Esta página proporciona límites predeterminados de uso y velocidad con respecto al comportamiento de activación. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información de detalles de sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se ha actualizado el `authorized` de un tipo booleano a una cadena. `season` y `episode` se han cambiado de números enteros a cadenas. |
| Tipo de datos | [[!UICONTROL Información de detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` se ha cambiado a `friendlyName`, y `ID` se ha cambiado a `name`. |
| Tipo de datos | [[!UICONTROL Información de detalles del error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` se ha cambiado a `name`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

Query Service permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unir cualquier conjunto de datos de [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para usar en sistema de informes, espacio de trabajo de ciencia de datos o para su inserción en el perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Monitorización de consultas a través de la IU de Platform | El servicio de consultas [!UICONTROL Consultas programadas] proporciona una visibilidad mejorada para el estado de todos los trabajos de consulta a través de la interfaz de usuario. Ahora puede encontrar información importante sobre el estado de las ejecuciones de consultas, incluidos mensajes de error y códigos en caso de error, desde [!UICONTROL Consultas programadas] pestaña. También puede suscribirse a alertas a través de la interfaz de usuario para cualquiera de estas consultas en función de su estado. Consulte la [Monitor de documento de consultas](../../query-service/ui/monitor-queries.md) para obtener más información sobre esta función. |
| Consultar modelo de datos de perspectivas de informes acelerados | Como parte del SKU de Data Distiller, el almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Con el almacén acelerado de consultas puede crear un modelo de datos personalizado o ampliar los modelos de datos de Adobe Real-time Customer Data Platform existentes para mejorar las perspectivas de creación de informes y sus visualizaciones. Consulte la [consultar documento de perspectivas de informes de tienda acelerados](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) para obtener más información sobre esta función. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, consulte [Introducción al servicio de consultas](../../query-service/home.md).
Nuevas funciones de Adobe Experience Platform:

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- | 
| Disponibilidad beta del origen de Adobe Workfront | Utilice el [fuente de Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para llevar los datos de Workfront al Experience Platform y realizar casos de uso, como combinar los registros de trabajo con datos de terceros, aplicar análisis históricos y de series temporales en registros de trabajo y consultar datos de trabajo mediante SQL estándar. Para obtener más información, lea la guía de [crear una conexión de origen de Workfront en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
