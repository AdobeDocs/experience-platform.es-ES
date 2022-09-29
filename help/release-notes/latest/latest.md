---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
source-git-commit: ea4d17459dcd7abd981260fe6733320b08af15e8
workflow-type: tm+mt
source-wordcount: '3124'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 28 de septiembre de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Control de acceso basado en atributos](#abac)
- [Higiene de los datos](#data-hygiene)
- [[!UICONTROL Consola de privacidad]](#privacy-console)

Actualizaciones de funciones existentes en Adobe Experience Platform:

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
>El control de acceso basado en atributos se habilitará a partir de octubre de 2022. Si desea ser uno de los primeros en adoptarlo, póngase en contacto con su representante del Adobe.

El control de acceso basado en atributos es una capacidad de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad buena flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a las funciones de usuario. Esta función le permite conceder o revocar acceso a objetos individuales para usuarios específicos de Platform de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a datos personales confidenciales (SPD), información de identificación personal (PII) y otro tipo personalizado de datos en todos los flujos de trabajo y recursos de Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que se correspondan con esos campos.

| Función | Descripción |
| --- | --- |
| Control de acceso basado en atributos | El control de acceso basado en atributos le permite etiquetar campos de esquema y segmentos del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos de uso de datos o de organización. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir políticas de acceso que cubran los campos y segmentos del esquema XDM para administrar mejor el acceso dado a los usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Para obtener más información, consulte la [información general sobre el control de acceso basado en atributos](../../access-control/abac/overview.md). |
| Permisos | Los permisos son el área del Experience Cloud en la que los administradores pueden definir funciones de usuario y políticas de acceso para administrar los permisos de acceso a funciones y objetos dentro de una aplicación de producto. Mediante Permisos, puede crear y administrar funciones, asignar los permisos de recursos deseados para estas funciones y crear políticas para aprovechar las etiquetas y definir qué funciones de usuario tienen acceso a recursos de Platform específicos. Los permisos también le permiten administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica. Para obtener más información, consulte la [Guía de la interfaz de usuario de permisos](../../access-control/abac/ui/browse.md). |

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general sobre el control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo del control de acceso basado en atributos, lea la [guía de extremo a extremo de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## Higiene de los datos {#data-hygiene}

Adobe Experience Platform proporciona un robusto conjunto de herramientas para administrar operaciones de datos grandes y complicadas con el fin de orquestar las experiencias de los consumidores. A medida que los datos se incorporan al sistema a lo largo del tiempo, cada vez es más importante administrar los almacenes de datos para que se utilicen como se espera, se actualicen cuando sea necesario corregir los datos incorrectos y se eliminen cuando las políticas organizativas lo consideren necesario.

Las funciones de higiene de datos de Adobe Experience Platform le permiten limpiar sus datos mediante la programación de caducidades automatizadas de conjuntos de datos y la eliminación programada de datos de consumidores por identidad.

>[!IMPORTANT]
>
>Las funciones de higiene de los datos solo están disponibles para las organizaciones que han adquirido Adobe Healthcare Shield o Privacy Shield.

Consulte la siguiente documentación para empezar a trabajar con la higiene de los datos:

- [Resumen de higiene de datos](../../hygiene/home.md): Conozca los conceptos básicos sobre las capacidades de higiene de datos de Platform.
- [[!UICONTROL Higiene de los datos] Guía de la interfaz de usuario](../../hygiene/ui/overview.md): Obtenga información sobre cómo programar caducidades de conjuntos de datos y solicitudes de eliminación de consumidores dentro de la interfaz de usuario de Platform.
- [Guía de API de higiene de datos](../../hygiene/api/overview.md): Todas las actividades de higiene de datos que se pueden realizar en la interfaz de usuario también se pueden programar

## [!UICONTROL Consola de privacidad] {#privacy-console}

La variable [!UICONTROL Consola de privacidad] en la interfaz de usuario del Experience Platform, se proporciona una vista de panel de información clave sobre funciones relacionadas con la privacidad, como [solicitudes del interesado del Privacy Service](../../privacy-service/home.md), [órdenes de trabajo de higiene de datos](../../hygiene/home.md)y [registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md). La consola también proporciona varias guías de casos de uso dentro del producto para ayudarle a guía a través de flujos de trabajo de privacidad comunes.

Consulte la [Información general de la Consola de privacidad](../../landing/governance-privacy-security/privacy-console.md) para obtener más información sobre la función.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Los servicios AI/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren modelos específicos de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar una configuración de modelo como una instancia de borrador y seguir editándola hasta que se complete antes de la formación y la puntuación. Los escenarios en los que esta función es útil incluyen, cuando un usuario tiene varios campos para definir en el flujo de trabajo, pero no puede completarlo debido a limitaciones de tiempo. Otro escenario es cuando se procesan una o más estadísticas del conjunto de datos y aún no están disponibles. Lea el [Guía del usuario del Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) para obtener más información. |
| Políticas de gobernanza | Una vez que los usuarios se envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de directiva en el uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing cumplan las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre la Attribution AI, la variable [Información general sobre la Attribution AI](../../intelligent-services/attribution-ai/overview.md). Para obtener información sobre las políticas de control de datos, lea la [información general sobre políticas](../../data-governance/policies/overview.md).

### Customer AI

La AI del cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar una configuración de modelo como una instancia de borrador y seguir editándola hasta que se complete antes de la formación y la puntuación. Los escenarios en los que esta función es útil incluyen, cuando un usuario tiene varios campos para definir en el flujo de trabajo, pero no puede completarlo debido a limitaciones de tiempo. Otro escenario es cuando se procesan una o más estadísticas del conjunto de datos y aún no están disponibles. Lea el [Guía del usuario de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) para obtener más información. |
| Políticas de gobernanza | Una vez que los usuarios se envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de directiva en el uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing cumplan las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre Customer AI, lea la [Información general sobre Customer AI](../../intelligent-services/customer-ai/overview.md). Para obtener información sobre las políticas de control de datos, lea la [información general sobre políticas](../../data-governance/policies/overview.md).

## Registros de auditoría {#audit-logs}

Experience Platform le permite auditar la actividad de los usuarios en relación con diversos servicios y funcionalidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Funciones actualizadas**

| Función | Nombre | Descripción |
| --- | --- | --- |
| Recursos añadidos | <ul><li>instancia de Attribution AI</li><li>Instancia de Customer AI</li><li>Datastream</li></ul> | Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad. Si la función está habilitada, no es necesario habilitar manualmente la recopilación de registros. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los distintos tipos de eventos específicos de recursos rastreados por los registros de auditoría en Platform, consulte la [información general sobre registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| Etiqueta en uso | Cuando se ve en la biblioteca de utilidades, la etiqueta en uso identifica fácilmente la presencia de utilidades existentes en el panel. Esto facilita evitar la duplicación, aunque aún puede añadir el mismo widget más de una vez si lo desea. |
| Tableros definidos por el usuario | Los tableros definidos por el usuario ayudan a acelerar las perspectivas y a personalizar las visualizaciones, ya que le permiten crear y administrar tableros personalizados. Con los tableros definidos por el usuario, puede crear, agregar y editar widgets personalizados para visualizar métricas clave relevantes para su organización. Lea el [guía de funciones](../../dashboards/user-defined-dashboards.md) para obtener más información. |
| Modelo de datos de Customer Data Platform Insights | La función Modelo de datos de perspectivas de la plataforma de datos del cliente (CDP) expone los modelos de datos y SQL que alimentan la información de varios widgets de perfil, destino y segmentación. Puede personalizar estas plantillas de consulta SQL para crear informes CDP para sus casos de uso de indicadores de rendimiento clave y de marketing. Estas perspectivas se pueden utilizar como utilidades personalizadas para los tableros definidos por el usuario. Lea el [Guía de funciones del Modelo de datos de CDP Insights](../../dashboards/cdp-insights-data-model.md) para obtener más información. |
| Widget de informes de superposición de audiencia | Esta utilidad está disponible para ambas [!UICONTROL Perfiles] y [!UICONTROL Segmentos] tableros. El informe proporciona una lista ordenada de audiencias clasificadas según los porcentajes de superposición más altos o más bajos del segmento elegido. En el [!UICONTROL Perfiles] tablero puede filtrar y ver la superposición de audiencias combinando la política de todos los segmentos disponibles. La variable [!UICONTROL Segmentos] los tableros le permiten filtrar la superposición de audiencias por un segmento específico.<br>Utilice este análisis para generar nuevos segmentos de alto rendimiento y evitar enviar la misma audiencia a diferentes destinos. El informe también ayuda a identificar perspectivas ocultas para mejorar la segmentación o localizar perfiles únicos para perseguir. Lea las [perfiles](../../dashboards/guides/profiles.md#audience-overlap-report) y [segmentos](../../dashboards/guides/segments.md#audience-overlap-report) guías del widget para obtener más información. |

Para obtener más información, consulte [!DNL Dashboards], consulte la [[!DNL Dashboards] información general](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Integración de navegación izquierda en la interfaz de usuario de Platform | Todas las funciones que anteriormente eran exclusivas de la interfaz de usuario de recopilación de datos (incluidas las etiquetas, el reenvío de eventos y los conjuntos de datos) ahora están disponibles en la navegación izquierda del Experience Platform, en la categoría **[!UICONTROL Recopilación de datos]**. Esto elimina la necesidad de cambiar entre las IU al trabajar con capacidades de recopilación de datos en Platform. |
| Atribución de usuario en etiquetas y reenvío de eventos | Cuando la lista esté disponible [!UICONTROL Propiedades] en las etiquetas y el reenvío de eventos, cada propiedad enumerada ahora muestra cuándo se actualizó por última vez y qué usuario realizó la actualización. |
| [[!DNL User-Agent Client Hints] en el SDK web](../../edge/fundamentals/user-agent-client-hints.md) | El SDK web ahora es compatible [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Las sugerencias del cliente permiten a los propietarios de sitios web acceder a gran parte de la misma información disponible en la [!DNL User-Agent] cadena, pero de una forma más preservada de la privacidad. |
| [Migración de SDK web página por página](../../edge/home.md#migrating-to-web-sdk) | Ahora puede migrar las propiedades web existentes de otras bibliotecas de Experience Cloud, como [!DNL at.js], al SDK web, de una página a la vez. Esto permite un enfoque por fases de la migración del SDK web, sin necesidad de migrar todas las páginas a la vez. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Para obtener más información sobre la recopilación de datos en Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| SDK de destino | Ahora, Destination SDK ofrece compatibilidad total con socios y clientes que crean destinos productivos o privados por lotes (o basados en archivos). Lea las siguientes páginas de documentación para obtener más información: <ul><li>[Información general del Destination SDK](/help/destinations/destination-sdk/overview.md)</li><li>[Configuración de un destino basado en archivos](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Configurar las opciones de formato de archivo para destinos basados en archivos](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Probar los destinos basados en archivos](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Destinos nuevos o actualizados**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services proporciona una plataforma para diseñar experiencias de clientes en canales múltiples y un entorno para la organización de campañas visuales, la administración de interacciones en tiempo real y la ejecución en canales cruzados. [Introducción a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Tenga en cuenta que esta integración funciona con Adobe Campaign versión 8.4 o superior. La versión 8.4 está programada para el 30 de septiembre de 2022. |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | La variable [!DNL Salesforce CRM] el destino se ha actualizado para admitir actualizaciones de contactos y posibles clientes, así como mejoras de rendimiento para actualizaciones más rápidas. |

{style=&quot;table-layout:auto&quot;}

**Documentación nueva o actualizada**

| Documentación | Descripción |
| ----------- | ----------- |
| Documentación de la API del servicio de flujo de destinos | La variable [Documentación de referencia de la API de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) se ha actualizado para incluir instrucciones sobre cómo realizar operaciones en destinos basados en archivos. Las operaciones para los destinos de flujo continuo se agregarán más adelante. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad de la interfaz de usuario con enumeraciones y valores sugeridos | Además de las enumeraciones que habilitan la validación de datos, ahora puede [agregar o eliminar valores sugeridos](../../xdm/ui/fields/enum.md) para campos de cadena estándar o personalizados, de modo que los usuarios de Platform tengan una lista de valores descriptivos que se pueden seleccionar al crear segmentos. |

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos de clasificación AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Propiedades de un elemento específico con el que se interactuó que activó el evento de propuesta. |
| Grupo de campos | [[!UICONTROL Detalles de interacción de MediaAnalytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Rastrea interacciones de medios a lo largo del tiempo. |
| Grupo de campos | [[!UICONTROL Información detallada de contenidos]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Realiza un seguimiento de la información detallada del contenido. |
| Grupo de campos | [[!UICONTROL Adobe CJM ExperienceEvent - Superficies]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Describe las superficies de los eventos de experiencia en Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Comportamiento | [[!UICONTROL Serie temporal]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Valores añadidos para `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Se han eliminado los valores de `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Grupo de campos | (Múltiple) | [Se han actualizado varias descripciones de campo](https://github.com/adobe/xdm/pull/1628/files) en los componentes del Journey Orchestration. |
| Grupo de campos | (Múltiple) | [Se han actualizado los títulos de varios componentes de Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) para mantener la coherencia. |
| Grupo de campos | [[!UICONTROL Campos de clasificación AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Se han actualizado las áreas de nombres de varios campos a `xdm`. |
| Grupo de campos | [[!UICONTROL Campos comunes de eventos de los pasos del Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Se ha añadido un nuevo campo, `isReadSegmentTriggerStartEvent`. |
| Grupo de campos | [[!UICONTROL Tiempo previsto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Se ha cambiado la variable `xdm:uvIndex` campo a un tipo entero y añadió la variable `xdm` área de nombres de varios campos en los que faltaba. |
| Grupo de campos | [[!UICONTROL Información detallada de contenidos]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` y `xdm:implementationDetails` se han eliminado del grupo de campos. |
| Tipo de datos | (Múltiple) | [Se han actualizado varios nombres de propiedades de medios](https://github.com/adobe/xdm/pull/1626/files) en varios tipos de datos para mantener la coherencia. |
| Tipo de datos | [[!UICONTROL Detalles de implementación]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Se agregaron nombres conocidos para la herramienta de flutter. |
| Tipo de datos | [[!UICONTROL Detalles del punto de interés]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | El tipo de datos ahora puede aceptar una lista de pares de clave-valor de metadatos asociados al punto de interés. |
| Tipo de datos | [[!UICONTROL Acción de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] se ha cambiado el nombre a [!UICONTROL Acción de propuesta]. |
| Tipo de datos | [[!UICONTROL Tipo de evento de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] se ha cambiado el nombre a [!UICONTROL Acción de propuesta]. |
| (Múltiple) | (Múltiple) | Se han utilizado propiedades experimentales [estabilizado en todos los componentes B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Múltiple) | (Múltiple) | Las entidades de Adobe Journey Optimizer se han [estabilizado](https://github.com/adobe/xdm/pull/1625/files). |
| (Múltiple) | (Múltiple) | Las áreas de nombres de ciertos campos en varios componentes experimentales se han [actualizado para mantener la coherencia](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente parezca tener múltiples &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales y impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la eliminación de conjuntos de datos | El servicio de identidad ahora admite la eliminación de conjuntos de datos al solicitar a través de la variable [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), la interfaz de usuario o la higiene de los datos. Lea la guía de [eliminación de conjuntos de datos en la interfaz de usuario](../../catalog/datasets/user-guide.md#delete-a-dataset) para obtener más información. |

Para obtener más información sobre el servicio de identidad, lea la [Información general del servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| API de suscripción de alerta | El servicio de consulta de Adobe Experience Platform le permite suscribirse a las alertas para consultas ad hoc y programadas. Las alertas se pueden recibir por correo electrónico, en la interfaz de usuario de Platform o en ambos. Actualmente, las alertas de consulta solo se pueden suscribir a mediante el uso de [API del servicio de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/). Consulte la [documentación de alertas de consulta](../../query-service/api/alert-subscriptions.md) para obtener más información. |
| Ejemplos de conjuntos de datos | Los ejemplos de conjuntos de datos del servicio de consulta le permiten realizar consultas exploratorias sobre grandes datos con un tiempo de procesamiento considerablemente reducido al coste de la precisión de la consulta. Consulte la [guía de muestras de conjuntos de datos](../../query-service/sql/dataset-samples.md) para obtener más información. |

Para obtener más información, consulte [!DNL Query Service], consulte la [[!DNL Query Service] información general](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Impacto de la población del segmento del Audience Manager en el perfil del cliente en tiempo real | La ingesta de grandes poblaciones de segmentos de Audience Manager tiene un impacto directo en el recuento total de perfiles cuando envía por primera vez un segmento de Audience Manager a Platform mediante la fuente de Audience Manager. Esto significa que si selecciona todos los segmentos, es posible que se produzca un recuento de perfiles superior a su derecho de uso de licencia. Para obtener más información, lea la [Información general de la fuente del Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obtener información sobre el uso de las licencias, consulte la documentación de [uso del panel de uso de licencias](../../dashboards/guides/license-usage.md). |
| Compatibilidad con el Cloud Service administrado de Adobe Campaign | Utilice la fuente del Cloud Service administrado de Adobe Campaign para llevar los datos de envío y registro de seguimiento de Adobe Campaign v8.4 al Experience Platform. Lea la guía de [creación de una conexión de origen de Adobe Campaign Managed Cloud Service en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/campaign.md) para obtener más información. |
| Compatibilidad de API para la ingesta bajo demanda de orígenes por lotes | Utilice la ingesta bajo demanda para crear ejecuciones de flujo ad hoc para un flujo de datos determinado con la variable [!DNL Flow Service] API. Las ejecuciones de flujo creadas deben establecerse en ingesta única. Para obtener más información, consulte la guía de [creación de una ejecución de flujo para la ingesta bajo demanda mediante la API](../../sources/tutorials/api/on-demand-ingestion.md) para obtener más información. |
| Compatibilidad de API para reintentar ejecuciones de flujo de datos fallidas para orígenes por lotes | Utilice la variable `re-trigger` para reintentar el flujo de datos fallido mediante la API. Lea la guía de [volver a intentar ejecutar el flujo de datos fallido mediante la API](../../sources/tutorials/api/retry-flows.md) para obtener más información. |
| Compatibilidad API para filtrar datos de nivel de fila para la variable [!DNL Google BigQuery] y [!DNL Snowflake] sources | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para la variable [!DNL Google BigQuery] y [!DNL Snowflake] fuentes. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).