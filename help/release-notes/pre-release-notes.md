---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: fddefb7de85b5dcb8c8721e14d04efc0567ccae4
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 22%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: miércoles, 29 de julio de 2025**

Estas son las nuevas funciones y actualizaciones de las existentes en Adobe Experience Platform:

- [Destinos](#destinations)
- [Ingesta de datos](#ingestion)
- [Servicio de consultas](#query-service)
- [Real-time CDP edición B2B](#b2b)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos actualizados**

| Destino | Descripción |
| --- | --- |
| Consolidación de tarjetas de destino de Marketo | Las tarjetas de destino de Marketo V2 y Marketo Engage Person Sync se han consolidado en una sola tarjeta de destino unificada. Esta consolidación simplifica el proceso de selección de destinos y proporciona una experiencia más optimizada para las integraciones de Marketo. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Información mejorada del flujo de datos para destinos Edge | La información mejorada del carril derecho para destinos de Adobe Target y Personalization personalizados ahora muestra el nombre del flujo de datos, lo que proporciona una visibilidad más clara de las configuraciones del flujo de datos asociadas y reduce las confusiones al revisar los flujos de datos existentes. El selector **[!UICONTROL Datastream ID]** de la pantalla de configuración de destino se ha actualizado a **[!UICONTROL Datastream]** para mejorar la claridad en la interfaz de usuario. |
| Visibilidad de acciones de marketing en selección de destino | Las acciones de marketing ahora se muestran en el carril derecho de la pestaña **[!UICONTROL Examinar]** de destino y en la página **[!UICONTROL Ejecuciones de flujo de datos]**, lo que proporciona una visibilidad inmediata de los cambios de las acciones de marketing sin que sea necesario navegar a la página de vista. Esta mejora mejora mejora la experiencia del usuario al facilitar la verificación de las configuraciones de acciones de marketing durante la configuración del destino. |
| (Beta limitada) Editar acciones de marketing para destinos | Ahora puede editar acciones de marketing para destinos existentes. Esta funcionalidad está en versión beta limitada. Para solicitar acceso, póngase en contacto con su representante de Adobe. |
| Nombres de cuenta y descripciones para conexiones de destino | Ahora puede agregar nombres y descripciones de cuentas al conectarse a destinos, lo que permite una mejor administración de los destinos con varias cuentas. |

**Correcciones**

| Problema | Descripción |
| --- | --- |
| Funcionalidad de desplazamiento por categorías | Se ha corregido un problema en el cual el menú del lado de categorías del catálogo de destinos y fuentes no se desplazaba correctamente al pasar el ratón, lo que mejoraba la capacidad de navegación de los usuarios al examinar las categorías de destino. |

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Ingesta de datos {#ingestion}

Experience Platform proporciona un marco de trabajo completo de ingesta de datos que admite la ingesta de datos por lotes y de flujo continuo desde varias fuentes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la monitorización de la ingesta de perfiles de streaming | Ya está disponible la monitorización en tiempo real de la ingesta de perfiles de flujo continuo, lo que proporciona transparencia en el rendimiento, la latencia y las métricas de calidad de los datos. Esto admite alertas proactivas y perspectivas procesables para ayudar a los ingenieros de datos a identificar infracciones de capacidad y problemas de ingesta. |

Para obtener más información, lea la [descripción general de la ingesta de datos](../ingestion/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas de Adobe Experience Platform proporciona una interfaz SQL sólida para el análisis y la exploración de datos en toda la plataforma.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Administración de sesiones mejorada | Data Distiller ahora incluye funciones mejoradas de administración de sesiones, lo que proporciona un mejor control sobre las sesiones de los usuarios y una monitorización del rendimiento mejorada en los entornos de desarrollo y producción. |
| Compatibilidad con credenciales que no caducan restricciones de caracteres de contraseña | Data Distiller ahora admite credenciales que no caducan con restricciones de caracteres específicas. Aunque las contraseñas requieren al menos un número, una letra minúscula, una letra mayúscula y un carácter especial, no se admite el signo de dólar ($). Los caracteres especiales recomendados incluyen `!, @, #, ^, or &`. |
| Se ha mejorado la coherencia de rendimiento en entornos | El rendimiento de Data Distiller ahora es coherente entre los entornos limitados de desarrollo y producción, con recursos backend similares disponibles en ambos entornos. Las horas de cálculo consumidas pueden variar en función del volumen de datos y los recursos de cálculo back-end disponibles en el momento del procesamiento. |

Para obtener más información, lea [Introducción al servicio de consultas](../query-service/home.md).

## Real-time CDP edición B2B {#b2b}

Real-Time CDP B2B edition ofrece funciones completas de administración de datos de clientes B2B, lo que permite a las organizaciones crear perfiles unificados de clientes, crear audiencias B2B sofisticadas y activar datos en varios canales de marketing.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización de la arquitectura B2B | Experience Platform actualiza a una nueva arquitectura B2B que introduce mejoras significativas en las audiencias de varias entidades con atributos B2B. Esta actualización consolida la compatibilidad con las políticas de combinación, mejora la precisión de los recuentos de audiencia y mejora las capacidades de resolución de entidades. |
| Política de combinación Consolidación para audiencias de varias entidades | Las audiencias de varias entidades con atributos B2B ahora solo admiten una única política de combinación (la política de combinación predeterminada), en lugar de admitir varias políticas de combinación. Este cambio garantiza una composición de audiencia coherente y simplifica la administración de la lógica de combinación. |
| Actualizaciones de restricciones de audiencia de cuenta | Las audiencias de cuenta ya no tienen las restricciones anteriores de una ventana retrospectiva de 30 días para eventos de experiencia, restricciones de entidad personalizadas o limitaciones al usar eventos de `inSegment`. Estas actualizaciones proporcionan una mayor flexibilidad para crear definiciones de audiencia B2B complejas. |
| Recuentos de audiencia mejorados para entidades B2B | Las estimaciones del tamaño de la audiencia para audiencias con entidades B2B como Cuentas y Oportunidades son ahora exactas, según los resultados de segmentación en tiempo real. Esta mejora proporciona estimaciones más precisas y fiables para las audiencias que implican relaciones B2B complejas. |
| Instantáneas de cuenta para miembros de audiencia | Los detalles de pertenencia a audiencias ahora se incluyen para las entidades de cuenta en las exportaciones de instantáneas, lo que permite el acceso al estado de audiencia de nivel de cuenta, las marcas de tiempo y los indicadores de pertenencia. Esto aporta paridad de características entre los modelos de segmentación de Perfil (persona) y Cuenta. |
| Cambios en las herramientas de la zona protegida para audiencias de varias entidades | Ya no es compatible la importación de audiencias de varias entidades con entidades B2B y eventos de experiencia exportados antes de la migración. Estas audiencias no podrán importar la validación y no se podrán convertir automáticamente a la nueva arquitectura. Las audiencias deben volver a exportarse después de la migración antes de importarse en las zonas protegidas de destino. |
| Degradaciones de API de entidad B2B | La creación de audiencias mediante API para entidades B2B (cuenta, oportunidad, relación cuenta-persona, relación oportunidad-persona, campaña, miembro de campaña, lista de marketing y miembro de lista de marketing) ya no se utiliza. Además, las operaciones de búsqueda y eliminación de la API de acceso a perfiles para estas entidades B2B también están en desuso. |
| Actualizaciones del área de nombres de identidad para la resolución de entidades | Las entidades Cuenta y Oportunidad ahora usan la combinación basada en la prioridad temporal con áreas de nombres de identidad específicas (`b2b_account` para Cuenta, `b2b_opportunity` para Oportunidad). Todas las demás entidades se unifican con superposiciones de identidad principales combinadas mediante una combinación basada en la prioridad temporal. |

Para obtener más información, lea la [descripción general de Real-Time CDP B2B edition](../rtcdp/b2b-overview.md).

## Zonas protegidas {#sandboxes}

Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en las importaciones de audiencias de varias entidades | La herramienta de zona protegida se ha actualizado para admitir la nueva actualización de la arquitectura B2B. Las audiencias de varias entidades que contienen entidades B2B y eventos de experiencia deben reexportarse después de la actualización de la arquitectura antes de importarse en los entornos limitados de destino mediante las herramientas de entorno limitado. La importación de versiones anteriores a la actualización no superará la validación. |

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| API de audiencia externa | Puede utilizar la API de audiencias externas para importar mediante programación audiencias generadas externamente en Adobe Experience Platform. |

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevos orígenes**

| Fuente | Descripción |
| --- | --- |
| Compatibilidad con [!DNL Didomi] (Streaming SDK) | El conector de origen [!DNL Didomi] le permite introducir datos de administración de consentimiento de la plataforma de [!DNL Didomi], lo que admite el cumplimiento de las regulaciones de privacidad y las estrategias de marketing basadas en el consentimiento. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la captura de datos de cambio en fuentes seleccionadas | Ahora puede crear flujos de datos que permitan la captura de datos modificados para la ingesta incremental mediante conectores de origen. Esta capacidad permite a los clientes introducir tipos de datos de cambio para la ingesta incremental, lo que mejora la actualización de los datos y reduce la sobrecarga de procesamiento. |
| Compatibilidad con la eliminación suave de registros en [!DNL Salesforce] | El origen [!DNL Salesforce] ahora admite la inclusión de registros eliminados de forma suave mediante un parámetro `includeDeletedObjects` opcional. Cuando se establece en true, los clientes pueden incluir registros eliminados temporalmente en sus consultas [!DNL Salesforce] e incluir estos registros en Experience Platform. |

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
