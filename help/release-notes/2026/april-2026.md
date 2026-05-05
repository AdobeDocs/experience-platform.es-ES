---
title: Notas de la versión de Adobe Experience Platform, abril de 2026
description: Las notas de la versión de abril de 2026 de Adobe Experience Platform.
exl-id: 47070fcf-b585-43f4-b43b-0d62c18f0693
source-git-commit: 9ebf498257378f4c5002276a84f104cf2d337601
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 22%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: 28 de abril de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time CDP](#rtcdp)
- [Zonas protegidas](#sandboxes)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Ver detalles de compilación | Ahora puede acceder a las compilaciones y los detalles de la compilación desde una biblioteca o un entorno para ver la compilación activa actual e inspeccionar el contenido (extensiones, elementos de datos y reglas). Para obtener más información, consulte [Información general sobre compilaciones](../../tags/ui/publishing/builds.md#build-details). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la recopilación de datos](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino. Utilice destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Coincidencia de clientes de Microsoft Ads](../../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Hacer coincidir clientes por dirección de correo electrónico y volver a interactuar con ellos en [!DNL Microsoft Advertising Network], incluidos los anuncios de búsqueda y de audiencia. Vincule su cuenta de [!DNL Microsoft Advertising] a Real-Time CDP para automatizar la creación y administración de listas de coincidencia de clientes directamente desde Experience Platform. Para obtener acceso, póngase en contacto con el administrador de cuentas de Adobe. |
| [!BADGE Beta]{type=Informative} [Audiencia personalizada Reddit](../../destinations/catalog/advertising/reddit-custom-audience.md) | Enviar audiencias de Experience Platform a [!DNL Reddit Ads]. Conecte su cuenta de [!DNL Reddit], asigne identidades y active audiencias para llegar a las personas que exploran activamente sus intereses en [!DNL Reddit]. |
| [Amazon Ads v2](../../destinations/catalog/advertising/amazon-ads-v2.md) | Utilice la tarjeta [!DNL Amazon Ads v2] para todas las conexiones nuevas de [!DNL Amazon Ads]. [!DNL Amazon Ads v2] se conecta a [!DNL Ads Data Manager], que proporciona compatibilidad con tipos de identidad ampliados, campos relacionados con direcciones y uso compartido de datos entre productos de [!DNL Amazon Ads], lo que mejora las tasas de coincidencia de audiencia y segmentación. Se cambió el nombre del conector [!DNL Amazon Ads] existente en el catálogo a [(heredado) [!DNL Amazon Ads]](../../destinations/catalog/advertising/amazon-ads.md). Si tiene una conexión heredada existente, continúa funcionando sin ningún cambio requerido. |
| [[!DNL Rokt]](../../destinations/catalog/advertising/rokt.md) | Utilice [!DNL Rokt] para conectar las audiencias de Experience Platform a la toma de decisiones en tiempo real impulsada por IA, lo que mejora el rendimiento de la campaña mediante una segmentación, supresión y personalización más precisas. |
| [Conexión de audiencia Acxiom](../../destinations/catalog/advertising/acxiom-audience-connection.md) | El destino [!DNL Acxiom Audience Connection] ya está disponible de forma general. Utilícelo para mejorar audiencias con tecnología [!DNL Acxiom's Real ID] y activarlas en [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] y [!DNL Viant]. |
| [Conexión de audiencia de Real ID de Acxiom](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | El destino [!DNL Acxiom Real ID Audience Connection] ya está disponible de forma general. Utilícelo para activar audiencias usando [!DNL Acxiom's Real ID] como clave de coincidencia en [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] y [!DNL Viant]. |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Corregir | Descripción |
| --- | --- |
| Nueva columna `TS` para [Transmisión de Snowflake](../../destinations/catalog/warehouses/snowflake.md) destinos | El destino [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) ahora incluye una columna de marca de tiempo `TS` en la tabla compartida, que muestra cuándo se actualizó cada fila por última vez. Esta actualización estará disponible hasta finales de abril. |
| Supervisando la compatibilidad con [destinos Personalization personalizados](../../destinations/catalog/personalization/custom-personalization.md) | La página [ejecución de flujo de datos](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) ahora muestra métricas para [destinos Personalization personalizados](../../destinations/catalog/personalization/custom-personalization.md). Anteriormente, estas métricas no estaban disponibles para este tipo de destino. Utilícelos para verificar que las audiencias se activan según lo esperado y para diagnosticar problemas. <br> ![El flujo de datos ejecuta las métricas mostradas para un destino de Personalization personalizado y muestra las identidades activadas, excluidas y fallidas.](./assets/april/dataflow-run-custom-personalization.png "Flujo de datos ejecuta métricas para destinos personalizados de Personalization."){zoomable="yes"} |
| Recuentos de perfiles en el paso de revisión del flujo de trabajo de activación | El paso de revisión del flujo de trabajo de activación ahora muestra los recuentos de perfiles de las audiencias que ya están activadas. Los recuentos de perfiles también se muestran para [destinos de streaming](../../destinations/ui/activate-segment-streaming-destinations.md), no solo para [destinos por lotes](../../destinations/ui/activate-batch-profile-destinations.md). <br> ![Recuentos de perfiles mostrados en el paso de revisión del flujo de trabajo de activación para audiencias ya activadas y de flujo continuo.](./assets/april/profile-count-review.png "Recuentos de perfiles en el paso de revisión del flujo de trabajo de activación."){zoomable="yes"} |
| Visibilidad de caducidad de token [!DNL Pinterest] | El destino [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) ahora muestra la fecha de caducidad del token para que pueda ver cuándo es necesaria la reautenticación. [!DNL Pinterest] tokens caducan cada 30 días. Cuando caduca un token, las exportaciones de datos dejan de funcionar. Para evitar interrupciones, [actualice sus credenciales de autenticación](../../destinations/catalog/advertising/pinterest.md#refresh-authentication-credentials) antes de que caduque el token. |
| Exportar archivo ahora deshabilitado para las programaciones caducadas | Cuando la programación de audiencias ha caducado, **[!UICONTROL Export file now]** se desactiva antes de intentar usarlo y una información de objeto explica por qué. Anteriormente, la selección de la acción producía un error. <br> ![La acción Exportar archivo ahora se deshabilitó con información sobre herramientas que explica por qué la acción no está disponible.](./assets/april/export-file-now-disabled.png "Se deshabilitó la acción Exportar archivo ahora."){zoomable="yes"} |
| Corrección de visibilidad de columna en el flujo de trabajo de activación | Se corrigió un problema en el cual el cambio de columnas visibles en una tabla afectaba incorrectamente a otras tablas del flujo de trabajo de activación. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

| Función | Descripción |
| --- | --- |
| Mejoras En El Uso Y Descubrimiento De Grupos De Campo | Vea qué esquemas utilizan un grupo de campos y acceden a metadatos como clases compatibles, atributos obligatorios y etiquetas de gobernanza directamente en la interfaz de usuario. También puede filtrar grupos de campos por compatibilidad de clases y etiquetas del sector para descubrir de forma más eficaz los recursos relevantes y evaluar el impacto antes de realizar cambios. Consulte la [guía Explorar grupos de campos](../../xdm/ui/explore.md#explore-field-groups.md) para obtener más información. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

Use el servicio de consultas para consultar datos en Adobe Experience Platform [!DNL Data Lake] con SQL estándar. Únase a cualquier conjunto de datos de [!DNL Data Lake] y capture los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, Data Science Workspace o la ingesta en el Perfil del cliente en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de sesiones del servicio de consultas | Vea y finalice las sesiones activas del servicio de consultas desde la ficha [!UICONTROL Admin] para supervisar el uso y la capacidad de sesión inactiva gratuita. Esto ayuda a los administradores a mantener flujos de trabajo de Data Distiller fiables al recuperar la capacidad de sesiones inactivas. Consulte la [Guía de sesiones de Administrar servicio de consultas](../../query-service/ui/session-management.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea [Introducción al servicio de consultas](../../query-service/home.md).

## Real-Time CDP {#rtcdp}

Real-Time CDP proporciona perfiles de cliente unificados y procesables mediante la ingesta, el procesamiento y la activación de datos en varios canales en tiempo real. Con Real-Time CDP, las organizaciones pueden conectar las fuentes de datos existentes, crear y activar audiencias enriquecidas y garantizar la activación compatible con la privacidad en todos los destinos, todo ello desde Experience Platform. Esto permite a los especialistas en marketing, analistas y equipos de TI ofrecer experiencias puntuales y altamente personalizadas para sus clientes a través de campañas de marketing multicanal sin problemas.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Real-Time CDP MCP (Beta) | Use [Real-Time CDP MCP](../../rtcdp/rtcdp-mcp.md) para incorporar Real-Time CDP a los agentes de IA y a los clientes compatibles con MCP, lo que le permitirá interactuar con las herramientas de Real-Time CDP directamente a través de su experiencia LLM nativa. Al conectar un cliente compatible con MCP (como Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code) al punto final proporcionado por su representante de Adobe, puede utilizar el lenguaje natural para inspeccionar audiencias, configurar el destino y el historial de ejecución de la activación, sin escribir llamadas a la API de REST de Experience Platform ni navegar por varios flujos de trabajo de interfaz de usuario. Después de completar un inicio de sesión de Adobe basado en explorador, tendrá acceso de solo lectura a las herramientas, que incluyen: <ul><li>Buscar audiencias existentes</li><li>Previsualizar pertenencia A Audiencia</li><li>Enumerar tipos de destino</li><li>Enumerar cuentas configuradas</li><li>Enumerar destinos configurados</li><li>Enumerar conexiones de Source</li><li>Enumerar conexiones de destino</li><li>Inspeccionar ejecuciones de activación</li></ul>. Cada solicitud requiere `imsOrgId` y `sandboxName` parámetros para garantizar que las acciones tengan ámbitos para su organización y zona protegida. **Nota**: las operaciones de escritura no se admiten en esta versión de Beta. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de Real-Time CDP](../../rtcdp/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Express Copy | Use la copia rápida para copiar objetos en una zona protegida de destino en una sola acción desde la [IU de herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Los objetos dependientes se detectan automáticamente y se crean en la zona protegida de destino o se reutilizan cuando ya existen. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de las zonas protegidas](../../sandboxes/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.One] | La fuente [[!DNL Talon.One] source](../../sources/connectors/loyalty/talon-one.md) para Experience Platform ya está disponible en los modos por lotes y streaming. Use [[!DNL Talon.One Batch Source Connector]](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) para introducir periódicamente sesiones cerradas y transacciones de fidelidad históricas, y el origen [[!DNL Talon.One Streaming Events]](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) para traer [!DNL Talon.One] eventos a Experience Platform en tiempo casi real. En conjunto, facilitan la carga y activación de los datos de fidelidad de [!DNL Talon.One] en Real-Time CDP, Adobe Journey Optimizer y Offer Decisioning. |
| Compatibilidad con filtrado de nivel de fila para [!DNL Salesforce] mediante SOQL | Ahora puede aplicar filtros SOQL (Lenguaje de consulta de objetos) [!DNL Salesforce] directamente en [!DNL Salesforce] conexiones de origen, lo que le permite restringir los datos de nivel de fila antes de ingerirlos en Experience Platform. Utilice esta capacidad para lo siguiente: <ul><li>Defina las condiciones de estilo de la cláusula WHERE de SOQL en objetos de Salesforce (por ejemplo, solo posibles clientes con correo electrónico != nulos u oportunidades en fases específicas)</li><li>Limite la ingesta únicamente a las filas que cumplan con sus criterios, lo que reduce el movimiento de datos, el almacenamiento y el procesamiento descendente innecesarios</li><li>Alinee la ingesta de Experience Platform más estrechamente con las reglas de cumplimiento y acceso a los datos de CRM, controlando qué registros se llevan a Experience Platform en origen</li></ul>. Para obtener más información, lea la guía sobre [filtrado de nivel de fila para orígenes](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

<!--

| Data Distiller Accelerators | Run and schedule Adobe-managed, parameterized SQL templates in the Query Service UI to perform common analyses without writing SQL. This helps you standardize analytics workflows and reuse trusted query logic across your organization. See the [Data Distiller accelerators guide](../../query-service/ui/accelerators.md) for more details. |

| [!DNL Delta Sharing] | You can use the [!DNL Delta Sharing] source to bring Delta tables into Experience Platform through a secure, open data‑sharing protocol. After you configure a [!DNL Delta Sharing] connection and select the shares and tables you want to ingest, Platform automatically brings that data into your datasets so you can use it for analysis, segmentation, and activation. |
| [!DNL Meta Ads] (Beta) | You can use the [!DNL Meta Ads] source connector (Beta) in the Sources workspace to authenticate to [!DNL Meta], select your ad accounts, and schedule ingestion of [!DNL Meta Ads] campaign and performance data into Experience Platform datasets. |

| Automatic dataflow disabling | Sources ingestion dataflows that fail continuously for 30 days are automatically disabled, helping to surface unhealthy dataflows and reduce repeated failed runs. |

-->
