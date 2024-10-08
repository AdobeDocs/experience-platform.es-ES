---
keywords: editar activación, editar destino, editar destino
title: Editar flujos de datos de activación
type: Tutorial
description: Siga los pasos de este artículo para editar un flujo de datos de activación existente en Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ca33131c505803b74075f6d8331095b016a301a0
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Editar flujos de datos de activación {#edit-activation-flows}

En Adobe Experience Platform, puede configurar varios componentes de flujos de datos de activación existentes en destinos como, por ejemplo:

* [Habilitar o deshabilitar](#enable-disable-dataflows) flujos de datos de activación;
* [Agregar audiencias y atributos de perfil adicionales](#add-audiences) a flujos de datos de activación;
* [Agregar conjuntos de datos adicionales](#add-datasets) a flujos de trabajo de activación;
* [Editar nombres y descripciones](#edit-names-descriptions) para sus flujos de datos de activación;

<!-- * [Apply access labels](#apply-access-labels) to exported data; -->

## Examinar flujos de datos de activación {#browse-activation-dataflows}

Siga los pasos a continuación para examinar los flujos de datos de activación existentes e identificar el que desea editar.

1. Inicie sesión en la [interfaz de usuario del Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccione **[!UICONTROL Examinar]** en el encabezado superior para ver los flujos de datos de destino existentes.

   ![Destinos de exploración](../assets/ui/edit-activation/browse-destinations.png)

2. Seleccione el icono de filtro ![Filter-icon](../../images/icons/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Seleccione el nombre del flujo de datos de destino que desea editar.

   ![Seleccionar destino](../assets/ui/edit-activation/destination-select.png)

4. Aparecerá la página **[!UICONTROL Flujo de datos ejecuta]** para el destino, mostrando sus controles disponibles. Según el tipo de destino, puede realizar varias operaciones de flujo de datos. Consulte las secciones siguientes para cada operación de flujo de datos admitida.

## Habilitar o deshabilitar flujos de datos de activación {#enable-disable-dataflows}

Utilice la opción **[!UICONTROL Habilitado]/[!UICONTROL Deshabilitado]** para iniciar o pausar todas las exportaciones de datos al destino.

![Imagen de la interfaz de usuario del Experience Platform que muestra la opción de ejecución de flujo de datos habilitada/deshabilitada.](../assets/ui/edit-activation/enable-toggle.png)

## Añadir audiencias a un flujo de datos de activación {#add-audiences}

Seleccione **[!UICONTROL Activar audiencias]** en el carril derecho para cambiar qué audiencias o atributos de perfil se enviarán al destino. Esta acción le lleva al flujo de trabajo de activación, que difiere según el tipo de destino.

![Imagen de la interfaz de usuario del Experience Platform que muestra la opción Activar ejecución del flujo de datos de audiencias.](../assets/ui/edit-activation/activate-audiences.png)

Para obtener más información sobre los flujos de trabajo de activación para cada tipo de destino, consulte las siguientes guías:

* [Activar audiencias en destinos de flujo continuo](./activate-segment-streaming-destinations.md) (por ejemplo, Facebook o Twitter);
* [Activar audiencias para destinos de exportación de perfiles por lotes](./activate-batch-profile-destinations.md) (por ejemplo, Amazon S3 o Oracle Eloqua);
* [Activar audiencias en destinos de exportación de perfiles de streaming](./activate-streaming-profile-destinations.md) (por ejemplo, API HTTP o Amazon Kinesis).

## Adición de conjuntos de datos a un flujo de datos de activación {#add-datasets}

Seleccione **[!UICONTROL Exportar conjuntos de datos]** en el carril derecho para seleccionar conjuntos de datos adicionales para exportarlos a su destino. Esta opción lo lleva al [flujo de trabajo de exportación del conjunto de datos](export-datasets.md).

>[!NOTE]
>
>Esta opción solo está visible para [destinos que admiten la exportación del conjunto de datos](export-datasets.md#supported-destinations).

![Imagen de la interfaz de usuario del Experience Platform que muestra la opción Exportar conjuntos de datos del flujo de datos.](../assets/ui/edit-activation/export-datasets.png)

<!-- ## Apply access labels {#apply-access-labels}

Select **[!UICONTROL Apply access labels]** to edit the data usage labels for the exported data. See the [data usage labels documentation](../../data-governance/labels/overview.md) to learn more.

![Experience Platform UI image showing the Export datasets dataflow run option.](../assets/ui/edit-activation/apply-access-labels.png) -->

## Editar nombres y descripciones de flujo de datos de activación {#edit-names-descriptions}

Para editar el nombre y la descripción del flujo de datos de activación, use los campos **[!UICONTROL Nombre de destino]** y **[!UICONTROL Descripción]**.

![Detalles del destino](../assets/ui/edit-activation/edit-destination-name-description.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo **[!UICONTROL destinos]** para actualizar los flujos de datos de destino existentes.

Para obtener más información sobre los destinos, consulte la [descripción general de los destinos](../catalog/overview.md).
