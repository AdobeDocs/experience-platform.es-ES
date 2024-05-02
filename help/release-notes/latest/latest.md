---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión de abril de 2024 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 17%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: miércoles, 30 de abril de 2024**

>[!TIP]
>
>Utilice el [Glosario de Adobe Experience Platform](/help/landing/glossary.md) para familiarizarse con la terminología utilizada en Real-time Customer Data Platform y Adobe Experience Platform. Si no encuentra un término específico que esté buscando, utilice las opciones de comentarios de la página para solicitar que se añadan nuevos términos al glosario.

Actualizaciones de funciones existentes en Experience Platform:

- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Servicio de identidad](#identity-service)
- [Monitoreo](#monitoring)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Perspectivas de Real-time Customer Data Platform B2B | Explorar configuración previa [Perspectivas de datos de Real-Time CDP B2B sobre cuentas y oportunidades](../../dashboards/insights/account-profiles.md) para ayudarle a comprender sus datos e informar sus decisiones comerciales. También puede [cree sus propias perspectivas con el modelo de datos B2B de Real-Time CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) para visualizar y explorar los datos y guardar las visualizaciones personalizadas en el tablero. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos al Edge Network del Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Extensiones | [!DNL Acxiom Anonymous Visitor Insights] Extensión de etiquetas | Descubra de dónde provienen los visitantes de su sitio web con [!DNL Acxiom's Visitor Insights]. Al utilizar la tecnología de búsqueda de IP geográfica, Acxiom puede localizar la ubicación de navegadores anónimos. Una vez identificados, una búsqueda en la base de datos organizada genera perspectivas adicionales que se devuelven al explorador. Por lo tanto, los creadores de contenido pueden adaptar su contenido para que coincida con estos puntos de datos, lo que proporciona una experiencia más personalizada y atractiva para los visitantes, incluso si empezaron siendo desconocidos. |
| Secuencias de datos | [detección de bots de Edge Network](../../datastreams/bot-detection.md) | El tráfico proveniente de entidades no humanas, como programas automatizados, raspadores web, arañas web o escáneres de secuencias de comandos, puede dificultar la identificación de eventos que ocurren desde visitantes humanos. Este tipo de tráfico puede afectar negativamente a métricas comerciales importantes, lo que provoca informes de tráfico incorrectos. <br>La detección de bots permite identificar eventos generados por el [SDK web](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) y [[!DNL Server API]](../../server-api/overview.md) generadas por arañas web y bots conocidos. Al configurar la detección de bots para sus flujos de datos, puede identificar direcciones IP específicas, intervalos de IP y encabezados de solicitud que desee clasificar como eventos de bots. <br> La identificación del tráfico de bots puede proporcionar una medición más precisa de la actividad del usuario en el sitio o la aplicación móvil. |
| SDK móvil | Versión principal | Se han lanzado nuevas versiones principales del SDK móvil para las plataformas siguientes: iOS Mobile Core 5.x y extensiones de iOS compatibles, Android Mobile Core 3.x y extensiones de Android compatibles, React Native Core 6.x y extensiones de React Native compatibles, Flutter Core 4.x y extensiones de Flutter compatibles. Estas versiones proporcionan varias funciones y mejoras nuevas, incluida la compatibilidad con el SDK para Android para Jetpack Compose, la compatibilidad con experiencias basadas en código de Adobe Journey Optimizer y la disponibilidad general de la extensión de mensajería de Adobe Journey Optimizer para Flutter. Para ver notas de la versión más detalladas, consulte [Notas de la versión de Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK móvil | Privacidad | Debido a la actualización de la política de Apple, a partir del 1 de mayo de 2024, los desarrolladores deben implementar nuevas funciones de privacidad para enviarlas a App Store. Todos los clientes de Adobe que utilicen el SDK móvil deberán actualizar a la versión 5.x del SDK si desean recibir la aprobación de App Store después del 1 de mayo. |
| SDK de Roku | SDK de Roku | La primera versión principal del SDK de Roku se ha lanzado con compatibilidad con medios de streaming para el Edge Network de Platform. |
| Reenvío de eventos y etiquetas | Guía interna del producto | Experience Platform [Etiquetas](../../tags/home.md) y [Reenvío de eventos](../../tags/ui/event-forwarding/overview.md) ofrezca una nueva gama de experiencias que le ayudarán a empezar rápidamente y a disfrutar de un tiempo de valor rápido. Estas experiencias incluyen nuevas pantallas de incorporación, tutoriales del producto y consejos sobre herramientas. <br>![Reenvío de eventos con la guía del producto resaltada.](../2024/assets/april/event-forwarding.png "Editor de esquemas con los campos Tipo y Tipo de valor de asignación resaltados."){width="100" zoomable="yes"}<br> |
| SDK web | Simplificación de la adopción del SDK web para clientes Audience Manager | Varias actualizaciones del SDK web ahora simplifican la adopción del SDK web sin utilizar el modelo de datos de experiencia (XDM) para soluciones de Experience Cloud, como Audience Manager, Analytics y Target. Obtenga más información acerca de la adopción del SDK web de Audience Manager en las siguientes guías: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Actualice la biblioteca de recopilación de datos para el Audience Manager de la extensión de etiqueta de Audience Manager a la extensión de etiqueta del SDK web</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Actualice la biblioteca de recopilación de datos para Audience Manager de la biblioteca JavaScript de AppMeasurement a la biblioteca JavaScript del SDK web</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Para obtener más información sobre las colecciones de datos, lea la [resumen de recopilación de datos](../../collection/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| `isRequired` el parámetro ya está disponible para campos de datos de cliente anidados en Destination SDK | Al configurar un destino en Destination SDK, ahora puede [establezca los campos de datos de cliente anidados según sea necesario](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). De este modo, los usuarios que configuren el destino no pueden continuar con su flujo de activación hasta que seleccionen un valor para ese campo. |
| La segmentación de Edge ya no es un requisito obligatorio al configurar un destino de Adobe Target con SDK web | Anteriormente, al configurar un [Adobe Target destination](/help/destinations/catalog/personalization/adobe-target-connection.md) con el SDK web, la secuencia de datos tenía que habilitarse para la personalización y la segmentación de Edge. El requisito de que la secuencia de datos esté habilitada para la segmentación de Edge [ahora se ha eliminado](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Tenga en cuenta que este patrón de integración solo le permite beneficiarse de un subconjunto de casos de uso de personalización al utilizar Adobe Target con Real-Time CDP. Más información sobre la [casos de uso habilitados por tipo de integración](/help/destinations/catalog/personalization/adobe-target-connection.md#parameters). |
| [!BADGE Beta]{type=Informative} Eliminar varias audiencias y conjuntos de datos de los flujos de activación | Ahora puede seleccionar y eliminar varias audiencias y conjuntos de datos de los flujos de activación de destino. Consulte la [detalles del destino](../../destinations/ui/destination-details-page.md#bulk-remove) y [exportación de conjuntos de datos](../../destinations/ui/export-datasets.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de identidad {#identity-service}

Utilice el servicio de identidad de Adobe Experience Platform para crear una vista completa de sus clientes y sus comportamientos mediante la fusión de identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Obsolescencia del `/orgs/{ORG}/` puntos finales en la API | Los siguientes extremos en la variable [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) se han desaprobado:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Puede usar el `/idnamespace/identities` y el `/idnamespace/identities/{ID}` extremos para realizar las mismas tareas y recuperar todas las áreas de nombres de una organización o un área de nombres específica de una organización. |

{style="table-layout:auto"}

Para obtener más información sobre el servicio de identidad, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## Monitoreo {#monitoring}

Utilice el panel de monitorización de la IU de Experience Platform para monitorizar el recorrido de los datos de las fuentes, el servicio de identidad, el perfil del cliente en tiempo real, las audiencias y los destinos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Monitorización de la expansión de tableros | Ahora puede utilizar el tablero de monitorización para diferentes tipos de datos en función de su caso práctico comercial. Utilice el panel de monitorización para monitorizar las actividades de tipo de datos de persona, cuenta y cliente potencial en fuentes, audiencias y destinos. |

{style="table-layout:auto"}

Para obtener más información, lea la guía de [uso del panel de monitorización](../../dataflows/ui/monitor.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos de [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para usar en sistema de informes, espacio de trabajo de ciencia de datos o para su inserción en el perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Cuarentena de consultas | Aísle automáticamente las ejecuciones de consulta fallidas para evitar interrupciones y mantener un rendimiento coherente. Consulte la [cuarentena de consultas](../../query-service/ui/query-schedules.md#quarantine) para obtener más información. |
| Cancelar consulta | Tome el control de la ejecución de consultas y mejore su productividad cancelando consultas de larga duración. Consulte la [cancelar consulta](../../query-service/ui/user-guide.md#cancel-query) para obtener más información. |
| Alertas de consulta programadas | Manténgase informado con notificaciones proactivas mientras planifica las consultas, lo que garantiza una administración eficiente y oportuna de las tareas. Puede [suscribirse a alertas al crear una consulta](../../query-service/ui/query-schedules.md#alerts-for-query-status) o mediante acciones en línea para consultas programadas existentes. Consulte la [suscripción a alertas con acciones en línea](../../query-service/ui/monitor-queries.md#alert-subscription) para obtener más información. |
| Navegación de consultas programadas mejorada | Navegue fácilmente entre plantillas de consulta y ejecuciones programadas para aumentar la productividad. Consulte la documentación sobre [ver ejecuciones de consulta programadas](../../query-service/ui/query-schedules.md#scheduled-query-runs) para obtener más información. |
| Salida de consulta extendida | Acceda a hasta 500 filas de resultados de consulta dentro de la consola para un análisis más profundo de los datos. Consulte la [recuento de resultados](../../query-service/ui/user-guide.md#result-count) para obtener más información. |
| Finalización del Editor de consultas heredadas | A partir del 30 de abril de 2024, el Editor de consultas mejorado se ha convertido en el editor predeterminado para todos los usuarios. El editor anterior dejará de usarse el 30 de mayo de 2024 y ya no estará disponible para su uso. Consulte la [Guía del usuario del Editor de consultas](../../query-service/ui/user-guide.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, vea la [Información general del servicio de consulta](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudarle a desarrollar aplicaciones de experiencia digital y hacer que evolucionen.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [Herramientas de la zona protegida](../../sandboxes/ui/sandbox-tooling.md) | Utilice las herramientas de zona protegida para [exportar](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) todos los tipos de objetos admitidos en un paquete de zona protegida completo y, a continuación, [importar](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) Haga clic en el paquete en varios entornos limitados para replicar las configuraciones de objeto. |

{style="table-layout:auto"}

Para obtener más información sobre los entornos limitados, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Función actualizada**

| Función | Descripción |
| ------- | ----------- |
| Estados del ciclo vital de audiencia | Los estados del ciclo vital de las audiencias se han optimizado para simplificar la administración del ciclo vital. Para obtener más información sobre estos estados de ciclo vital, lea la [Preguntas frecuentes sobre Segmentation Service](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Nuevas fuentes**

| Nuevas fuentes | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Utilice el [[!DNL PathFactory] origen](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) para integrar los datos de visitante, sesión y vista de página desde [!DNL PathFactory] al Experience Platform. Lea el [[!DNL PathFactory] descripción general](../../sources/connectors/marketing-automation/pathfactory.md) para obtener información sobre cómo empezar. |
| [!DNL Teradata Vantage] | Utilice el [[!DNL Teradata Vantage] origen](../../sources/tutorials/ui/create/databases/teradata-vantage.md) para introducir datos de entornos híbridos de varias nubes en Experience Platform. Lea el [[!DNL Teradata Vantage] descripción general](../../sources/connectors/databases/teradata-vantage.md) para obtener información sobre cómo empezar. |

{style="table-layout:auto"}

**Funciones nuevas y actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones de las direcciones IP para la inclusión en la lista de permitidos en VA7 | Las siguientes direcciones IP se han agregado a la lista de direcciones IP para agregarlas a su lista de permitidos de VA7 (Norteamérica): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Para obtener una lista completa de las direcciones IP que añadir a la lista de permitidos, lea la [Documento de lista de permitidos de direcciones IP](../../sources/ip-address-allow-list.md). |
| Compatibilidad con nuevos tipos de autenticación con [!DNL Azure Event Hubs] origen | Ahora puede conectar su [!DNL Event Hubs] de origen a Experience Platform mediante [!DNL Azure Active Directory Authentication] o [!DNL Scoped Azure Active Directory Authentication]. Lea la guía de [conectador [!DNL Event Hubs] al Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) para obtener más información. |
| Actualizaciones de [!DNL Data Landing Zone] recuperación de credenciales | Ahora puede utilizar el carril derecho en el espacio de trabajo de orígenes para recuperar su [!DNL Data Landing Zone] credenciales. Ahora también puede utilizar el carril derecho para actualizar las credenciales. Lea el [[!DNL Data Landing Zone] Guía de IU](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) para obtener más información. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
