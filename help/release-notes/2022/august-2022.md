---
title: Notas de la versión de Adobe Experience Platform, agosto de 2022
description: Notas de la versión de agosto de 2022 de Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 24 de agosto de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Los servicios de IA/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing configurar modelos específicos para las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de tener experiencia en la ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la privacidad | <ul><li> Attribution AI ahora admite la definición de funciones de usuario y directivas de acceso para administrar [permissions](../../../help/access-control/abac/ui/permissions.md) para funciones y objetos dentro de una aplicación de producto. </li><li>Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad.</li><li> Pasante [control de acceso basado en atributos](../../access-control/abac/overview.md), los administradores pueden controlar el acceso a objetos específicos o a capacidades basadas en determinados atributos, que pueden ser metadatos añadidos a un objeto, como etiquetas. Los administradores también pueden definir funciones de usuario que solo tengan acceso a campos específicos y a los datos correspondientes a esos campos.</li><li>Attribution AI aprovecha los conjuntos de datos de Platform. Para admitir solicitudes de derechos de consumidor que una marca pueda recibir, las marcas deben utilizar Platform Privacy Service para enviar solicitudes de acceso y eliminación de consumidores con el fin de eliminar sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real.  </li><li>Todos los conjuntos de datos utilizados para la entrada/salida de modelos seguirán las directrices de Platform. El cifrado de datos de Platform se aplica a los datos en reposo y en tránsito. Consulte la documentación para obtener más información sobre [cifrado de datos](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: la Attribution AI no estará disponible con los clientes existentes de Healthcare Shield hasta nuevo aviso.

Para obtener más información sobre Attribution AI, consulte la [Attribution AI](../../intelligent-services/attribution-ai/overview.md) información general.

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la privacidad | <ul><li> La inteligencia artificial aplicada al cliente ahora admite la definición de funciones de usuario y políticas de acceso para administrar [permissions](../../../help/access-control/abac/ui/permissions.md) para funciones y objetos dentro de una aplicación de producto. </li><li>Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad.</li><li> Pasante [control de acceso basado en atributos](../../access-control/abac/overview.md), los administradores pueden controlar el acceso a objetos específicos o capacidades en función de determinados atributos. Estos atributos pueden ser metadatos añadidos a un objeto, como etiquetas. Los administradores también pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.</li><li>Customer AI aprovecha los conjuntos de datos de Platform. Para admitir solicitudes de derechos de consumidor que una marca pueda recibir, las marcas deben utilizar Platform Privacy Service para enviar solicitudes de acceso y eliminación de consumidores con el fin de eliminar sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real. </li><li>Todos los conjuntos de datos utilizados para la entrada/salida de modelos seguirán las directrices de Platform. El cifrado de datos de Platform se aplica a los datos en reposo y en tránsito. Consulte la documentación para obtener más información sobre [cifrado de datos](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: la inteligencia artificial aplicada al cliente no estará disponible con los clientes existentes de Healthcare Shield hasta nuevo aviso.

Para obtener más información sobre Customer AI, consulte la [Inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/overview.md) información general.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través del cual puede ver información importante acerca de los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de activaciones programadas | El [!UICONTROL Activaciones programadas] El widget proporciona una vista tabulada de los destinos activados más recientemente. Para cada segmento, incluye el nombre, la plataforma de destino y las fechas de inicio y finalización de la activación. Este widget le permite descubrir de un vistazo dónde y cuándo se está activando la audiencia, y hace que las activaciones duplicadas o innecesarias sean más transparentes. Esta información acumulada también resalta dónde se ha dejado de lado cualquier activación. |

Para obtener más información sobre [!DNL Dashboards], consulte la [[!DNL Dashboards] descripción general](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la ingesta de registros con advertencias | La preparación de datos ahora localizará advertencias (errores no críticos) en los campos y permitirá la ingesta del resto de la fila. Todos los errores de transformación del asignador ahora se registran como advertencias y las filas introducidas parcialmente se consideran correctas, con una advertencia.  La monitorización también se admite en registros con advertencias y detalles de diagnóstico. Actualmente, la ingesta parcial de registros con advertencias solo está disponible para la transmisión de datos. Revise la documentación de [ingesta de registros con advertencias](../../sources/tutorials/ui/monitor-streaming.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información acerca de [!DNL Data Prep], consulte la [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| (Beta) Compatibilidad de personalización basada en atributos para destinos de personalización | Con la versión beta de la personalización basada en atributos, verá dos nuevas tarjetas en la [catálogo de destino](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: este conector está actualmente en versión beta y solo está disponible para un número selecto de clientes. Además de la funcionalidad proporcionada por la tarjeta de Adobe Target V1, el conector de Target V2 agrega una [paso de asignación](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) al flujo de trabajo de activación, que le permite asignar atributos de perfil a Adobe Target, lo que permite la personalización en la misma página y en la siguiente página basada en atributos.</li><li>**[!UICONTROL Personalización personalizada con atributos]**: este conector está actualmente en versión beta y solo está disponible para un número selecto de clientes. Además de la funcionalidad proporcionada por **[!UICONTROL Personalización personalizada]**, el **[!UICONTROL Personalización personalizada con atributos]** El conector añade un [paso de asignación](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) al flujo de trabajo de activación, que le permite asignar atributos de perfil a su destino de personalización personalizado, lo que permite la personalización de la misma página y de la página siguiente basada en atributos.</li></ul> <br> Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, la variable **[!UICONTROL Personalización personalizada con atributos]** El destino requiere que utilice el [API del servidor de red perimetral](../../server-api/overview.md) para la recopilación de datos. Además, todas las llamadas a la API de servidor deben realizarse en un [contexto autenticado](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) es una plataforma de ejecución de ventas con la mayor cantidad de datos de interacción comprador-vendedor B2B en el mundo e inversiones significativas en tecnologías de IA propietarias para traducir datos de ventas en inteligencia. [!DNL Outreach] ayuda a las organizaciones a automatizar la participación en ventas y actuar en base a la inteligencia de ingresos para mejorar su eficiencia, previsibilidad y crecimiento. |

{style="table-layout:auto"}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Clase de entidad AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Una clase basada en registros para crear esquemas de búsqueda para Adobe Journey Optimizer. |
| Grupo de campos | [[!UICONTROL Objetos de trabajo de Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Grupo de campos envolvente que hace referencia a todos los grupos de campos específicos de objetos de nivel inferior para Adobe Workfront. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos comunes de eventos de pasos de Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Se han añadido dos nuevas propiedades: `origTimeStamp` y `experienceID`. |
| Grupo de campos | [[!UICONTROL Detalles de abono de segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Además de [!UICONTROL Perfil individual de XDM]Sin embargo, este grupo de campos ahora también se puede utilizar en esquemas basados en la clase de cuenta empresarial de XDM. |
| Grupo de campos | (Múltiple) | Se han actualizado varios grupos de campo relacionados con actividades B2B de Marketo a un estado estable. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1593/files) para obtener más información. |
| Grupo de campos | (Múltiple) | Se han actualizado varios grupos de campos relacionados con el tiempo para corregir los errores que se estaban produciendo para `uvIndex` y `sunsetTime`. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1602/files) para obtener más información. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Una nueva propiedad `productImageUrl` se ha añadido. |
| Tipo de datos | [[!UICONTROL Información de detalles de datos Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Una nueva propiedad `framesPerSecond` se ha añadido. |
| Tipo de datos | [[!UICONTROL Información de detalles de sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` se ha cambiado a `appVersion`. `meta:enum` y `description` Los campos de también se han actualizado. |
| Tipos de datos y grupos de campos | (Múltiple) | Varios tipos de datos de medios y grupos de campos tienen campos nuevos y descripciones actualizadas. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1582/files) para obtener más información. |
| (Todas) | (Múltiple) | Todos los objetos de esquema que contienen un `enum` ahora también contienen un campo correspondiente `meta:enum` para denotar los valores de visualización de cada restricción. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1601/files) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Límite estricto de políticas de combinación | Platform impondrá ahora un límite estricto de **cinco** políticas de combinación por zona protegida. Si la zona protegida tiene actualmente más de cinco políticas de combinación, deberá **no** poder crear nuevas políticas de combinación hasta que la zona protegida tenga menos de cinco políticas de combinación. |
| Limpieza de atributo perimetral de perfil huérfano | Para todas las organizaciones, el servicio de perfiles ahora elimina diariamente los atributos de borde sobrantes de la región de actividad del usuario para proporcionar una representación más precisa de los perfiles en el sistema. Esta limpieza se produce después de eliminar todos los fragmentos de perfil de un perfil determinado y debe afectar a los perfiles que se combinan desde conjuntos de datos en los que `com_adobe_aep_profile_region_dataset` está marcado como `true`. Esto puede mostrar una caída en la métrica &quot;Audiencia direccionable&quot; en el panel de uso de licencias y puede mostrar una caída en la métrica &quot;Recuento de perfiles&quot; en el panel de perfiles, ya que estas métricas incluían fragmentos de atributos de borde sobrantes antes antes de esta versión. |

{style="table-layout:auto"}

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, comience por leer el [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con 4000 segmentos | Todas las organizaciones con Platform ahora admiten hasta 4000 definiciones de segmentos. Para obtener más información sobre cómo afecta este cambio a las API del trabajo de segmentación, lea la [guía de extremo de trabajo de segmentación](../../segmentation/api/segment-jobs.md) |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de orígenes de autoservicio (SDK por lotes) | Desarrolle, pruebe e integre su fuente de datos basada en la API de REST para introducir datos por lotes en Experience Platform mediante especificaciones de fuente fáciles de configurar. Con el SDK de fuentes puede: <ul><li>Configure una nueva fuente para el catálogo de Experience Platform.</li><li>Defina especificaciones para su fuente, incluida la información perteneciente a los tipos de autenticación admitidos, la programación y cómo se recuperan los datos de recursos.</li><li>Cree documentación orientada al usuario para la nueva fuente.</li></ul> Para obtener más información, lea la documentación sobre [Fuentes de autoservicio (SDK por lotes)](../../sources/sources-sdk/overview.md). |
| Disponibilidad general de [!DNL Google BigQuery] origen | Utilice el [!DNL Google BigQuery] origen para introducir datos de su [!DNL Google BigQuery] data warehouse para Experience Platform. Para obtener más información, lea la documentación de la [[!DNL Google BigQuery] origen](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] origen (beta) | Utilice el [!DNL Teradata Vantage] origen para introducir datos de entornos híbridos de varias nubes en Experience Platform. Para obtener más información, lea la documentación de la [[!DNL Teradata Vantage] origen](../../sources/connectors/databases/teradata-vantage.md). |
| Compatibilidad entre regiones para orígenes de Adobe Analytics | Ahora puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur). Los grupos de informes deben asignarse a la misma organización que la instancia de zona protegida de Experience Platform en la que se está creando la conexión de origen en. Para obtener más información, lea la guía de [crear una conexión de origen de Adobe Analytics en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
