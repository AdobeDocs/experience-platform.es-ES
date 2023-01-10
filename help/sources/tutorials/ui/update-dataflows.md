---
keywords: Experience Platform;inicio;temas populares;actualizar flujos de datos;editar programación
description: Este tutorial trata los pasos para actualizar una programación de flujo de datos, incluida la frecuencia de ingesta y la velocidad de intervalo, mediante el espacio de trabajo de fuentes.
solution: Experience Platform
title: Actualizar un flujo de datos de conexión de origen en la interfaz de usuario
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Actualizar flujos de datos en la interfaz de usuario

Este tutorial le proporciona pasos sobre cómo actualizar un flujo de datos existente, incluida su programación y asignación, utilizando el espacio de trabajo de fuentes.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Actualizar flujos de datos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. Select **[!UICONTROL Flujos de datos]** en el encabezado superior para ver una lista de flujos de datos existentes.

![catálogo](../../images/tutorials/update-dataflows/catalog.png)

La variable [!UICONTROL Flujos de datos] contiene una lista de todos los flujos de datos existentes, incluida la información sobre su conjunto de datos de destino, fuente y nombre de cuenta correspondientes.

Para ordenar por la lista, seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para utilizar el panel de ordenación.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

El panel de ordenación proporciona una lista de todos los orígenes disponibles. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de flujos de datos pertenecientes a diferentes fuentes.

Seleccione el origen con el que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Aparecerá un menú desplegable con las opciones para actualizar el flujo de datos seleccionado. Desde aquí, puede elegir actualizar los conjuntos de asignaciones y la programación de ingesta de un flujo de datos. También puede seleccionar opciones para inspeccionar el flujo de datos en el panel de monitorización, suscribirse a las alertas y deshabilitar o eliminar el flujo de datos.

Para actualizar la información del flujo de datos, seleccione **[!UICONTROL Actualizar flujo de datos]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Adición de datos

La variable [!UICONTROL Añadir datos] aparece. Seleccione el formato de datos adecuado para revisar el contenido de los datos seleccionados y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Detalles de flujo de datos

En el [!UICONTROL Detalles de flujo de datos] , puede proporcionar un nombre y una descripción actualizados para su flujo de datos, así como reconfigurar el umbral de error del flujo de datos. Durante este paso, también puede configurar o modificar la configuración de la suscripción de alertas.

Una vez que haya proporcionado los valores actualizados, seleccione **[!UICONTROL Siguiente]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Asignación

>[!NOTE]
>
>Actualmente, la función de edición de asignación no es compatible con las siguientes fuentes: Adobe Analytics, Adobe Audience Manager, API HTTP y [!DNL Marketo Engage].

La variable [!UICONTROL Asignación] proporciona una interfaz donde puede agregar y eliminar conjuntos de asignaciones asociados con su flujo de datos.

La interfaz de asignación muestra el conjunto de asignación existente de su flujo de datos y no un nuevo conjunto de asignación recomendado. Las actualizaciones de asignación solo se aplican a ejecuciones de flujo de datos programadas en el futuro. Un flujo de datos programado para una ingesta única no puede tener sus conjuntos de asignaciones actualizados.

Desde aquí, puede utilizar la interfaz de asignación para modificar los conjuntos de asignación aplicados a su flujo de datos. Para ver los pasos completos sobre cómo utilizar la interfaz de asignación, consulte la [guía de interfaz de usuario de preparación de datos](../../../data-prep/ui/mapping.md) para obtener más información.

![asignación](../../images/tutorials/update-dataflows/mapping.png)

### Programación

La variable [!UICONTROL Programación] , lo que le permite actualizar la programación de ingesta del flujo de datos e introducir automáticamente los datos de origen seleccionados con las asignaciones actualizadas.

>[!NOTE]
>
>No se puede volver a programar un flujo de datos programado para una ingesta única.

![nueva programación](../../images/tutorials/update-dataflows/new-schedule.png)

También puede actualizar la programación de ingesta del flujo de datos mediante la opción de actualización en línea que se proporciona en la página flujos de datos.

En la página flujos de datos, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Editar programación]** del menú desplegable que aparece.

![editar-programar](../../images/tutorials/update-dataflows/edit-schedule.png)

La variable **[!UICONTROL Editar programación]** El cuadro de diálogo le ofrece opciones para actualizar la frecuencia de ingesta y la velocidad de intervalo del flujo de datos. Una vez configurados los valores de frecuencia e intervalo actualizados, seleccione **[!UICONTROL Guardar]**.

![elemento emergente de programación](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisión

La variable **[!UICONTROL Consulte]** aparece, lo que le permite revisar el flujo de datos antes de actualizarlo.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que transcurra algún tiempo para que se cree el flujo de datos con los nuevos conjuntos de asignación.

![review](../../images/tutorials/update-dataflows/review.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!UICONTROL Fuentes] espacio de trabajo para actualizar la programación de ingesta y los conjuntos de asignación de su flujo de datos.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación usando la variable [!DNL Flow Service] API, consulte el tutorial sobre [actualización de flujos de datos mediante la API del servicio de flujo](../../tutorials/api/update-dataflows.md).
