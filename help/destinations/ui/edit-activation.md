---
keywords: editar activación, editar destino, editar destino
title: Editar flujos de datos de activación
type: Tutorial
description: Siga los pasos de este artículo para editar un flujo de datos de activación existente en Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Editar flujos de datos de activación {#edit-activation-flows}

En Adobe Experience Platform, puede editar varios componentes de flujos de datos de activación existentes en destinos, como las audiencias y atributos de perfil exportados, la frecuencia de exportación, si el flujo de datos de activación está habilitado o deshabilitado, y más.

## Editar flujos de datos {#edit-dataflows}

Siga los pasos a continuación para editar los flujos de datos de activación existentes:

1. Inicie sesión en [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccionar **[!UICONTROL Examinar]** en el encabezado superior para ver los flujos de datos de destino existentes.

   ![Explorar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/edit-activation/filter.png) en la parte superior izquierda para iniciar el panel ordenar. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Seleccione el nombre del flujo de datos de destino que desea editar.

   ![Seleccionar destino](../assets/ui/edit-activation/destination-select.png)

4. El **[!UICONTROL Ejecuciones de flujo de datos]** para el destino, mostrando sus controles disponibles. En este punto, puede editar varios componentes del flujo de datos de destino:

   * Seleccionar **[!UICONTROL Activar audiencias]** en el carril derecho para cambiar qué audiencias o atributos de perfil enviar al destino. Esta acción le lleva al flujo de trabajo de activación, que difiere según el tipo de destino. Para obtener más información, consulte las guías sobre:
      * [activación de datos de audiencia en destinos de streaming de audiencia](./activate-segment-streaming-destinations.md) (por ejemplo, Facebook o Twitter);
      * [activación de datos de audiencia en destinos basados en perfiles por lotes](./activate-batch-profile-destinations.md) (por ejemplo, Amazon S3 o Oracle Eloqua);
      * [activación de datos de audiencia a destinos basados en perfiles de streaming](./activate-streaming-profile-destinations.md) (por ejemplo, la API HTTP o Amazon Kinesis).

   * Además, puede editar el nombre y la descripción del flujo de datos de destino.
   * Puede usar el complemento **[!UICONTROL Habilitado]/[!UICONTROL Desactivado]** conmutar para iniciar y pausar todas las exportaciones de datos al destino.

   ![Detalles del destino](../assets/ui/edit-activation/destination-details.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha utilizado correctamente la variable **[!UICONTROL destinos]** workspace para actualizar los flujos de datos de destino existentes.

Para obtener más información sobre los destinos, consulte la [información general sobre destinos](../catalog/overview.md).
