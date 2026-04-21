---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5d1825bad97d3ec4beece416dc3e0fc9f6ca636d
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 20%

---

# Notas previas al lanzamiento de Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento está diseñado como **vista previa** de las notas de la versión del mes actual. Los elementos de la versión están sujetos a cambios y se pueden añadir o eliminar en la versión final.

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: abril de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time CDP](#rtcdp)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Coincidencia de clientes de Microsoft Ads](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Hacer coincidir clientes por dirección de correo electrónico y volver a interactuar con ellos en [!DNL Microsoft Advertising Network], incluidos los anuncios de búsqueda y de audiencia. Vincule su cuenta de [!DNL Microsoft Advertising] a Real-Time CDP para automatizar la creación y administración de listas de coincidencia de clientes directamente desde Experience Platform. |
| [!BADGE Beta]{type=Informative} [Audiencia personalizada Reddit](../destinations/catalog/advertising/reddit-custom-audience.md) | Enviar audiencias de Experience Platform a [!DNL Reddit Ads]. Conecte su cuenta de [!DNL Reddit], asigne identidades y active audiencias para llegar a las personas que exploran activamente sus intereses en [!DNL Reddit]. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] es el destino actual de todas las nuevas conexiones de [!DNL Amazon Ads]. Si tiene una conexión [(heredada) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) existente, seguirá funcionando sin los cambios necesarios. [!DNL Amazon Ads v2] se conecta a [!DNL Ads Data Manager], que proporciona compatibilidad con tipos de identidad expandidos, campos relacionados con direcciones y uso compartido de datos entre [!DNL Amazon Ads] productos, lo que mejora las tasas de coincidencia de audiencia y segmentación en comparación con [&#x200B; (heredado) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Utilice [!DNL Rokt] para conectar las audiencias de Experience Platform a la toma de decisiones en tiempo real impulsada por IA, lo que mejora el rendimiento de la campaña mediante una segmentación, supresión y personalización más precisas. |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Se ha corregido un problema que hacía que se mostrara | Descripción |
| --- | --- |
| Compatibilidad de monitorización de Personalization personalizada | El panel de supervisión de destinos ahora admite [!DNL Custom Personalization] destinos. Se ha eliminado la nota de limitación que excluía a [!DNL Custom Personalization] de la supervisión. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos introducidos en Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Visibilidad del uso del esquema del grupo de campos | Vea qué esquemas utilizan un grupo de campos de la página de detalles y explórelos en un cuadro de diálogo ordenable con metadatos de esquema. Esto le ayuda a evaluar rápidamente las dependencias y el impacto sin salir. |

{style="table-layout:auto"}

Para obtener más información, lea la [Descripción general del sistema XDM](../xdm/home.md).

## Servicio de consultas {#query-service}

Use el servicio de consultas para consultar datos en Adobe Experience Platform [!DNL Data Lake] con SQL estándar. Únase a cualquier conjunto de datos de [!DNL Data Lake] y capture los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, Data Science Workspace o la ingesta en el Perfil del cliente en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Data Distiller Accelerators | Ejecute y programe plantillas SQL parametrizadas y administradas por Adobe en la interfaz de usuario del servicio de consultas para realizar análisis comunes sin escribir SQL. Esto le ayuda a estandarizar los flujos de trabajo de análisis y a reutilizar la lógica de consulta de confianza en toda la organización. |

{style="table-layout:auto"}

Para obtener más información, lea [Introducción al servicio de consultas](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] proporciona perfiles de cliente unificados y procesables mediante la ingesta, el procesamiento y la activación de datos en varios canales en tiempo real. Con Real-Time CDP, las organizaciones pueden conectar las fuentes de datos existentes, crear y activar audiencias enriquecidas y garantizar la activación compatible con la privacidad en todos los destinos, todo ello desde Experience Platform. Esto permite a los especialistas en marketing, analistas y equipos de TI ofrecer experiencias puntuales y altamente personalizadas para sus clientes a través de campañas de marketing multicanal sin problemas.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Real-Time CDP MCP (Beta) | Utilice el MCP de Real-Time CDP para incorporar Real-Time CDP a los agentes de IA y a los clientes compatibles con MCP, lo que le permite interactuar con las herramientas de Real-Time CDP directamente a través de su experiencia LLM nativa. Al conectar un cliente compatible con MCP (como Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code) a `https://rtcdp-mcp.adobe.io/mcp`, puede utilizar el lenguaje natural para inspeccionar audiencias, la configuración de destino y el historial de ejecución de activación, sin escribir llamadas a la API de REST de Experience Platform ni navegar por varios flujos de trabajo de interfaz de usuario. Después de completar un inicio de sesión de Adobe basado en explorador, tendrá acceso de solo lectura a las herramientas, que incluyen: <ul><li>Buscar audiencias existentes</li><li>Previsualizar pertenencia A Audiencia</li><li>Enumerar tipos de destino</li><li>Enumerar cuentas configuradas</li><li>Enumerar destinos configurados</li><li>Enumerar conexiones de Source</li><li>Enumerar conexiones de destino</li><li>Inspeccionar ejecuciones de activación</li></ul>. Cada solicitud requiere `imsOrgId` y `sandboxName` parámetros para garantizar que las acciones tengan ámbitos para su organización y zona protegida. Tenga en cuenta que las operaciones de escritura no son compatibles con esta versión de Beta. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de Real-Time CDP](../rtcdp/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Express Copy | Use la copia rápida para copiar objetos en una zona protegida de destino en una sola acción desde la [IU de herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Los objetos dependientes se detectan automáticamente y se crean en la zona protegida de destino o se reutilizan cuando ya existen. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de las zonas protegidas](../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

Utilice el servicio de segmentación para crear audiencias a partir de los datos de sus clientes y administrar todo su ciclo de vida en Experience Platform.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Monitorización de segmentación de streaming | Monitorice la segmentación de streaming con visibilidad en tiempo real de la tasa de evaluación, la latencia de ingesta y las métricas de calidad de datos en el nivel de zona protegida, conjunto de datos y segmento. Ver métricas que incluyen tasa de evaluación, latencia de ingesta de P95, registros recibidos, registros evaluados, registros fallidos y registros omitidos. Vea también los nuevos perfiles netos clasificados y descalificados por segmento. Utilice estas perspectivas para identificar infracciones de capacidad y problemas de ingesta antes de que afecten a los datos. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre audiencias](../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| Desactivación automática de flujo de datos | Los flujos de datos de ingesta de fuentes que fallan continuamente durante 30 días se desactivan automáticamente, lo que ayuda a que aparezcan flujos de datos no en buen estado y a reducir las ejecuciones fallidas repetidas. |
| [!DNL Delta Sharing] | Puede usar el origen [!DNL Delta Sharing] para llevar tablas Delta a Experience Platform a través de un protocolo seguro y abierto para compartir datos. Después de configurar una conexión de [!DNL Delta Sharing] y seleccionar los recursos compartidos y las tablas que desea introducir, Platform introduce automáticamente esos datos en los conjuntos de datos para que pueda utilizarlos en el análisis, la segmentación y la activación. |
| [!DNL Meta Ads] (Beta) | Puede usar el conector de origen [!DNL Meta Ads] (Beta) en el área de trabajo de fuentes para autenticarse en [!DNL Meta], seleccionar las cuentas de publicidad y programar la ingesta de datos de rendimiento y campaña de [!DNL Meta Ads] en los conjuntos de datos de Experience Platform. |
| [!DNL Talon.One] | Ahora puede conectar Experience Platform a [!DNL Talon.One] con los nuevos orígenes de flujo continuo y lote de [!DNL Talon.One]. Utilice las nuevas fuentes para introducir datos del perfil de lealtad, así como eventos de transacciones y actividades de lealtad en Experience Platform. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
