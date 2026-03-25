---
title: Información general sobre Ejecutar y operar
description: Inspeccione, solucione problemas y optimice las implementaciones de Experience Platform con las herramientas Ejecutar y operar. Obtenga visibilidad sobre las activaciones por lotes programadas, identifique los problemas de configuración y mejore la fiabilidad del sistema.
solution: Experience Platform
type: Documentation
role: Admin, User
exl-id: 7f44cdf3-4db1-47f9-bcde-401f6dcfc551
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# Información general sobre Ejecutar y operar

Cuando los trabajos por lotes fallan o entregan datos incompletos, debe comprender rápidamente qué causó el problema. La causa raíz podrían ser problemas de disponibilidad de datos, tiempos incorrectos, problemas de configuración o restricciones de capacidad del sistema. Sin una visibilidad clara, puede pasar horas investigando varios sistemas antes de encontrar la respuesta.

Con las herramientas de [!UICONTROL Run and Operate], puede:

* **Inspeccione sus operaciones de datos**: obtenga una vista completa del estado y el estado de ejecución del trabajo en todos sus flujos de trabajo.
* **Solucionar problemas más rápido**: Acceda a información detallada de diagnóstico e historial de ejecución para identificar rápidamente las causas raíz y reducir el tiempo medio de resolución.
* **Evitar problemas de forma proactiva**: Analice los patrones de trabajo, detecte los problemas de configuración antes de que causen errores y optimice las operaciones de datos.

## Públicos destinatarios {#target-audiences}

[!UICONTROL Run and Operate] herramientas están diseñadas para servir varias audiencias en su organización:

* **Equipos de datos y TI**: Administradores de sistemas e ingenieros de datos que mantienen canalizaciones de datos confiables y solucionan problemas técnicos.
* **Operaciones de marketing**: Los tecnólogos de marketing que inspeccionan la entrega de datos a las plataformas de marketing y resuelven los problemas de activación.
* **Implementadores**: Profesionales que validan la eficiencia y confiabilidad de la implementación y que solucionan problemas técnicos.

## Requisitos previos {#prerequisites}

Para acceder a las herramientas Ejecutar y operar, necesita los **[!UICONTROL View Job Schedules]** y **[!UICONTROL View Profile Management]** [permisos de control de acceso](/help/access-control/home.md#permissions). Póngase en contacto con el administrador del sistema para asegurarse de que tiene los permisos adecuados.

## Introducción {#getting-started}

Para acceder a las herramientas Ejecutar y Operar desde la interfaz de usuario de Experience Platform:

1. Inicie sesión en su cuenta de Experience Platform y seleccione **[!UICONTROL Run and Operate]** en el panel de navegación izquierdo.
2. Seleccione la herramienta que coincida con sus necesidades de inspección o solución de problemas.

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
> * Activación de destino del lote

Con [Programas de trabajos](job-schedules.md), puede inspeccionar todas las operaciones por lotes programadas en su organización, por zona protegida, incluida la ingesta del lago de datos, la ingesta de perfiles, la segmentación y la activación de destino. Vea el estado de ejecución del trabajo, las métricas de rendimiento y el historial de ejecución para identificar patrones y diagnosticar problemas de configuración que afectan a la fiabilidad.

![IU de Experience Platform que muestra la pantalla Horarios de trabajo.](assets/overview/job-schedules-interface.png)

Los horarios de trabajo ofrecen tres niveles de investigación:

* **[Inspeccionar programaciones de trabajos](job-schedules.md)**: vea todos los conjuntos de datos y sus trabajos programados en una cronología para identificar patrones y conflictos de programación en toda la canalización.
* **[Identificar antipatrones](job-schedules-anti-patterns.md)**: Aprenda a detectar y resolver problemas comunes de configuración, como superposición de programación, apilamiento de lotes denso y procesamiento por lotes excesivo que afectan el rendimiento.
* **[Ver detalles del trabajo](job-schedules-details.md)**: Explore en profundidad conjuntos de datos específicos y ejecuciones de trabajos individuales para investigar errores, comprobar el tiempo y comprobar los registros procesados.

También puede comprender las dependencias entre las fases de procesamiento de datos, lo que le ayuda a garantizar un flujo de datos fiable a través de los flujos de trabajo de Experience Platform.

### Comprobaciones de estado {#health-checks}

Con las [comprobaciones de estado](health-checks.md), puede detectar de forma proactiva los problemas de configuración de identidades y esquemas antes de que afecten a las operaciones empresariales. Actualmente, las comprobaciones de estado ejecutan análisis estáticos diarios en los esquemas y áreas de nombres de identidad, mostrando las prácticas recomendadas, las configuraciones incorrectas y los patrones que faltan y que conducen a errores descendentes.

Actualmente se evalúan cinco áreas fundacionales:

* **[Validación de campo de identidad](health-checks.md#identity-field-validation)**: compruebe que los campos de identidad tengan las restricciones de longitud y patrón adecuadas.
* **[Reglas de vinculación de gráficos de identidad](health-checks.md#identity-graph-linking-rules)**: confirme que las reglas de vinculación están configuradas para evitar el colapso del perfil.
* **[Configuración de identidad de personas y no personas](health-checks.md#people-non-people-identity)**: valide el uso correcto del tipo de identidad en todas las clases de esquema.
* **[Descripción del área de nombres de identidad personalizada](health-checks.md#namespace-missing-description)**: Asegúrese de que los metadatos del área de nombres estén completos.
* **[Áreas de nombres de identidad obsoletas](health-checks.md#deprecated-namespace)**: detecte áreas de nombres obsoletas para la limpieza.

## Próximos pasos {#next-steps}

Ahora que comprende el propósito y las capacidades de las herramientas de [!UICONTROL Run and Operate], explore los siguientes recursos para profundizar sus conocimientos:

* Aprenda a utilizar [comprobaciones de estado](health-checks.md) para detectar problemas de configuración de identidad y esquema
* Aprenda a [inspeccionar los horarios de trabajo](job-schedules.md) para la ingesta y las activaciones por lotes
* Obtenga información sobre la [ingesta por lotes](../ingestion/batch-ingestion/overview.md) para comprender cómo se incorporan los datos en Experience Platform
* Obtenga información sobre cómo [configurar activaciones programadas](../destinations/ui/activate-batch-profile-destinations.md) para destinos por lotes
* Explorar [monitorización de flujo de datos](../dataflows/ui/monitor-destinations.md) para destinos
