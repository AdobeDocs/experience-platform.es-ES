---
keywords: destinos;destino;página de detalles de destinos;página de detalles de destinos
title: Ver detalles de destino
description: La página de detalles de un destino individual proporciona una descripción general de los detalles de destino. Los detalles de destino incluyen el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a84d67e433d70cc6194ca20abc656e4b141d42a6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 2%

---

# Ver detalles de destino

## Información general {#overview}

En la interfaz de usuario de Adobe Experience Platform, puede ver y supervisar los atributos y las actividades de los destinos. Estos detalles incluyen el nombre y el ID del destino, los controles para activar o desactivar los destinos y mucho más. Los detalles también incluyen métricas para registros de perfil activados, identidades activadas, fallidas y excluidas, y un historial de ejecuciones de flujo de datos.

>[!NOTE]
>
>La página de detalles de destinos forma parte de [!UICONTROL Destinos] espacio de trabajo [!DNL Platform] [!DNL UI]. Consulte la [[!UICONTROL Destinos] información general del espacio de trabajo](./destinations-workspace.md) para obtener más información.

## Ver detalles de destino {#view-details}

Siga los pasos a continuación para ver más detalles sobre un destino existente.

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Select **[!UICONTROL Examinar]** en el encabezado superior para ver los destinos existentes.

   ![Examinar destinos](../assets/ui/details-page/browse-destinations.png)

1. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/details-page/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/details-page/filter-destinations.png)

1. Seleccione el nombre del destino que desea ver.

   ![Seleccionar destino](../assets/ui/details-page/destination-select.png)

1. Aparecerá la página de detalles del destino, que muestra sus controles disponibles.

   ![Detalles de destino](../assets/ui/details-page/destination-details.png)

## Carril derecho {#right-rail}

El carril derecho muestra la información básica sobre el destino seleccionado.

![carril derecho](../assets/ui/details-page/right-sidebar.png)

La tabla siguiente abarca los controles y detalles proporcionados por el carril derecho:

| Elemento de carril derecho | Descripción |
| --- | --- |
| [!UICONTROL Activar segmentos] | Seleccione este control para editar qué segmentos están asignados al destino, actualizar programas de exportación o agregar y eliminar atributos e identidades asignados. Consulte las guías de [activación de datos de audiencia en destinos de flujo continuo de segmento](./activate-segment-streaming-destinations.md), [activación de datos de audiencia en destinos basados en perfiles por lotes](./activate-batch-profile-destinations.md)y [activación de datos de audiencia en destinos basados en perfiles de flujo continuo](./activate-streaming-profile-destinations.md) para obtener más información. |
| [!UICONTROL Eliminar] | Permite eliminar este flujo de datos y desasigna los segmentos que se activaron anteriormente, si existen. |
| [!UICONTROL Nombre de destino] | Este campo se puede editar para actualizar el nombre del destino. |
| [!UICONTROL Descripción] | Este campo se puede editar para actualizar o añadir una descripción opcional al destino. |
| [!UICONTROL Destino] | Representa la plataforma de destino a la que se envían las audiencias. Consulte la [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Estado] | Indica si el destino está habilitado o deshabilitado. |
| [!UICONTROL Acciones de marketing] | Indica las acciones de marketing (casos de uso) que se aplican a este destino con fines de control de datos. |
| [!UICONTROL Categoría] | Indica el tipo de destino. Consulte la [catálogo de destinos](../catalog/overview.md) para obtener más información. |
| [!UICONTROL Tipo de conexión] | Indica la forma en que se envían las audiencias al destino. Los valores posibles incluyen [!UICONTROL Cookie] y [!UICONTROL Basado en perfiles]. |
| [!UICONTROL Frecuencia] | Indica la frecuencia con la que se envían las audiencias al destino. Los valores posibles incluyen [!UICONTROL Transmisión] y [!UICONTROL Lote]. |
| [!UICONTROL Identidad] | Representa el área de nombres de identidad aceptada por el destino, como `GAID`, `IDFA`o `email`. Para obtener más información sobre los espacios de nombres de identidad aceptados, consulte la [información general del área de nombres de identidad](../../identity-service/namespaces.md). |
| [!UICONTROL Creado por] | Indica el usuario que ha creado este destino. |
| [!UICONTROL Creado] | Indica la fecha y hora UTC en la que se creó este destino. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Habilitado]/[!UICONTROL Desactivado] alternar {#enabled-disabled-toggle}

Puede usar la variable **[!UICONTROL Habilitado]/[!UICONTROL Desactivado]** para iniciar y pausar todas las exportaciones de datos al destino.

![Activar o desactivar la opción de flujo de datos](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Ejecuciones de flujo de datos] {#dataflow-runs}

La variable [!UICONTROL Ejecuciones de flujo de datos] proporciona datos de métricas sobre su flujo de datos que se ejecuta en destinos de flujo de datos y por lotes. Consulte [Monitorizar flujos de datos](monitor-dataflows.md) para obtener más información y definiciones de métricas.

>[!NOTE]
>
>* La funcionalidad de monitorización de destinos está actualmente admitida para todos los destinos en el Experience Platform *except* el [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md) y [Audiencias de Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinos.
>* Para la variable [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Centros de eventos de Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)y [API HTTP](/help/destinations/catalog/streaming/http-destination.md) destinos, identidades excluidas, fallidas y activadas no se muestran actualmente.


![Vista de ejecución de flujo de datos](../assets/ui/details-page/dataflow-runs.png)

### Duración de las ejecuciones de Dataflow {#dataflow-runs-duration}

Hay un problema conocido en la duración mostrada de las ejecuciones de flujo de datos. Mientras que la variable **[!UICONTROL Duración del procesamiento]** para la mayoría de las ejecuciones de flujo de datos es de unas cuatro horas, como se muestra en la imagen siguiente, el tiempo de procesamiento real para cualquier ejecución de flujo de datos es mucho más corto. Las ventanas de ejecución de flujo de datos permanecen abiertas durante más tiempo en el caso de que el Experience Platform tenga que volver a intentar realizar llamadas al destino.

![Imagen de la página Dataflow run con la columna Processing time resaltada.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run.png)

## [!UICONTROL Datos de activación] {#activation-data}

La variable [!UICONTROL Datos de activación] muestra una lista de segmentos que se han asignado al destino, incluida la fecha de inicio y la fecha de finalización (si corresponde), así como otra información relevante para la exportación de datos, como el tipo de exportación, la programación y la frecuencia. Para ver los detalles de un segmento en particular, seleccione su nombre en la lista.

>[!TIP]
>
>Para ver y editar detalles sobre los atributos y las identidades asignados a un destino, seleccione **[!UICONTROL Activar segmentos]** en el [carril derecho](#right-rail).

![Destino del lote de vista de datos de activación](../assets/ui/details-page/activation-data-batch.png)

![Destino de flujo de vista de datos de activación](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Para obtener más información sobre cómo explorar la página de detalles de un segmento, consulte la [Información general sobre la interfaz de usuario de segmentación](../../segmentation/ui/overview.md#segment-details).
