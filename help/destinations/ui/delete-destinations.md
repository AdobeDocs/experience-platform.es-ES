---
keywords: eliminar destinos, eliminar destinos, eliminar destino
title: Eliminar destinos
type: Tutorial
description: Este tutorial enumera los pasos para eliminar un destino existente en la interfaz de usuario de Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Eliminar destinos {#delete-destinations}

## Información general {#overview}

En la interfaz de usuario de Adobe Experience Platform, puede eliminar las conexiones existentes a los destinos.

Al eliminar un destino, se eliminan los flujos de datos existentes en ese destino. Todos los segmentos activados en los destinos que elimine no estarán asignados antes de que se elimine el flujo de datos.

Existen dos maneras de eliminar destinos de la variable [!DNL Platform] [!DNL UI]. Puede:

* [Eliminar destinos de [!UICONTROL Examinar] ficha](#delete-browse-tab)
* [Eliminar destinos de la página de detalles de destino](#delete-destination-details-page)

## Eliminar destinos de la ficha Examinar{#delete-browse-tab}

Siga los pasos a continuación para eliminar un destino de la variable [!UICONTROL Examinar] pestaña .

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Para ver los destinos existentes, seleccione **[!UICONTROL Examinar]** en el encabezado superior.

   ![Examinar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/delete-destinations/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleccione el ![Botón Más](../assets/ui/delete-destinations/more-icon.png) en la columna Nombre y, a continuación, seleccione ![Botón Eliminar](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Eliminar]** para quitar una conexión de destino existente.
   ![Eliminar destinos](../assets/ui/delete-destinations/delete-destinations.png)

4. Select **[!UICONTROL Eliminar]** para confirmar la eliminación de la conexión de destino.

   ![Confirmar eliminación de destino](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Eliminar destinos de la página de detalles de destino{#delete-destination-details-page}

Siga los pasos a continuación para eliminar un destino de la página de detalles de destino.

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Para ver los destinos existentes, seleccione **[!UICONTROL Examinar]** en el encabezado superior.

   ![Examinar destinos](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/delete-destinations/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleccione el nombre del destino que desea eliminar.

   ![Seleccionar destino](../assets/ui/delete-destinations/delete-destination-select.png)

   * Si el destino tiene flujos de datos existentes, se le redirigirá al [!UICONTROL Ejecuciones de flujo de datos] pestaña .

      ![Pestaña de ejecución de flujo de datos](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Si el destino no tiene flujos de datos existentes, se le redirigirá a una página vacía en la que podrá empezar a activar audiencias.

      ![Detalles de destino](../assets/ui/delete-destinations/destination-details-empty.png)

4. Select **[!UICONTROL Eliminar]** en el carril derecho.

   ![Eliminar destino](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Select **[!UICONTROL Eliminar]** en el cuadro de diálogo de confirmación para eliminar el destino.

   ![Eliminar confirmación de destino](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Dependiendo de la carga del servidor, puede tardar unos minutos en [!DNL Platform] para eliminar el destino.
