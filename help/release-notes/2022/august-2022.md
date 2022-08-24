---
title: Notas de la versión de Adobe Experience Platform, agosto de 2022
description: Notas de la versión de agosto de 2022 para Adobe Experience Platform.
source-git-commit: 24f16e315607a1076ff2efef129d9e97040a9500
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 24 de agosto de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:


- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Preparación de datos](#data-prep)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Los servicios AI/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren modelos específicos de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la privacidad | <li> Attribution AI ahora admite la definición de funciones de usuario y políticas de acceso para administrar [permissions](../../help/access-control/abac/ui/permissions.md) para características y objetos de una aplicación de producto. </li><li>Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad.</li> <li> Hasta [control de acceso basado en atributos](../../access-control/abac/overview.md), los administradores pueden controlar el acceso a objetos específicos o a funciones basadas en determinados atributos, que pueden ser metadatos agregados a un objeto, como etiquetas. Los administradores también pueden definir funciones de usuario que solo tengan acceso a campos específicos y datos que correspondan a esos campos.</li> <li>[Higiene de los datos](../../help/hygiene/home.md) las funciones de Attribution AI solo permiten utilizar datos actualizados para obtener más información y puntuación. Del mismo modo, cuando se solicita la eliminación de datos, la Attribution AI se abstiene de utilizarlos.</li><li>Attribution AI aprovecha los conjuntos de datos de Platform. Para facilitar el cumplimiento del RGPD, puede utilizar Adobe Experience Platform Privacy Service para configurar protocolos que satisfagan las solicitudes de los clientes de acceso y eliminación de sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real. Todos los datos se cifran en tránsito y en reposo.</li> |

{style=&quot;table-layout:auto&quot;}

**Nota**: No estarán disponibles para los clientes de Healthcare Shield hasta finales del cuarto trimestre de 2022.

Para obtener más información sobre la Attribution AI, consulte la [Attribution AI](../../intelligent-services/attribution-ai/overview.md) información general.

### Customer AI

La AI del cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la privacidad | <li> La Customer AI ahora admite la definición de funciones de usuario y políticas de acceso para administrar [permissions](../../help/access-control/abac/ui/permissions.md) para características y objetos de una aplicación de producto. </li><li>Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad.</li> <li> Hasta [control de acceso basado en atributos](../../access-control/abac/overview.md), los administradores pueden controlar el acceso a objetos o capacidades específicos en función de determinados atributos. Estos atributos pueden ser metadatos agregados a un objeto, como etiquetas. Los administradores también pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que se correspondan con esos campos.</li> <li>[Higiene de los datos](../../help/hygiene/home.md) las funciones de Customer AI solo permiten utilizar datos actualizados para obtener más información y puntuación. Del mismo modo, cuando se solicita la eliminación de datos, la AI del cliente se abstiene de utilizarlos.</li><li>Customer AI aprovecha los conjuntos de datos de Platform. Para facilitar el cumplimiento del RGPD, puede utilizar Adobe Experience Platform Privacy Service para configurar protocolos que satisfagan las solicitudes de los clientes de acceso y eliminación de sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real. Todos los datos se cifran en tránsito y en reposo.</li> |

{style=&quot;table-layout:auto&quot;}

**Nota**: Customer AI no estará disponible para los clientes de Healthcare Shield hasta finales del cuarto trimestre de 2022.

Para obtener más información sobre Customer AI, consulte la [Customer AI](../../intelligent-services/customer-ai/overview.md) información general.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través de la cual puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de activaciones programadas | La variable [!UICONTROL Activaciones programadas] proporciona una vista tabularizada de los destinos activados más recientemente. Para cada segmento, incluye el nombre, la plataforma de destino y la fecha de inicio y finalización de la activación. Esta utilidad le permite descubrir de un vistazo dónde y cuándo se está activando la audiencia y hace que las activaciones duplicadas o innecesarias sean más transparentes. Esta información acumulada también resalta dónde se han dejado de lado las activaciones. |

Para obtener más información, consulte [!DNL Dashboards], consulte la [[!DNL Dashboards] información general](../../dashboards/home.md).

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

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Limpieza de atributos perimetrales de perfil huérfanos | Para todas las organizaciones, el servicio de perfil ahora elimina diariamente los atributos perimetrales sobrantes de la región de actividad del usuario para proporcionar una representación más precisa de sus perfiles en su sistema. Esta limpieza se produce después de que se eliminan todos los fragmentos de perfil de un perfil determinado y debe afectar a los perfiles que se combinan desde conjuntos de datos en los que `com_adobe_aep_profile_region_dataset` está marcado como `true`. Esto puede mostrar una caída en la métrica &quot;Audiencia direccionable&quot; en el panel de uso de licencias y mostrar una caída en la métrica &quot;Recuento de perfiles&quot; en el panel de perfiles, ya que estas métricas incluían fragmentos de atributos perimetrales restantes antes de esta versión. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con 4000 segmentos | Todas las organizaciones con Platform ahora admiten hasta 4000 definiciones de segmentos. Para obtener más información sobre cómo afecta este cambio a las API de trabajos de segmentos, lea la [guía de extremo de trabajo del segmento](../../segmentation/api/segment-jobs.md) |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

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

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).