---
title: 'Notas de la versión de Adobe Experience Platform: mayo de 2025'
description: Las notas de la versión de mayo de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f143c34d31483e91e176b1c69d82db38a8bc6b5
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 46%

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

**Fecha de versión: miércoles, 20 de mayo de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Servicio de catálogo](#catalog-service)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Servicio de identidad](#identity)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

| Función | Descripción |
| --- | --- |
| Optimizar el almacenamiento de datos con reglas de retención de nivel de conjunto de datos | Administre de forma eficaz el almacenamiento de datos con políticas de retención que eliminen los datos obsoletos en función del periodo de tiempo especificado. <ul><li>**Retención de conjuntos de datos**: defina reglas de conjuntos de datos para quitar datos obsoletos del lago de datos y del almacén de perfiles.</li><li>**Perspectivas de almacenamiento**: supervise el uso y asegure el cumplimiento de los derechos con licencia a través de métricas en línea.</li><li>**Visibilidad mejorada**: rastree la actividad del conjunto de datos desde la ingesta hasta la eliminación con una supervisión mejorada.</li><li>**Administración optimizada**: Acceda a la configuración de retención, supervisión, registros de auditoría y perspectivas en una sola vista unificada.</li></ul> Lea la guía sobre [reglas de retención de conjuntos de datos](../../catalog/datasets/user-guide.md#data-retention-policy) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea [Descripción general del servicio de catálogo](../../catalog/home.md).

## Preparación de los datos {#data-prep}

Utilice la preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con asignaciones de importación y exportación para Adobe Analytics | Ahora puede utilizar las funcionalidades de importación y exportación de asignación para los datos del grupo de informes de Adobe Analytics al utilizar el conector de origen de Adobe Analytics. <br><br>Exporte sus asignaciones a un archivo CSV y configúrelas localmente en una hoja de cálculo. A continuación, puede importar las asignaciones actualizadas a Experience Platform mediante la interfaz de asignación en la interfaz de usuario. Puede utilizar esta función para configurar grandes cantidades de asignaciones sin tener que crearlas manualmente en la interfaz de usuario. Además, al crear un nuevo flujo de datos, puede cargar una copia de las asignaciones directamente en Experience Platform para acelerar el flujo de trabajo. <br><br>Para obtener más información, lea la guía de [conexión de Adobe Analytics a Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la preparación de los datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| Actualización de [Audiencia personalizada de Facebook](../../destinations/catalog/social/facebook.md) y compatibilidad con identificadores relacionados con direcciones | A partir del 23 de mayo de 2025 y durante junio de 2025, es posible que vea temporalmente dos tarjetas de destino **[!DNL Facebook Custom Audience]** en el catálogo de destinos durante un máximo de unas horas. Esto se debe a una actualización interna del servicio de destinos y a la compatibilidad con nuevos campos para mejorar la segmentación y la coincidencia con perfiles en las propiedades de Facebook. Para obtener más información sobre los nuevos campos relacionados con direcciones, consulte la sección [identidades admitidas](#supported-identities). <br><br>Si ve una tarjeta denominada **[!UICONTROL (Nueva) Audiencia personalizada de Facebook]**, use esta tarjeta para nuevos flujos de datos de activación. Los flujos de datos existentes se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. Cualquier cambio que realice en los flujos de datos existentes durante este período se conservará después de la actualización. Una vez completada la actualización, se cambiará el nombre de la tarjeta de destino de **[!UICONTROL (nueva) audiencia personalizada de Facebook]** a **[!DNL Facebook Custom Audience]**. <br><br>Si está creando flujos de datos mediante la [API de Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar sus [!DNL flow spec ID] y [!DNL connection spec ID] con los siguientes valores: <ul><li>ID de especificación de flujo: `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>ID de especificación de conexión: `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Compatibilidad con identificadores adicionales para [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) | El destino de Google Customer Match ahora admite la asignación de campos relacionados con direcciones para mejorar las tasas de coincidencia en la plataforma de Google. <br><br>Para asegurarse de que Google coincida con la dirección, debe asignar los cuatro campos de dirección (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`) y asegurarse de que ninguno de estos campos contiene datos ausentes en los perfiles exportados. <br> Si algún campo no está asignado o contiene datos que faltan, Google no coincidirá con la dirección. |
| Columna de caducidad de la cuenta para [conexiones de Facebook](../../destinations/catalog/social/facebook.md) | Ahora puede ver las fechas de caducidad del token de la cuenta de Facebook en las pestañas [Examinar](../../destinations/ui/destinations-workspace.md#browse) y [Cuentas](../../destinations/ui/destinations-workspace.md#accounts). |
| Exportar conjuntos de datos creados por API | Ahora puede exportar conjuntos de datos creados por API. Se ha eliminado la limitación anterior, en la que solo los conjuntos de datos creados en la interfaz de usuario estaban disponibles para la exportación. Más información sobre [exportar conjuntos de datos](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre destinos](../../destinations/home.md).

## Servicio de identidad {#identity}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] ya está disponible de forma general. [!DNL Identity Graph Linking Rules] evita el &quot;colapso del gráfico&quot;, lo que garantiza perfiles de clientes distintos y precisos para el marketing personalizado en Experience Platform y aplicaciones. Las funciones principales incluyen:<ul><li>[Herramienta de simulación de gráficos](../../identity-service/identity-graph-linking-rules/graph-simulation.md): Explore el algoritmo y pruebe las configuraciones de la configuración de identidad.</li><li> [Configuración de identidad](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md): configure áreas de nombres únicas y establezca prioridades.</li><li>[Tablero de identidad](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs): supervisa los gráficos y valida la configuración de identidad.</li></ul> **Nota**: no habrá cambios en tus datos hasta que configures manualmente tus parámetros de identidad. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general del servicio de identidad](../../identity-service/home.md).

## Servicio de consultas {#query-service}

Consulte datos en el lago de datos de Adobe Experience Platform utilizando SQL estándar con el Servicio de consultas. Combine conjuntos de datos sin problemas y genere otros nuevos a partir de los resultados de su consulta para impulsar la creación de informes, habilitar flujos de trabajo de ciencia de datos o facilitar la ingesta en el Perfil del cliente en tiempo real. Por ejemplo, puede combinar los datos de transacciones de clientes con datos de comportamiento para identificar públicos de alto valor para campañas de marketing dirigidas.

**Funciones nuevas o actualizadas**

| Función | Descripción |
|--------|-------------|
| Migración de credenciales de JWT a OAuth | Las credenciales de JWT que no caduquen deben migrarse a OAuth Server-to-Server antes del 30 de junio de 2025 para evitar interrupciones del servicio. Este cambio mejora la seguridad y la coherencia de la plataforma. Consulte la [Guía de credenciales de JWT a servidor OAuth ](../../query-service/ui/migrate-jwt-to-oauth.md) para obtener más información. |
| Tabla de resultados heredados (disponibilidad limitada) | Los usuarios que dependen de flujos de trabajo de arrastrar y seleccionar pueden solicitar acceso a una tabla de resultados heredada que admita la selección nativa del explorador y el comportamiento de copia. La salida pegada está delimitada por tabulaciones, por lo que las columnas permanecen alineadas y son legibles en Excel, lo que permite revisar las hojas de cálculo y realizar controles de calidad con mayor facilidad. Consulte la [guía de la interfaz de usuario del editor de consultas](../../query-service/ui/user-guide.md#legacy-results-table) para obtener más información. |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Experience Platform en entornos virtuales separados para ayudar a que se desarrollan y evolucionen las aplicaciones de experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Ampliación de compatibilidad de complemento de herramientas de zona protegida | Ahora, las campañas se pueden migrar con objetos dependientes adicionales mediante herramientas de zona protegida, incluida la configuración de canal, la decisión unificada, la configuración/variantes del experimento, etc. Para obtener una lista completa de los objetos de campaña admitidos, así como de todos los objetos de Adobe Journey Optimizer admitidos, lea la guía de [herramientas de zona protegida](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Las audiencias pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de criterios de segmentación de streaming | A partir de la versión de mayo de 2025, se han actualizado los criterios para que sus audiencias puedan optar a la segmentación de streaming. Encontrará más información sobre estos cambios en la [actualización de los criterios de idoneidad para la segmentación de streaming](../../segmentation/eligibility-criteria-update.md). |

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con autenticación básica para [!DNL MySQL] | Ahora puede usar la autenticación básica para conectar su base de datos de [!DNL MySQL] a Experience Platform. Lea la [[!DNL MySQL] descripción general del origen](../../sources/connectors/databases/mysql.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).