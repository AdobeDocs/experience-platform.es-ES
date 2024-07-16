---
title: Prácticas recomendadas para la administración avanzada del ciclo de vida de datos
description: Aprenda a administrar de forma eficaz las solicitudes de higiene de los datos en Adobe Experience Platform mediante la interfaz de usuario avanzada de administración del ciclo vital de datos y la API de higiene de datos. Esta guía describe las prácticas recomendadas, como maximizar identidades por solicitud, especificar conjuntos de datos individuales y tener en cuenta la limitación de API para evitar ralentizaciones. El documento incluye instrucciones para configurar la limpieza automática de conjuntos de datos, cómo monitorizar los estados de las órdenes de trabajo y métodos de recuperación de respuestas detallados. Siga estas prácticas para optimizar el procesamiento de las solicitudes y los tiempos de respuesta.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Prácticas recomendadas para la administración avanzada del ciclo de vida de datos

Utilice la IU de administración avanzada del ciclo vital de datos y la API de higiene de datos para administrar de forma eficaz las solicitudes de limpieza y eliminar datos de los servicios de Adobe Experience Platform. Siga estas prácticas recomendadas para optimizar el procesamiento de solicitudes y los tiempos de respuesta de finalización.

## Requisitos previos {#prerequisites}

Esta guía requiere una comprensión práctica del espacio de trabajo del ciclo vital de datos y de la [API de higiene de datos](./api/overview.md). Antes de continuar con este documento, familiarícese con las guías de [Administración avanzada del ciclo de vida de los datos](./home.md) y [creación de solicitudes de eliminación de registros](./ui/record-delete.md) o [caducidades de conjuntos de datos en la interfaz de usuario](./ui/dataset-expiration.md), o a través de la API.

## Directrices de creación de órdenes de trabajo {#work-order-creation-guidelines}

Puede usar el extremo `/workorder` en la API de higiene de datos para administrar mediante programación las solicitudes de eliminación de registros en el Experience Platform. Con este punto de conexión, puede crear una solicitud de eliminación, comprobar su estado o actualizar una solicitud existente. Consulte el [documento de extremo de orden de trabajo](./api/workorder.md) para obtener información sobre cómo realizar estas acciones mediante la API.

>[!TIP]
>
>Una orden de trabajo es una solicitud estructurada que realiza operaciones específicas de administración de datos, como la limpieza o transformación, para garantizar un procesamiento eficiente y sistemático.

Siga estas directrices para optimizar los envíos de solicitudes de limpieza:

1. **Maximizar identidades por solicitud:** Incluya hasta 100.000 identidades por solicitud de limpieza para mejorar la eficiencia. Agrupar varias identidades en una sola solicitud ayuda a reducir la frecuencia de las llamadas a la API y minimiza el riesgo de problemas de rendimiento debido a un exceso de solicitudes de identidad única. Envíe solicitudes con los recuentos de identidad máximos para lograr un procesamiento más rápido, ya que las órdenes de trabajo se procesan por lotes para lograr una mayor eficiencia.
2. **Especificar conjuntos de datos individuales:** Para lograr la máxima eficiencia, especifique el conjunto de datos individual que se procesará.
3. **Consideraciones sobre la limitación de API:** Tenga en cuenta la limitación de API para evitar ralentizaciones. Solicitudes más pequeñas (&lt; 100 ID) a frecuencias más altas pueden dar lugar a 429 respuestas y requerir una nueva presentación a tasas aceptables.

### Administrar errores 429 {#manage-429-errors}

Si recibe un error 429, indica que ha superado la cantidad permitida de solicitudes en un período de tiempo determinado. Siga estas prácticas recomendadas para administrar los errores 429 de forma eficaz:

- **Leer el encabezado &#39;Retry-After&#39;**: Cuando se devuelva un error 429, compruebe el encabezado de respuesta &#39;Retry-After&#39;. Este encabezado especifica el tiempo de espera antes de reintentar la solicitud.
- **Implementar lógica de reintento**: Use el valor &quot;Reintentar después&quot; para implementar la lógica de reintento en su aplicación, asegurándose de que los reintentos se intenten después del tiempo especificado para evitar errores 429 subsiguientes.
- **Procese sus solicitudes**: Evite enviar numerosas solicitudes pequeñas en sucesión rápida. En su lugar, agrupe varias identidades en una sola solicitud para reducir la frecuencia de las llamadas y minimizar el riesgo de alcanzar los límites de tasa.

## Caducidad del conjunto de datos {#dataset-expiration}

Configure la limpieza automática de conjuntos de datos para datos de corta duración. Utilice el extremo `/ttl` de la API de higiene de datos para programar fechas de caducidad de conjuntos de datos para la limpieza en función de una hora o fecha especificadas. Consulte la guía de extremo de caducidad del conjunto de datos para obtener información sobre cómo [crear una caducidad del conjunto de datos](./api/dataset-expiration.md) y los [parámetros de consulta aceptados](./api/dataset-expiration.md#query-params).

## Supervisar el estado de caducidad del orden de trabajo y el conjunto de datos {#monitor}

Puede supervisar de manera eficaz el progreso de la administración del ciclo de vida de los datos mediante **Eventos de E/S**. Un evento de E/S es un mecanismo para recibir notificaciones en tiempo real sobre cambios o actualizaciones en varios servicios dentro de Platform.

Las alertas de eventos de E/S se pueden enviar a un webhook configurado para habilitar la automatización de la monitorización de actividades. Para recibir alertas a través de un webhook, debe registrar su webhook para recibir alertas de Platform en Adobe Developer Console. Consulte la guía de [suscripción a notificaciones de eventos de Adobe I/O](../observability/alerts/subscribe.md) para obtener instrucciones detalladas.

Utilice los siguientes métodos y directrices del ciclo vital de datos para recuperar y supervisar de forma eficaz los estados de los trabajos:

### Eventos de E/S {#io-events}

Para supervisar de forma eficaz el progreso de las tareas del ciclo vital de datos, configure y utilice Eventos de E/S siguiendo estos pasos:

- Configure los webhooks para recibir notificaciones push para los cambios de estado.
- Utilice las notificaciones para monitorizar el progreso y recibir actualizaciones una vez completadas.
- Evite implementar mecanismos de sondeo para minimizar el tráfico de API.

### Recuperar respuestas detalladas para una única orden de trabajo {#retrieve-detailed-work-order-response}

Para obtener información detallada sobre órdenes de trabajo individuales, utilice el siguiente método:

- Realice una solicitud de GET al extremo `/workorder/{work_order_id}` para obtener datos de respuesta detallados.
- Recupere respuestas y mensajes de éxito específicos del producto.
- Evite utilizar este método para las actividades de sondeo regulares.

Si sigue estas prácticas recomendadas, podrá administrar de forma eficaz las solicitudes de limpieza y optimizar los tiempos de respuesta dentro de la administración avanzada del ciclo de vida de los datos.
