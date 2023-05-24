---
title: Monitorizar uso de licencia de consulta por lotes
description: La interfaz de usuario de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre el uso de la licencia de Data Distiller de su organización.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
hide: true
hidefromtoc: true
recommendations: noCatalog, display
source-git-commit: fa573dcf03eb711e946afe40d107871f5166ff58
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alpha) Monitorizar el uso de licencias de consulta por lotes {#monitor-license-usage}

>[!IMPORTANT]
>
>La capacidad de monitorizar el uso de licencias de consulta por lotes a través de la IU aún no está disponible para todos los usuarios. Esta función está en formato alfa y aún se está probando. Este documento está sujeto a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre el uso de la licencia del servicio de consultas de su organización.

Para obtener instrucciones detalladas sobre cómo acceder al panel de uso de licencias e interactuar con él en la interfaz de usuario, así como para obtener más información acerca de las métricas disponibles que se muestran en el panel, visite la [guía del tablero de uso de licencias](../../dashboards/guides/license-usage.md).

Lea el [información general sobre paneles](../../dashboards/home.md) para obtener un resumen de todas las funciones de tablero de Experience Platform.

## Widgets {#widgets}

El tablero de uso de licencias está compuesto por widgets, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Las métricas visibles dependen de las licencias específicas de su organización.

Seleccione un botón de opción para elegir una zona protegida para el análisis y utilice la lista desplegable para seleccionar un período de tiempo para el análisis. Las opciones disponibles son un periodo de 30 días, 90 días, 12 meses, el último año, el periodo contractual completo o una fecha personalizada.

## Calcular horas {#compute-hours}

El [!UICONTROL Calcular horas] Este widget utiliza un gráfico de líneas para visualizar el tiempo de procesamiento de las consultas por lotes de su organización cada día. El widget muestra tres métricas indicadas por un número en la parte superior izquierda del widget. Estos son

- [!UICONTROL Real]: El número total de horas de cálculo para el período de tiempo elegido en la lista desplegable de información general. Esta métrica también se indica en el gráfico mediante una línea sólida.
- [!UICONTROL Con licencia]: Número total de horas de cálculo permitidas por el contrato de licencia de su organización. Esta métrica también se indica en el gráfico mediante una línea de puntos.
- [!UICONTROL Uso]: Este es el porcentaje de uso en relación con las horas de cálculo máximas acordadas por la licencia.

>[!IMPORTANT]
>
>El [!UICONTROL Calcular horas] El widget solo es aplicable a los clientes con la licencia de Data Distiller para consultas por lotes.

![El tablero de uso de licencias con el widget de cálculo de horas resaltado.](../images/data-distiller/compute-hours.png)

