---
keywords: destinos;destino;destinos página de detalles;destinos página de detalles
title: Detalles del destino de vista
description: 'La página de detalles de un destino individual proporciona una visión general de los detalles del destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
seo-description: 'La página de detalles de un destino individual proporciona una visión general de los detalles del destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---


# Detalles del destino de vista

En la interfaz de usuario de Adobe Experience Platform, puede realizar vistas y controlar los atributos y actividades de los destinos. Estos detalles incluyen el nombre y la ID del destino, los controles para activar o desactivar los destinos, etc. Los detalles de los destinos de lote también incluyen métricas de registros de perfil activados y un historial de ejecuciones de flujo de datos.

>[!NOTE]
>
>La página de detalles de destinos forma parte del espacio de trabajo [!UICONTROL Destinations] en la interfaz de usuario de la plataforma. Consulte la información general del [[!UICONTROL espacio de trabajo] Destinations](./destinations-workspace.md) para obtener más información.

En el espacio de trabajo **[!UICONTROL Destinations]** dentro de la interfaz de usuario de la plataforma, navegue a la ficha **[!UICONTROL Browse]** y seleccione el nombre de un destino al que desee realizar la vista.

![](../assets/ui/details-page/select-destination.png)

Aparece la página de detalles del destino, que muestra los controles disponibles. Si está viendo los detalles de un destino de lote, también aparece un panel de supervisión.

![](../assets/ui/details-page/details.png)

Además, en la ficha Examinar, puede elegir eliminar el flujo de datos seleccionado seleccionando el icono ![papelera](../assets/ui/details-page/trash-icon.png). Todos los segmentos que se activen en un destino no se asignarán antes de que se elimine el flujo de datos.

![](../assets/ui/details-page/delete-flow.png)

## Carril derecho

El carril derecho muestra la información básica sobre el destino.

![](../assets/ui/details-page/right-rail.png)

El cuadro siguiente abarca los controles y detalles facilitados por el carril derecho:

| Elemento del carril derecho | Descripción |
| --- | --- |
| [!UICONTROL Activar] | Seleccione este control para editar qué segmentos están asignados al destino. Consulte la guía sobre [activación de segmentos en un destino](./activate-destinations.md) para obtener más información. |
| [!UICONTROL Eliminar] | Permite eliminar este flujo de datos y desasignar los segmentos que se activaron anteriormente, si existe. |
| [!UICONTROL Nombre de destino] | Este campo se puede editar para actualizar el nombre del destino. |
| [!UICONTROL Descripción] | Este campo se puede editar para actualizar o agregar una descripción opcional al destino. |
| [!UICONTROL Destino] | Representa la plataforma de destino a la que se envían las audiencias. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Estado] | Indica si el destino está habilitado o deshabilitado. |
| [!UICONTROL Acciones de mercadotecnia] | Indica las acciones de mercadotecnia (casos de uso) que se aplican a este destino para fines de administración de datos. |
| [!UICONTROL Categoría] | Indica el tipo de destino. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Tipo de conexión] | Indica el formulario mediante el cual se envían las audiencias al destino. Los valores posibles incluyen &quot;[!UICONTROL Cookie]&quot; y &quot;[!UICONTROL basada en Perfil]&quot;. |
| [!UICONTROL Frecuencia] | Indica la frecuencia con la que se envían las audiencias al destino. Los valores posibles incluyen &quot;[!UICONTROL Streaming]&quot; y &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identidad] | Representa la Área de nombres de identidad aceptada por el destino, como `GAID`, `IDFA` o `email`. Para obtener más información sobre las Áreas de nombres de identidad aceptadas, consulte la [información general de la Área de nombres de identidad](../../identity-service/namespaces.md). |
| [!UICONTROL Creado por] | Indica el usuario que creó este destino. |
| [!UICONTROL Creado] | Indica la fecha y hora UTC en que se creó este destino. |

## [!UICONTROL Habilitado]/ Deshabilitado

Puede utilizar el **[!UICONTROL Habilitado]/[!UICONTROL Deshabilitado]** para alternar al inicio y pausar todas las exportaciones de datos al destino.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Ejecuciones de flujo de datos]

La ficha [!UICONTROL Dataflow ejecuta] proporciona datos de métricas en las ejecuciones de flujo de datos a destinos por lotes. Se muestra una lista de ejecuciones individuales y sus métricas específicas, junto con los siguientes totales para los registros de perfiles:

* **[!UICONTROL Registros de perfil activados]**: Recuento total de registros de perfiles que se crearon o actualizaron para la activación.
* **[!UICONTROL Se omitieron]** los registros de perfil: Recuento total de registros de perfiles que se omiten para la activación en función de las salidas de perfiles o los atributos que faltan.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Las ejecuciones de flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se realiza una ejecución de flujo de datos independiente para cada directiva de combinación aplicada a un segmento.

Para vista de los detalles de una ejecución de flujo de datos concreta, seleccione la hora de inicio de la ejecución en la lista. La página de detalles de una ejecución de flujo de datos contiene información adicional, como el tamaño de los datos procesados y una lista de los errores que se han producido con detalles de los diagnósticos de error.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Datos de activación]

La ficha [!UICONTROL datos de Activación] muestra una lista de segmentos que se han asignado al destino, incluyendo la fecha de inicio y la fecha de finalización (si corresponde). Para vista de los detalles de un segmento en particular, seleccione su nombre en la lista.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Para obtener más información sobre cómo explorar la página de detalles de un segmento, consulte la [información general de la interfaz de usuario de segmentación](../../segmentation/ui/overview.md#segment-details).

## Pasos siguientes

Este documento abarcaba las funciones de la página de detalles de destino. Para obtener más información sobre la administración de destinos en la interfaz de usuario, consulte la descripción general del [[!UICONTROL espacio de trabajo] destinos](./destinations-workspace.md).