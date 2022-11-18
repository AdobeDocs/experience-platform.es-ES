---
title: Monitorización del uso de licencias de consulta por lotes
description: La interfaz de usuario de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias Data Distiller de su organización.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: 9d543b5c7c7f39e809b6a13b8adc46b9a99f51c7
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# (Beta) Monitorizar el uso de licencias de consulta por lotes {#monitor-license-usage}

>[!IMPORTANT]
>
>La capacidad de monitorizar el uso de licencias de consulta por lotes a través de la interfaz de usuario está en fase beta. Sus características y documentación están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias del servicio de consulta de su organización.

Para obtener instrucciones detalladas sobre cómo acceder e interactuar con el panel de uso de licencias en la interfaz de usuario, así como para obtener más información sobre las métricas disponibles que se muestran en el panel, visite [guía del panel de uso de licencias](../../dashboards/guides/license-usage.md).

Lea el [información general sobre los paneles](../../dashboards/home.md) para obtener un resumen de todas las funciones del panel en Experience Platform.

## Widgets {#widgets}

El panel de uso de licencias está compuesto por utilidades, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Las métricas visibles dependen de las licencias específicas de su organización.

Seleccione un botón de opción para elegir un simulador para análisis y utilice la lista desplegable para seleccionar un período de tiempo para el análisis. Las opciones disponibles son un período de 30 días, 90 días, 12 meses, el último año, el período de contrato completo o una fecha personalizada.

## Horas de cómputo {#compute-hours}

La variable [!UICONTROL Horas de cómputo] utiliza un gráfico de líneas para visualizar el tiempo de procesamiento diario de las consultas por lotes de su organización. El widget muestra tres métricas indicadas por un número en la parte superior izquierda del widget. Estos son

- [!UICONTROL Real]: Número total de horas de cálculo para el período de tiempo elegido en la lista desplegable Información general . Esta métrica también se indica en el gráfico mediante una línea sólida.
- [!UICONTROL Con licencia]: Número total de horas computacionales permitidas por el contrato de licencia de su organización. Esta métrica también se indica en el gráfico mediante una línea de puntos.
- [!UICONTROL Uso]: Este es el porcentaje de su uso en relación con el número máximo de horas de cálculo acordadas por su licencia.

>[!IMPORTANT]
>
>La variable [!UICONTROL Horas de cómputo] La utilidad solo es aplicable a los clientes con la licencia de Data Distiller para consultas por lotes.

![Panel de uso de licencias con el widget de horas computadas resaltado.](../images/data-distiller/compute-hours.png)
