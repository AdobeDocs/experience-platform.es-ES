---
title: 'Notas de la versión de Adobe Experience Platform: octubre de 2022'
description: Las notas de la versión de octubre de 2022 de Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 33%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 26 de octubre de 2022**

- [Claves administradas por el cliente](#cmk)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Servicio de consultas](#query-service)

## Claves administradas por el cliente {#cmk}

Todos los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves de nivel de sistema. Si utiliza una aplicación basada en Experience Platform, ahora puede optar por utilizar sus propias claves de cifrado, lo que le proporciona un mayor control sobre la seguridad de los datos.

Consulte la descripción general de [claves administradas por el cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) para obtener detalles sobre la función.

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de datos confidenciales para flujos de datos | Ahora, las secuencias de datos aprovechan varias tecnologías de Experience Platform para gestionar correctamente los datos confidenciales, tal como se exige en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Portability and Accountability Act). Consulte la sección sobre [administración de datos confidenciales en las secuencias de datos](../../datastreams/overview.md#sensitive) para obtener más información. |
| Extensión [!DNL Splunk] para el reenvío de eventos | Ahora puede enviar datos a [!DNL Splunk] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Splunk] información general sobre las extensiones](../../tags/extensions/server/splunk/overview.md) para obtener más detalles. |
| Extensión [!DNL Zendesk] para el reenvío de eventos | Ahora puede enviar datos a [!DNL Zendesk] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Zendesk] información general sobre las extensiones](../../tags/extensions/server/zendesk/overview.md) para obtener más detalles. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Exportaciones de conjuntos de datos (Beta) | El [conjunto de datos exporta la funcionalidad de Beta](/help/destinations/ui/export-datasets.md) le permite exportar datos de primera generación (tal como se define en la [descripción del producto de Real-Time Customer Data Platform](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) desde Adobe Experience Platform a sus propios sistemas de clientes externos, a través de la interfaz de usuario de destinos. Esto le permite obtener datos de Experience Platform con un flujo de trabajo sin código/de código bajo a seis destinos de almacenamiento en la nube (enumerados en la tabla siguiente) para casos de uso analíticos y de conformidad. |
| (Beta) Funciones mejoradas de exportación de archivos | Ahora puede beneficiarse de la funcionalidad de personalización mejorada al exportar archivos desde Experience Platform: <br><ul><li>[Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) adicionales.</li><li>Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidad para personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Esta funcionalidad es compatible con las seis nuevas tarjetas de almacenamiento en la nube beta que se enumeran en la tabla siguiente. |

{style="table-layout:auto"}

**Destinos nuevos o actualizados** {#new-or-updated-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line es una popular plataforma de comunicación que conecta personas, servicios e información y que ha crecido desde una aplicación de chat hasta un centro para actividades de entretenimiento, sociales y diarias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 es una plataforma de aplicaciones empresariales basada en la nube que combina la planificación de recursos empresariales (ERP) y la gestión de relaciones con el cliente (CRM) junto con aplicaciones de productividad y herramientas de IA, para ofrecer operaciones de extremo a extremo más suaves y controladas, un mejor potencial de crecimiento y costes reducidos. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | El conector de destino [!DNL (Beta) Adobe Commerce] le permite seleccionar uno o más segmentos de Real-Time CDP para activarlos en su cuenta de [!DNL Adobe Commerce] y así ofrecer una experiencia dinámica y personalizada a sus compradores. En [!DNL Adobe Commerce], puede seleccionar esos segmentos de Real-Time CDP para personalizar ofertas únicas en el carro de compras, como &quot;comprar 2 y obtener 1 gratis&quot;. También puede mostrar banners de pantalla completa y modificar los precios de los productos mediante ofertas promocionales, todas ellas personalizadas para segmentos de Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Cree una conexión saliente activa a [!DNL Azure Data Lake Storage Gen2] para exportar periódicamente los archivos de datos de Adobe Experience Platform a su propia ubicación de almacenamiento. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] es una interfaz de almacenamiento [!DNL Azure Blob] aprovisionada por Adobe Experience Platform, que le concede acceso a una función de almacenamiento de archivos segura y basada en la nube para exportar archivos desde Experience Platform. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Cree una conexión saliente activa a [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios contenedores. Este nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Los participantes de Beta ahora están viendo dos tarjetas de destino [!DNL Amazon S3] en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Los participantes de Beta ahora están viendo dos tarjetas de destino [!DNL Azure Blob] en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Los participantes de Beta ahora están viendo dos tarjetas de destino [!DNL SFTP] en paralelo en el catálogo de destinos. El nuevo destino beta proporciona una funcionalidad mejorada de exportación de archivos y admite exportaciones de conjuntos de datos. |

{style="table-layout:auto"}

**Documentación nueva o actualizada**

| Documentación | Descripción |
| ----------- | ----------- |
| [Protecciones de destinos](../../destinations/guardrails.md) | Esta página proporciona límites predeterminados de uso y velocidad con respecto al comportamiento de activación. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información de detalles de sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se ha actualizado el campo `authorized` de un tipo booleano a una cadena. `season` y `episode` se han cambiado de números enteros a cadenas. |
| Tipo de datos | [[!UICONTROL Información de detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Se cambió el nombre de `name` a `friendlyName` y el de `ID` a `name`. |
| Tipo de datos | [[!UICONTROL Información de detalles del error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` cambió su nombre a `name`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [descripción general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Monitorización de consultas a través de la IU de Experience Platform | La ficha Consultas programadas [!UICONTROL del servicio de consultas] proporciona una visibilidad mejorada para el estado de todos los trabajos de consulta a través de la interfaz de usuario. Ahora puede encontrar información importante sobre el estado de las ejecuciones de consultas, incluidos mensajes de error y códigos en caso de error, en la ficha [!UICONTROL Consultas programadas]. También puede suscribirse a alertas a través de la interfaz de usuario para cualquiera de estas consultas en función de su estado. Consulte el [documento Supervisar consultas](../../query-service/ui/monitor-queries.md) para obtener más información sobre esta característica. |
| Consultar modelo de datos de perspectivas de informes acelerados | Como parte del SKU de Data Distiller, el almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Con el almacén acelerado de consultas puede crear un modelo de datos personalizado o ampliar los modelos de datos de Adobe Real-Time Customer Data Platform existentes para mejorar las perspectivas de creación de informes y sus visualizaciones. Consulte el [documento de información de informes de almacén acelerado de consultas](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) para obtener más información acerca de esta característica. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, consulte la [descripción general del servicio de consulta](../../query-service/home.md).
Nuevas funciones de Adobe Experience Platform:

