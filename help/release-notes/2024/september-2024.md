---
title: Notas de la versión de Adobe Experience Platform de septiembre de 2024
description: Las notas de la versión de septiembre de 2024 para Adobe Experience Platform.
source-git-commit: 33d1305aef7c763e7b0bd8c6db6a1a9417cc2a9d
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 24%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 24 de septiembre de 2024**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [Paneles](#dashboards)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de consultas](#query-service)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a diferentes reglas de alerta a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con zona protegida de desarrollo | Ahora puede [suscribirse a alertas](../../observability/alerts/ui.md) tanto en entornos limitados de producción como de desarrollo, lo que permite una supervisión perfecta en todos los entornos. |
| Plantillas de correo electrónico | [Las alertas por correo electrónico](../../observability/alerts/ui.md) ahora incluyen información detallada sobre los recursos, para asegurarte de tener todos los detalles clave al alcance de tu mano. |
| Personalización mejorada | Ahora puede configurar [umbrales de alerta](../../observability/alerts/ui.md#alert-threshold), lo que ofrece una mayor flexibilidad para adaptar las alertas a sus necesidades específicas para los siguientes tipos de alerta:<br><ul><li>Retraso del trabajo del segmento</li><li>Retraso de exportación de segmentos</li><li>Retraso de ejecución de flujo de destino</li><li>Retraso de ejecución de flujo de servicio de identidad</li><li>Retraso de ejecución de flujo de perfil</li><li>Retraso de ejecución de flujo de orígenes</li><li>Retraso de ejecución de consulta</li><li>Tasa de omisión de activación superada</li><li>Tasa de error de ingesta de fuentes superada</ul> |
| Alertas ampliadas | Las alertas de información de eventos de auditoría ya están disponibles para la suscripción de las siguientes [reglas de alerta](../../observability/alerts/rules.md):<br><ul><li>Creación de audiencia</li><li>Actualización de audiencia</li><li>Audience delete</li><li>Crear conjunto de datos</li><li>Actualización de conjuntos de datos</li><li>Eliminación de conjunto de datos</li><li>Creación de esquema</li><li>Actualización de esquema</li><li>Eliminación de esquema. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] descripción general](../../observability/home.md).

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Tabla de complementos de uso de licencias | Obtenga visibilidad granular sobre el uso de licencias y administre sus recursos de Platform con tablas dedicadas para productos principales y complementos. Rastree y analice métricas clave para cada producto principal con vistas de obtención de detalles en el nivel de zona protegida. Las métricas de complementos se integran perfectamente con las métricas de productos principales y ofrecen una vista completa del uso. La visibilidad mejorada le ayuda a optimizar la administración de licencias y a alinear los recursos con las necesidades de la organización. Consulte la [[!UICONTROL Guía de tablero para uso de licencias]](../../dashboards/guides/license-usage.md#overview-tab) para obtener más detalles. |
| Modo Query Pro: actualizaciones del filtro global | Mejore el análisis con el nuevo filtro de fechas del modo Query Pro. Refine las perspectivas con parámetros de fecha dinámicos en las consultas SQL y filtre los datos por intervalos de tiempo específicos. Elija intervalos de fechas preestablecidos o personalizados con una interfaz de usuario intuitiva, lo que mantiene los paneles relevantes para todos los usuarios. Simplifique los flujos de trabajo, mantenga la precisión y tome decisiones oportunas. Lea la [guía sobre la creación de filtros de fecha](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md) para obtener más información. |
| Modos de Query Pro: obtención de detalles | Desbloquee perspectivas más profundas con la función de obtención de detalles del modo Query Pro y navegue sin problemas desde gráficos de alto nivel a paneles detallados. Utilice esta función para pasar sin esfuerzo de resúmenes a análisis en profundidad y explorar tendencias, comportamientos de clientes y KPI. Los pasos de filtro automáticos y las perforaciones de varios niveles mantienen la homogeneidad de los datos, lo que garantiza una exploración sin problemas. Simplifique los flujos de trabajo, mantenga el contexto y acelere las decisiones. Lea la [guía paso a paso sobre la creación de obtención de detalles](../../dashboards/data-distiller/query-pro-mode/drill-through.md) para obtener más información. |
| Query Pro Mode: atributos de tabla avanzados | Utilice los atributos avanzados de tabla del modo Query Pro para optimizar la visualización de datos, mejorar la eficacia del flujo de trabajo y mejorar la claridad de los datos. Agregue ordenación automática, cambio de tamaño y paginación a las tablas directamente desde los paneles personalizados. Ordene columnas para priorizar los datos clave, cambiar el tamaño para obtener una legibilidad óptima y navegar por conjuntos de datos grandes sin problemas sin modificar las consultas SQL. Lea la guía &#39;[Ver más](../../dashboards/data-distiller/query-pro-mode/view-more.md)&#39; para obtener información sobre cómo integrar estas características y mejorar sus datos. |
| Volumen total de datos | La métrica &quot;Riqueza de perfil promedio&quot; se ha reemplazado con la métrica &quot;Volumen de datos total&quot;. Volumen total de datos hace referencia a la cantidad total de datos disponibles que se pueden utilizar con el perfil del cliente en tiempo real para los flujos de trabajo de participación y personalización. Encontrará más detalles sobre este cambio en la [guía Volumen total de datos](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Preparación de los datos {#data-prep}

Utilice la preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} Nuevas funciones de preparación de datos para su uso en destinos | Ahora puede utilizar las siguientes funciones de matriz para casos de uso de destinos:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea [Información general de preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

**Actualizado: 30 de septiembre de 2024**

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | La versión de septiembre de 2024 agrega la opción de asignación para exportar el parámetro `countryCode` a Amazon Ads. Use `countryCode` en el [paso de asignación](/help/destinations/catalog/advertising/amazon-ads.md#map) para mejorar las tasas de coincidencia de identidad con Amazon. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Utilice este destino para activar las audiencias de su cuenta para los casos de uso de Account-Based Marketing (ABM). Anuncie a personalidades y roles relevantes en sus cuentas de destinatario a través del Demand Side Platform DSP B2B () de DemandBase. Las cuentas de Target también se pueden enriquecer con datos de terceros de Demandbase para otros casos de uso posteriores en marketing y ventas. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| [Mejoras en la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md) | La versión de septiembre de 2024 de Experience Platform incluye varias mejoras en las funciones de la función de exportación de conjuntos de datos para admitir mejor varios casos de uso de salida de datos. Estas mejoras de funciones incluyen: <ul><li>Nuevas opciones de configuración de la carpeta de datos, incluida la opción para agregar y quitar subcarpetas.</li><li>Nuevas opciones de exportación, incluida la exportación completa de archivos (una vez) y la capacidad de especificar fechas de finalización</li><li>Nota: Adobe también introduce una fecha de finalización predeterminada del 1 de mayo de 2025 para todos los flujos de datos de exportación de conjuntos de datos creados antes de la versión de septiembre. Para cualquiera de estos flujos de datos, los clientes deberán actualizar la fecha de finalización del flujo de datos manualmente antes de la fecha de finalización; de lo contrario, las exportaciones se detendrán en esta fecha.</li></ul> <br> ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar programación y carpetas en el paso de programación.](../2024/assets/september/edit-schedule-folders.png "Editar la opción de programación y carpetas en el paso de programación."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general de destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en el Editor de esquemas | Tome el control de las relaciones de esquema con un flujo de trabajo de relación actualizado en el Editor de esquemas. Actualice o elimine fácilmente las relaciones existentes directamente desde la interfaz de usuario de Experience Platform, lo que facilita la administración de esquemas y hace que sea más intuitiva. Ajuste los esquemas de referencia y cambie el nombre de las relaciones con confianza, lo que garantiza una integridad de los datos sin problemas en la segmentación y otros procesos clave. Para obtener más información sobre cómo administrar de forma eficaz las relaciones de esquema, consulte las guías sobre [definición de campos de relación en la interfaz de usuario](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) y sobre [relaciones B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Para obtener más información sobre XDM, lea la [descripción general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Característica actualizada**

| Función | Descripción |
| --- | --- |
| Disponibilidad limitada de las reglas de vinculación de gráficos de identidad | Las reglas de vinculación de gráficos de identidad son un conjunto de herramientas en Identity Service que puede utilizar para garantizar una personalización precisa para los usuarios. <ul><li>Ahora puede usar el [algoritmo de optimización de identidad](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) para asegurarse de que un gráfico de identidad sea representativo de una sola persona y, por lo tanto, evitar la combinación no deseada de identidades en el perfil del cliente en tiempo real.</li><li>Configure [prioridades del área de nombres](../../identity-service/identity-graph-linking-rules/namespace-priority.md) para definir la importancia de sus respectivas áreas de nombres e influir en la forma y segmentación de sus perfiles.</li><li>Use la [herramienta de simulación de gráficos en la interfaz de usuario](../../identity-service/identity-graph-linking-rules/graph-simulation.md) para simular gráficos de identidad con configuraciones variables.</li><li>Use la [interfaz de configuración de identidad](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) para designar su área de nombres única y establecer prioridades para todas las áreas de nombres de su organización.</li><li>Consulte [tablero de identidad](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) para ver las métricas y tendencias relacionadas con los datos de gráficos.</li></ul> Para probar las reglas de vinculación de gráficos de identidad, póngase en contacto con el equipo de cuenta de Adobe para obtener acceso a los entornos limitados de desarrollo. |

**Documentación actualizada**

| Función | Descripción |
| --- | --- |
| Guía de resolución de problemas para reglas de vinculación de gráficos de identidad | Lea la nueva [guía de solución de problemas para reglas de vinculación de gráficos de identidad](../../identity-service/identity-graph-linking-rules/troubleshooting.md) para conocer los enfoques y las soluciones de depuración que puede emprender para resolver problemas comunes que podrían surgir al trabajar con reglas de vinculación de gráficos de identidad. |
| Preguntas frecuentes sobre las reglas de vinculación de gráficos de identidad | Lea las nuevas [reglas de vinculación de gráficos de identidad FAQ](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) para obtener una lista de respuestas a las preguntas más frecuentes sobre la prioridad del área de nombres, el algoritmo de optimización de identidad y otras facetas de las reglas de vinculación de gráficos de identidad. |

{style="table-layout:auto"}

Para obtener más información sobre el Servicio de identidad, consulte la [Información general del Servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL data lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su inserción en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Audiencias de Data Distiller | Cree, administre y active audiencias fácilmente con la extensión de audiencia SQL en el Distiller de datos de Experience Platform. Defina segmentos de audiencia con comandos SQL directamente desde el lago de datos, evitando la necesidad de datos sin procesar en los perfiles. Refine las estrategias de segmentación y sincronice automáticamente las audiencias con destinos basados en archivos con este enfoque flexible basado en datos. Optimice los flujos de trabajo, optimice la gestión de público y desbloquee todo el potencial de los datos. Lea la [guía sobre el uso de la extensión de audiencia SQL](../../query-service/data-distiller-audiences/overview.md) para elevar sus estrategias de audiencia. |
| Datos Estadísticas de Distiller - Hypercubes | Optimizar el análisis de big data con Hypercubes. Gestionar cálculos complejos, como recuentos distintos y análisis multidimensional, sin volver a procesar datos históricos. Actualice los datos de forma incremental, optimice los flujos de trabajo y reduzca el tiempo de procesamiento a la vez que mantiene la precisión y la eficacia. Obtenga perspectivas más rápidas, escalables y rentables que transforman la toma de decisiones. Explore la [guía sobre el uso de Hypercubes](../../query-service/hypercubes/overview.md) para desbloquear análisis avanzados. |
| Explorador de objetos del Editor de consultas | Aumente la eficacia de las consultas con el nuevo Examinador de objetos del Editor de consultas. Busque, filtre y acceda rápidamente a conjuntos de datos para escribir y refinar consultas más rápido. Con las actualizaciones de esquema en tiempo real y los metadatos de tabla instantáneos, puede optimizar los flujos de trabajo, reducir el tiempo de navegación y mejorar la experiencia de consulta. Libere el potencial de sus datos y optimice el análisis. Lea la [guía sobre el uso del Examinador de objetos](../../query-service/ui/user-guide.md#object-browser) para obtener más información. |
| Calcular horas | Obtenga control sobre el uso de los recursos con la métrica de horas calculadas recién visible para consultas programadas. Vea las horas de cálculo en el nivel de ejecución de la consulta para monitorizar y optimizar el uso de los recursos para consultas por lotes CTAS/ITAS. Rastree las horas de inicio, el estado de finalización y calcule el tiempo de cada ejecución de consulta. Ajuste el rendimiento y reduzca los costes sin esfuerzo. Lea la [guía de Horas calculadas](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) para obtener información sobre cómo maximizar la eficacia de las consultas. |

{style="table-layout:auto"}

Para obtener más información acerca del servicio de consultas, lea la [descripción general del servicio de consultas](../../query-service/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de criterios de segmentación de streaming | A partir de la versión de septiembre de 2024 de, se han actualizado los criterios para que sus audiencias puedan optar a la segmentación de streaming. Encontrará más información sobre estos cambios en la [actualización de los criterios de idoneidad para la segmentación de streaming](../../segmentation/eligibility-criteria-update.md). |
| Implementación de búsqueda unificada | El comportamiento de búsqueda dentro del Generador de segmentos ahora utilizará la búsqueda unificada. Esto ofrece una experiencia más sólida a la hora de administrar y buscar audiencias que reutilizar para la pertenencia a segmentos. Para obtener más información sobre este cambio, lea la [guía del Generador de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], lea [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Característica actualizada**

| Función | Descripción |
| --- | --- |
| [!BADGE Compatibilidad de Beta]{type=Informative} con la ingesta de datos cifrados en la IU | Ahora puede introducir datos cifrados desde un origen por lotes de almacenamiento en la nube mediante el espacio de trabajo de orígenes en la interfaz de usuario de Experience Platform. Lea el tutorial sobre [ingesta de datos cifrados en la interfaz de usuario](../../sources/tutorials/ui/encryped-ingestion.md) para obtener más información. |
| Disponibilidad general del origen [!DNL Snowflake Streaming] | El origen [!DNL Snowflake Streaming] ahora está en GA. Utilice esta fuente para transmitir datos de su cuenta de [!DNL Snowflake] al Experience Platform. Lea la [[!DNL Snowflake Streaming] descripción general](../../sources/connectors/databases/snowflake-streaming.md)para obtener más información. |
| Compatibilidad con la autenticación de cuentas de servicio en [!DNL Google BigQuery] | Ahora puede conectar su cuenta de [!DNL Google BigQuery] al Experience Platform mediante la autenticación de cuenta de servicio. Lea [[!DNL Google BigQuery] información general](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) para obtener más información. <br> ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar programación y carpetas en el paso de programación.](../2024/assets/september/service_auth.png "Autenticación de servicio para Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Compatibilidad para omitir la previsualización de datos de ejemplo | Ahora puede optar por omitir la previsualización de datos al crear una conexión de origen con los siguientes orígenes: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Puede omitir la previsualización de datos para evitar un tiempo de espera que se pueda producir al ingerir lotes de datos grandes. Al hacerlo, puede evitar la validación automática de los campos calculados y requeridos. Si elige omitir la previsualización de datos, es posible que tenga que validar manualmente los campos calculados y requeridos durante la asignación. |
| Compatibilidad para deshabilitar la fragmentación en [!DNL SFTP] | Ahora puede configurar una opción que le permita deshabilitar la fragmentación en el origen [!DNL SFTP]. Consulte la [[!DNL SFTP] información general](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de fuentes](../../sources/home.md).
