---
title: Información general sobre Ejecutar y operar
description: Inspeccione, solucione problemas y optimice las implementaciones de Adobe Experience Platform con las herramientas Ejecutar y operar. Obtenga visibilidad sobre las activaciones por lotes programadas, identifique los problemas de configuración y mejore la fiabilidad del sistema.
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Información general sobre Ejecutar y operar

>[!AVAILABILITY]
>
>Actualmente, las funciones Ejecutar y Operar están disponibles como una versión limitada.

Cuando los trabajos por lotes fallan o entregan datos incompletos, debe comprender rápidamente qué causó el problema. La causa raíz podrían ser problemas de disponibilidad de datos, tiempos incorrectos, problemas de configuración o restricciones de capacidad del sistema. Sin una visibilidad clara, puede pasar horas investigando varios sistemas antes de encontrar la respuesta.

Con las herramientas de [!UICONTROL Run and Operate], puede:

* **Inspeccione sus operaciones de datos**: obtenga una vista completa del estado y el estado de ejecución del trabajo en todos sus flujos de trabajo.
* **Solucionar problemas más rápido**: Acceda a información detallada de diagnóstico e historial de ejecución para identificar rápidamente las causas raíz y reducir el tiempo medio de resolución.
* **Evitar problemas de forma proactiva**: Analice los patrones de trabajo, detecte los problemas de configuración antes de que causen errores y optimice las operaciones de datos.

## Públicos destinatarios {#target-audiences}

[!UICONTROL Run and Operate] herramientas están diseñadas para servir varias audiencias en su organización:

* **Equipos de datos y TI**: Administradores de sistemas e ingenieros de datos que mantienen canalizaciones de datos confiables y solucionan problemas técnicos.
* **Operaciones de marketing**: Los tecnólogos de marketing que inspeccionan la entrega de datos a las plataformas de marketing y resuelven los problemas de activación.
* **Implementadores**: Profesionales que validan la eficacia, confiabilidad y solución de problemas técnicos de la implementación.

## Requisitos previos {#prerequisites}

Para acceder a las herramientas Ejecutar y operar, necesita los **[!UICONTROL View Job Schedules]** y **[!UICONTROL View Profile Management]** [permisos de control de acceso](/help/access-control/home.md#permissions).
La página [!UICONTROL Job Schedules] proporciona una descripción general de todos sus trabajos de procesamiento por lotes programados.
Póngase en contacto con el administrador del sistema para asegurarse de que tiene los permisos adecuados.

## Introducción {#getting-started}

Para acceder a las herramientas Ejecutar y Operar desde la interfaz de usuario de Experience Platform:

1. Inicie sesión en su cuenta de Experience Platform y seleccione **[!UICONTROL Run and Operate]** en el panel de navegación izquierdo.
2. Seleccione la herramienta que coincida con sus necesidades de inspección o solución de problemas.

   >[!NOTE]
   >
   >Actualmente, la única capacidad disponible es [Horarios de trabajo](job-schedules.md).

![Interfaz de usuario de Experience Platform que muestra la navegación izquierda Ejecutar y operar.](assets/overview/run-and-operate.png)

## Herramientas disponibles {#available-tools}

Las siguientes herramientas le ayudan a inspeccionar y optimizar sus operaciones de datos.

### Programaciones de trabajo {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] actualmente solo están disponibles para los siguientes trabajos de Real-Time CDP:
>
> * Ingesta de lago de datos por lotes
> * Ingesta de perfil por lotes
> * Segmentación por lotes
> * Activación de destino del lote.

Con [Programas de trabajos](job-schedules.md), puede inspeccionar todas las operaciones por lotes programadas en su organización, por zona protegida, incluida la ingesta del lago de datos, la ingesta de perfiles, la segmentación y la activación de destino. Vea el estado de ejecución del trabajo, las métricas de rendimiento y el historial de ejecución para identificar patrones y diagnosticar problemas de configuración que afectan a la fiabilidad.

![IU de Experience Platform que muestra la pantalla Horarios de trabajo.](assets/overview/job-schedules-interface.png)

Los horarios de trabajo ofrecen tres niveles de investigación:

* **[Inspeccionar programaciones de trabajos](job-schedules.md)**: vea todos los conjuntos de datos y sus trabajos programados en una cronología para identificar patrones y conflictos de programación en toda la canalización.
* **[Identificar antipatrones](job-schedules-anti-patterns.md)**: Aprenda a detectar y resolver problemas comunes de configuración, como superposición de programación, apilamiento de lotes denso y procesamiento por lotes excesivo que afectan el rendimiento.
* **[Ver detalles del trabajo](job-schedules-details.md)**: Explore en profundidad conjuntos de datos específicos y ejecuciones de trabajos individuales para investigar errores, comprobar el tiempo y comprobar los registros procesados.

También puede comprender las dependencias entre las fases de procesamiento de datos, lo que le ayuda a garantizar un flujo de datos fiable a través de los flujos de trabajo de Experience Platform.

## Próximos pasos {#next-steps}

Ahora que comprende el propósito y las capacidades de las herramientas de [!UICONTROL Run and Operate], explore los siguientes recursos para profundizar sus conocimientos:

* Obtenga información sobre la [ingesta por lotes](../ingestion/batch-ingestion/overview.md) para comprender cómo se incorporan los datos en Experience Platform
* Aprenda a [inspeccionar los horarios de trabajo](job-schedules.md) para la ingesta y las activaciones por lotes
* Obtenga información sobre cómo [configurar activaciones programadas](../destinations/ui/activate-batch-profile-destinations.md) para destinos por lotes
* Explorar [monitorización de flujo de datos](../dataflows/ui/monitor-destinations.md) para destinos

