---
title: 'Notas de la versión de Adobe Experience Platform: septiembre de 2022'
description: Las notas de la versión de septiembre de 2022 de Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 24%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 28 de septiembre de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Control de acceso basado en atributos](#abac)

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Registros de auditoría](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

## Control de acceso basado en atributos {#abac}

>[!IMPORTANT]
>
>El control de acceso basado en atributos se habilitará a partir de octubre de 2022. Si desea ser uno de los primeros en adoptarlo, póngase en contacto con su representante de Adobe.

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad una mayor flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a funciones de usuario. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Experience Platform específicos de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y otros tipos personalizados de datos en todos los flujos de trabajo y recursos de Experience Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

| Función | Descripción |
| --- | --- |
| Control de acceso basado en atributos | El control de acceso basado en atributos le permite etiquetar campos y segmentos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir políticas de acceso que cubran los campos y segmentos de esquema XDM para administrar mejor el acceso dado a usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Para obtener más información, consulte la [descripción general del control de acceso basado en atributos](../../access-control/abac/overview.md). |
| Permisos | Permisos es el área de Experience Cloud donde los administradores pueden definir funciones de usuario y directivas de acceso para administrar permisos de acceso para funciones y objetos dentro de una aplicación de producto. Mediante Permisos, puede crear y administrar funciones, asignar los permisos de recursos deseados para estas funciones y crear directivas para aprovechar las etiquetas y definir qué funciones de usuario tienen acceso a recursos específicos de Experience Platform. Los permisos también le permiten administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica. Para obtener más información, consulte la [Guía de la interfaz de usuario de permisos](../../access-control/abac/ui/browse.md). |

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general del control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo de control de acceso basado en atributos, lea la [guía completa de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Los servicios de IA/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing configurar modelos específicos para las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de tener experiencia en la ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar una configuración de modelo como instancia de borrador y seguir editándola hasta que se complete antes de la formación y la puntuación. Los escenarios en los que esta función resulta útil incluyen aquellos en los que un usuario tiene varios campos que definir en el flujo de trabajo, pero no puede completarlos debido a limitaciones de tiempo. Otro escenario es cuando se procesan una o más estadísticas de conjuntos de datos y aún no están disponibles. Lea [Guía del usuario de inteligencia artificial aplicada a la atribución](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) para obtener más información. |
| Directivas de gobernanza | Una vez que los usuarios envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de política del uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing sean compatibles con las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre la inteligencia artificial aplicada a la atribución, consulte [Descripción general de la inteligencia artificial aplicada a la atribución](../../intelligent-services/attribution-ai/overview.md). Para obtener información sobre las directivas de control de datos, lea la [descripción general de directivas](../../data-governance/policies/overview.md).

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente disponible en Real-Time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar una configuración de modelo como instancia de borrador y seguir editándola hasta que se complete antes de la formación y la puntuación. Los escenarios en los que esta función resulta útil incluyen aquellos en los que un usuario tiene varios campos que definir en el flujo de trabajo, pero no puede completarlos debido a limitaciones de tiempo. Otro escenario es cuando se procesan una o más estadísticas de conjuntos de datos y aún no están disponibles. Lea la [Guía del usuario de inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) para obtener más información. |
| Directivas de gobernanza | Una vez que los usuarios envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de política del uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing sean compatibles con las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre la inteligencia artificial aplicada al cliente, lea la [Descripción general de la inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/overview.md). Para obtener información sobre las directivas de control de datos, lea la [descripción general de directivas](../../data-governance/policies/overview.md).

## Registros de auditoría {#audit-logs}

Experience Platform le permite auditar la actividad del usuario para varios servicios y funcionalidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Funciones actualizadas**

| Función | Nombre | Descripción |
| --- | --- | --- |
| Recursos añadidos | <ul><li>Instancia de Attribution AI</li><li>Instancia de Customer AI</li><li>Secuencia de datos</li></ul> | Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad. Si la función está habilitada, no es necesario habilitar manualmente la recopilación de registros. |

{style="table-layout:auto"}

Para obtener más información sobre los distintos tipos de eventos específicos de recursos que se registran en los registros de auditoría de Experience Platform, consulte [información general sobre los registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| Etiqueta en uso | Cuando se visualiza en la biblioteca de widgets, la etiqueta en uso identifica fácilmente la presencia de widgets existentes en el tablero. Esto facilita evitar la duplicación, aunque puede añadir el mismo widget más de una vez si lo desea. |
| Paneles definidos por el usuario | Los paneles definidos por el usuario ayudan a acelerar las perspectivas y personalizar las visualizaciones, lo que le permite crear y administrar paneles personalizados. Con los paneles definidos por el usuario puede crear, añadir y editar widgets personalizados para visualizar métricas clave relevantes para su organización. Lee la [guía de características](../../dashboards/standard-dashboards.md) para obtener más información. |
| Modelo de datos de perspectivas de Customer Data Platform | La función del modelo de datos de perspectivas de la plataforma de datos del cliente (CDP) expone los modelos de datos y SQL que alimenta las perspectivas para varios widgets de perfil, destino y segmentación. Puede personalizar estas plantillas de consulta SQL para crear informes CDP para los casos de uso de indicadores de rendimiento clave y marketing. Estas perspectivas pueden utilizarse como widgets personalizados para los paneles definidos por el usuario. Lea la [guía de características del modelo de datos de perspectivas de CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) para obtener más información. |
| Widget del informe de superposición de audiencia | Este widget está disponible tanto para paneles de [!UICONTROL Perfiles] como de [!UICONTROL Segmentos]. El informe proporciona una lista ordenada de audiencias clasificadas según los porcentajes de superposición más altos o más bajos para el segmento elegido. En el panel [!UICONTROL Perfiles] puede filtrar y ver la superposición de audiencias mediante una política de combinación a partir de todos los segmentos disponibles. Los paneles [!UICONTROL Segmentos] le permiten filtrar la superposición de audiencias según un segmento específico.<br>Use este análisis para generar nuevos segmentos de alto rendimiento y evitar enviar la misma audiencia a diferentes destinos. El informe también ayuda a identificar perspectivas ocultas para mejorar la segmentación o localizar perfiles únicos que perseguir. Lea las respectivas guías de los widgets [perfiles](../../dashboards/guides/profiles.md#audience-overlap-report) y [segmentos](../../dashboards/guides/audiences.md#audience-overlap-report) para obtener más información. |

Para obtener más información sobre [!DNL Dashboards], consulte la [[!DNL Dashboards] Información general](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Integración de navegación izquierda en la IU de Experience Platform | Todas las funcionalidades que anteriormente eran exclusivas de la IU de recopilación de datos (incluidas las etiquetas, el reenvío de eventos y las secuencias de datos) ahora también están disponibles a través de la navegación izquierda en Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre IU al trabajar con funciones de recopilación de datos en Experience Platform. |
| Atribución de usuario en etiquetas y reenvío de eventos | Al enumerar [!UICONTROL Propiedades] disponibles en las etiquetas y el reenvío de eventos, cada propiedad enumerada ahora muestra cuándo se actualizó por última vez y qué usuario realizó la actualización. |
| [[!DNL Snap Conversions API] extensión](https://exchange.adobe.com/apps/ec/108550) para reenvío de eventos | Ahora puede enviar datos a [!DNL Snapchat Conversions API] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Para obtener más información sobre cómo autenticar y utilizar la API, consulte la [[!DNL Snapchat Marketing API] documentación](https://marketingapi.snapchat.com/docs/conversion.html). |
| [Sugerencias del cliente agente de usuario en Web SDK](/help/web-sdk/use-cases/client-hints.md) | Web SDK ahora admite [User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Las sugerencias del cliente permiten a los propietarios de sitios web tener acceso a gran parte de la misma información disponible en la cadena [!DNL User-Agent], pero de una manera que preserva la privacidad. |
| [Migración página por página de Web SDK](../../web-sdk/home.md#migrating-to-web-sdk) | Ahora puede migrar las propiedades web existentes desde otras bibliotecas de Experience Cloud, como [!DNL at.js], a Web SDK, página por página. Esto permite un enfoque gradual de la migración a Web SDK, sin necesidad de migrar todas las páginas a la vez. |
| [[!DNL Adobe Journey Optimizer] compatibilidad con flujos de datos](../../datastreams/overview.md#aep) | El servicio Adobe Experience Platform para flujos de datos ahora admite [!DNL Adobe Journey Optimizer]. Esta opción le permite usar canales entrantes web y basados en aplicaciones en [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Para obtener más información sobre la recopilación de datos en Experience Platform, consulte [descripción general de la recopilación de datos](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Destination SDK | Destination SDK ahora es totalmente compatible con los socios y clientes que crean destinos privados o producidos por lotes (o basados en archivos). Lea las siguientes páginas de documentación para obtener más información: <ul><li>[Información general de Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Configurar un destino basado en archivos](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Configurar opciones de formato de archivo para destinos basados en archivos](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Pruebe sus destinos basados en archivos](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Destinos nuevos o actualizados**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal. [Introducción a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=es). Tenga en cuenta que esta integración funciona con [Adobe Campaign versión 8.4 o superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=es#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | El destino [!DNL Salesforce CRM] se ha actualizado para admitir actualizaciones de contactos y posibles clientes, así como mejoras de rendimiento para actualizaciones más rápidas. |

{style="table-layout:auto"}

**Documentación nueva o actualizada**

| Documentación | Descripción |
| ----------- | ----------- |
| Documentación de API del servicio de flujo de destinos | La [documentación de referencia de la API de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) se ha actualizado para incluir instrucciones sobre cómo realizar operaciones en destinos basados en archivos. Las operaciones para los destinos de flujo continuo se agregarán más adelante. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad de la IU con enumeraciones y valores sugeridos | Además de las enumeraciones que habilitan la validación de datos, ahora puede [agregar o quitar valores sugeridos](../../xdm/ui/fields/enum.md) para campos de cadena estándar o personalizados, de modo que los usuarios de Experience Platform tengan una lista de valores descriptivos para seleccionar al crear segmentos. |

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos de clasificación de AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Propiedades de un elemento específico con el que se interactuó y que provocó que se activara el evento de la propuesta. |
| Grupo de campo | [[!UICONTROL Detalles de interacción de Media Analytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Rastrea interacciones de medios a lo largo del tiempo. |
| Grupo de campo | [[!UICONTROL Información de detalles de medios]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Registra información de detalles de medios. |
| Grupo de campo | [[!UICONTROL Evento de experiencia de Adobe CJM - Superficies]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Describe las superficies de los eventos de experiencia en Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Comportamiento | [[!UICONTROL Serie temporal]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Valores agregados para `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valores eliminados de `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Grupo de campo | (Múltiple) | [Se han actualizado varias descripciones de los campos](https://github.com/adobe/xdm/pull/1628/files) en todos los componentes de Journey Orchestration. |
| Grupo de campo | (Múltiple) | [Se han actualizado los títulos de varios componentes de Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) para mantener la coherencia. |
| Grupo de campo | [[!UICONTROL Campos de clasificación de AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Se actualizaron las áreas de nombres de varios campos a `xdm`. |
| Grupo de campo | [[!UICONTROL Campos comunes de eventos de pasos de Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Se agregó un nuevo campo, `isReadSegmentTriggerStartEvent`. |
| Grupo de campo | [[!UICONTROL Pronóstico del Tiempo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Se ha cambiado el campo `xdm:uvIndex` a un tipo entero y se ha agregado el área de nombres `xdm` a varios campos en los que faltaba is. |
| Grupo de campo | [[!UICONTROL Información de detalles de medios]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` y `xdm:implementationDetails` se han quitado del grupo de campos. |
| Tipo de datos | (Múltiple) | [Se han actualizado varios nombres de propiedades de medios](https://github.com/adobe/xdm/pull/1626/files) en varios tipos de datos para mantener la coherencia. |
| Tipo de datos | [[!UICONTROL Detalles de implementación]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Se han añadido nombres conocidos para flutter. |
| Tipo de datos | [[!UICONTROL Detalles del punto de interés]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | El tipo de datos ahora puede aceptar una lista de pares de clave-valor de metadatos asociados con el punto de interés. |
| Tipo de datos | [[!UICONTROL Acción de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Se cambió el nombre de [!DNL AJO Classification Fields] a [!UICONTROL Acción de propuesta]. |
| Tipo de datos | [[!UICONTROL Tipo de evento de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Se cambió el nombre de [!DNL AJO Classification Fields] a [!UICONTROL Acción de propuesta]. |
| (Múltiple) | (Múltiple) | Las propiedades experimentales se han [estabilizado en todos los componentes B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Múltiple) | (Múltiple) | Las entidades de Adobe Journey Optimizer se han [estabilizado](https://github.com/adobe/xdm/pull/1625/files). |
| (Múltiple) | (Múltiple) | Se han [actualizado las áreas de nombres de ciertos campos en varios componentes experimentales para mantener la coherencia](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [descripción general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente parezca tener varias &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la eliminación de conjuntos de datos | El servicio de identidad ahora admite la eliminación de conjuntos de datos al solicitar a través de la [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), la interfaz de usuario o la higiene de datos. Lea la guía sobre [eliminación de conjuntos de datos en la interfaz de usuario](../../catalog/datasets/user-guide.md#delete-a-dataset) para obtener más información. |

Para obtener más información acerca del servicio de identidad, lea la [descripción general del servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| API de suscripción de alerta | El servicio de consultas de Adobe Experience Platform le permite suscribirse a alertas para consultas ad hoc y programadas. Las alertas se pueden recibir por correo electrónico, en la interfaz de usuario de Experience Platform o en ambas. Actualmente, las alertas de consulta solo se pueden suscribir a mediante la [API del servicio de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Ejemplos de conjuntos de datos | Los ejemplos de conjuntos de datos del servicio de consultas permiten realizar consultas exploratorias de big data con un tiempo de procesamiento muy reducido a costa de la precisión de las consultas. Consulte la [guía de ejemplos de conjuntos de datos](../../query-service/key-concepts/dataset-samples.md) para obtener más información. |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../../query-service/home.md).

Consulte la [documentación de alertas de consulta](../../query-service/api/alert-subscriptions.md) para obtener más información.

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Impacto de la población de segmentos de Audience Manager en el perfil del cliente en tiempo real | La ingesta de poblaciones de segmentos de Audience Manager de tamaño considerable tiene un impacto directo en el recuento total de perfiles la primera vez que envía un segmento de Audience Manager a Experience Platform mediante la fuente de Audience Manager. Esto significa que la selección de todos los segmentos puede dar lugar potencialmente a un recuento de perfiles que supere el derecho de uso de la licencia. Para obtener más información, lea la [descripción general del origen de Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obtener información sobre el uso de la licencia, lea la documentación de [mediante el uso del tablero de licencias](../../dashboards/guides/license-usage.md). |
| Compatibilidad con Adobe Campaign Managed Cloud Service | Utilice la fuente de Cloud Service administrada por Adobe Campaign para llevar los datos de los registros de envío y seguimiento de la versión 8.4 de Adobe Campaign a Experience Platform. Lea la guía sobre [creación de una conexión de origen de Adobe Campaign Managed Cloud Service en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/campaign.md) para obtener más información. |
| Compatibilidad de API para la ingesta bajo demanda para orígenes por lotes | Utilice la ingesta bajo demanda para crear ejecuciones de flujo ad hoc para un flujo de datos determinado con la API [!DNL Flow Service]. Las ejecuciones de flujo creadas deben configurarse como ingestas únicas. Para obtener más información, lea la guía sobre [creación de una ejecución de flujo para la ingesta bajo demanda mediante la API](../../sources/tutorials/api/on-demand-ingestion.md). |
| Compatibilidad con API para reintentar ejecuciones de flujo de datos fallidas para orígenes por lotes | Utilice la operación `re-trigger` para reintentar el flujo de datos con errores a través de la API. Lea la guía sobre [reintentos de ejecuciones de flujo de datos con errores mediante la API](../../sources/tutorials/api/retry-flows.md) para obtener más información. |
| Compatibilidad con API para filtrar datos de nivel de fila para los orígenes [!DNL Google BigQuery] y [!DNL Snowflake] | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para los orígenes [!DNL Google BigQuery] y [!DNL Snowflake]. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |

Para obtener más información acerca de las fuentes, lea la [Información general de fuentes](../../sources/home.md).
