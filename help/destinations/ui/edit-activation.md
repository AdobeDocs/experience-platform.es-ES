---
keywords: editar activación, editar destino, editar destino
title: Editar flujos de datos de activación
type: Tutorial
seo-title: Edit activation dataflows
description: Siga los pasos de este artículo para editar un flujo de datos de activación existente en Adobe Experience Platform.
seo-description: Follow the steps in this article to edit an existing activation dataflow in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 2d944c7bd237efbbd4a770b3a6dd03c4133bc901
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Editar flujos de datos de activación {#edit-activation-flows}

En Adobe Experience Platform, puede editar varios componentes de flujos de datos de activación existentes en destinos, como los segmentos exportados y los atributos de perfil, la frecuencia de exportación, si el flujo de datos de activación está habilitado o deshabilitado, etc.

Siga los pasos a continuación para editar los flujos de datos de activación existentes:

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Select **[!UICONTROL Examinar]** del encabezado superior para ver los flujos de datos de destino existentes.

   ![Examinar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/edit-activation/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Seleccione el nombre del flujo de datos de destino que desea editar.

   ![Seleccionar destino](../assets/ui/edit-activation/destination-select.png)

4. La variable **[!UICONTROL Ejecuciones de flujo de datos]** para el destino, mostrando sus controles disponibles. En este punto, puede editar varios componentes del flujo de datos de destino:

   * Select **[!UICONTROL Activar segmentos]** en el carril derecho para cambiar qué segmentos o atributos de perfil se envían al destino. Esta acción le lleva al flujo de trabajo de activación, que difiere según el tipo de destino. Para obtener más información, consulte las guías sobre:
      * [activación de datos de audiencia en destinos de flujo continuo de segmento](./activate-segment-streaming-destinations.md) (por ejemplo, Facebook o Twitter);
      * [activación de datos de audiencia en destinos basados en perfiles por lotes](./activate-batch-profile-destinations.md) (por ejemplo, Amazon S3 o Oracle Eloqua);
      * [activación de datos de audiencia en destinos basados en perfiles de flujo continuo](./activate-streaming-profile-destinations.md) (por ejemplo, API HTTP o Amazon Kinesis).
   * Además, puede editar el nombre y la descripción del flujo de datos de destino.
   * Puede usar la variable **[!UICONTROL Habilitado]/[!UICONTROL Desactivado]** para iniciar y pausar todas las exportaciones de datos al destino.

   ![Detalles de destino](../assets/ui/edit-activation/destination-details.png)

5. Consulte [Información general de Activation](activation-overview.md) para obtener más información sobre cómo activar nuevos segmentos en los destinos.
