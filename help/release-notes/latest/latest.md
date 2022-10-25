---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
source-git-commit: 0ea2718247792e997b7a90ab9027946e800c8157
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de octubre de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Claves gestionadas por el cliente](#cmk)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

## Claves gestionadas por el cliente {#cmk}

Todos los datos almacenados en Adobe Experience Platform se cifran en reposo utilizando claves a nivel de sistema. Si utiliza una aplicación creada sobre Platform, ahora puede optar por utilizar sus propias claves de cifrado, lo que le otorga un bueno control sobre la seguridad de los datos.

Consulte la descripción general sobre [claves administradas por el cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obtener más información sobre la función.

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de datos confidenciales para conjuntos de datos | Los conjuntos de datos ahora aprovechan varias tecnologías de plataforma para manejar adecuadamente los datos confidenciales según se aplican en regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, Health Insurance Porability and Accounability Act). Consulte la sección sobre [gestión de datos confidenciales en flujos de datos](../../edge/datastreams/overview.md#sensitive) para obtener más información. |
| [!DNL Splunk] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Splunk] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Splunk] información general de la extensión](../../tags/extensions/web/splunk/overview.md) para obtener más información. |
| [!DNL Zendesk] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Zendesk] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Zendesk] información general de la extensión](../../tags/extensions/web/zendesk/overview.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información detallada de la sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se ha actualizado el `authorized` de un tipo booleano a una cadena. `season` y `episode` se han cambiado de enteros a cadenas. |
| Tipo de datos | [[!UICONTROL Información sobre los detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` se ha cambiado el nombre a `friendlyName`y `ID` se ha cambiado el nombre a `name`. |
| Tipo de datos | [[!UICONTROL Información de detalles de error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` se ha cambiado a `name`. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Modelo de datos de perspectivas de informes acelerados de consulta | Como parte del SKU de Distiller de datos, el almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Con el almacén acelerado de consultas, puede crear un modelo de datos personalizado o ampliar los modelos de datos de Adobe Real-time Customer Data Platform existentes para mejorar sus perspectivas de informes y sus visualizaciones. Consulte la [documento de perspectivas de informes de almacén acelerado de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/query-accelerated-store/reporting-insights-data-model.html) para obtener más información sobre esta función. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los servicios de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md).
Nuevas funciones de Adobe Experience Platform:

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- | 
| Disponibilidad beta del origen de Adobe Workfront | Utilice la variable [Fuente de Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para llevar los datos de Workfront al Experience Platform y realizar casos de uso, como combinar los registros de trabajo con datos de terceros, aplicar análisis históricos y de series temporales en registros de trabajo y consultar datos de trabajo mediante SQL estándar. Para obtener más información, consulte la guía de [creación de una conexión de origen de Workfront en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilidad beta del origen de Oracle Service Cloud | Utilice la fuente de nube de servicio de Oracle para ingerir los datos de su cuenta de Oracle Service Cloud en Experience Platform. Para obtener más información, consulte la documentación de [Origen de nube de servicio de oracle](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
