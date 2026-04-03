---
title: 'Notas de la versión de Adobe Experience Platform: abril de 2022'
description: Las notas de la versión de abril de 2022 de Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 82e41af32468febeda2dce6b471d72ef74359ea9
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 20%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: jueves, 27 de abril de 2022**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Flujos de datos](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [Fuentes](#sources)

## [!DNL Dashboards] {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

Los paneles proporcionan opciones de informes preconfiguradas para los datos de su organización y están integrados directamente en el flujo de trabajo del experto en marketing dentro de Experience Platform. Estos paneles están disponibles sin necesidad de soporte de TI adicional ni el tiempo y esfuerzo que, de lo contrario, tomaría exportar y procesar los datos con el diseño y la implementación de almacenamiento de datos adicional.

Los siguientes widgets están disponibles a través de la biblioteca Widget en sus respectivos paneles. Consulte la documentación para obtener más información sobre [cómo agregar widgets a través de la biblioteca de widgets](../../dashboards/customize/widget-library.md).

**Nuevos widgets**

| Widget | Panel de control | Descripción |
| ------ | --------- | ----------- |
| [!UICONTROL Profiles added trend] | Perfiles | Este widget utiliza un gráfico de líneas para ilustrar el número total de perfiles combinados que se han agregado al almacén de perfiles diariamente en los últimos 30 días, 90 días o 12 meses. |
| [!UICONTROL Audiences mapped to destination status] | Perfiles | Este widget muestra el número total de audiencias asignadas y no asignadas en una sola métrica y utiliza un gráfico de anillos para ilustrar la diferencia proporcional entre sus totales. |
| [!UICONTROL Audiences size] | Perfiles | Este widget proporciona una tabla de dos columnas que enumera hasta 20 segmentos y el número total de audiencias que contiene cada segmento. La lista depende de la política de combinación aplicada y se ordena de alta a baja según el número total de audiencias. |
| [!UICONTROL Profile count trend] | Perfiles | Este widget utiliza un gráfico de líneas para ilustrar la tendencia en el número total de perfiles contenidos en el sistema a lo largo del tiempo. Los datos se pueden visualizar en períodos de 30 días, 90 días y 12 meses. |
| [!UICONTROL Single identity profiles by identity] | Perfiles | Este widget utiliza un gráfico de barras para ilustrar el número total de perfiles que se identifican con un solo identificador único. El widget admite hasta cinco de las identidades más comunes. |
| [!UICONTROL Destination status] | Destinos | Este widget muestra el número total de destinos habilitados como una sola métrica y utiliza un gráfico de anillos para ilustrar la diferencia proporcional entre los destinos habilitados y deshabilitados. |
| [!UICONTROL Active destinations by destination platform] | Destinos | Este widget utiliza una tabla de dos columnas para mostrar una lista de las plataformas de destino activas y el número total de destinos activos para cada plataforma de destino. |
| [!UICONTROL Activated audiences across all destinations] | Destinos | Este widget proporciona el número total de audiencias activadas en todos los destinos en una sola métrica. |
| [!UICONTROL Audience activation order] | Segmentos | Este widget proporciona una tabla de tres columnas que enumera el nombre de destino, la plataforma y la fecha de activación de la audiencia. |
| [!UICONTROL Audience size trend] | Segmentos | Este widget proporciona una ilustración de gráfico de líneas para el número total de perfiles que cumplen los criterios de cualquier definición de segmento en períodos de 30 días, 90 días y 12 meses. |
| [!UICONTROL Audience size change trend] | Segmentos | Este widget proporciona un gráfico de líneas que ilustra la diferencia en el número total de perfiles aptos para un segmento determinado entre las instantáneas diarias más recientes. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. |
| [!UICONTROL Audience size trend by identity] | Segmentos | Este widget ilustra la tendencia del tamaño de la audiencia de un segmento en particular en función de un tipo de identidad seleccionado. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. |

**Nuevas funciones** {#new-features}

| Función | Panel de control | Descripción |
| ------- | --------- | ----------- |
| Limpieza de pertenencia a segmento de perfil huérfano | Perfiles y uso de licencias | El servicio de perfil ahora elimina diariamente los miembros de segmentos que quedan para proporcionar una representación más precisa de los perfiles del sistema. Esta limpieza se produce después de eliminar todos los fragmentos de perfil de un perfil determinado. Esto puede mostrar una caída en la métrica &quot;Audiencia direccionable&quot; en el panel de uso de licencias y puede mostrar una caída en la métrica &quot;Recuento de perfiles&quot; en el panel de perfiles, ya que estas métricas incluían fragmentos de segmentos que quedaban antes de esta versión. |

{style="table-layout:auto"}

Consulte la documentación para obtener más información sobre los paneles de [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md) y [[!DNL Segments]](../../dashboards/guides/audiences.md).

## Flujos de datos {#dataflows}

En Experience Platform, los datos se incorporan desde muchas fuentes diferentes, se analizan dentro del sistema y se activan en una amplia variedad de destinos. Experience Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia a los flujos de datos.

Los flujos de datos son una representación de los trabajos que mueven datos a través de Experience Platform. Estos flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, donde luego los utilizan el servicio de identidad y el perfil del cliente en tiempo real antes de activarse finalmente en destinos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Panel de segmentos | Ahora puede utilizar el panel de monitorización para monitorizar los flujos de datos de los segmentos. Para obtener más información, lea la guía de [supervisión de segmentos en la interfaz de usuario](../../dataflows/ui/monitor-audiences.md) |

Para obtener información más general sobre los flujos de datos, consulte la [descripción general de los flujos de datos](../../dataflows/home.md). Para obtener más información sobre la segmentación, consulte [descripción general de la segmentación](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la fuente de Adobe Analytics | La fuente de Adobe Analytics ahora admite funciones de preparación de datos, que le permiten asignar los datos del grupo de informes de Analytics a un esquema XDM de destino al crear un flujo de datos. Consulte el tutorial sobre [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad con la importación de reglas de asignación existentes | Ahora puede importar reglas de asignación de un flujo de datos existente para acelerar las configuraciones del flujo de datos y limitar los errores. Consulte el tutorial sobre [importación de reglas de asignación existentes](../../data-prep/ui/mapping.md) para obtener más información. |

Para obtener más información sobre [!DNL Data Prep], consulte la [[!DNL Data Prep] Información general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Conectores de destino empresariales avanzados | Ahora hay tres conectores de destino de empresa disponibles generalmente: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) y [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> La disponibilidad general de los conectores de destino empresariales incluye todas las funcionalidades ofrecidas anteriormente en la fase de Beta, entre otras: <ul><li>Nuevas funciones de autenticación, incluida la [firma de acceso compartido en los centros de eventos de Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) y más [tipos de autenticación](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens de portador, OAuth 2) en el destino de la API HTTP;</li><li>[Rellenar los datos de perfil históricos](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (enviando perfiles históricos calificados para el segmento la primera vez que se activó);</li><li>Las métricas de ejecución de flujo de datos ahora son compatibles con estos destinos;</li><li>[Metadatos de segmento adicionales](../../destinations/catalog/streaming/http-destination.md#destination-details) incluidos en la carga de datos, incluidos nombres de segmento y marcas de tiempo de segmento;</li><li>Compatibilidad con [direcciones IP estáticas](/help/destinations/catalog/streaming/ip-address-allow-list.md) para clientes que necesitan lista de permitidos con Experience Platform.</li></ul> |
| Alertas en contexto para flujos de datos de destino | Ahora puede [suscribirse a alertas](../../destinations/ui/alerts.md) al crear un flujo de datos de destino para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo de datos. Puede elegir recibir alertas en la interfaz de usuario de Experience Platform o por correo electrónico. |

### Proceso de lanzamiento de conectores de destino empresariales avanzados {#release-process-enterprise-destinations}

Para los destinos Amazon Kinesis, Azure Event Hubs y HTTP API, durante el proceso de lanzamiento (a partir del 27 de abril), verá la tarjeta de destino Beta anterior, así como la nueva tarjeta de destino disponible generalmente (GA) en el catálogo de destinos. Cualquier flujo de datos configurado por los clientes que utilizan los destinos beta se migrará en los próximos días a la versión GA del mismo destino. Esta migración debería completarse antes del final del día, el viernes 29 de abril. Los destinos de Beta seguirán estando visibles durante este breve período de tiempo y se etiquetarán como **Obsoletos**.

Si ha estado utilizando estos destinos en la fase de Beta, tenga en cuenta lo siguiente:

- Si ha estado anteriormente en Beta con cualquiera de los 3 destinos, no es necesario realizar ninguna acción. Todos los flujos de datos configurados como parte de Beta seguirán funcionando y se migrarán a la versión de GA.
- Si desea configurar estos destinos a partir del 27 de abril, hágalo con la nueva versión de GA de los destinos.
- Las tarjetas beta marcadas como obsoletas se eliminarán una vez que se complete la operación de lanzamiento, estimada para el final del día viernes, 29 de abril. El equipo de ingeniería de Experience Platform realiza un seguimiento atento para garantizar que la operación de lanzamiento se realice correctamente.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [!DNL Criteo] | Conectar y activar datos a la plataforma de publicidad [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md). |
| [!DNL Sendgrid] | Conecte y active datos a la plataforma [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) para correos electrónicos transaccionales y de marketing. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Agregar o quitar campos estándar individuales de un esquema | La interfaz de usuario del Editor de Esquemas ahora le permite agregar partes de grupos de campos estándar a los esquemas, lo que proporciona más flexibilidad para los campos que decide incluir sin necesidad de generar recursos personalizados desde cero.<br><br>Ahora también puede definir campos personalizados específicos directamente dentro de la estructura del esquema y asignarlos a un grupo de campos personalizados nuevo o existente sin necesidad de crear o editar el grupo de campos de antemano.<br><br>Consulte la guía sobre [creación y edición de esquemas en la interfaz de usuario](../../xdm/ui/resources/schemas.md) para obtener más información sobre estos nuevos flujos de trabajo. |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Registra los detalles de una solicitud de limpieza de datos para eliminar o modificar registros en un conjunto de datos o zona protegida especificados. |
| Descriptor | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularidad de los datos de series temporales y resumen. Cuando se aplica a un esquema, el campo `timestamp` del esquema es la primera marca de tiempo en un periodo de esta granularidad. |
| Clase | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Proporciona métricas resumidas previamente con dimensiones de agrupación, como los resultados de una SQL SELECT con un GROUP BY. |
| Grupo de campo | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Registra el resultado de la evaluación de la política de consentimiento de un individuo. |
| Grupo de campo | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Registra información relacionada con la búsqueda del sitio, como la consulta de búsqueda, el filtrado y el orden. |
| Grupo de campo | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Registra los detalles de un evento en el que se combinan dos o más posibles clientes. |
| Grupo de campo | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Registra los detalles de un evento en el que se envía un correo electrónico a un destinatario. |
| Grupo de campo | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Registra valores calculados a través del proceso de vinculación de identidad para un evento. |
| Grupo de campo | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Grupo de campos de Adobe Journey Optimizer que captura un detalle de destinatario secundario para una auditoría. |
| Grupo de campo | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Registra detalles relacionados con una relación cuenta-persona. |
| Grupo de campo | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Registra detalles relacionados con una relación cuenta-persona. |
| Tipo de datos | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Registra información sobre un carro de compras de comercio electrónico. |
| Tipo de datos | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Registra la información de envío de uno o más productos. |
| Tipo de datos | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Registra información sobre la actividad de búsqueda del sitio. |
| Extensión (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Registra detalles relacionados con una tarea operativa. |
| Extensión (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Registra detalles relacionados con un portafolio de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Registra detalles relacionados con un programa de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Registra detalles relacionados con un proyecto de trabajo. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuevos valores de enumeración para `destinationCategory`. |
| Descriptor | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Se agregó compatibilidad para eliminar los valores sugeridos (`meta:enum`) que no se necesitan en los campos estándar. |
| Grupo de campo | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo agregado. |
| Tipo de datos | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Se han añadido varios campos relacionados con el carro de compras. |
| Tipo de datos | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Se han añadido nuevos campos para las opciones seleccionadas y el importe de descuento. |
| Extensión (servicios inteligentes) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimizar el formato de almacenamiento para las puntuaciones de tiempo de envío. |
| Extensión (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Se reemplazaron varios campos por un campo `workfront:customData` para los campos de formulario personalizados. |
| Extensión (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Se han añadido varios campos. |
| Extensión (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuevos campos para el tipo de objeto principal y los campos de formulario personalizados. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

Los servicios de IA/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a analistas de marketing formular predicciones concretas de las necesidades de una compañía mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con varios conjuntos de datos | La función Varios conjuntos de datos ahora es compatible con todos los conjuntos de datos de evento de experiencia, así como con la selección del mapa de identidad como identidad. Los clientes pueden seleccionar el mapa de identidad y los ID asociados, siempre y cuando haya un área de nombres de identidad común en los conjuntos de datos. Inteligencia artificial aplicada a la atribución admite los siguientes esquemas: Adobe Analytics, Evento de experiencia, Evento de experiencia del consumidor. Para obtener más información sobre la compatibilidad con varios conjuntos de datos en la inteligencia artificial aplicada a la atribución, consulte la [guía del usuario de inteligencia artificial aplicada a la atribución](../../intelligent-services/attribution-ai/user-guide.md). |

Para obtener más información sobre [!DNL Intelligent Services], consulte la [[!DNL Intelligent Services] Información general](../../intelligent-services/home.md).

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente disponible en Real-Time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades empresariales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con varios conjuntos de datos | La función Varios conjuntos de datos ahora es compatible con todos los conjuntos de datos de evento de experiencia, así como con la selección del mapa de identidad como identidad. Los clientes pueden seleccionar el mapa de identidad y los ID asociados, siempre y cuando haya un área de nombres de identidad común en los conjuntos de datos. La inteligencia artificial aplicada al cliente admite los siguientes esquemas: Adobe Analytics, Evento de experiencia, Evento de experiencia del consumidor y el esquema de Adobe Audience Manager. Para obtener más información sobre la compatibilidad con varios conjuntos de datos en la inteligencia artificial aplicada al cliente, consulte la [guía del usuario de inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nuevas métricas de evaluación de modelos en Customer AI | Los nuevos gráficos de Ganancias de la inteligencia artificial aplicada al cliente permiten a los especialistas en marketing determinar el tamaño del grupo objetivo en función de su presupuesto y los objetivos de ROI. Los nuevos gráficos de alza miden la calidad del modelo, lo que proporciona una mejor visibilidad del alza que obtendrían sobre la segmentación aleatoria. Para obtener más información, consulte el documento [Discover insights with Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md). |

Para obtener más información sobre [!DNL Intelligent Services], consulte la [[!DNL Intelligent Services] Información general](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B Edition {#B2B}

Real-Time CDP edición B2B, que se creó en Real-time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a públicos específicos con precisión y captarlos en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la funcionalidad `isDeleted` | Todos los conjuntos de datos de [!DNL Marketo] excepto `Activities` ahora admiten la asignación de `isDeleted`. La nueva asignación se añade automáticamente a los flujos de datos B2B existentes. Puede usar la asignación `isDeleted` para filtrar los registros que se han eliminado de modo que los datos del [!DNL Data Lake] sean coherentes con los datos de origen. Consulte la [[!DNL Marketo] guía de asignación de campos](../../sources/connectors/adobe-applications/mapping/marketo.md) para obtener más información sobre `isDeleted`. |

Para obtener más información acerca de Real-Time Customer Data Platform B2B edition, consulte la [descripción general de B2B](../../rtcdp/b2b-overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con [!DNL OneTrust Integration] | Ahora puede usar el origen [!DNL OneTrust Integration] para ingerir datos de consentimiento y preferencias de su cuenta de [!DNL OneTrust] en Experience Platform. Consulte la documentación sobre [creación de una [!DNL OneTrust Integration] conexión de origen](../../sources/connectors/consent-and-preferences/onetrust.md) para obtener más información. |
| Compatibilidad con [!DNL Square] | Ahora puede usar el origen [!DNL Square] para ingerir datos de pagos de su cuenta de [!DNL Square] en Experience Platform. |
| Compatibilidad con la eliminación de flujos de datos de Atributos del cliente | Ahora puede eliminar flujos de datos creados con el conector de origen Atributos del cliente. |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
