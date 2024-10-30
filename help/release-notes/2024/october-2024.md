---
title: Notas de la versión de Adobe Experience Platform de octubre de 2024
description: Las notas de la versión de octubre de 2024 de Adobe Experience Platform.
source-git-commit: 5fc786058a187b161a147a8bd361d19c5f35105d
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 35%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de octubre de 2024**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Paneles {#dashboards}](#dashboards-dashboards)<!-- omit in toc -->
- [Recopilación de datos {#collection}](#data-collection-collection)
- [Destinos {#destinations}](#destinations-destinations)
- [Servicio de segmentación {#segmentation-service}](#segmentation-service-segmentation-service)
- [Zonas protegidas {#sandboxes}](#sandboxes-sandboxes)
- [Fuentes {#sources}](#sources-sources)

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Plantillas de Distiller de datos | Explore varias plantillas para obtener información estructurada sobre los datos de audiencia. Use paneles como **Superposiciones de audiencias [!UICONTROL avanzadas]**, **[!UICONTROL Comparación de audiencias]**, **[!UICONTROL Tendencias de audiencias]** y **[!UICONTROL Superposiciones de identidades de audiencias]** para tomar decisiones basadas en datos, optimizar la segmentación y mejorar las estrategias de participación. Consulte la [Guía de plantillas de Distiller de datos](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) para obtener más información. |
| Superposiciones de público avanzadas | Analice rápidamente las intersecciones de audiencia para audiencias específicas o vea todas las superposiciones para descubrir perspectivas valiosas en todo el conjunto de audiencias. Utilice estas perspectivas para refinar la segmentación, reducir la mensajería redundante y crear campañas más específicas para mejorar la eficacia del marketing. Consulte la [Guía de superposiciones de audiencias avanzadas](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) para obtener más información. |
| Mejoras de Audience Comparison | Vea una comparación en paralelo de métricas clave entre diferentes grupos de audiencias mediante el panel **Comparación de audiencias**. Con este tablero puede seleccionar lapsos de tiempo y KPI específicos, como el tamaño de la audiencia y la composición de la identidad, para tomar decisiones más informadas sobre la segmentación de audiencia y las estrategias de segmentación. Lea la [guía de comparación de audiencias](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) para obtener más información. |
| Visualización de tendencias de audiencia | Analice las métricas de audiencia con el tiempo con el panel **[!UICONTROL Tendencias de audiencia]**. Visualice tendencias sobre el tamaño de la audiencia, el número de identidades y el número de perfiles de identidad únicos para ayudarle a monitorizar la evolución de la audiencia, medir el crecimiento y refinar sus estrategias de participación. Consulte la [Guía de tendencias de audiencia](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) para obtener más información. |
| Análisis de superposiciones de identidad | Analizar superposiciones de identidades en audiencias seleccionadas con el panel **[!UICONTROL Superposiciones de identidades de audiencias]**. Vea las tendencias y desgloses de identidad para comprender cómo se relacionan los distintos tipos de identidad dentro de la audiencia, mejorando la vinculación de identidad y la precisión de la segmentación de clientes. Consulte la [guía de superposiciones de identidad de audiencia](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la Edge Network de Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Etiquetas y extensiones | Vista JSON de Adobe Analytics | Ahora puede utilizar la extensión de etiquetas de Adobe Analytics para examinar eVars, props y configuración de eventos como JSON, que ahora se puede incluir en la extensión del SDK web y exportar para su edición. También puede cargar o copiar estos datos y almacenarlos en su dispositivo. Lea la [documentación de la extensión de Adobe Analytics](../../tags/extensions/client/analytics/overview.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general sobre la recopilación de datos](../../collection/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| ----------- | ----------- |
| [Compatibilidad con exportación de matrices disponible en general](../../destinations/ui/export-arrays-calculated-fields.md) | Ahora todos los clientes pueden usar la opción **[!UICONTROL Agregar campo calculado]** al activar las audiencias *en destinos basados en archivos* para exportar matrices completas o elementos de matrices. Tenga en cuenta que todavía necesita utilizar la función `array_to_string` para acoplar la matriz en una cadena en el archivo de destino. <br> ![Agregar selección de campo calculado con funciones y campos.](../2024/assets/october/array-export.gif "Agregue un campo calculado con una selección de la función array_to_string y la matriz de organizaciones."){width="250" align="center" zoomable="yes"} |
| [Mejoras en la precisión de los informes para destinos de streaming](/help/destinations/ui/export-datasets.md) | A partir de octubre de 2024, Adobe implementará una actualización para aumentar la precisión de la creación de informes en los destinos de flujo continuo. Esta mejora garantiza una mejor alineación entre el Experience Platform y los informes de las plataformas de destino. <br> Antes de esta actualización, **[!UICONTROL las identidades fallaron]** e incluyeron todos los reintentos de activación. Después de esta actualización, solo se incluye el último reintento de activación en el recuento total. <br> Esta mejora se aplica actualmente a [Google Customer Match destination](../../destinations/catalog/advertising/google-customer-match.md), pero se implementará gradualmente en otros destinos de flujo de Experience Platform. Tras esta mejora, es posible que los usuarios del destino [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) vean una caída esperada en su recuento de **[!UICONTROL Identidades con errores]**. |
| Implicaciones flexibles de evaluación de audiencia en [activación de audiencia por lotes](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Si ejecuta [evaluación de audiencia flexible](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) en audiencias que ya están configuradas para activarse después de la evaluación de segmentos, las audiencias se activarán en cuanto finalice el trabajo de evaluación de audiencia flexible, independientemente de cualquier trabajo de activación diario anterior. <br> Esto podría hacer que las audiencias se exporten varias veces al día, según las acciones que realice. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de destinos](../../destinations/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| [!BADGE Disponibilidad limitada]{type=Informative} Evaluación flexible de la audiencia | La evaluación flexible de audiencias le permite crear rápidamente nuevas audiencias bajo demanda para comunicaciones en las que el tiempo es un factor importante. Encontrará más información sobre esta nueva característica en la [documentación de Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Platform en entornos virtuales separados para ayudar a desarrollar y evolucionar las aplicaciones de la experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Uso compartido de paquetes de herramientas de zona protegida | Ahora puede utilizar las herramientas de zona protegida para exportar e importar fácilmente configuraciones de zona protegida entre zonas protegidas de diferentes organizaciones. Ahora hay dos categorías de paquetes compartidos disponibles: <br><ul><li>**[Paquete privado](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Use el uso compartido de paquetes privados con organizaciones que hayan aprobado la solicitud de uso compartido de la organización de origen.</li><li>**[Paquete público](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** Los paquetes públicos se pueden compartir sin aprobaciones adicionales y se importan fácilmente mediante la carga útil del paquete.</li></ul><br>Para obtener más información sobre estas características, lea la guía sobre [compartir paquetes entre organizaciones](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Uso compartido de paquetes](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) en la API de herramientas de la zona protegida | Utilice la API de herramientas de zona protegida para realizar solicitudes a dos nuevos extremos, `/handshake` y `/transfer`, para compartir en varias organizaciones, recuperar y crear solicitudes de uso compartido de paquetes. Se ha agregado una solicitud adicional al extremo `/packages` para recuperar la carga útil de un paquete. |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Característica actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el filtrado de entidades de actividad estándar en [!DNL Marketo Engage] | Puede usar la API [!DNL Flow Service] para filtrar entidades de actividad estándar al ingerir datos de su origen [!DNL Marketo Engage]. Lea la guía sobre [filtrado [!DNL Marketo] datos de actividad estándar](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de fuentes](../../sources/home.md).
