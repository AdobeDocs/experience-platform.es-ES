---
keywords: Experience Platform;inicio;temas populares;actualizar flujos de datos;editar programación
description: Este tutorial trata los pasos para actualizar una programación de flujo de datos, incluida su frecuencia de ingesta y tasa de intervalo, mediante el espacio de trabajo Fuentes.
solution: Experience Platform
title: Actualizar un flujo de datos de conexión de origen en la IU
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 8%

---

# Actualización de flujos de datos en la IU

Este tutorial proporciona pasos sobre cómo actualizar un flujo de datos existente, incluida su programación y asignación, mediante el espacio de trabajo de fuentes.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Actualizar flujos de datos {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Caducidad del conjunto de datos"
>abstract="Esta columna indica el número de días que le quedan al conjunto de datos de destinatario antes de que caduque automáticamente.<br>Un flujo de datos fallará si caduca el conjunto de datos de destino. Para evitar que un flujo de datos falle, asegúrese de que un conjunto de datos de destinatario esté configurado para que caduque en la fecha correcta. Consulte la documentación para obtener información sobre cómo actualizar las fechas de caducidad."

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Seleccionar **[!UICONTROL Flujos de datos]** en el encabezado superior para ver una lista de los flujos de datos existentes.

![catalogar](../../images/tutorials/update-dataflows/catalog.png)

El [!UICONTROL Flujos de datos] Esta página contiene una lista de todos los flujos de datos existentes, incluida la información sobre su conjunto de datos de destino, origen y nombre de cuenta correspondientes.

Para ordenar por la lista, seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para utilizar el panel ordenar.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

El panel de ordenación proporciona una lista de todos los orígenes disponibles. Puede seleccionar más de una fuente en la lista para acceder a una selección filtrada de flujos de datos que pertenecen a diferentes fuentes.

Seleccione la fuente con la que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Aparecerá un menú desplegable con opciones para actualizar el flujo de datos seleccionado. Desde aquí, puede elegir actualizar los conjuntos de asignaciones y la programación de ingesta de un flujo de datos. También puede seleccionar opciones para inspeccionar el flujo de datos en el panel de monitorización, suscribirse a alertas, así como deshabilitar o eliminar el flujo de datos.

Para actualizar la información del flujo de datos, seleccione **[!UICONTROL Actualizar flujo de datos]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Adición de datos

El [!UICONTROL Añadir datos] aparece el paso. Seleccione el formato de datos adecuado para revisar el contenido de los datos seleccionados y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Detalles del flujo de datos

En el [!UICONTROL Detalles del flujo de datos] , puede proporcionar un nombre y una descripción actualizados para su flujo de datos, así como reconfigurar el umbral de error del flujo de datos. Durante este paso, también puede configurar o modificar la configuración de la suscripción de alertas.

Una vez proporcionados los valores actualizados, seleccione **[!UICONTROL Siguiente]**.

![data-flow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Asignación

>[!NOTE]
>
>Actualmente, la función de asignación de edición no es compatible con las siguientes fuentes: Adobe Analytics, Adobe Audience Manager, API HTTP y [!DNL Marketo Engage].

El [!UICONTROL Asignación] proporciona una interfaz en la que puede añadir y eliminar conjuntos de asignaciones asociados al flujo de datos.

La interfaz de asignación muestra el conjunto de asignaciones existente del flujo de datos y no un nuevo conjunto de asignaciones recomendado. Las actualizaciones de asignación solo se aplican a ejecuciones de flujo de datos programadas en el futuro. No se pueden actualizar los conjuntos de asignaciones de un flujo de datos programado para una ingesta única.

Desde aquí, puede utilizar la interfaz de asignación para modificar los conjuntos de asignación aplicados al flujo de datos. Para ver los pasos detallados sobre cómo utilizar la interfaz de asignación, consulte la [guía de IU de preparación de datos](../../../data-prep/ui/mapping.md) para obtener más información.

![asignación](../../images/tutorials/update-dataflows/mapping.png)

### Programación

El [!UICONTROL Programación] Este paso aparece, lo que le permite actualizar la programación de ingesta del flujo de datos e introducir automáticamente los datos de origen seleccionados con las asignaciones actualizadas.

>[!NOTE]
>
>No puede reprogramar un flujo de datos programado para una ingesta única.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

También puede actualizar la programación de ingesta del flujo de datos mediante la opción de actualización en línea proporcionada en la página de flujos de datos.

En la página de flujos de datos, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y seleccione **[!UICONTROL Editar programación]** en el menú desplegable que aparece.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

El **[!UICONTROL Editar programación]** Este cuadro de diálogo proporciona opciones para actualizar la frecuencia de ingesta y la velocidad de intervalo del flujo de datos. Una vez configurados los valores de frecuencia e intervalo actualizados, seleccione **[!UICONTROL Guardar]**.

![ventana emergente de programación](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisión

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el flujo de datos antes de actualizarlo.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos con los nuevos conjuntos de asignaciones.

![reseña](../../images/tutorials/update-dataflows/review.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!UICONTROL Fuentes] workspace para actualizar la programación de ingesta y los conjuntos de asignaciones del flujo de datos.

Para obtener información sobre los pasos para realizar estas operaciones mediante programación usando [!DNL Flow Service] API, consulte el tutorial sobre [actualización de flujos de datos mediante la API de Flow Service](../../tutorials/api/update-dataflows.md).
