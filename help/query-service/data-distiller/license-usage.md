---
title: Monitorizar uso de licencia de consulta por lotes
description: La interfaz de usuario de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre el uso de la licencia de Data Distiller de su organización.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: dce631923bd38f3237da3e1928e2203dc1a266ca
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Monitorizar uso de licencias de consulta por lotes {#monitor-license-usage}

El panel de uso de licencias proporciona informes granulares sobre el uso de licencias del servicio de consultas de su organización y las métricas de uso de cada producto comprado. Para obtener más información acerca de las métricas disponibles que se muestran en el panel, visite la [guía del panel de uso de licencias](../../dashboards/guides/license-usage.md#available-metrics).

El panel proporciona métricas de uso para cada producto comprado, el uso consolidado de métricas en todas las zonas protegidas de producción o desarrollo y las métricas de uso de una zona protegida específica. La información que se muestra aquí se captura durante una captura diaria de la instancia de Experience Platform. Los administradores pueden monitorizar y finalizar las sesiones del servicio de consulta inactivas para liberar capacidad cuando no haya sesiones adicionales disponibles y los usuarios estén bloqueados debido a sesiones inactivas (no activas). Consulte [Administrar sesiones del servicio de consultas](../ui/session-management.md) para obtener más información.

>[!NOTE]
>
>El panel de uso de licencias no está habilitado de forma predeterminada. Los usuarios deben tener permiso para &quot;Ver tablero de uso de licencias&quot; para poder ver el tablero. Para obtener los pasos sobre la concesión de permisos de acceso para ver el tablero de uso de licencias, consulte la [guía de permisos de tablero](../../dashboards/permissions.md).

## Calcular horas {#compute-hours}

La métrica [!UICONTROL Compute hours] solo se aplica a los clientes con licencia de Data Distiller para consultas por lotes. [!UICONTROL Compute hours] es la medida del tiempo que tardan los motores de servicios de consulta en leer, procesar y escribir datos en el lago de datos cuando se ejecuta una consulta por lotes.

![Panel de uso de licencias con la métrica de cálculo de horas resaltada.](../images/data-distiller/compute-hours.png)

Para obtener más información sobre las métricas disponibles para su organización según la licencia adquirida en su organización, consulte la [guía del tablero de uso de licencias](../../dashboards/guides/license-usage.md).
