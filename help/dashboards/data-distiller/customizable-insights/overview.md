---
title: Perspectivas personalizables para informes de aplicaciones ampliados
description: Aprenda a utilizar consultas SQL para generar perspectivas para sus paneles personalizados.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Perspectivas personalizables para informes de aplicaciones ampliados

Utilice consultas SQL personalizadas para extraer de forma eficaz perspectivas de diversos conjuntos de datos estructurados. Los técnicos pueden utilizar el modo query pro para realizar análisis complejos con SQL y luego compartir este análisis con usuarios no técnicos a través de gráficos en su panel personalizado o exportarlos en archivos CSV. Este método de creación de perspectivas es adecuado para tablas con relaciones claras y permite un mayor grado de personalización dentro de las perspectivas y los filtros que pueden adaptarse a casos de uso específicos.

>[!IMPORTANT]
>
>El modo de consulta profesional solo está disponible para los usuarios que han adquirido el [SKU de Data Distiller](../../../query-service/data-distiller/overview.md).

Para generar perspectivas desde SQL, primero debe crear un panel.

## Crear un tablero personalizado {#create-custom-dashboard}

Para crear un tablero personalizado, seleccione **[!UICONTROL Paneles]** en el panel de navegación izquierdo para abrir el espacio de trabajo Paneles. A continuación, seleccione **[!UICONTROL Crear tablero]**.

![El inventario Panel con el panel Crear resaltado.](../../images/customizable-insights/create-dashboard.png)

El **[!UICONTROL Crear tablero]** aparece el cuadro de diálogo. Existen dos opciones para elegir el método de creación de tableros. Para crear sus perspectivas, puede utilizar un modelo de datos existente con [[!UICONTROL Modo de diseño guiado]](../../user-defined-dashboards.md) o su propio SQL con [!UICONTROL Modo de consulta profesional].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

El uso de un modelo de datos existente tiene las ventajas de proporcionar un marco de trabajo estructurado, eficiente y escalable, adaptado a las necesidades específicas de su empresa. Para obtener información sobre cómo [crear perspectivas a partir de un modelo de datos existente](../../user-defined-dashboards.md#create-widget), consulte la guía de panel personalizado.

Las perspectivas generadas a partir de consultas SQL ofrecen una flexibilidad y una personalización mucho mayores. Los técnicos pueden utilizar el modo query pro para realizar análisis complejos en SQL y luego compartir este análisis con usuarios no técnicos a través de esta capacidad de panel. Seleccionar **[!UICONTROL Modo de consulta profesional]** seguido de **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Una vez realizada una selección, no puede cambiarla dentro de ese panel. En su lugar, debe crear un nuevo tablero con un método de creación de tablero diferente.

![El [!UICONTROL Crear tablero] Cuadro de diálogo con el modo de profesional de consulta y Guardar resaltado.](../../images/customizable-insights/query-pro-mode.png)

## Creación de un gráfico {#create-a-chart}

Consulte la [guía del modo query pro](./query-pro-mode.md) para obtener instrucciones paso a paso sobre cómo crear un gráfico con SQL.
