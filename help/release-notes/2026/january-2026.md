---
title: Notas de la versión de Adobe Experience Platform, enero de 2026
description: Las notas de la versión de enero de 2026 de Adobe Experience Platform.
source-git-commit: 49074f3ea2650254863a58a488c626f683ba7f06
workflow-type: tm+mt
source-wordcount: '1570'
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

**Fecha de la versión: miércoles, 27 de enero de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Destinos](#destinations)
- [Perfil del cliente en tiempo real](#real-time-customer-profile)
- [Esquemas](#schemas)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator le permite crear e implementar agentes con tecnología de IA que pueden automatizar flujos de trabajo e interactuar con los clientes en varios canales.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Prueba enlazada al uso de agentes de Adobe Experience Platform | **Algunos clientes ahora tienen acceso de prueba gratuito a los agentes de Adobe Experience Platform**. Puede utilizar la prueba para explorar e interactuar con agentes a través de la interfaz del asistente de IA con tecnología de Adobe Experience Platform Agent Orchestrator. La prueba ofrece experiencia práctica con agentes de IA que operan en el contexto de los productos y entornos de Experience Cloud existentes de los clientes, lo que permite a los equipos evaluar el valor antes de comprometerse a realizar una compra completa. Los agentes de Adobe Experience Platform se guían por la entrada y supervisión del usuario y respetan los controles de acceso de nivel de producto existentes, lo que garantiza que los usuarios solo puedan realizar acciones o ver los datos para los que están autorizados dentro de las aplicaciones de Experience Cloud subyacentes. Lea la [descripción general de la versión de prueba de los agentes de Experience Platform](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) para obtener información sobre cómo empezar. |

{style="table-layout:auto"}

Para obtener más información, consulte la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| Ya está disponible el conector [Kevel destination](/help/destinations/catalog/advertising/kevel.md) | El destino de streaming de [!DNL Kevel] para Adobe Experience Platform permite a los clientes activar audiencias de Adobe directamente en las API de UserDB y Administración de segmentos de [!DNL Kevel] para admitir el direccionamiento en tiempo real en el momento de la decisión de anuncios. [[!DNL Kevel]](https://www.kevel.com/) proporciona la tecnología habilitada para IA y la guía de expertos que ayudan a los líderes innovadores en comercio a lanzar, escalar y tener éxito en los medios minoristas. Retail Media Cloud de [!DNL Kevel] alimenta los formatos de anuncio personalizables, atribuibles y orientados para la publicidad dentro y fuera del sitio. |
| Ya está disponible el conector de destino [Index Exchange](/help/destinations/catalog/advertising/index-exchange.md) | Utilice este conector de destino para exportar segmentos de audiencia de Adobe Experience Platform directamente a la plataforma de publicidad programática de [!DNL Index Exchange]. [!DNL Index] es una plataforma global de suministro de publicidad que ayuda a los propietarios de medios a maximizar el valor de su contenido en todas las pantallas. Con más de 20 años de liderazgo en la industria, [!DNL Index] conecta las marcas más grandes del mundo con los creadores de experiencia premium para ofrecer experiencias de alta calidad a los consumidores. |
| Compatibilidad con puntos finales regionales para conexiones de Brazo | Todos los [extremos específicos de región](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) admitidos por [!DNL Braze] están ahora disponibles para su selección durante el flujo de configuración de destino. Pregunte a su representante de [!DNL Braze] qué instancia de extremo debe utilizar. |
| Soporte de programación semanal y mensual para [Liveramp Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Ahora puede configurar programas de exportación semanales y mensuales para el destino de incorporación de Liveramp. <br> Esta versión se está implementando gradualmente y se completará para el 30 de enero. |
| Experiencia de activación mejorada para [The Trade Desk](../../destinations/catalog/advertising/tradedesk.md) y [Microsoft Bing](../../destinations/catalog/advertising/bing.md) destinos | Los destinos de Trade Desk y Microsoft Bing ahora incluyen asignaciones obligatorias predefinidas para una experiencia de activación optimizada.  <br> Esta versión se está implementando gradualmente y se completará para el 30 de enero. ![Imagen que muestra asignaciones predefinidas para la oficina de ventas](assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![Imagen que muestra asignaciones predefinidas para Microsoft Bing](assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| Compatibilidad con activación de número de teléfono para [la conexión de Trade Desk - CRM](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) | El destino de Trade Desk - CRM ahora admite la activación de números de teléfono además de direcciones de correo electrónico. Puede activar números de teléfono sin hash en formato E.164 y números de teléfono con hash (formato SHA256_E.164) en su cuenta de Trade Desk para la segmentación y supresión de audiencias en función de los datos de CRM. Los números de teléfono deben normalizarse al formato E.164 antes de la activación. |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) actualizaciones de destino | El destino de lote de Snowflake ahora incluye la capacidad de selección de regiones durante la configuración del destino. Ahora puede seleccionar la región de Snowflake específica en la que está aprovisionada la instancia, lo que garantiza una transferencia de datos óptima y el cumplimiento de los requisitos regionales. Además, se ha eliminado la restricción predeterminada de la política de combinación, lo que le permite exportar audiencias asignadas a cualquier política de combinación. <br>: actualmente, el destino de lote [!DNL Snowflake] solo está disponible para los clientes de Real-Time CDP aprovisionados en la región de Experience Platform VA7. |


<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <ul><li>**[!UICONTROL Default]**: Data will be encrypted at rest with the default encryption algorithm set on your bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest with the AES256 algorithm when it lands in S3. **This option takes precedence over any default encryption algorithm configured on your S3 bucket**.</li></ul> This release is being rolled out gradually and will be complete by January 30th.| -->

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Se han actualizado los límites de protección para [destinos de Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | El número máximo de audiencias que se pueden asignar a un único destino de Adobe Target ha aumentado de 50 a 250. Esto alinea Adobe Target con el límite de audiencia estándar para otros destinos, lo que proporciona una mayor flexibilidad para los flujos de trabajo de activación de audiencia. Ahora puede activar más audiencias en destinos de Adobe Target sin necesidad de crear varios flujos de datos. |
| [Editar destinos](/help/destinations/ui/edit-destination.md) y [editar acciones de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilidad general | La opción para editar destinos y acciones de marketing ya está disponible para todos los usuarios. |
| Alternar nombres para mostrar de campo en el [paso](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de la asignación | Al asignar campos de esquema a un destino, ahora puede alternar entre mostrar el nombre del campo XDM completo y mostrar solo el nombre para mostrar. <br> ![Grabación de pantalla que muestra la opción de nombre para mostrar.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Perfil del cliente en tiempo real {#real-time-customer-profile}

El perfil del cliente en tiempo real permite ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Aplicación de [capacidad de transmisión](/help/landing/license-usage-and-guardrails/capacity.md) | Experience Platform ahora impone capacidades de rendimiento de flujo continuo para el perfil del cliente en tiempo real y el servicio de identidad. Cuando los clientes exceden su capacidad de transmisión contratada, los datos se ponen en cola y se procesan del primer ingreso al primer envío. Esto garantiza un rendimiento predecible del sistema y evita que las infracciones de capacidad afecten a la calidad de la ingesta de datos. Notas importantes: <ul><li>Las actualizaciones de streaming no estarán disponibles en el lago de datos cuando se exceda la capacidad</li><li>Esta aplicación no se aplica a los clientes con licencias de Adobe Journey Optimizer</li><li>Los datos en cola se procesarán secuencialmente una vez que la capacidad esté disponible.</li></ul> Para obtener más información, lea [descripción general de la capacidad](/help/landing/license-usage-and-guardrails/capacity.md). |
| Obsolescencia de búsqueda de entidad | El uso de la API de búsqueda de entidades para eventos de experiencia ya no se utiliza para todos los clientes de Real-Time CDP Prime. Esta desaprobación ayuda a alinear Real-Time CDP con la funcionalidad de las licencias. Los clientes de Real-Time CDP Ultimate que tengan intención de utilizar esta funcionalidad pueden ponerse en contacto con el Servicio de atención al cliente de Adobe para volver a habilitar esta función.  Para obtener más información, lea la [guía de API de entidades](/help/profile/api/entities.md). |
| Monitorización del estado del trabajo de ingesta de perfiles | Ahora puede monitorizar el porcentaje de progreso a nivel de trabajo para las ejecuciones del flujo de datos de ingesta de perfiles por lotes. Esta función proporciona visibilidad en tiempo real del progreso actual de los trabajos de ingesta por lotes, incluidos los puntos de comprobación críticos que indican si la ingesta está lista para la segmentación de clientes y las búsquedas de Adobe Journey Optimizer. Para las ingestas grandes que pueden tardar varias horas en procesarse, esta transparencia de progreso le ayuda a comprender si el trabajo progresa con normalidad o si encuentra problemas, lo que reduce la incertidumbre durante el procesamiento de datos.Para obtener más información, lea la [guía de perfiles de monitor](/help/dataflows/ui/monitor-profiles.md). |
| Mejoras del visor de perfiles (GA) | Las siguientes mejoras del Visor de perfiles ya están disponibles de forma general. <ul><li>**Vista combinada**: los atributos, los eventos y los datos se han combinado en una sola vista.</li><li>**Información generada por IA**: la página de detalles del perfil ahora muestra información generada por IA, lo que le permite conocer detalles generados a partir de su perfil. Estos datos pueden incluir información como las puntuaciones de las tendencias y el análisis de tendencias.</li><li>**Actualización del estilo**: la página de detalles del perfil se ha actualizado visualmente.</li><li>**Examinar**: ahora puede explorar sus perfiles a través de un carrusel interactivo basado en tarjetas con búsqueda y personalización.</li></ul> Para obtener más información, lea la [guía del visor de perfiles](/help/profile/ui/user-guide.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Real-Time Customer Profile] información general](../../profile/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de caducidad de datos de audiencia externa | Las audiencias externas (como las cargas de CSV) ahora admiten la función de actualización forzada de la configuración de caducidad de los datos. Esta función permite a los usuarios actualizar de forma manual la caducidad de los datos de las audiencias externas, lo que proporciona un mayor control sobre la administración del ciclo vital de las audiencias. Esto resulta particularmente útil en audiencias que deben persistir más allá del periodo de caducidad inicial de los datos o que requieren reactivación sin volver a cargar los datos. Para obtener más información acerca de esta característica, lea la [descripción general de Audience Portal](../../segmentation/ui/audience-portal.md#audience-summary). |
| Validación de audiencia | Experience Platform ahora proporciona validaciones integradas para garantizar que sus audiencias sean precisas, estables y escalables. Estas comprobaciones se ejecutan automáticamente en tiempo real mientras crea las definiciones de audiencia. Para obtener más información, lea la [descripción general de validación de audiencias](/help/segmentation/validation.md). |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2 de origen | Ya está disponible un nuevo conector de origen [!DNL Oracle Eloqua] que reemplaza el [conector obsoleto](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Este conector actualizado proporciona funcionalidad y confiabilidad mejoradas para la ingesta de datos de [!DNL Oracle Eloqua] en Experience Platform. Los clientes que utilicen el conector existente deben migrar a la nueva implementación, ya que las conexiones existentes dejarán de funcionar. El nuevo conector admite todos los pasos de instalación y configuración necesarios para conectarse a [!DNL Oracle Eloqua] e introducir datos de automatización de marketing. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2 de origen | Ya está disponible un nuevo conector de origen [!DNL Salesforce Marketing Cloud] que reemplaza el [conector obsoleto](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Este conector actualizado proporciona un rendimiento mejorado y capacidades adicionales para la ingesta de datos de [!DNL Salesforce Marketing Cloud] en Experience Platform. Los clientes que utilicen el conector existente deben realizar la transición a la nueva implementación. El nuevo conector incluye instrucciones de configuración completas para conectarse a [!DNL Salesforce Marketing Cloud] e ingerir datos de automatización de marketing. |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

