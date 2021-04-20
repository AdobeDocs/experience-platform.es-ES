---
keywords: Experience Platform;inicio;temas populares;actualizar flujos de datos;editar programación
description: Este tutorial trata los pasos para actualizar una programación de flujo de datos, incluida la frecuencia de ingesta y la velocidad de intervalo, mediante el espacio de trabajo de fuentes.
solution: Experience Platform
title: Actualizar un flujo de datos de conexión de origen en la interfaz de usuario
topic: sobre validación
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Actualizar flujos de datos en la interfaz de usuario

Este tutorial le proporciona pasos sobre cómo actualizar un flujo de datos de origen existente, incluida información sobre la edición de una programación y asignación de flujo de datos, mediante el espacio de trabajo [!UICONTROL Sources].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
- [Simuladores para pruebas](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Editar asignación

>[!NOTE]
>
>Actualmente, la función de edición de asignación no es compatible con las siguientes fuentes: Adobe Analytics, Adobe Audience Manager, API HTTP y [!DNL Marketo Engage].

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. Seleccione **[!UICONTROL Dataflows]** en el encabezado superior para ver una lista de flujos de datos existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

La página [!UICONTROL Dataflows] contiene una lista de todos los flujos de datos existentes, incluida la información sobre su estado de ejecución, fecha de última ejecución y nombre de cuenta.

Seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para iniciar el panel de ordenación.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

El panel de ordenación proporciona una lista de todos los orígenes disponibles. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de flujos de datos pertenecientes a diferentes fuentes.

Seleccione el origen con el que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Aparecerá un menú desplegable con las opciones para actualizar el flujo de datos seleccionado. Desde aquí, puede elegir actualizar los conjuntos de asignaciones y la programación de ingesta de un flujo de datos. También puede seleccionar opciones para inspeccionar el flujo de datos en el panel de monitorización, así como desactivar o eliminar el flujo de datos.

Seleccione **[!UICONTROL Edit source]** para actualizar su asignación.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

Aparece el paso [!UICONTROL Add data]. Seleccione el formato de datos adecuado para revisar el contenido de los datos seleccionados y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

La página [!UICONTROL Mapping] proporciona una interfaz donde puede agregar y eliminar conjuntos de asignación asociados con su conjunto de datos.

>[!TIP]
>
>Las actualizaciones de asignación solo se aplican a ejecuciones de flujo de datos programadas en el futuro.

Seleccione **[!UICONTROL Add new mapping]** para agregar un nuevo conjunto de asignaciones.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

A continuación, introduzca el atributo de campo de origen adecuado y los valores de campo XDM de destino para completar el conjunto de asignación adicional. Seleccione **[!UICONTROL Next]** para continuar.

![new-mapping-added](../../images/tutorials/update-dataflows/new-mapping-added.png)

Aparece el paso [!UICONTROL Scheduling], que le permite actualizar la programación de ingesta del flujo de datos e introducir automáticamente los datos de origen seleccionados con las asignaciones actualizadas.

>[!NOTE]
>
>No se pueden actualizar conjuntos de asignaciones para flujos de datos programados para una ingesta única y la hora de inicio ya está en el pasado.

![programación](../../images/tutorials/update-dataflows/scheduling.png)

En la página [!UICONTROL Dataflow detail] puede proporcionar un nombre y una descripción actualizados para su flujo de datos, así como reconfigurar el umbral de error del flujo de datos.

Una vez que haya proporcionado los valores actualizados, seleccione **[!UICONTROL Next]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

Aparece el paso **[!UICONTROL Review]**, que le permite revisar el flujo de datos antes de actualizarlo.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finish]** y permita que transcurra algún tiempo para el flujo de datos con los nuevos conjuntos de asignaciones que se van a crear.

![review](../../images/tutorials/update-dataflows/review.png)

## Editar programación

Para editar la programación de ingesta de un flujo de datos existente, seleccione los puntos suspensivos (`...`) junto a un nombre de flujo de datos y, a continuación, seleccione **[!UICONTROL Edit schedule]** en el menú desplegable.

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

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para actualizar la programación de ingesta y los conjuntos de asignación de su flujo de datos.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante la API [!DNL Flow Service], consulte el tutorial sobre la [actualización de flujos de datos mediante la API de servicio de flujo](../../tutorials/api/update-dataflows.md).
