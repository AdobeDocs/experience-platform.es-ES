---
keywords: destinos;destino;página de detalles de destinos;página de detalles de destinos
title: Ver detalles de destino
description: La página de detalles de un destino individual proporciona información general sobre los detalles del destino. Los detalles del destino incluyen el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y para habilitar y deshabilitar el flujo de datos.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: dcbc0c3ef87be0bc296992819c9b1bc3ba6317e4
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 1%

---

# Ver detalles de destino

## Información general {#overview}

En la interfaz de usuario de Adobe Experience Platform, puede ver y monitorizar los atributos y las actividades de sus destinos. Estos detalles incluyen el nombre y el ID del destino, controles para activar o desactivar los destinos, etc. Los detalles también incluyen métricas para registros de perfil activados, identidades activadas, fallidas y excluidas, y un historial de ejecuciones de flujo de datos.

>[!NOTE]
>
>La página de detalles de destinos forma parte de [!UICONTROL Destinos] workspace en [!DNL Platform] [!DNL UI]. Consulte la [[!UICONTROL Destinos] información general de workspace](./destinations-workspace.md) para obtener más información.

## Ver detalles de destino {#view-details}

Siga los pasos a continuación para ver más detalles sobre un destino existente.

1. Inicie sesión en [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccionar **[!UICONTROL Examinar]** en el encabezado superior para ver los destinos existentes.

   ![Explorar destinos](../assets/ui/details-page/browse-destinations.png)

1. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/details-page/filter.png) en la parte superior izquierda para iniciar el panel ordenar. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/details-page/filter-destinations.png)

1. Seleccione el nombre del destino que desea ver.

   ![Seleccionar destino](../assets/ui/details-page/destination-select.png)

1. Aparecerá la página de detalles del destino, con sus controles disponibles.

   ![Detalles del destino](../assets/ui/details-page/destination-details.png)

## Carril derecho {#right-rail}

El carril derecho muestra información básica sobre el destino seleccionado.

![carril derecho](../assets/ui/details-page/right-sidebar.png)

La siguiente tabla recoge los controles y detalles proporcionados por el carril derecho:

| Elemento del carril derecho | Descripción |
| --- | --- |
| [!UICONTROL Activar segmentos] | Seleccione este control para editar qué segmentos se asignan al destino, actualizar las programaciones de exportación o añadir y eliminar atributos e identidades asignados. Consulte las guías sobre [activación de datos de audiencia en destinos de flujo de segmentos](./activate-segment-streaming-destinations.md), [activación de datos de audiencia en destinos basados en perfiles por lotes](./activate-batch-profile-destinations.md), y [activación de datos de audiencia a destinos basados en perfiles de streaming](./activate-streaming-profile-destinations.md) para obtener más información. |
| [!UICONTROL Eliminar] | Permite eliminar este flujo de datos y desasigna los segmentos que se activaron anteriormente, si los hay. |
| [!UICONTROL Nombre del destino] | Este campo se puede editar para actualizar el nombre del destino. |
| [!UICONTROL Descripción] | Este campo se puede editar para actualizar o añadir una descripción opcional al destino. |
| [!UICONTROL Destino] | Representa la plataforma de destino a la que se envían las audiencias. Consulte la [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Estado] | Indica si el destino está habilitado o deshabilitado. |
| [!UICONTROL Acciones de marketing] | Indica las acciones de marketing (casos de uso) que se aplican a este destino con fines de control de datos. |
| [!UICONTROL Categoría] | Indica el tipo de destino. Consulte la [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Tipo de conexión] | Indica el formulario mediante el cual las audiencias se envían al destino. Los valores posibles incluyen [!UICONTROL Cookie] y [!UICONTROL Basado en perfiles]. |
| [!UICONTROL Frecuencia] | Indica la frecuencia con la que las audiencias se envían al destino. Los valores posibles incluyen [!UICONTROL Transmisión] y [!UICONTROL Lote]. |
| [!UICONTROL Identidad] | Representa el área de nombres de identidad aceptada por el destino, como `GAID`, `IDFA`, o `email`. Para obtener más información sobre áreas de nombres de identidad aceptadas, consulte la [información general del área de nombres de identidad](../../identity-service/namespaces.md). |
| [!UICONTROL Creado por] | Indica el usuario que creó este destino. |
| [!UICONTROL Creado] | Indica la fecha y hora UTC en que se creó este destino. |

