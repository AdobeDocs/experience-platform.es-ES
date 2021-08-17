---
keywords: destinos;destino;página de detalles de destinos;página de detalles de destinos
title: Ver detalles de destino
description: 'La página de detalles de un destino individual proporciona una descripción general de los detalles de destino. Los detalles de destino incluyen el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
seo-description: La página de detalles de un destino individual proporciona una descripción general de los detalles de destino. Los detalles de destino incluyen el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# Ver detalles de destino

## Información general {#overview}

En la interfaz de usuario de Adobe Experience Platform, puede ver y supervisar los atributos y las actividades de los destinos. Estos detalles incluyen el nombre y el ID del destino, los controles para activar o desactivar los destinos y mucho más. Los detalles de los destinos por lotes también incluyen métricas para los registros de perfil activados y un historial de ejecuciones de flujo de datos.

>[!NOTE]
>
>La página de detalles de destinos forma parte del espacio de trabajo [!UICONTROL Destinations] en [!DNL Platform] [!DNL UI]. Consulte la [[!UICONTROL Destinations] descripción general del espacio de trabajo](./destinations-workspace.md) para obtener más información.

## Ver detalles de destino {#view-details}

Siga los pasos a continuación para ver más detalles sobre un destino existente.

1. Inicie sesión en la [interfaz de usuario del Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda. Seleccione **[!UICONTROL Browse]** en el encabezado superior para ver los destinos existentes.

   ![Examinar destinos](../assets/ui/details-page/browse-destinations.png)

1. Seleccione el icono de filtro ![Filter-icon](../assets/ui/details-page/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/details-page/filter-destinations.png)

1. Seleccione el nombre del destino que desea ver.

   ![Seleccionar destino](../assets/ui/details-page/destination-select.png)

1. Aparecerá la página de detalles del destino, que muestra sus controles disponibles. Si está viendo los detalles de un destino de lote, también aparecerá un panel de monitorización.

   ![Detalles de destino](../assets/ui/details-page/destination-details.png)

## Carril derecho

El carril derecho muestra la información básica sobre el destino seleccionado.

![carril derecho](../assets/ui/details-page/right-sidebar.png)

La tabla siguiente abarca los controles y detalles proporcionados por el carril derecho:

| Elemento de carril derecho | Descripción |
| --- | --- |
| [!UICONTROL Activar] | Seleccione este control para editar qué segmentos están asignados al destino. Para obtener más información, consulte las guías sobre [activación de datos de audiencia en destinos de flujo continuo de segmento](./activate-segment-streaming-destinations.md), [activación de datos de audiencia en destinos basados en perfiles por lotes](./activate-batch-profile-destinations.md) y [activación de datos de audiencia en destinos basados en perfiles](./activate-streaming-profile-destinations.md) de flujo continuo. |
| [!UICONTROL Eliminar] | Permite eliminar este flujo de datos y desasigna los segmentos que se activaron anteriormente, si existen. |
| [!UICONTROL Nombre de destino] | Este campo se puede editar para actualizar el nombre del destino. |
| [!UICONTROL Descripción] | Este campo se puede editar para actualizar o añadir una descripción opcional al destino. |
| [!UICONTROL Destino] | Representa la plataforma de destino a la que se envían las audiencias. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Estado] | Indica si el destino está habilitado o deshabilitado. |
| [!UICONTROL Acciones de marketing] | Indica las acciones de marketing (casos de uso) que se aplican a este destino con fines de control de datos. |
| [!UICONTROL Categoría] | Indica el tipo de destino. Consulte el [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Tipo de conexión] | Indica el formulario mediante el cual se envían las audiencias al destino. Los valores posibles incluyen [!UICONTROL Cookie] y [!UICONTROL Basada en perfiles]. |
| [!UICONTROL Frecuencia] | Indica la frecuencia con la que se envían las audiencias al destino. Los valores posibles incluyen [!UICONTROL Streaming] y [!UICONTROL Batch]. |
| [!UICONTROL Identidad] | Representa el área de nombres de identidad aceptada por el destino, como `GAID`, `IDFA` o `email`. Para obtener más información sobre los espacios de nombres de identidad aceptados, consulte la [descripción general del área de nombres de identidad](../../identity-service/namespaces.md). |
| [!UICONTROL Creado por] | Indica el usuario que ha creado este destino. |
| [!UICONTROL Creado] | Indica la fecha y hora UTC en la que se creó este destino. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Activada]/ Deshabilitada

Puede utilizar la opción **[!UICONTROL Enabled]/[!UICONTROL Disabled]** para iniciar y pausar todas las exportaciones de datos al destino.

![Activar la opción de desactivación](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Ejecuciones de flujo de datos]

La pestaña [!UICONTROL Dataflow run] proporciona datos de métricas sobre las ejecuciones del flujo de datos a destinos por lotes. Consulte [Flujos de datos del monitor](monitor-dataflows.md) para obtener más información.

## [!UICONTROL Datos de activación] {#activation-data}

La pestaña [!UICONTROL Activation data] muestra una lista de segmentos que se han asignado al destino, incluida su fecha de inicio y fecha de finalización (si corresponde). Para ver los detalles de un segmento en particular, seleccione su nombre en la lista.

![Datos de activación](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Para obtener más información sobre cómo explorar la página de detalles de un segmento, consulte [Información general de la interfaz de segmentación](../../segmentation/ui/overview.md#segment-details).
