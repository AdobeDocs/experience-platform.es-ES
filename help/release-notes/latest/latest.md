---
title: Notas de la versión de Adobe Experience Platform de junio de 2024
description: Las notas de la versión de junio de 2024 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b9707c40beec3000456510a8a384a0af58d6d9fa
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 18%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: junio de 2024**

>[!TIP]
>
>[Asistente de IA en Experience Platform](https://platform.adobe.com) ya está disponible. Utilice el asistente de IA para acelerar los flujos de trabajo en las aplicaciones de Adobe. [Más información](#ai-assistant) sobre la nueva funcionalidad.

Nuevas funciones de Adobe Experience Platform:

- [Asistente de IA](#ai-assistant)
- [Autenticación en las API de Experience Platform](#authentication-platform-apis)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Servicio de identidad](#identity-service)
- [Privacy Service](#privacy)
- [Servicio de segmentación](#segmentation)
- [Manuales de tácticas de casos de uso](#use-case-playbooks)

## Asistente de IA {#ai-assistant}

El asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

**Nueva funcionalidad**

| Función | Descripción |
| --- | --- |
| Asistente de IA en Experience Platform | Ahora puede utilizar el Asistente de IA en Experience Platform. El asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics. <br> ![Asistente de IA en Experience Platform.](../2024/assets/june/ai-assistant-full.png "Asistente de IA en Experience Platform."){width="100" zoomable="yes"} <br> Para obtener más información acerca de esta función, lea la [Guía de IU del asistente de IA](../../ai-assistant/ui-guide.md). |
| Soporte para preguntas de conocimiento del producto | [Conocimiento del producto](../../ai-assistant/home.md#product-knowledge) son conceptos y temas basados en la documentación de Experience League y pueden utilizarse para el aprendizaje específico, la detección abierta y la resolución de problemas. Puede hacer preguntas sobre el conocimiento del producto del asistente de IA como: <ul><li>¿Qué son las audiencias de similitud?</li><li>¿Cómo se calcula la riqueza de perfiles?</li><li> ¿Puedo eliminar un esquema habilitado para perfiles después de la ingesta de datos?</li></ul> |
| [!BADGE Beta]{type=Informative} Asistencia para preguntas de información operativa | [Perspectivas operativas](../../ai-assistant/home.md#operational-insights) son respuestas que genera AI Assistant sobre los objetos de metadatos, incluidos recuentos, búsquedas e impacto en el linaje. Operational Insights no observa ningún dato dentro de su zona protegida. Puede hacer preguntas sobre la información operativa del Asistente de IA como: <ul><li>¿Qué destinos están en estado activo?</li><li>¿Cuántos conjuntos de datos tengo?</li><li>Enumerar las audiencias que se utilizan en recorridos activos.</li></ul> Las perspectivas operativas son compatibles con los siguientes dominios: atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes. |
| Acceder al asistente de IA | Para acceder al Asistente de IA para Experience Platform, Real-Time CDP y Journey Optimizer, se le debe añadir a un rol que incluya el **Habilitar el asistente de IA** y **Ver perspectivas operativas** permisos. Para obtener más información, lea la [guía de acceso a funciones](../../ai-assistant/access.md). Debe utilizar el Admin Console para lo siguiente: [acceso en Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

Para obtener más información sobre el asistente de IA, lea la [Información general del asistente de IA](../../ai-assistant/home.md).

## Autenticación en las API de Experience Platform {#authentication-platform-apis}

El método JWT para obtener tokens de acceso ya no se utiliza en las nuevas integraciones y se ha sustituido por un método de autenticación de servidor a servidor OAuth más sencillo.<p>![Nuevo método de autenticación OAuth para resaltar los tokens de acceso.](/help/landing/images/api-authentication/oauth-authentication-method.png "Nuevo método de autenticación OAuth para resaltar los tokens de acceso."){width="100" zoomable="yes"}</p>

Aunque las integraciones de API existentes que utilicen el método de autenticación JWT seguirán funcionando hasta el 1 de enero de 2025, Adobe recomienda migrar las integraciones existentes al nuevo método de servidor a servidor OAuth antes de esa fecha. Lea la guía de [migración de la credencial de cuenta de servicio (JWT) a la credencial de servidor a servidor OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

## Preparación de los datos {#data-prep}

Utilice la preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Adiciones a la lista de palabras clave reservadas | Se han agregado las siguientes palabras a la lista de palabras clave reservadas de preparación de datos:<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul> Para obtener más información, lea la [guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea la [Resumen de preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Mejora de la API de exportación ad hoc para exportar audiencias externas | Ahora puede utilizar la API de exportación específica para exportar audiencias externas (carga personalizada). [Más información](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta) Funciones adicionales admitidas en la fase beta de compatibilidad con matrices de exportación | Anteriormente, al activar audiencias en destinos basados en archivos y seleccionar Usar campo calculado, se limitaba a utilizar un subconjunto de las audiencias disponibles mediante la preparación de datos. Esa limitación se ha eliminado y los clientes tienen acceso a todas las funciones disponibles a través de la preparación de datos al exportar audiencias a destinos basados en archivos. [Más información](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions). |
| Mostrar solo campos con datos en el paso de asignación | Al asignar atributos de perfil a sus destinos, ahora puede alternar entre todos los atributos de perfil o solo aquellos que contienen datos. De forma predeterminada, solo se muestran los campos con datos. Consulte las guías de activación para [lote](../../destinations/ui/activate-batch-profile-destinations.md#mapping) y [transmisión](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) destinos para obtener más información. |

{style="table-layout:auto"}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de identidad {#identity-service}

Utilice el servicio de identidad de Adobe Experience Platform para crear una vista completa de sus clientes y sus comportamientos mediante la fusión de identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Próximas funciones**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} reglas de vinculación de gráficos de identidad | Los participantes del programa beta pueden utilizar reglas de vinculación de gráficos de identidad para garantizar la representación de la entidad de la persona en el sistema al evitar &quot;dispositivos compartidos&quot; y otros escenarios de colapso de gráficos. Para lograr este objetivo, los participantes durante el programa beta tendrán acceso a tres funciones en un entorno de desarrollo limitado: <ul><li>La herramienta de simulación de gráficos para comprender cómo funciona el algoritmo de gráficos.</li><li>La pantalla de configuración de identidad para configurar áreas de nombres únicas y prioridades de área de nombres.</li><li>Un panel de identidad para obtener información sobre los gráficos ingeridos.</li></ul> Además, el programa beta incluirá mejoras en la estabilidad del comportamiento del perfil. Para obtener más información, lea la [reglas de vinculación de gráfico de identidad](../../identity-service/identity-graph-linking-rules/overview.md) documentación. |

{style="table-layout:auto"}

Para obtener más información sobre el servicio de identidad, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## [!DNL Privacy Service] {#privacy}

Varias regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad del Privacy Service con Adobe Journey Optimizer | Las funciones de Privacy Service ahora son compatibles con los protocolos de Adobe Journey Optimizer para procesar solicitudes de eliminación. Consulte la [Documentación de solicitudes de privacidad de Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) para obtener más información, o la documentación del Experience Platform para obtener una lista de [Aplicaciones de Experience Cloud integradas con Privacy Service](../../privacy-service/experience-cloud-apps.md). |

Consulte la [Introducción al Privacy Service](../../privacy-service/home.md) para obtener más información sobre el servicio.

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de restricciones de tiempo | Se ha actualizado el comportamiento para &quot;Este mes&quot; y &quot;Este año&quot;, y ahora representan el &quot;mes hasta la fecha&quot; y el &quot;año hasta la fecha&quot; respectivamente. Para obtener más información sobre este cambio, lea la [Guía del Generador de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Manuales de tácticas de casos de uso {#use-case-playbooks}

[!DNL Use Case Playbooks] están disponibles sin coste adicional para todos los clientes de Adobe Experience Platform. Para acceder a una amplia galería de libros de reproducción de casos de uso en la IU de Experience Platform, ahora puede seleccionar **[!UICONTROL Manuales]** en el panel de navegación izquierdo.

[!DNL Use Case Playbooks] están diseñadas para ayudar a superar los desafíos al comenzar con Real-time Customer Data Platform o Adobe Journey Optimizer. Ofrecen directrices y generan varios recursos que puede probar e importar en entornos de producción cuando esté listo, aunque no esté seguro de por dónde empezar o cómo producir los recursos correctos para los casos de uso previstos.

Para empezar, lea la [Resumen de casos de uso](/help/use-case-playbooks/playbooks/overview.md), que proporciona información general sobre la funcionalidad de los libros de reproducción, su propósito y una demostración completa, incluido cómo crear instancias e importar recursos generados en otros entornos de zona protegida.

Para obtener información sobre cómo acceder y configurar una zona protegida inspiradora para experimentar y explorar varios libros de reproducción de casos de uso, consulte la [Descubra el manual de implementación correcto](/help/use-case-playbooks/playbooks/discover.md) documento.

Para obtener más información acerca de [!DNL Use Case Playbooks], lea las siguientes páginas de documentación:

- Obtener una lista de todos los [manuales disponibles](/help/use-case-playbooks/playbooks/playbooks-list.md), agrupadas por producto (Real-Time CDP o Journey Optimizer).
- Obtenga información sobre qué [permissions](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) son necesarios para usted o utilice libros de reproducción y los recursos que crean.
- Comprender el [funcionalidad de sensibilización de datos](/help/use-case-playbooks/playbooks/data-awareness.md) lo que le permite duplicar recursos generados en otros entornos de zona protegida.
