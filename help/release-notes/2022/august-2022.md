---
title: Notas de la versión de Adobe Experience Platform, agosto de 2022
description: Notas de la versión de agosto de 2022 para Adobe Experience Platform.
source-git-commit: 925991d58c3cdd84e13b12a095e9681b8f4b254b
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 24 de agosto de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Preparación de datos](#data-prep)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Fuentes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la ingesta de registros con advertencias | La preparación de datos ahora localizará las advertencias (errores no críticos) en los campos y permitirá que se ingrese el resto de la fila. Todos los errores de transformación del asignador ahora se notifican como advertencias y las filas parcialmente ingeridas se consideran correctas, con una advertencia.  La supervisión también se admite en registros con advertencias y detalles de diagnóstico. Actualmente, la ingesta parcial de registros con advertencias solo está disponible para la transmisión de datos. Consulte la documentación de [ingesta de registros con advertencias](../../sources/tutorials/ui/monitor-streaming.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Esquema de entidad AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Describe las entidades no normalizadas para Adobe Journey Optimizer. |
| Clase | [[!UICONTROL Entidades de ejecución de AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Describe las entidades de ejecución de Adobe Journey Optimizer para utilizarlas en la segmentación. |
| Grupo de campos | [[!UICONTROL Objetos de trabajo de Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Grupo de campos de envoltura que hace referencia a todos los grupos de campos específicos de objetos de nivel inferior para Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos comunes de eventos de los pasos del Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Se han agregado dos propiedades nuevas: `origTimeStamp` y `experienceID`. |
| Grupo de campos | [[!UICONTROL Detalles de pertenencia a segmentos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Además de [!UICONTROL Perfil individual XDM], este grupo de campos ahora también se puede utilizar en esquemas basados en la clase XDM Business Account. |
| Grupo de campos | (Múltiple) | Se han actualizado varios grupos de campos relacionados con las actividades B2B de Marketo a un estado estable. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1593/files) para obtener más información. |
| Grupo de campos | (Múltiple) | Se han actualizado varios grupos de campo relacionados con el tiempo para corregir errores que se estaban produciendo en `uvIndex` y `sunsetTime`. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1602/files) para obtener más información. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Una propiedad nueva `productImageUrl` se ha añadido. |
| Tipo de datos | [[!UICONTROL Información de detalles de la solicitud]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Una propiedad nueva `framesPerSecond` se ha añadido. |
| Tipo de datos | [[!UICONTROL Información detallada de la sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` se ha cambiado a `appVersion`. `meta:enum` y `description` también se han actualizado. |
| Tipos de datos y grupos de campos | (Múltiple) | Varios tipos de datos de medios y grupos de campos tienen campos nuevos y descripciones actualizadas. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1582/files) para obtener más información. |
| (Todas) | (Múltiple) | Todos los objetos de esquema que contienen un `enum` ahora también contiene un `meta:enum` para denotar valores de visualización para cada restricción. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1601/files) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de fuentes de autoservicio (SDK por lotes) | Desarrolle, pruebe e integre su fuente de datos basada en la API de REST para introducir datos por lotes en el Experience Platform mediante la fácil configuración de las especificaciones de origen. Con el SDK de fuentes, puede: <ul><li>Configure un nuevo origen en el catálogo de Experience Platform.</li><li>Defina especificaciones para su fuente, incluida información relacionada con tipos de autenticación admitidos, programación y cómo se recuperan los datos de los recursos.</li><li>Cree documentación de cara al usuario para la nueva fuente.</li></ul> Para obtener más información, consulte la documentación de [Fuentes de autoservicio (SDK por lotes)](../../sources/sources-sdk/overview.md). |
| Disponibilidad general [!DNL Google BigQuery] source | Utilice la variable [!DNL Google BigQuery] fuente para introducir datos de su [!DNL Google BigQuery] almacén de datos al Experience Platform. Para obtener más información, consulte la documentación de [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (Beta) | Utilice la variable [!DNL Teradata Vantage] fuente para introducir datos de entornos híbridos de nube múltiple a Experience Platform. Para obtener más información, consulte la documentación de [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Compatibilidad entre regiones para el origen de Adobe Analytics | Ahora puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur). Los grupos de informes deben asignarse a la misma organización que la instancia de espacio aislado del Experience Platform en la que se está creando la conexión de origen. Para obtener más información, consulte la guía de [creación de una conexión de origen de Adobe Analytics en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Compatibilidad de API para la ingesta bajo demanda | Utilice la ingesta bajo demanda para crear ejecuciones de flujo ad hoc para un flujo de datos determinado con la variable [!DNL Flow Service] API. Las ejecuciones de flujo creadas deben establecerse en ingesta única. Para obtener más información, consulte la guía de [creación de una ejecución de flujo para la ingesta bajo demanda mediante la API](../../sources/tutorials/api/on-demand-ingestion.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
