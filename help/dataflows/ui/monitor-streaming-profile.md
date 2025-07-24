---
title: Monitorización de la ingesta de perfiles de streaming
description: Aprenda a utilizar el tablero de monitorización para monitorizar la ingesta de perfiles de flujo continuo
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# Monitorización de la ingesta de perfiles de streaming

Puede utilizar el panel de monitorización de la interfaz de usuario de Adobe Experience Platform para realizar una monitorización en tiempo real de las tasas de ingesta de perfiles de streaming en su organización. Utilice esta función para mejorar la transparencia del rendimiento, la latencia y las métricas de calidad de los datos que rodean los datos de flujo continuo. Además, puede utilizar esta función para alertas proactivas y recuperar perspectivas procesables para identificar posibles infracciones de capacidad y problemas de ingesta de datos.

Lea la siguiente guía para aprender a utilizar el panel de monitorización para monitorizar las tasas y métricas de los trabajos de ingesta de perfiles de streaming en su organización.

## Explicación del panel de ingesta de perfiles de streaming

Puede utilizar tres categorías de métricas diferentes en el panel de monitorización para la transmisión de la ingesta de perfiles: [!UICONTROL Rendimiento], [!UICONTROL Ingesta] y [!UICONTROL Latencia].

* **Rendimiento**: seleccione **[!UICONTROL Rendimiento]** para ver información sobre la cantidad de datos que Experience Platform está procesando durante un período de tiempo configurado. Consulte esta métrica para evaluar la eficiencia y la capacidad del sistema.
   * **Capacidad**: La cantidad máxima de datos que su zona protegida puede procesar en condiciones definidas.
   * **Rendimiento de solicitudes**: Velocidad a la que el sistema de ingesta recibe eventos, medida en eventos por segundo.
   * **Rendimiento de procesamiento**: Velocidad a la que el sistema ingiere y procesa correctamente las cargas útiles de eventos entrantes, medida en eventos por segundo.
* **Ingesta**: seleccione [!UICONTROL Ingesta] para ver información sobre los trabajos de ingesta en su zona protegida. Estos trabajos de ingesta se miden con tres métricas diferentes:
   * **Registros creados**: Cantidad total de registros creados en un período de tiempo determinado. Esta métrica representa los procesos de ingesta de datos correctos en la zona protegida.
   * **Registros con errores**: El número total de registros que no se ingirieron debido a errores.
   * **Registros perdidos**: El número total de registros que se perdieron debido a una infracción de los límites de capacidad.
* **Latencia**: seleccione [!UICONTROL Latencia] para ver información sobre la cantidad de tiempo que Experience Platform tarda en responder a una solicitud o completar una operación en un período de tiempo determinado.

## Monitorización de métricas para la ingesta de perfiles de streaming {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Monitorización de la ingesta de perfiles de streaming"
>abstract="El panel de monitorización de perfiles de flujo continuo muestra información sobre el rendimiento, las tasas de ingesta y la latencia. Utilice este tablero para ver, comprender y analizar las métricas de procesamiento de datos. de sus perfiles de streaming en Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Rendimiento de solicitudes"
>abstract="Esta métrica representa el número de eventos que entran en el sistema de ingesta por segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Rendimiento de procesamiento"
>abstract="Esta métrica representa el número de eventos que el sistema ingiere correctamente cada segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="Latencia de ingesta de P95"
>abstract="Esta métrica mide la latencia del percentil 95 desde el momento en que un evento llega a Experience Platform hasta el momento en que se incorpora correctamente en el almacén de perfiles."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Rendimiento máximo"
>abstract="Esta métrica representa el número máximo de solicitudes entrantes por segundo que entran en la ingesta de perfiles de flujo continuo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Registros ingeridos"
>abstract="Esta métrica representa el número total de registros ingeridos en el almacén de perfiles en un período de tiempo configurado."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Error de registros"
>abstract="Esta métrica representa el número total de registros que no se pudieron ingerir en el almacén de perfiles, dentro de un intervalo de tiempo configurado, debido a errores."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Registros omitidos"
>abstract="Esta métrica representa el número total de registros que se perdieron dentro de un período de tiempo configurado, debido a infracciones de configuración o capacidad."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Detalles del error"
>abstract="Esta métrica representa el número de eventos fallidos debido a errores."
>text="Learn more in documentation"

| Métrica | Descripción | Dimensiones | Frecuencia de medición |
| --- | --- | --- | --- |
| Rendimiento de solicitudes | Esta métrica representa el número de eventos que entran en el sistema de ingesta por segundo. | Zona protegida/Flujo de datos | Monitorización en tiempo real con actualización de datos cada 60 segundos. |
| Rendimiento de procesamiento | Esta métrica representa el número de eventos que el sistema ingiere correctamente cada segundo. | Zona protegida/Flujo de datos | Monitorización en tiempo real con actualización de datos cada 60 segundos. |
| Latencia de ingesta de P95 | Esta métrica mide la latencia del percentil 95 desde el momento en que un evento llega a Experience Platform hasta el momento en que se incorpora correctamente en el almacén de perfiles. | Zona protegida/Flujo de datos | Monitorización en tiempo real con actualización de datos cada 60 segundos. |
| Rendimiento máximo |
| Registros ingeridos | Esta métrica representa el número total de registros ingeridos en el almacén de perfiles en un período de tiempo configurado. | <ul><li>Zona protegida/Flujo de datos</li><li>Ejecución de flujo de datos</li></ul> | <ul><li>Zona protegida/Flujo de datos: Monitorización en tiempo real con una actualización de datos cada 60 segundos.</li><li>Ejecución de flujo de datos: Agrupado en 15 minutos.</li></ul> |
| Error de registros | Esta métrica representa el número total de registros que no se pudieron ingerir en el almacén de perfiles, dentro de un intervalo de tiempo configurado, debido a errores. | <ul><li>Zona protegida/Flujo de datos</li><li>Ejecución de flujo de datos</li></ul> | <ul><li>Zona protegida/Flujo de datos: Monitorización en tiempo real con una actualización de datos cada 60 segundos.</li><li>Ejecución de flujo de datos: Agrupado en 15 minutos.</li></ul> |
| Registros omitidos | Esta métrica representa el número total de registros que se perdieron dentro de un período de tiempo configurado, debido a infracciones de configuración o capacidad. | <ul><li>Zona protegida/Flujo de datos</li><li>Ejecución de flujo de datos</li></ul> | <ul><li>Zona protegida/Flujo de datos: Monitorización en tiempo real con una actualización de datos cada 60 segundos.</li><li>Ejecución de flujo de datos: Agrupado en 15 minutos.</li></ul> |
| Detalles del error | Esta métrica representa el número de eventos fallidos debido a errores. | Ejecución de flujo de datos | Agrupado en una ventana por hora. |

{style="table-layout:auto"}