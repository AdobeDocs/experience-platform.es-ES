---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: eceafa1852fc7c17660263d6ef7878a3e7bd0841
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 32%

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

**Fecha de lanzamiento: febrero de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Alertas](#alerts)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator le permite crear e implementar agentes con tecnología de IA que pueden automatizar flujos de trabajo e interactuar con los clientes en varios canales.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Agente de incorporación de datos | Utilice el agente de incorporación de datos para configurar conexiones de origen, validar la calidad de los datos, aplicar un enriquecimiento semántico, revisar y validar esquemas y ejecutar la ingesta de datos. Siga los flujos de trabajo paso a paso para los flujos B2C y B2B, revise las salidas esperadas y solucione problemas comunes. |
| Agente de Data Distiller | Utilice el agente de Data Distiller para crear trabajos de SQL a partir de lenguaje natural, optimizar el rendimiento de SQL, recuperarse de errores de SQL, programar y administrar trabajos de SQL y supervisar el estado del trabajo. Revise las protecciones, los permisos necesarios y las directrices para solucionar problemas para empezar. |
| Agente de recopilación de datos | Utilice el agente de recopilación de datos para obtener orientación en contexto sobre configuraciones de recopilación de datos complejas y para explorar el linaje, las dependencias y las relaciones en los objetos de recopilación de datos a través de perspectivas conversacionales. |

{style="table-layout:auto"}

Para obtener más información, consulte la [documentación de Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a distintas reglas de alerta a través de la ficha [!UICONTROL Alerts] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Integración de [!DNL Slack] para alertas de cara al cliente | Ahora puede enviar alertas de cara al cliente a [!DNL Slack]. Siga el tutorial paso a paso para configurar la integración de [!DNL Slack] y recibir notificaciones de alerta directamente en el área de trabajo de [!DNL Slack]. |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Observability Insights] información general](../observability/home.md).

## Recopilación de datos {#data-collection}

La recopilación de datos de Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a Adobe Experience Platform Edge Network y otros destinos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Administración de extensiones de etiquetas de Adobe Platform | Utilice la nueva capacidad Extension Management para cargar, empaquetar y publicar las extensiones de su organización en desarrollo y distribución pública y privada. Encuentre extensiones privadas compartidas junto con sus extensiones propias en la vista de empresa de nivel superior. Esta función es compatible con extensiones web, Edge y móviles. |

{style="table-layout:auto"}

Para obtener más información, lea la [Documentación de recopilación de datos](https://experienceleague.adobe.com/es/docs/experience-platform/collection/home).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [!DNL Snowflake] lote disponible en general | El destino del lote [!DNL Snowflake] se ha trasladado a la disponibilidad general. Ahora puede ver la columna de ID de la política de combinación en los datos exportados junto con las columnas existentes, como la marca de tiempo, los atributos de asignación y la pertenencia a audiencias. |
| Compatibilidad con cifrado AES256 para [destinos de Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Ahora puede configurar el cifrado AES256 para sus exportaciones de Amazon S3. Elija entre dos opciones: <ul><li>**[!UICONTROL Default]**: Experience Platform cifra los datos en reposo con el algoritmo de cifrado predeterminado establecido en su bloque.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform agrega el encabezado `s3:x-amz-server-side-encryption": "AES256` a la exportación y cifra los datos en reposo con el algoritmo AES256 cuando aterriza en S3. **Esta opción tiene prioridad sobre cualquier algoritmo de cifrado predeterminado que configure en su compartimento de S3**.</li></ul> |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Búsqueda y Organización de Inventario de Esquema | La página de exploración de esquemas ahora incluye búsqueda y filtrado mejorados, acciones en línea y compatibilidad con etiquetas y carpetas definidas por el usuario. Estas actualizaciones facilitan la búsqueda, organización y administración de esquemas en entornos limitados, a la vez que reducen la navegación manual y el esfuerzo de mantenimiento. |
| Edición restringida para esquemas con conjuntos de datos | Las operaciones de edición que resultan en cambios importantes ahora están restringidas una vez que existe un conjunto de datos para un esquema. Cuando se asocia un conjunto de datos, ya no puede cambiar el nombre ni eliminar campos, cambiar los tipos de datos o formatos de los campos, modificar los descriptores de identidad, administrar campos relacionados para eliminar campos existentes o cambiar la clase asignada; los cambios aditivos y la obsolescencia de los campos siguen siendo compatibles. |

Para obtener más información, lea la [[!DNL XDM] información general](../xdm/home.md).

## Servicio de consultas {#query-service}

El Servicio de consultas le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Alineación de fechas de restablecimiento de proceso anual de Data Distiller (versión limitada) | Las horas de cálculo anuales de Data Distiller ahora se restablecen en la fecha de aniversario de su contrato de Data Distiller, en función del momento en que se compró o renovó la licencia. Esto alinea los informes de Uso de licencias con los términos del contrato y puede resultar en un ajuste único a los valores de uso actuales. |
| Administración de sesiones de Data Distiller (versión limitada) | Como administrador autorizado, puede ver y administrar sesiones activas del servicio de consultas y de Data Distiller dentro de su organización y zona protegida a través de la interfaz de usuario de. Utilice la administración de sesiones para identificar sesiones inactivas y finalizarlas para liberar capacidad. Las protecciones integradas evitan que termine las sesiones con consultas activas. La función registra todas las acciones de desalojo para auditar y notifica a los usuarios afectados. Necesita el permiso **Administrar sesiones de consulta** para tener acceso a esta característica. |

{style="table-layout:auto"}

Para obtener más información, lea [Introducción al servicio de consultas](../query-service/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| Compatibilidad con el catálogo Unity en el conector de origen [!DNL Databricks] | El conector de origen [!DNL Databricks] ahora es compatible con Unity Catalog. Lea la documentación actualizada de [[!DNL Databricks]](../sources/connectors/databases/databricks.md) para aprender a utilizar el catálogo Unity al configurar la conexión de origen. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