{style="table-layout:auto"}

## [!UICONTROL Habilitado]/[!UICONTROL Desactivado] alternar {#enabled-disabled-toggle}

Puede usar el complemento **[!UICONTROL Habilitado]/[!UICONTROL Desactivado]** conmutar para iniciar y pausar todas las exportaciones de datos al destino.

![Habilitar o deshabilitar la alternancia de flujo de datos](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Ejecuciones de flujo de datos] {#dataflow-runs}

El [!UICONTROL Ejecuciones de flujo de datos] Esta pestaña proporciona datos de métricas sobre las ejecuciones del flujo de datos a destinos de flujo y por lotes. Consulte [Monitorización de flujos de datos](monitor-dataflows.md) para obtener detalles y definiciones de métricas.

>[!NOTE]
>
>* Actualmente, la funcionalidad de monitorización de destinos es compatible con todos los destinos de Experience Platform *excepto* el [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md) y [Audiencias de Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinos.
>* Para el [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), y [API HTTP](/help/destinations/catalog/streaming/http-destination.md) destinos, se estiman las métricas relacionadas con identidades excluidas, fallidas y activadas. Los volúmenes más altos de datos de activación conducen a una mayor precisión de las métricas.


![Vista de ejecuciones de flujo de datos](../assets/ui/details-page/dataflow-runs.png)

### Duración de ejecuciones de flujo de datos {#dataflow-runs-duration}

Hay una diferencia en la duración mostrada de las ejecuciones de flujo de datos entre los destinos de flujo continuo y los basados en archivos.

### Destinos de streaming {#streaming}

Mientras que el **[!UICONTROL Duración del procesamiento]** indicado para la mayoría de las ejecuciones de flujo de datos de streaming es de unas cuatro horas, como se muestra en la imagen siguiente, el tiempo de procesamiento real de cualquier ejecución de flujo de datos es mucho más corto. Las ventanas de ejecución de flujo de datos permanecen abiertas durante más tiempo en el caso de que el Experience Platform necesite volver a intentar realizar llamadas al destino y también asegurarse de que no se pierda ningún dato que llegue tarde para la misma ventana de tiempo.

![Imagen de la página de ejecuciones de flujo de datos con la columna Tiempo de procesamiento resaltada para un destino de flujo continuo.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Para obtener más información, consulte [el flujo de datos se ejecuta en destinos de streaming](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) en la documentación de monitorización.

### Destinos basados en archivos {#file-based}

Para las ejecuciones de flujo de datos a destinos basados en archivos, la variable **[!UICONTROL Duración del procesamiento]** depende del tamaño de los datos que se exportan y de la carga del sistema. Tenga en cuenta también que el flujo de datos se ejecuta en destinos basados en archivos y se desglosa por segmento.

![Imagen de la página de ejecución del flujo de datos con la columna Tiempo de procesamiento resaltada para un destino basado en archivos.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Para obtener más información, consulte [el flujo de datos se ejecuta en destinos por lotes (basados en archivos)](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) en la documentación de monitorización.

## [!UICONTROL Datos de activación] {#activation-data}

El [!UICONTROL Datos de activación] Esta pestaña muestra una lista de los segmentos que se han asignado al destino, incluida su fecha de inicio y finalización (si corresponde), y otra información relevante para la exportación de datos, como el tipo de exportación, la programación y la frecuencia. Para ver los detalles de un segmento concreto, seleccione su nombre en la lista.

>[!TIP]
>
>Para ver y editar detalles sobre los atributos y las identidades asignadas a un destino, seleccione **[!UICONTROL Activar segmentos]** en el [carril derecho](#right-rail).

![Destino del lote de vista de datos de activación](../assets/ui/details-page/activation-data-batch.png)

![Destino de flujo de vista de datos de activación](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Para obtener más información sobre cómo explorar la página de detalles de un segmento, consulte la [Resumen de IU de segmentación](../../segmentation/ui/overview.md#segment-details).
