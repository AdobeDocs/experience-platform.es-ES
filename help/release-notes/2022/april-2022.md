---
title: Notas de la versión de Adobe Experience Platform, abril de 2022
description: Notas de la versión de abril de 2022 para Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 27 de abril de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Flujos de datos](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Real-Time Customer Data Platform edición B2B](#B2B)
- [Fuentes](#sources)

## [!DNL Dashboards] {#dashboards}

Platform proporciona varios tableros a través de los cuales puede ver información importante sobre los datos de su organización, tal como se captura durante las instantáneas diarias.

Los tableros proporcionan opciones de informes preconfiguradas para los datos de su organización y están integrados directamente en el flujo de trabajo de los especialistas en marketing dentro de Platform. Estos tableros están disponibles sin necesidad de soporte de TI adicional o sin el tiempo y esfuerzo que de otro modo se necesitarían para exportar y procesar datos con diseño e implementación adicionales de almacenamiento de datos.

Las siguientes utilidades están disponibles a través de la biblioteca Widget en sus respectivos paneles. Consulte la documentación para obtener más información sobre [cómo añadir utilidades a través de la biblioteca de utilidades](../../dashboards/customize/widget-library.md).

**Nuevas utilidades**

| Widget | Panel | Descripción |
| ------ | --------- | ----------- |
| [!UICONTROL Tendencia añadida de perfiles] | Perfiles | Esta utilidad utiliza un gráfico de líneas para ilustrar el número total de perfiles combinados que se han agregado diariamente al Almacenamiento de perfiles durante los últimos 30 días, 90 días o 12 meses. |
| [!UICONTROL Audiencias asignadas al estado de destino] | Perfiles | Esta utilidad muestra el número total de audiencias asignadas y no asignadas en una única métrica y utiliza un gráfico de anillos para ilustrar la diferencia proporcional entre sus totales. |
| [!UICONTROL Tamaño de las audiencias] | Perfiles | Esta utilidad proporciona una tabla de dos columnas que enumera hasta 20 segmentos y el número total de audiencias contenidas en cada segmento. La lista depende de la política de combinación aplicada y ordenada de mayor a menor según el número total de audiencias. |
| [!UICONTROL Tendencia del recuento de perfiles] | Perfiles | Esta utilidad utiliza un gráfico de líneas para ilustrar la tendencia del número total de perfiles contenidos en el sistema a lo largo del tiempo. Los datos se pueden visualizar en períodos de 30 días, 90 días y 12 meses. |
| [!UICONTROL Perfiles de identidad únicos por identidad] | Perfiles | Esta utilidad utiliza un gráfico de barras para ilustrar el número total de perfiles identificados con un único identificador. La utilidad admite hasta cinco de las identidades más comunes. |
| [!UICONTROL Estado del destino] | Destinos | Este widget muestra el número total de destinos habilitados como una única métrica y utiliza un gráfico de anillos para ilustrar la diferencia proporcional entre los destinos habilitados y deshabilitados. |
| [!UICONTROL Destinos activos por plataforma de destino] | Destinos | Esta utilidad utiliza una tabla de dos columnas para mostrar una lista de plataformas de destino activas y el número total de destinos activos para cada plataforma de destino. |
| [!UICONTROL Audiencias activadas en todos los destinos] | Destinos | Esta utilidad proporciona el número total de audiencias activadas en todos los destinos en una única métrica. |
| [!UICONTROL Orden de activación de la audiencia] | Segmentos | Este widget proporciona una tabla de tres columnas que indica el nombre de destino, la plataforma y la fecha de activación de la audiencia. |
| [!UICONTROL Tendencia del tamaño de la audiencia] | Segmentos | Esta utilidad proporciona una ilustración de gráfico de líneas para el número total de perfiles que cumplen los criterios de cualquier definición de segmento durante 30 días, 90 días y 12 meses. |
| [!UICONTROL Tendencia del cambio de tamaño de la audiencia] | Segmentos | Esta utilidad proporciona un gráfico de líneas con la diferencia en la cantidad total de perfiles que cumplen los requisitos para un segmento determinado entre las instantáneas diarias más recientes. El período de análisis de tendencias se puede visualizar a lo largo de 30 días, 90 días y 12 meses. |
| [!UICONTROL Tendencia del tamaño de la audiencia por identidad] | Segmentos | Esta utilidad ilustra la tendencia del tamaño de la audiencia de un segmento concreto en función de un tipo de identidad seleccionado. El período de análisis de tendencias se puede visualizar a lo largo de 30 días, 90 días y 12 meses. |

**Nuevas funciones** {#new-features}

| Función | Panel | Descripción |
| ------- | --------- | ----------- |
| Limpieza de pertenencia a segmentos de perfil huérfano | Perfiles y uso de licencias | El servicio de perfil ahora elimina a los miembros del segmento que quedan diariamente para proporcionar una representación más precisa de sus perfiles en su sistema. Esta limpieza se produce después de que se eliminan todos los fragmentos de perfil de un perfil determinado. Esto puede mostrar una caída en la métrica &quot;Audiencia direccionable&quot; en el panel de uso de licencias y puede mostrar una caída en la métrica &quot;Recuento de perfiles&quot; en el panel de perfiles, ya que estas métricas incluían fragmentos de segmento sobrantes de esta versión. |

{style=&quot;table-layout:auto&quot;}

Consulte la documentación para obtener más información sobre [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)y [[!DNL Segments]](../../dashboards/guides/segments.md) tableros.

## Flujos de datos {#dataflows}

En Platform, los datos se incorporan de muchas fuentes diferentes, se analizan dentro del sistema y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia con flujos de datos.

Los flujos de datos son una representación de trabajos que mueven datos a través de Platform. Estos flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, donde el servicio de identidad y el perfil del cliente en tiempo real los utilizan antes de activarse finalmente en los destinos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Panel de segmentos | Ahora puede utilizar el panel de monitorización para monitorizar los flujos de datos de los segmentos. Para obtener más información, consulte la guía de [monitorización de segmentos en la interfaz de usuario](../../dataflows/ui/monitor-segments.md) |

Para obtener información más general sobre flujos de datos, consulte la [información general sobre flujos de datos](../../dataflows/home.md). Para obtener más información sobre la segmentación, consulte [información general sobre segmentación](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con orígenes Adobe Analytics | El origen de Adobe Analytics ahora admite las funciones de preparación de datos, que le permiten asignar los datos del grupo de informes de Analytics a un esquema XDM de destino al crear un flujo de datos. Consulte el tutorial en [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad con la importación de reglas de asignación existentes | Ahora puede importar reglas de asignación de un flujo de datos existente para acelerar las configuraciones del flujo de datos y limitar los errores. Consulte el tutorial en [importación de reglas de asignación existentes](../../data-prep/ui/mapping.md) para obtener más información. |

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Conectores de destino empresarial avanzados | Ahora hay tres conectores de destino empresariales disponibles: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)y [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> La disponibilidad general de los conectores de destino empresarial incluye todas las funciones ofrecidas anteriormente en la fase beta y más: <ul><li>Nuevas funciones de autenticación, incluidas [Firma de acceso compartido en centros de eventos de Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) y más [tipos de autenticación](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens de portador, OAuth 2) en el destino de la API HTTP;</li><li>[Rellenar datos de perfil históricos](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (envío de perfiles históricos cualificados para el segmento cuando se activa por primera vez);</li><li>Ahora se admiten métricas de ejecución de flujo de datos para estos destinos;</li><li>[Metadatos de segmentos adicionales](../../destinations/catalog/streaming/http-destination.md#destination-details) incluido en la carga útil de datos, incluidos los nombres de segmentos y las marcas de tiempo de los segmentos;</li><li>Compatibilidad con [direcciones IP estáticas](/help/destinations/catalog/streaming/ip-address-allow-list.md) para clientes que necesitan lista de permitidos de Experience Platform.</li></ul> |
| Alertas en contexto para flujos de datos de destino | Ahora puede [suscripción a alertas](../../destinations/ui/alerts.md) al crear un flujo de datos de destino, para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo de datos. Puede optar por recibir alertas en la interfaz de usuario del Experience Platform o por correo electrónico. |

### Proceso de versiones para conectores de destino empresarial avanzados {#release-process-enterprise-destinations}

Para los destinos de Amazon Kinesis, Azure Event Hubs y HTTP API durante el proceso de lanzamiento (a partir del 27 de abril), verá la tarjeta de destino Beta anterior, así como la nueva tarjeta de destino disponible de forma general (GA) en el catálogo de destinos. Los flujos de datos configurados por los clientes que utilicen los destinos beta se migrarán en los próximos días a la versión GA del mismo destino. Esta migración debería completarse finalmente antes del final del viernes 29 de abril. Los destinos Beta seguirán estando visibles durante este breve periodo de tiempo y etiquetados como **Obsoleto**.

Si ha estado utilizando estos destinos en la fase beta, tenga en cuenta lo siguiente:

- Si anteriormente ha estado en versión beta con cualquiera de los 3 destinos, no es necesario realizar ninguna acción. Todos los flujos de datos configurados como parte de Beta seguirán funcionando y se migrarán a la versión GA.
- Si desea configurar estos destinos a partir del 27 de abril, hágalo con la nueva versión GA de los destinos.
- Las tarjetas beta marcadas como obsoletas se eliminarán una vez finalizada la operación de lanzamiento, estimada para finales del viernes 29 de abril. El equipo de ingeniería del Experience Platform realiza un seguimiento atento para comprobar si la operación de lanzamiento se ha realizado correctamente.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [!DNL Criteo] | Conecte y active los datos en la [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) plataforma publicitaria. |
| [!DNL Sendgrid] | Conecte y active los datos en la [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) para correos electrónicos de marketing y transaccionales. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Adición o eliminación de campos estándar individuales para un esquema | La interfaz de usuario del Editor de esquemas ahora le permite añadir partes de grupos de campos estándar a sus esquemas, lo que proporciona más flexibilidad para los campos que elija incluir sin necesidad de crear recursos personalizados desde cero.<br><br>Ahora también puede definir campos personalizados específicos directamente dentro de la estructura de esquema y asignarlos a un grupo de campos personalizados nuevo o existente sin necesidad de crear o editar el grupo de campos de antemano.<br><br>Consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../xdm/ui/resources/schemas.md) para obtener más información sobre estos nuevos flujos de trabajo. |

{style=&quot;table-layout:auto&quot;}

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Solicitud de operación de higiene de datos]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Captura los detalles de una solicitud de limpieza de datos para eliminar o modificar registros en un conjunto de datos o simulador de pruebas especificado. |
| Descriptor | [[!UICONTROL Descriptor de granularidad de series temporales]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularidad de los datos de resumen y series temporales. Cuando se aplica a un esquema, el esquema `timestamp` es la primera marca de tiempo de un periodo de esta granularidad. |
| Clase | [[!UICONTROL Métricas de resumen de XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Proporciona métricas resumidas previamente con dimensiones de agrupación, como los resultados de un SQL SELECT con un GROUP BY. |
| Grupo de campos | [[!UICONTROL Mapa de resultados de evaluación de políticas de consentimiento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Captura el resultado de la evaluación de la directiva de consentimiento para un individuo. |
| Grupo de campos | [[!UICONTROL Búsqueda del sitio]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura la información relacionada con la búsqueda del sitio, como la consulta de búsqueda, el filtrado y el pedido. |
| Grupo de campos | [[!UICONTROL Combinar posibles clientes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Captura los detalles de un evento en el que se combinan dos o más posibles clientes. |
| Grupo de campos | [[!UICONTROL Correo electrónico enviado]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Captura los detalles de un evento en el que se envía un correo electrónico a un destinatario. |
| Grupo de campos | [[!UICONTROL Definición de campos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Captura valores calculados mediante el proceso de vinculación de identidad para un evento. |
| Grupo de campos | [[!UICONTROL Detalle del destinatario secundario para auditoría]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Grupo de campos de Adobe Journey Optimizer que captura un detalle de destinatario secundario para una auditoría. |
| Grupo de campos | [[!UICONTROL Detalles de relación de persona de cuenta comercial XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalles relacionados con una relación entre cuenta y persona. |
| Grupo de campos | [[!UICONTROL Detalles de la persona de la cuenta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalles relacionados con una relación entre cuenta y persona. |
| Tipo de datos | [[!UICONTROL Carro de compras]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Captura información sobre un carro de compras de comercio electrónico. |
| Tipo de datos | [[!UICONTROL Envío]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Captura la información de envío de uno o más productos. |
| Tipo de datos | [[!UICONTROL Búsqueda del sitio]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Captura información sobre la actividad de búsqueda de sitios. |
| Extensión (Workfront) | [[!UICONTROL Atributos de tarea operativa]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captura detalles relacionados con una tarea operativa. |
| Extensión (Workfront) | [[!UICONTROL Atributos del Portfolio de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Captura detalles relacionados con un portafolio de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Atributos del programa de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Captura detalles relacionados con un programa de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Atributos del proyecto de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Captura detalles relacionados con un proyecto de trabajo. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Destinos ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuevos valores de enumeración para `destinationCategory`. |
| Descriptor | [[!UICONTROL Descriptor de nombres descriptivos]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Se agregó compatibilidad para eliminar los valores sugeridos (`meta:enum`) que no son necesarios en los campos estándar. |
| Grupo de campos | [[!UICONTROL Proceso de inicio de sesión del usuario]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` se ha añadido. |
| Tipo de datos | [[!UICONTROL Comercio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Se han agregado varios campos relacionados con el carro de compras. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Se han añadido nuevos campos para las opciones seleccionadas y la cantidad de descuento. |
| Extensión (servicios inteligentes) | [[!UICONTROL Optimización del tiempo de envío de JourneyAI de servicios inteligentes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimizar el formato de almacenamiento para puntuaciones de tiempo de envío. |
| Extensión (Workfront) | [[!UICONTROL Evento de cambio de Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Varios campos se han sustituido por un `workfront:customData` para campos de formulario personalizados. |
| Extensión (Workfront) | [[!UICONTROL Atributos de tarea de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Se han añadido varios campos. |
| Extensión (Workfront) | [[!UICONTROL Objeto Work]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuevos campos para el tipo de objeto principal y campos de formulario personalizados. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

Los servicios AI/ML permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones concretas de las necesidades de una compañía mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con varios conjuntos de datos | La función Conjunto de datos múltiples ahora es compatible con todos los conjuntos de datos de Evento de experiencia, así como con la selección de Mapa de identidad como identidad. Los clientes pueden seleccionar el mapa de identidad y cualquier ID asociado siempre que haya un área de nombres de identidad común entre conjuntos de datos. Attribution AI admite los siguientes esquemas: Adobe Analytics, Evento De Experiencia, Evento De Experiencia Del Consumidor. Para obtener más información sobre la compatibilidad con Multi Dataset en Attribution AI, consulte la [Guía del usuario del Attribution AI](../../intelligent-services/attribution-ai/user-guide.md). |

Para obtener más información, consulte [!DNL Intelligent Services], consulte la [[!DNL Intelligent Services] información general](../../intelligent-services/home.md).

### Customer AI

La AI del cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con varios conjuntos de datos | La función Conjunto de datos múltiples ahora es compatible con todos los conjuntos de datos de Evento de experiencia, así como con la selección de Mapa de identidad como identidad. Los clientes pueden seleccionar el mapa de identidad y cualquier ID asociado siempre que haya un área de nombres de identidad común entre conjuntos de datos. Customer AI admite los siguientes esquemas: Adobe Analytics, Experience Event, Consumer Experience Event y el esquema de Adobe Audience Manager. Para obtener más información sobre la compatibilidad con Multi Dataset en Customer AI, consulte la [Guía del usuario de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nuevas métricas de evaluación de modelos en Customer AI | Los nuevos gráficos de ganancia en Customer AI permiten a los especialistas en marketing determinar el tamaño del grupo objetivo en función de sus objetivos de presupuesto y ROI. Los nuevos gráficos de alza miden la calidad del modelo, lo que proporciona una mejor visibilidad del alza que obtendrían sobre la orientación aleatoria. Para obtener más información, consulte la [descubra perspectivas con Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md) documento. |

Para obtener más información, consulte [!DNL Intelligent Services], consulte la [[!DNL Intelligent Services] información general](../../intelligent-services/home.md).

## Real-Time Customer Data Platform edición B2B {#B2B}

Basado en Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con `isDeleted` funcionalidad | Todo [!DNL Marketo] conjuntos de datos excepto `Activities` ahora admita el `isDeleted` asignación. La nueva asignación se agrega automáticamente a los flujos de datos B2B existentes. Puede usar la variable `isDeleted` asignación para filtrar los registros que se han eliminado para que sus datos en la [!DNL Data Lake] es coherente con los datos de origen. Consulte la [[!DNL Marketo] guía de campos de asignación](../../sources/connectors/adobe-applications/mapping/marketo.md) para obtener más información sobre `isDeleted`. |

Para obtener más información sobre Real-time Customer Data Platform B2B Edition, consulte la [Información general de B2B](../../rtcdp/b2b-overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con [!DNL OneTrust Integration] | Ahora puede usar la variable [!DNL OneTrust Integration] fuente para introducir datos de consentimiento y preferencias de su [!DNL OneTrust] a Platform. Consulte la documentación sobre [crear un [!DNL OneTrust Integration] conexión de origen](../../sources/connectors/consent-and-preferences/onetrust.md) para obtener más información. |
| Compatibilidad con [!DNL Square] | Ahora puede usar la variable [!DNL Square] fuente para introducir datos de pagos de su [!DNL Square] a Platform. |
| Compatibilidad con la eliminación de flujos de datos de Atributos del cliente | Ahora puede eliminar flujos de datos creados con el conector de origen de Atributos del cliente. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
