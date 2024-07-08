---
title: Prácticas recomendadas para Avanzadas la administración del ciclo de vida de los datos
description: Aprenda a administrar de manera eficiente las solicitudes de higiene de datos en Adobe Experience Platform utilizando la IU de administración del ciclo de vida de los datos de Avanzadas y la API de higiene de datos. Este guía cubre prácticas recomendadas, como maximizar identidades por solicitud, especificar conjuntos de datos individuales y tener en cuenta la limitación de API para evitar ralentizaciones. El documento incluye directrices para configurar la limpieza automática de conjunto de datos, cómo monitor los estados de las órdenes de trabajo y métodos detallados de recuperación de respuestas. Siga estas prácticas para optimizar el procesamiento de solicitud y optimizar los tiempos de respuesta.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Prácticas recomendadas para Avanzadas la administración del ciclo de vida de los datos

Use la IU de administración del ciclo de vida de los datos de Avanzadas y la API de higiene de datos para administrar solicitudes de limpieza y eliminar datos de Adobe Experience Platform servicios de manera eficiente. Siga estas prácticas recomendadas para optimizar el procesamiento de solicitud y optimizar los tiempos de respuesta de finalización.

## Requisitos previos {#prerequisites}

Este guía requiere una comprensión práctica del espacio de trabajo del ciclo de vida de los datos y de la API](./api/overview.md) de higiene de [datos. Antes de continuar con este documento, familiarícese con las guías sobre [administración Avanzadas ciclo de](./home.md) vida de datos y [creación de solicitudes](./ui/record-delete.md) de eliminación de registros o [caducidades de conjunto de datos en el IU](./ui/dataset-expiration.md) o a través de la API.

## Directrices para la creación de órdenes de trabajo {#work-order-creation-guidelines}

Puede usar el `/workorder` extremo de la API de limpieza de datos para registrar mediante programación administrar las solicitudes de eliminación en Experience Platform. Con este punto de conexión, puede crear una solicitud de eliminación, comprobar su estado o actualizar una solicitud existente. Consulte la [Documento final de orden de trabajo](./api/workorder.md) para obtener información sobre cómo realizar estas acciones mediante la API.

>[!TIP]
>
>Una orden de trabajo es una solicitud estructurada que realiza operaciones específicas de administración de datos, como la limpieza o transformación, para garantizar un procesamiento eficiente y sistemático.

Siga estas directrices para optimizar los envíos de solicitudes de limpieza:

1. **Maximizar identidades por solicitud:** Incluya hasta 100 000 identidades por solicitud de limpieza para mejorar la eficacia. Agrupar varias identidades en una sola solicitud ayuda a reducir la frecuencia de las llamadas a la API y minimiza el riesgo de problemas de rendimiento debido a un exceso de solicitudes de identidad única. Envíe solicitudes con los recuentos de identidad máximos para lograr un procesamiento más rápido, ya que las órdenes de trabajo se procesan por lotes para lograr una mayor eficiencia.
2. **Especifique conjuntos de datos individuales:** Para obtener la máxima eficacia, especifique el conjunto de datos individual que se va a procesar.
3. **Consideraciones de limitación de API:** Tenga en cuenta la limitación de API para evitar ralentizaciones. Solicitudes más pequeñas (&lt; 100 ID) a frecuencias más altas pueden dar lugar a 429 respuestas y requerir una nueva presentación a tasas aceptables.

### Administrar errores 429 {#manage-429-errors}

Si recibe un error 429, indica que ha superado la cantidad permitida de solicitudes en un período de tiempo determinado. Siga estas prácticas recomendadas para administrar los errores 429 de forma eficaz:

- **Lea el encabezado &quot;Reintentar después&quot;**: Cuando se devuelve un error 429, compruebe el encabezado de respuesta &quot;Reintentar después&quot;. Este encabezado especifica el tiempo de espera antes de volver a intentar el solicitud.
- **Implementar lógica** de reintento: utilice el valor &quot;Reintentar después&quot; para implementar lógica de reintento en su aplicación, asegurándose de que los reintentos se intenten después del tiempo especificado para evitar errores 429 posteriores.
- **Lote sus solicitudes**: Evite enviar numerosas solicitudes pequeñas en rápida sucesión. En su lugar, agrupe varias identidades en una sola solicitud para reducir el Frecuencia de llamadas y minimizar el riesgo de alcanzar los límites de velocidad.

## Caducidad del conjunto de datos {#dataset-expiration}

Configure la limpieza automática de conjuntos de datos para datos de corta duración. Utilice el `/ttl` punto de conexión de la API de limpieza de datos para programar fechas de caducidad para la limpieza de conjuntos de datos en función de una hora o fecha especificadas. Consulte el guía de puntos finales de caducidad de conjuntos de datos para obtener información sobre [cómo crear una caducidad](./api/dataset-expiration.md) de conjunto de datos y los [parámetros de consulta aceptados](./api/dataset-expiration.md#query-params).

## Supervise el estado de vencimiento de la orden de trabajo y del conjunto de datos {#monitor}

Puede monitor de manera eficiente el progreso de la administración del ciclo de vida de sus datos mediante el uso de eventos de **E/S**. Un evento de E/S es un mecanismo para recibir notificaciones en tiempo real sobre cambios o actualizaciones en varios servicios dentro de Platform.

Las alertas de eventos de E/S se pueden enviar a un webhook configurado para permitir la automatización de la supervisión de actividad. Para recibir alertas a través de webhook, debe registrar su webhook para Platform alertas en Adobe Systems Developer Console. Consulte el guía sobre [la suscripción a Adobe Systems notificaciones](../observability/alerts/subscribe.md) de eventos de E/S para obtener instrucciones detalladas.

Utilice los siguientes métodos y directrices del ciclo vital de datos para recuperar y supervisar de forma eficaz los estados de los trabajos:

### Eventos de E/S {#io-events}

Para supervisar de forma eficaz el progreso de las tareas del ciclo vital de datos, configure y utilice Eventos de E/S siguiendo estos pasos:

- Configure los webhooks para recibir notificaciones push para los cambios de estado.
- Utilice las notificaciones para monitorizar el progreso y recibir actualizaciones una vez completadas.
- Evite implementar mecanismos de sondeo para minimizar el tráfico de API.

### Recuperar respuestas detalladas para una única orden de trabajo {#retrieve-detailed-work-order-response}

Para obtener información detallada sobre órdenes de trabajo individuales, utilice el siguiente método:

- Realice una solicitud de GET a `/workorder/{work_order_id}` extremo para datos de respuesta detallados.
- Recupere respuestas y mensajes de éxito específicos del producto.
- Evite utilizar este método para las actividades de sondeo regulares.

Al adherirse a estas mejores prácticas, puede administrar de manera efectiva las solicitudes de limpieza y optimizar los tiempos de respuesta dentro de Avanzadas Gestión del ciclo de vida de los datos.
