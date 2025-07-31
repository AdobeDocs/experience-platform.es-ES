---
title: Notas de la versión de Adobe Experience Platform, julio de 2025
description: Las notas de la versión de julio de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 2553b8f016a20678550eed50671e3549ec42aae7
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 23%

---


# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: miércoles, 29 de julio de 2025**

Estas son las nuevas funciones y actualizaciones de las existentes en Adobe Experience Platform:

- [Capacidad](#capacity)
- [Destinos](#destinations)
- [Ingesta de datos](#data-ingestion)
- [Real-time CDP edición B2B](#b2b)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Capacidad {#capacity}

>[!AVAILABILITY]
>
>Esta función estará disponible para su uso en función de su región. Para los usuarios de las Américas, esto estará disponible a partir del 11 de agosto. Para usuarios de Europa, estará disponible a partir del 25 de agosto. Para usuarios de Asia, estará disponible a partir del 8 de septiembre.

Capacity proporciona una vista completa de las [protecciones](../../rtcdp/guardrails/overview.md) de su organización y ofrece recomendaciones sobre cómo resolver posibles infracciones de la capacidad mediante la asignación de sus capacidades en un nivel de zona protegida. Con esta versión, puede ver su capacidad de ingesta de transmisión y segmentación de transmisión.

Para obtener más información, lea [Descripción general de la capacidad](../../landing/license-usage-and-guardrails/capacity.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos actualizados**

| Destino | Descripción |
| --- | --- |
| Disponibilidad limitada de la conexión [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Después de estar disponible brevemente para todos los clientes en junio, Adobe ha devuelto esta integración a una disponibilidad limitada. Actualmente, el acceso a este destino está restringido a los clientes que ya están habilitados, mientras que Adobe y Google trabajan para resolver los problemas de implementación. Si le interesa utilizar esta integración una vez que se reanude el despliegue más amplio, póngase en contacto con su representante de Adobe para expresar su intención. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Nombres de cuenta y descripciones para conexiones de destino | Ahora puede [agregar nombres y descripciones de cuentas](/help/destinations/ui/connect-destination.md) al conectarse a destinos, lo que permite una mejor administración de los destinos con varias cuentas. |
| Información mejorada del flujo de datos para destinos Edge | La información del carril derecho para los destinos [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) y [Personalization personalizado](/help/destinations/catalog/personalization/custom-personalization.md) se ha mejorado para mostrar el nombre de la secuencia de datos, lo que ofrece una visibilidad más clara de las configuraciones de secuencia de datos asociadas y ayuda a reducir la confusión al revisar los flujos de datos existentes. El selector **[!UICONTROL Datastream ID]** de la pantalla de configuración de destino se ha actualizado a **[!UICONTROL Datastream]** para mejorar la claridad en la interfaz de usuario. |
| Visibilidad de acciones de marketing en selección de destino | Las acciones de marketing ahora se muestran en el carril derecho de la pestaña **[[!UICONTROL Examinar]](/help/destinations/ui/destinations-workspace.md#browse)** del área de trabajo Destinos y en la página **[[!UICONTROL Ejecuciones de flujo de datos]](/help/dataflows/ui/monitor-destinations.md)**, lo que proporciona visibilidad inmediata de los cambios en las acciones de marketing sin necesidad de navegar a la página de vista. Esta mejora mejora mejora la experiencia del usuario al facilitar la verificación de las configuraciones de acciones de marketing durante la configuración del destino. |
| [!BADGE Versión beta limitada]{type=Informative} Editar acciones de marketing para destinos | Ahora puede [editar acciones de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) para destinos existentes. Actualmente, esta función está en versión beta limitada. Para solicitar acceso, póngase en contacto con su representante de Adobe. |
| [!BADGE Versión beta limitada]{type=Informative} Editar destinos | Ahora puede [editar la configuración de destino](/help/destinations/ui/edit-destination.md) después de crearla. Actualmente, esta función está en versión beta limitada. Para solicitar acceso, póngase en contacto con su representante de Adobe. |

**Correcciones**

| Problema | Descripción |
| --- | --- |
| Funcionalidad de desplazamiento por categorías | Se ha corregido un problema en el cual el menú del lado de categorías del catálogo de destinos y fuentes no se desplazaba correctamente al pasar el ratón, lo que mejoraba la capacidad de navegación de los usuarios al examinar las categorías de destino. |

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Ingesta de datos {#ingestion}

Experience Platform proporciona un marco de trabajo completo de ingesta de datos que admite la ingesta de datos por lotes y de flujo continuo desde varias fuentes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la monitorización de la ingesta de perfiles de streaming | Ya está disponible la monitorización en tiempo real de la ingesta de perfiles de flujo continuo, lo que proporciona transparencia en el rendimiento, la latencia y las métricas de calidad de los datos. Esto admite alertas proactivas y perspectivas procesables para ayudar a los ingenieros de datos a identificar infracciones de capacidad y problemas de ingesta. Lea la guía sobre [supervisión de la ingesta de perfiles de transmisión](../../dataflows/ui/monitor-streaming-profile.md) para obtener más información. |

Para obtener más información, lea la [descripción general de la ingesta de datos](../../ingestion/home.md).

## Real-time CDP edición B2B {#b2b}

Real-Time CDP B2B edition ofrece funciones completas de administración de datos de clientes B2B, lo que permite a las organizaciones crear perfiles unificados de clientes, crear audiencias B2B sofisticadas y activar datos en varios canales de marketing.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de la arquitectura B2B | Experience Platform actualiza a una nueva arquitectura B2B que introduce mejoras significativas en las audiencias de varias entidades con atributos B2B. Esta actualización consolida la compatibilidad con las políticas de combinación, mejora la precisión de los recuentos de audiencia y mejora las capacidades de resolución de entidades. Lea la [descripción general de la actualización de la arquitectura de Real-Time CDP B2B edition](../../rtcdp/b2b-architecture-upgrade.md) para obtener un desglose completo de los cambios. |
| Consolidación de políticas de combinación para audiencias de varias entidades | Las audiencias de varias entidades con atributos B2B ahora solo admiten una única política de combinación (la política de combinación predeterminada), en lugar de admitir varias políticas de combinación. Este cambio garantiza una composición de audiencia coherente y simplifica la administración de la lógica de combinación. Para obtener más información, lea la [descripción general de las políticas de combinación](../../profile/merge-policies/overview.md). |
| Recuentos de audiencia mejorados para entidades B2B | Las estimaciones del tamaño de la audiencia para audiencias con entidades B2B como Cuentas y Oportunidades son ahora exactas, según los resultados de segmentación en tiempo real. Esta mejora proporciona estimaciones más precisas y fiables para las audiencias que implican relaciones B2B complejas. |
| Instantáneas de cuenta para miembros de audiencia | Los detalles de pertenencia a audiencias ahora se incluyen para las entidades de cuenta en las exportaciones de instantáneas, lo que permite el acceso al estado de audiencia de nivel de cuenta, las marcas de tiempo y los indicadores de pertenencia. Esto aporta paridad de características entre los modelos de segmentación de Perfil (persona) y Cuenta. |
| Cambios en las herramientas de la zona protegida para audiencias de varias entidades | Ya no es compatible la importación de audiencias de varias entidades con entidades B2B y eventos de experiencia exportados antes de la migración. Estas audiencias no podrán importar la validación y no se podrán convertir automáticamente a la nueva arquitectura. Las audiencias deben volver a exportarse después de la migración antes de importarse en las zonas protegidas de destino. Para obtener más información, lea la [guía de objetos admitidos para las herramientas de zonas protegidas](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Degradaciones de la API de entidad B2B | [!DNL Profile Access] operaciones de búsqueda de API para entidades B2B (relación cuenta-persona, relación oportunidad-persona, campaña, miembro de campaña, lista de marketing y miembros de lista de marketing) ya no se utilizan. Además, las operaciones de eliminación de la API [!DNL Profile Access] para entidades B2B (cuenta, relación cuenta-persona, oportunidad, relación persona-oportunidad, campaña, miembro de campaña, lista de marketing y miembros de lista de marketing) también están en desuso. Para obtener más información, lea la [guía de API de extremo de entidades](../../profile/api/entities.md). |
| Actualizaciones del área de nombres de identidad para la resolución de entidades | Las entidades Cuenta y Oportunidad ahora usan la combinación basada en la prioridad temporal con áreas de nombres de identidad específicas (`b2b_account` para Cuenta, `b2b_opportunity` para Oportunidad). Todas las demás entidades se unifican con superposiciones de identidad principales combinadas mediante una combinación basada en la prioridad temporal. Para obtener más información sobre la resolución de entidades, lea la [guía de API de extremo de entidades](../../profile/api/entities.md). |

Para obtener más información, lea la [descripción general de Real-Time CDP B2B edition](../../rtcdp/b2b-overview.md).

## Zonas protegidas {#sandboxes}

Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en las importaciones de audiencias de varias entidades | La herramienta de zona protegida se ha actualizado para admitir la nueva actualización de la arquitectura B2B. Las audiencias de varias entidades que contienen entidades B2B y eventos de experiencia deben reexportarse después de la actualización de la arquitectura antes de importarse en los entornos limitados de destino mediante las herramientas de entorno limitado. La importación de versiones anteriores a la actualización no superará la validación. Para obtener más información, lea la [guía de objetos admitidos para las herramientas de zonas protegidas](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| API de audiencia externa | Puede utilizar la API de audiencias externas para importar mediante programación audiencias generadas externamente en Adobe Experience Platform. Para obtener más información, lea la [guía de extremo de audiencias externas](../../segmentation/api/external-audiences.md). |

Para obtener más información sobre la segmentación, lea la [Descripción general del servicio de segmentación](../../segmentation/home.md)

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevos orígenes**

| Fuente | Descripción |
| --- | --- |
| Compatibilidad con [!DNL Didomi] (Streaming SDK) | Utilice el origen [!DNL Didomi] para introducir datos de administración de preferencias y consentimiento de [!DNL Didomi], lo que admite el cumplimiento de las regulaciones de privacidad y las estrategias de marketing basadas en el consentimiento. Lea la [[!DNL Didomi] descripción general del origen](../../sources/connectors/consent-and-preferences/didomi.md) para obtener información sobre cómo configurarlo. Para ver los pasos para crear una conexión de origen, lea la [[!DNL Didomi] guía de conexión de origen](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la captura de datos de cambio en orígenes seleccionados mediante la API [!DNL Flow Service] | Ahora puede crear flujos de datos que permitan la captura de datos modificados para la ingesta incremental mediante conectores de origen. Esta capacidad permite a los clientes introducir tipos de datos de cambio para la ingesta incremental, lo que mejora la actualización de los datos y reduce la sobrecarga de procesamiento. Para obtener más información, lea la documentación sobre [usando la captura de datos modificados para las fuentes](../../sources/tutorials/api/change-data-capture.md) |
| Compatibilidad con la eliminación suave de registros en [!DNL Salesforce] | El origen [!DNL Salesforce] ahora admite la inclusión de registros eliminados de forma suave mediante un parámetro `includeDeletedObjects` opcional. Cuando se establece en true, los clientes pueden incluir registros eliminados temporalmente en sus consultas [!DNL Salesforce] e incluir estos registros en Experience Platform. Lea la documentación de fuentes de [[!DNL Salesforce] ](../../sources/connectors/crm/salesforce.md) para obtener más información. |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).