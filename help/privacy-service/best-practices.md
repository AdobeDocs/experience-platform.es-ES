---
title: Prácticas recomendadas para Privacy Service
description: Aprenda a reducir el tiempo de procesamiento y los costes incurridos para su organización al completar solicitudes de privacidad siguiendo estas directrices de uso óptimo.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Prácticas recomendadas para Privacy Service

Utilice Privacy Service para automatizar el cumplimiento de las regulaciones de privacidad de datos cuando los clientes deseen acceder o eliminar sus datos personales de sus almacenes de datos. Para abordar estas necesidades comerciales en evolución, Privacy Service ofrece una API y una IU de RESTful para enviar solicitudes de acceso y eliminación de datos de clientes entre aplicaciones de Adobe Experience Cloud.

Esta guía describe las prácticas recomendadas para procesar de forma eficaz las solicitudes de privacidad y optimizar los tiempos de respuesta de finalización al administrar las solicitudes de datos de los clientes.

## Introducción {#getting-started}

Esta guía requiere una comprensión práctica de [Privacy Service](./home.md) y de cómo le permite administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en las aplicaciones de Adobe Experience Cloud. También se recomienda leer la guía sobre [creación de una solicitud de trabajo de privacidad en la interfaz de usuario](./ui/user-guide.md#create-a-new-privacy-job-request) o [la API](./api/overview.md), y comprender cómo realizar estas operaciones mediante programación.

## Requisitos previos {#prerequisites}

El acceso a Adobe Experience Platform Privacy Service se controla mediante permisos granulares basados en funciones en Adobe Admin Console. Necesita los permisos relevantes en un perfil de producto para utilizar funciones específicas en la interfaz de usuario y la API de Privacy Service. Póngase en contacto con el administrador del sistema si necesita permisos adicionales.

Los administradores pueden consultar la guía sobre [administración de permisos para el Privacy Service](./permissions.md) para obtener más información.

## Directrices de creación de trabajos de privacidad {#creation-guidelines}

Para optimizar el procesamiento de solicitudes y mejorar los tiempos de respuesta, tenga en cuenta las siguientes directrices al crear trabajos de privacidad. Esto se aplica tanto a la API como a los métodos de interfaz de usuario.

1. **Maximizar interesados por solicitud:** Incluya tantos interesados como sea posible, hasta 1000, por solicitud.
2. **Identificadores de grupo por eficiencia:** Agrupe varios ID para un único interesado (hasta nueve) en cada solicitud. Los **ID pueden provenir de diferentes servicios de Adobe en la misma solicitud**.
3. **Combinar los trabajos de acceso y eliminación:** Incluir los tipos de trabajo de &quot;acceso&quot; y &quot;eliminación&quot; en una sola solicitud si el interesado lo requiere.
4. **Incluir solo los productos necesarios:** Incluir solo los productos requeridos o con licencia. Los productos adicionales pueden alargar el tiempo de procesamiento y aumentar los costes.

## Monitorización del estado de trabajos de privacidad {#monitor-status}

Para monitorizar de forma eficaz los trabajos de privacidad y comprobar su estado, Privacy Service proporciona tres métodos. Los métodos disponibles se enumeran a continuación en orden de supervisión de la eficiencia y la productividad. Cada método incluye directrices de prácticas recomendadas para mejorar su experiencia, seguidas de un ejemplo de escenario ideal que combina todos los enfoques.

### Recibir notificaciones en tiempo real {#real-time-notifications}

**Eventos de E/S** ofrecen supervisión de estado casi en tiempo real mediante eventos de estado. Este es el método más eficiente, ya que evita la necesidad de implementar mecanismos de sondeo e incurrir en tráfico de API adicional.

**Recommendations:**

- **Configuración de webhook:** Configure los webhooks para recibir notificaciones push cuando se produzcan cambios de estado en los trabajos enviados. Esto ayuda en la monitorización en tiempo real.
- **Notificaciones:** Use notificaciones tanto a nivel de trabajo como de producto para ayudar a supervisar el progreso de las solicitudes.

Consulte la documentación de [suscripción a eventos de Privacy Service](./privacy-events.md) para obtener instrucciones sobre cómo configurar un registro de evento para notificaciones de Privacy Service y cómo interpretar las cargas de notificación.

### Recuperar todos los trabajos basados en filtros {#retrieve-filtered-responses-for-all-jobs}

Para recuperar todos los datos del trabajo de privacidad en función de los filtros especificados, **realice una solicitud de GET al extremo `/jobs`**. Esta llamada de API es útil para proporcionar una vista de alto nivel del estado actual del trabajo para grandes conjuntos de ID de trabajo con una sola solicitud. No contiene respuestas detalladas al producto, pero se pueden encontrar usando el extremo [`/jobs/{jobID}` ](#retrieve-detailed-responses-for-specific-jobs).

Una solicitud de GET al extremo `/jobs` se usa mejor para recopilar o comparar los datos de estado de un gran conjunto de ID de trabajo, pero **no** está pensada para actividades regulares de tipo de sondeo.

**Recommendations:**

- **Parámetros de consulta:** Use filtros específicos para reducir los resultados, por ejemplo: rangos de datos, tipos de regulación y estado (procesamiento, finalización, etc.).

Puede ver una lista de todos los trabajos de privacidad actuales de su organización a través de la interfaz de usuario de Privacy Service. Consulte [administración de trabajos de privacidad en la documentación de la interfaz de usuario](./ui/user-guide.md#job-requests) para obtener información sobre cómo filtrar la lista de solicitudes de trabajo. Alternativamente, consulte la documentación sobre el uso [del extremo /job en la API del Privacy Service](./api/privacy-jobs.md).

La documentación de la API de Privacy Service contiene detalles sobre [los filtros de parámetros de consulta disponibles](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Recuperar respuestas detalladas para un solo trabajo {#retrieve-detailed-responses-for-specific-jobs}

Para recuperar respuestas detalladas para un solo trabajo, **realice una solicitud de GET al extremo /jobs/{jobID}**. Este método está diseñado para recopilar información más detallada, como respuestas específicas del producto y mensajes de éxito. Una llamada a este extremo es la mejor manera de ver qué productos han respondido y cuáles siguen pendientes, aunque **no** está destinado a la actividad de sondeo normal.

Consulte la documentación del extremo `/jobs/{JOB_ID}` para obtener detalles sobre [cómo comprobar el estado de un trabajo específico](./api/privacy-jobs.md#check-status).

### Ejemplo de escenario ideal {#ideal-scenario}

Utilice un webhook para que el sistema pueda actualizar automáticamente los registros y proporcionar informes o alertas cuando se completen grupos de los ID de una solicitud. Si los trabajos siguen pendientes, el sistema recupera estos estados de trabajo con una solicitud de GET al extremo de la API de Privacy Service `/jobs` y proporciona una actualización de alto nivel de la lista.

Si un trabajo en particular sigue pendiente o ha devuelto un error, puede recuperar la respuesta detallada con una solicitud de GET al extremo `/job/{jobId}`.

## Datos de solicitud de acceso {#access-request-data}

Cuando se solicita información del interesado, cada servicio devuelve los datos en un formato coherente con la forma en que almacenan y utilizan dichos datos. Una vez que todos los servicios hayan completado la solicitud, se proporciona una URL de archivo .ZIP en los detalles del trabajo para permitir la descarga de estos datos. Consulte la guía de solución de problemas para obtener información sobre [cómo descargar los resultados de los trabajos de privacidad](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

A continuación se indican algunos aspectos importantes relacionados con la gestión del archivo de datos:

- Todos los archivos de almacenamiento se eliminan de los servidores de Experience Platform pasados 30 días. No puede consultar datos de clientes anteriores a 30 días.
- La estructura del archivo de almacenamiento incluye carpetas para cada producto incluido en la solicitud y los archivos de datos contenidos en ella. Los archivos o carpetas de archivo pueden estar vacíos si no se encontraron datos para el ID especificado.
- Los datos de los trabajos creados anteriormente solo son accesibles durante 30 días después de la fecha de finalización. Después de ese tiempo, los datos se eliminan del sistema y se debe realizar una nueva solicitud.

**Recommendations:**

- **Archivos de datos de Protect:** Tanto la dirección URL como el archivo .ZIP deben estar protegidos, ya que pueden contener información personal identificable (PII) del interesado.

## Consideraciones técnicas {#technical-considerations}

Al completar las solicitudes de los Privacy Service, hay que tener en cuenta determinados aspectos técnicos:

- **Período de retención de datos:** El período retrospectivo máximo es de 60 días para cualquier grupo de trabajos y el período de tiempo máximo para una consulta es de 30 días (las fechas inicial y final).
- **Tiempo de espera de puerta de enlace:** Tenga en cuenta que su solicitud puede ser rechazada de la puerta de enlace si supera los 60 segundos.
- **Control de errores:** Revise a fondo los mensajes de error y vuelva a enviar las solicitudes donde corresponda. El Privacy Service no vuelve a procesar automáticamente los trabajos tras un error.
- **Comprender los errores HTTP 429:** Familiarícese con los mensajes de error HTTP 429 y con los pasos necesarios para mitigar los problemas. Los errores HTTP 429 son el resultado de &quot;Demasiadas solicitudes&quot;. Consulte la sección [Mensajes de error comunes](./troubleshooting-guide.md#common-error-messages) de la guía de solución de problemas para obtener más información sobre cómo resolver el problema.

## Pasos siguientes

Al leer este documento, ahora dispone de los conocimientos y prácticas necesarios para un uso eficiente y eficaz del Privacy Service. A continuación, consulte la [guía de solución de problemas](./troubleshooting-guide.md) para obtener respuestas a las preguntas más frecuentes sobre Privacy Service e información sobre los errores más comunes en la API.
