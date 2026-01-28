---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 6fa71c48151e937f2e18d8b9761aad94eca85ade
workflow-type: tm+mt
source-wordcount: '1316'
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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de la versión: Enero de 2026**

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
| Moción de prueba para Agent Orchestrator | Agent Orchestrator ahora ofrece un movimiento de prueba, que permite a los clientes explorar y probar el servicio antes de comprometerse a realizar una compra completa. Esta opción de prueba antes de la compra permite a las organizaciones evaluar las capacidades de Agent Orchestrator, incluidas las habilidades y las funciones de orquestación, en su propio entorno. La prueba proporciona experiencia práctica con la creación de agentes con tecnología de IA y la comprensión de cómo se pueden integrar en flujos de trabajo existentes. |

{style="table-layout:auto"}

Para obtener más información, consulte la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| Conector de destino de Kevel ya disponible | [[!DNL Kevel]](https://www.kevel.com/) proporciona la tecnología habilitada para IA y la guía de expertos que ayudan a los líderes innovadores en comercio a lanzar, escalar y tener éxito en los medios minoristas. Retail Media Cloud de [!DNL Kevel] alimenta los formatos de anuncio personalizables, atribuibles y orientados para la publicidad dentro y fuera del sitio. |
| Ya está disponible el conector de destino de Index Exchange | [!DNL Index] es una plataforma global de suministro de publicidad que ayuda a los propietarios de medios a maximizar el valor de su contenido en todas las pantallas. Con más de 20 años de liderazgo en la industria, [!DNL Index] conecta las marcas más grandes del mundo con los creadores de experiencia premium para ofrecer experiencias de alta calidad a los consumidores. |
| Compatibilidad con puntos finales regionales para conexiones de Brazo | Todos los [extremos específicos de región](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) admitidos por [!DNL Braze] están ahora disponibles para su selección durante el flujo de configuración de destino. Pregunte a su representante de [!DNL Braze] qué instancia de extremo debe utilizar. |
| Soporte de programación semanal y mensual para la incorporación de Liveramp | Ahora puede configurar programas de exportación semanales y mensuales para el destino de incorporación de Liveramp. |
| Compatibilidad con cifrado AES256 para destinos de Amazon S3 | Ahora puede configurar el cifrado AES256 para sus exportaciones de Amazon S3. |
| Experiencia de activación mejorada para los destinos de Trade Desk y Microsoft Bing | Los destinos de Trade Desk y Microsoft Bing ahora incluyen asignaciones obligatorias predefinidas para una experiencia de activación optimizada. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Límites de protección actualizados para el destino de Adobe Target | El número máximo de audiencias que se pueden asignar a un único destino de Adobe Target ha aumentado de 50 a 250. Esto alinea Adobe Target con el límite de audiencia estándar para otros destinos, lo que proporciona una mayor flexibilidad para los flujos de trabajo de activación de audiencia. Ahora puede activar más audiencias en destinos de Adobe Target sin necesidad de crear varios flujos de datos. |
| [Editar destinos](/help/destinations/ui/edit-destination.md) y [editar acciones de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilidad general | La opción para editar destinos y acciones de marketing ya está disponible para todos los usuarios. |
| Alternar los nombres para mostrar de los campos en el paso Asignación | Al asignar campos de esquema a un destino, ahora puede alternar entre mostrar el nombre del campo XDM completo y mostrar solo el nombre para mostrar. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Perfil del cliente en tiempo real {#real-time-customer-profile}

El perfil del cliente en tiempo real permite ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Aplicación de capacidad de streaming | Experience Platform ahora impone capacidades de rendimiento de flujo continuo para el perfil del cliente en tiempo real y el servicio de identidad. Cuando los clientes exceden su capacidad de transmisión contratada, los datos se ponen en cola y se procesan del primer ingreso al primer envío. Esto garantiza un rendimiento predecible del sistema y evita que las infracciones de capacidad afecten a la calidad de la ingesta de datos. Notas importantes: Las actualizaciones de streaming no estarán disponibles en el lago de datos cuando se exceda la capacidad, esta aplicación no se aplica a los clientes con licencias de Adobe Journey Optimizer y los datos en cola se procesarán secuencialmente una vez que la capacidad esté disponible. |
| Obsolescencia de acceso a API para Real-Time CDP Prime | El acceso a la API para eventos de experiencia ya no se utiliza para todos los clientes de Real-Time CDP Prime. Este cambio afecta a la capacidad de consultar eventos de experiencia directamente mediante API. Los clientes de Real-Time CDP Ultimate pueden solicitar una excepción a través de un proceso de excepción formal para habilitar el acceso a la API de eventos de experiencia si es necesario para sus casos de uso. Esta desaprobación ayuda a alinear Real-Time CDP con la funcionalidad de las licencias. |
| Monitorización de ejecución de flujo de datos | Ahora puede monitorizar el progreso y la preparación de las ejecuciones de flujo de datos en el perfil. |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Real-Time Customer Profile] información general](../profile/home.md).

## Esquemas {#schemas}

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. Los esquemas están compuestos por una clase base y cero o más grupos de campos de esquema.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Modernización del inventario de esquemas con búsqueda, filtro, etiquetas y carpetas | La página de exploración de esquemas se ha modernizado para proporcionar capacidades de organización y descubrimiento mejoradas. Las nuevas funciones incluyen opciones avanzadas de búsqueda y filtrado, compatibilidad con etiquetas y carpetas generadas por el usuario para organizar esquemas y acciones en línea para optimizar los flujos de trabajo. Las mejoras clave incluyen: columnas actualizadas (Nombre, Clase, Conjuntos de datos, Identidades, Relaciones, Habilitar para perfil, Comportamiento, Tipo de esquema, Etiquetas, Fecha de creación, Última modificación), filtros avanzados (Mostrar perfiles, Tipo de esquema, Clase, Tiene cualquier etiqueta, Creado por, Fecha de creación, Fecha de modificación, Tiene identidad principal, Tiene relación, Área de nombres de identidad principal), acciones en línea (Editar, Eliminar, Aplicar etiquetas, Crear conjunto de datos para esquemas no relacionales, Administrar etiquetas, Mover a carpeta, Agregar a paquete, Copiar estructura JSON, Descargar archivo de muestra) y la capacidad de organizar esquemas mediante etiquetas y carpetas. Estas mejoras proporcionan una visibilidad completa de los recursos de esquema y permiten una administración de esquemas más eficiente a nivel de entorno limitado. |

Para obtener más información, lea la [[!DNL Schemas] información general](../xdm/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Actualización del TTL de audiencia externa | Las audiencias externas (como las cargas de CSV) ahora admiten la función de actualización forzada para la configuración del tiempo de vida (TTL). Esta función permite a los usuarios actualizar manualmente la caducidad del TTL para audiencias externas, lo que proporciona un mayor control sobre la administración del ciclo vital de la audiencia. Esto es especialmente útil para las audiencias que deben persistir más allá de su periodo TTL inicial o que requieren reactivación sin volver a cargar los datos. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| [!DNL Oracle Eloqua] V2 de origen | Ya está disponible un nuevo conector de origen [!DNL Oracle Eloqua] que reemplaza el conector obsoleto. Este conector actualizado proporciona funcionalidad y confiabilidad mejoradas para la ingesta de datos de [!DNL Oracle Eloqua] en Experience Platform. Los clientes que utilicen el conector existente deben migrar a la nueva implementación, ya que las conexiones existentes dejarán de funcionar. El nuevo conector admite todos los pasos de instalación y configuración necesarios para conectarse a [!DNL Oracle Eloqua] e introducir datos de automatización de marketing. |
| [!DNL Salesforce Marketing Cloud] V2 de origen | Ya está disponible un nuevo conector de origen [!DNL Salesforce Marketing Cloud] que reemplaza el conector obsoleto. Este conector actualizado proporciona un rendimiento mejorado y capacidades adicionales para la ingesta de datos de [!DNL Salesforce Marketing Cloud] en Experience Platform. Los clientes que utilicen el conector existente deben realizar la transición a la nueva implementación. El nuevo conector incluye instrucciones de configuración completas para conectarse a [!DNL Salesforce Marketing Cloud] e ingerir datos de automatización de marketing. |

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).

