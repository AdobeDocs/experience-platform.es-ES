---
keywords: Experience Platform;inicio;temas populares;actualizar flujos de datos;editar programación
description: Este tutorial trata los pasos para actualizar una programación de flujo de datos, incluida la frecuencia de ingesta y la velocidad de intervalo, mediante el espacio de trabajo de fuentes.
solution: Experience Platform
title: Actualizar el programa de flujo de datos de la conexión de origen en la interfaz de usuario
topic: sobre validación
type: Tutorial
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# Actualizar flujos de datos en la interfaz de usuario

Este tutorial trata los pasos para actualizar una programación de flujo de datos, incluida su frecuencia de ingesta y velocidad de intervalo, utilizando el espacio de trabajo [!UICONTROL Sources].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
- [Simuladores para pruebas](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Editar programación

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. Seleccione **[!UICONTROL Dataflows]** en el encabezado superior para ver una lista de flujos de datos existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

La página [!UICONTROL Dataflows] contiene una lista de todos los flujos de datos existentes, incluida la información sobre su estado de ejecución, fecha de última ejecución y nombre de cuenta.

Seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para iniciar el panel de ordenación.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

El panel de ordenación proporciona una lista de todos los orígenes disponibles. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de flujos de datos pertenecientes a diferentes fuentes.

Seleccione el origen con el que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea volver a programar, seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta.

![volver a programar](../../images/tutorials/update-dataflows/reschedule.png)

Aparece un menú desplegable que le proporciona las opciones **[!UICONTROL Edit schedule]**, **[!UICONTROL Disable dataflow]**, **[!UICONTROL View in monitoring]** y **[!UICONTROL Delete]**. Seleccione **[!UICONTROL Edit schedule]** en el menú.

![editar-programar](../../images/tutorials/update-dataflows/edit-schedule.png)

El cuadro de diálogo **[!UICONTROL Edit schedule]** le ofrece opciones para actualizar la frecuencia de ingesta y la velocidad de intervalo del flujo de datos. Una vez configurados los valores de frecuencia e intervalo actualizados, seleccione **[!UICONTROL Save]**.

>[!NOTE]
>
>No se puede volver a programar un flujo de datos programado para una ingesta única.

![schedule-dialog](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Programación | Descripción |
| ---------- | ----------- |
| Frecuencia | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables para la programación de frecuencia de edición para un flujo de datos ya existente incluyen: `minute`, `hour`, `day` o `week`. |
| Intervalo | El intervalo designa el periodo entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero y debe ser bueno o igual a `15`. |

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la actualización se ha realizado correctamente.

![schedule-confirm](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para actualizar la programación de ingesta de un flujo de datos.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante la API [!DNL Flow Service], consulte el tutorial sobre la [actualización de flujos de datos mediante la API de servicio de flujo](../../tutorials/api/update-dataflows.md).