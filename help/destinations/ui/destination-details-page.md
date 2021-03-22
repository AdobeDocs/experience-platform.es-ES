---
keywords: destinos;destino;página de detalles de destinos;página de detalles de destinos
title: Ver detalles de destino
description: 'La página de detalles de un destino individual proporciona una descripción general de los detalles de destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
seo-description: 'La página de detalles de un destino individual proporciona una descripción general de los detalles de destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Ver detalles de destino

## Información general {#overview}

En la interfaz de usuario de Adobe Experience Platform, puede ver y supervisar los atributos y las actividades de los destinos. Estos detalles incluyen el nombre y el ID del destino, los controles para activar o desactivar los destinos y mucho más. Los detalles de los destinos por lotes también incluyen métricas para los registros de perfil activados y un historial de ejecuciones de flujo de datos.

>[!NOTE]
>
>La página de detalles de destinos forma parte del espacio de trabajo [!UICONTROL Destinations] en la interfaz de usuario de Platform. Consulte la [[!UICONTROL Destinations] descripción general del espacio de trabajo](./destinations-workspace.md) para obtener más información.

En el espacio de trabajo **[!UICONTROL Destinations]** dentro de la interfaz de usuario de Platform, vaya a la pestaña **[!UICONTROL Browse]** y seleccione el nombre de un destino que desea ver.

![](../assets/ui/details-page/select-destination.png)

Aparecerá la página de detalles del destino, que muestra sus controles disponibles. Si está viendo los detalles de un destino de lote, también aparecerá un panel de monitorización.

![](../assets/ui/details-page/details.png)

Además, en la ficha Examinar, puede elegir eliminar el flujo de datos seleccionado seleccionando el icono ![papelera](../assets/ui/details-page/trash-icon.png). Los segmentos que se activen en un destino no se asignarán antes de que se elimine el flujo de datos.

![](../assets/ui/details-page/delete-flow.png)

## Carril derecho

El carril derecho muestra la información básica sobre el destino.

![](../assets/ui/details-page/right-rail.png)

La tabla siguiente abarca los controles y detalles proporcionados por el carril derecho:

| Elemento del carril derecho | Descripción |
| --- | --- |
| [!UICONTROL Activate] | Seleccione este control para editar qué segmentos están asignados al destino. Consulte la guía sobre [activación de segmentos en un destino](./activate-destinations.md) para obtener más información. |
| [!UICONTROL Delete] | Permite eliminar este flujo de datos y desasignar los segmentos que se activaron anteriormente, si existen. |
| [!UICONTROL Destination name] | Este campo se puede editar para actualizar el nombre del destino. |
| [!UICONTROL Description] | Este campo se puede editar para actualizar o añadir una descripción opcional al destino. |
| [!UICONTROL Destination] | Representa la plataforma de destino a la que se envían las audiencias. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Status] | Indica si el destino está habilitado o deshabilitado. |
| [!UICONTROL Marketing actions] | Indica las acciones de marketing (casos de uso) que se aplican a este destino con fines de control de datos. |
| [!UICONTROL Category] | Indica el tipo de destino. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Connection type] | Indica el formulario mediante el cual se envían las audiencias al destino. Los valores posibles incluyen &quot;[!UICONTROL Cookie]&quot; y &quot;[!UICONTROL Profile-based]&quot;. |
| [!UICONTROL Frequency] | Indica la frecuencia con la que se envían las audiencias al destino. Los valores posibles incluyen &quot;[!UICONTROL Streaming]&quot; y &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identity] | Representa el área de nombres de identidad aceptada por el destino, como `GAID`, `IDFA` o `email`. Para obtener más información sobre los espacios de nombres de identidad aceptados, consulte la [descripción general del área de nombres de identidad](../../identity-service/namespaces.md). |
| [!UICONTROL Created by] | Indica el usuario que ha creado este destino. |
| [!UICONTROL Created] | Indica la fecha y hora UTC en la que se creó este destino. |

## [!UICONTROL Enabled]/[!UICONTROL Disabled] alternar

Puede utilizar la opción **[!UICONTROL Enabled]/[!UICONTROL Disabled]** para iniciar y pausar todas las exportaciones de datos al destino.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

La pestaña [!UICONTROL Dataflow runs] proporciona datos de métricas sobre su flujo de datos que se ejecuta en destinos por lotes. Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de registros de perfil:

* **[!UICONTROL Profile records activated]**: Recuento total de registros de perfil creados o actualizados para la activación.
* **[!UICONTROL Profile records skipped]**: Recuento total de registros de perfil que se omiten para su activación según las salidas de perfil o los atributos que faltan.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Las ejecuciones de flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se realiza una ejecución de flujo de datos independiente para cada política de combinación aplicada a un segmento.

Para ver los detalles de una ejecución de flujo de datos determinada, seleccione la hora de inicio de la ejecución en la lista. La página de detalles de una ejecución de flujo de datos contiene información adicional, como el tamaño de los datos procesados y una lista de cualquier error que se haya producido con detalles para el diagnóstico de errores.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activation data] {#activation-data}

La pestaña [!UICONTROL Activation data] muestra una lista de segmentos que se han asignado al destino, incluida la fecha de inicio y la fecha de finalización (si corresponde). Para ver los detalles de un segmento en particular, seleccione su nombre en la lista.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Para obtener más información sobre cómo explorar la página de detalles de un segmento, consulte [Información general de la interfaz de segmentación](../../segmentation/ui/overview.md#segment-details).

## Pasos siguientes

Este documento abarcaba las capacidades de la página de detalles de destino. Para obtener más información sobre la administración de destinos en la interfaz de usuario, consulte la descripción general del [[!UICONTROL Destinations] espacio de trabajo](./destinations-workspace.md).