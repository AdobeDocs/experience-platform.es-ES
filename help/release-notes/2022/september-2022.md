---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2022
description: Notas de la versión de septiembre de 2022 para Adobe Experience Platform.
source-git-commit: a3f12b9524d393441923cd11e09ed3e406814691
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 28 de septiembre de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Fuentes](#sources)

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

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Los servicios AI/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren modelos específicos de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar la configuración del modelo como una instancia de borrador durante las configuraciones y seguir editando el borrador hasta su finalización antes de la formación y la puntuación. Los escenarios en los que esta función es útil incluyen, entre otros, cuando los usuarios tienen varios campos para definir en el flujo de trabajo de configuración que no pueden completar de una sola vez o cuando una o más estadísticas del conjunto de datos (como la integridad de la columna) tardan un tiempo en procesarse antes de que estén disponibles. Lea el [Guía del usuario del Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) para obtener más información. |
| Políticas de gobernanza | Una vez que los usuarios se envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de directiva en el uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing cumplan las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre la Attribution AI, la variable [Información general sobre la Attribution AI](../../intelligent-services/attribution-ai/overview.md). Para obtener información sobre las políticas de control de datos, lea la [información general sobre políticas](../../data-governance/policies/overview.md).

### Customer AI

La AI del cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala.

| Función | Descripción |
| --- | --- |
| Guardar instancia de borrador | Esta nueva función permite a los analistas de marketing guardar la configuración del modelo como una instancia de borrador durante las configuraciones y seguir editando el borrador hasta su finalización antes de la formación y la puntuación. Los escenarios en los que esta función es útil incluyen, entre otros, cuando los usuarios tienen varios campos para definir en el flujo de trabajo de configuración que no pueden completar de una sola vez o cuando una o más estadísticas del conjunto de datos (como la integridad de la columna) tardan un tiempo en procesarse antes de que estén disponibles. Lea el [Guía del usuario de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md) para obtener más información. |
| Políticas de gobernanza | Una vez que los usuarios se envían para crear una instancia a través del flujo de trabajo de configuración, el nuevo servicio de aplicación de políticas comprueba si hay alguna infracción de directiva en el uso de datos y muestra los detalles en una ventana emergente. Garantiza que las operaciones de datos y las acciones de marketing cumplan las políticas de uso de datos configuradas en Adobe Experience Platform. |

Para obtener más información sobre Customer AI, lea la [Información general sobre Customer AI](../../intelligent-services/customer-ai/overview.md). Para obtener información sobre las políticas de control de datos, lea la [información general sobre políticas](../../data-governance/policies/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Impacto de la población del segmento del Audience Manager en el perfil del cliente en tiempo real | La ingesta de grandes poblaciones de segmentos de Audience Manager tiene un impacto directo en el recuento total de perfiles cuando envía por primera vez un segmento de Audience Manager a Platform mediante la fuente de Audience Manager. Esto significa que si selecciona todos los segmentos, es posible que se produzca un recuento de perfiles superior a su derecho de uso de licencia. Para obtener más información, lea la [Información general de la fuente del Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obtener información sobre el uso de las licencias, consulte la documentación de [uso del panel de uso de licencias](../../dashboards/guides/license-usage.md). |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).