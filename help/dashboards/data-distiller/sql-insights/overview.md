---
title: SQL Insights para informes de aplicaciones extendidos
description: Aprenda a utilizar consultas SQL para generar perspectivas para sus paneles personalizados.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 3435ddd4b235c1c66cd29c75b779bcca607a5d4f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# SQL Insights para informes de aplicaciones extendidos

Utilice consultas SQL personalizadas para extraer de forma eficaz perspectivas de diversos conjuntos de datos estructurados. Los técnicos pueden utilizar el modo query pro para realizar análisis complejos con SQL y luego compartir este análisis con usuarios no técnicos a través de gráficos en su panel personalizado o exportarlos en archivos CSV. Este método de creación de perspectivas es adecuado para tablas con relaciones claras y permite un mayor grado de personalización dentro de las perspectivas y los filtros que pueden adaptarse a casos de uso específicos.

>[!IMPORTANT]
>
>El modo Query Pro solo está disponible para usuarios que hayan adquirido el [SKU de Data Distiller](../../../query-service/data-distiller/overview.md).

Para generar perspectivas desde SQL, primero debe crear un panel.

## Crear un tablero personalizado {#create-custom-dashboard}

Para crear un panel personalizado, seleccione **[!UICONTROL Paneles]** en el panel de navegación izquierdo para abrir el área de trabajo Paneles. A continuación, seleccione **[!UICONTROL Crear tablero]**.

![Se ha resaltado el inventario del panel con Crear panel.](../../images/sql-insights/create-dashboard.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Crear tablero]**. Existen dos opciones para elegir el método de creación de tableros. Para crear tus perspectivas, puedes usar un modelo de datos existente con el [[!UICONTROL modo de diseño guiado]](../../user-defined-dashboards.md) o tu propio SQL con el [!UICONTROL modo Query pro].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

El uso de un modelo de datos existente tiene las ventajas de proporcionar un marco de trabajo estructurado, eficiente y escalable, adaptado a las necesidades específicas de su empresa. Para aprender a [crear perspectivas a partir de un modelo de datos existente](../../user-defined-dashboards.md#create-widget), consulte la guía de panel personalizada.

Las perspectivas generadas a partir de consultas SQL ofrecen una flexibilidad y una personalización mucho mayores. Los técnicos pueden utilizar el modo query pro para realizar análisis complejos en SQL y luego compartir este análisis con usuarios no técnicos a través de esta capacidad de panel. Seleccione **[!UICONTROL Modo de consulta profesional]** seguido de **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Una vez realizada una selección, no puede cambiarla dentro de ese panel. En su lugar, debe crear un nuevo tablero con un método de creación de tablero diferente.

![El cuadro de diálogo [!UICONTROL Crear tablero] con el modo de Query Pro y Guardar resaltado.](../../images/sql-insights/query-pro-mode.png)

## Creación de un gráfico {#create-a-chart}

Consulte la [guía de modo de query pro](../query-pro-mode/overview.md) para obtener instrucciones paso a paso sobre cómo crear un gráfico con SQL.
