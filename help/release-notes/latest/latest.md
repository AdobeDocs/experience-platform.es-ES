---
title: Notas de la versión de noviembre de 2024 de Adobe Experience Platform
description: Las notas de la versión de noviembre de 2024 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f43e120225bcca640cc46ebdce1e4d61100ad45
workflow-type: ht
source-wordcount: '852'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Ya está disponible la nueva [documentación del producto del Asistente de IA](../../ai-assistant/landing.md). Utilice esta página como centro para todos los recursos relacionados con el Asistente de IA.

**Fecha de lanzamiento: 26 de noviembre de 2024**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Asistente de IA](#ai-assistant)
- [Destinos](#destinations)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Actualizaciones de la documentación](#documentation-updates)
   - [Documentación de API de Experience Platform interactiva](#interactive-experience-platform-api-documentation)
   - [Nueva tabla de contenido en Experience League](#new-table-of-contents-on-experience-league)
   - [Nueva página de aterrizaje del Asistente de IA](#new-ai-assistant-landing-page)

## Asistente de IA {#ai-assistant}

El Asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el Asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El Asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Monitorización de cambios significativos y previsión del crecimiento del público | Utilice el Asistente de IA para monitorizar los cambios significativos y proporcionar previsiones de crecimiento para los tamaños del público y conjunto de datos.  A continuación, puede utilizar esta información para garantizar la integridad de los datos del público y ofrecer proyecciones de futuro que respalden la toma de decisiones basada en datos. Para obtener más información, lea la guía sobre [monitorización de cambios significativos y previsión del crecimiento del público](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Estimación del lenguaje natural | Utilice las capacidades de estimación del lenguaje natural del Asistente de IA para estimar los tamaños del público y predecir sus tendencias en función de preguntas simples y conversacionales. Para obtener más información, lea la guía sobre el [uso de la estimación del lenguaje natural con el Asistente de IA](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Streaming de Magnite en tiempo real](/help/destinations/catalog/advertising/magnite-streaming.md) | Exporte públicos para su activación, segmentación o supresión en la plataforma de streaming de Magnite. Tenga en cuenta que para que los públicos se exporten correctamente a Magnite, debe utilizar los destinos por lotes y en tiempo real. |
| [Lote de streaming de Magnite](/help/destinations/catalog/advertising/magnite-batch.md) | Exporte públicos para su activación, segmentación o supresión en la plataforma de streaming de Magnite. Tenga en cuenta que para que los públicos se exporten correctamente a Magnite, debe utilizar los destinos por lotes y en tiempo real. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| [Busque atributos de perfil en tiempo real en Edge](/help/destinations/ui/activate-edge-profile-lookup.md) | Aprenda a buscar atributos de perfil de Edge en tiempo real para ofrecer experiencias de personalización o informar de las reglas de toma de decisiones a través de aplicaciones descendentes, mediante la API de Edge Network y el destino de personalización personalizado. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de destinos](../../destinations/home.md).

## Servicio de consultas {#query-service}

Consulte datos en el lago de datos de Adobe Experience Platform utilizando SQL estándar con el Servicio de consultas. Combine conjuntos de datos sin problemas y genere otros nuevos a partir de los resultados de su consulta para impulsar la creación de informes, habilitar flujos de trabajo de ciencia de datos o facilitar la ingesta en el Perfil del cliente en tiempo real. Por ejemplo, puede combinar los datos de transacciones de clientes con datos de comportamiento para identificar públicos de alto valor para campañas de marketing dirigidas.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| API de autorización de Dater Distiller | Administre y aplique restricciones de acceso basadas en IP para las zonas protegidas del Servicio de consultas a fin de mejorar la seguridad de los datos y garantizar el cumplimiento de las políticas de la organización. Consulte la [Guía de la API de autorización de Data Distiller](../../query-service/auth-api/overview.md) para obtener más información sobre sus características y capacidades clave, o la [Documentación de OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) para obtener información completa, incluidos detalles de puntos finales, listas de parámetros, ejemplos de solicitud/respuesta y capacidades de prueba. |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Platform en entornos virtuales separados para ayudar a desarrollar y evolucionar las aplicaciones de la experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Uso compartido de paquetes en la API de herramientas de la zona protegida | Utilice dos nuevos puntos finales de la API, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) y [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), para controlar el uso compartido de paquetes entre organizaciones, como las aprobaciones de solicitudes, la visibilidad de paquetes y la importación de paquetes, mediante la API de herramientas de zona protegida. |

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Actualizaciones de la documentación {#documentation-updates}

### Documentación de API de Experience Platform interactiva {#interactive-api-documentation}

La [documentación de la API de Experience Platform](https://developer.adobe.com/experience-platform-apis/) es ahora completamente interactiva, lo que le permite autenticarse y explorar las API directamente en la página de documentación de referencia de la API. Ahora puede ir a la página de documentación de referencia de la API que desee, crear u obtener sus credenciales de autenticación de la API, pegarlas en el bloque **[!UICONTROL Try it]** y ejecutar la llamada. Todo en una página. [Más información](/help/landing/api-authentication.md#get-credentials-functionality) sobre la nueva funcionalidad.

### Nueva tabla de contenido en Experience League {#new-table-of-contents-on-experience-league}

Se ha mejorado la tabla de contenido de las páginas de documentación de Experience League para proporcionar una experiencia mejorada a los lectores, incluido un filtro de palabras clave para descubrir la página exacta que necesita, la capacidad de expandir todas las páginas, etc. <br> ![Nueva experiencia de tabla de contenido que incluye filtro de palabra clave y capacidad para expandir todas las páginas.](../2024/assets/november/new-toc-experience.gif "Nueva experiencia de tabla de contenido que incluye filtro de palabras clave y capacidad para expandir todas las páginas."){width="250" align="center" zoomable="yes"}

### Nueva página de aterrizaje del Asistente de IA {#new-ai-assistant-landing-page}

Utilice la nueva página de [documentación del producto del Asistente de IA](../../ai-assistant/landing.md) como centro para todas las cosas relacionadas con el Asistente de IA. Consulte la documentación del producto para ver tutoriales en vídeo, documentación técnica, casos de uso y vínculos a publicaciones de blog sobre el Asistente de IA.