---
keywords: Experience Platform;administrar etiquetas;tags;
title: Administración de etiquetas unificadas
description: Este documento proporciona información sobre la administración de etiquetas unificadas en Adobe Experience Cloud
exl-id: 179b0618-3bd3-435c-9d17-63681177ca47
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Guía de administración de etiquetas

Las etiquetas permiten administrar taxonomías de metadatos para clasificar objetos empresariales y facilitar así la detección y la categorización. Las etiquetas pueden ayudar a identificar atributos taxonómicos importantes para las audiencias con las que trabajarán sus equipos, de modo que puedan encontrarlos más rápidamente y también agrupar audiencias comunes en un descriptor. Debe identificar categorías de etiquetas comunes, como regiones geográficas, unidades de negocio, líneas de productos, proyectos, equipos, intervalos de tiempo (trimestres, meses, años) o cualquier otra cosa que pueda ayudar a aplicar un significado y facilitar la detección de audiencias para su equipo. 

## Crear una etiqueta {#create-tag}

Para crear una etiqueta nueva, seleccione **[!UICONTROL etiquetas]** en el panel de navegación izquierdo, seleccione la categoría de etiqueta que desee.

![Seleccione una categoría de etiqueta](./images/tag-selection.png)

Seleccionar **[!UICONTROL Crear etiqueta]** para crear una etiqueta nueva.

![Crear una etiqueta nueva](./images/new-tag.png)

El **[!UICONTROL Crear etiqueta]** aparece un cuadro de diálogo en el que se le solicita que introduzca un nombre de etiqueta único. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Crear etiqueta con nuevo nombre de etiqueta](./images/create-tag-dialog.png)

La nueva etiqueta se ha creado correctamente y se le redirigirá a la pantalla de etiquetas, donde verá la etiqueta recién creada aparecer en la lista.

![Etiqueta recién creada para la categoría de etiqueta](./images/new-tag-listed.png)

## Edición de una etiqueta {#edit-tag}

La edición de una etiqueta es útil cuando hay errores ortográficos, actualizaciones de las convenciones de nomenclatura o actualizaciones de terminología. Si edita una etiqueta, se mantendrá la asociación de la etiqueta con cualquier objeto donde se aplique actualmente.

Para editar una etiqueta existente, en la lista de categoría de etiqueta, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desee editar. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Seleccionar **[!UICONTROL Editar]** en el menú desplegable.

![Editar acción que se muestra en la lista desplegable](./images/edit-action.png)

El **[!UICONTROL Editar etiqueta]** , solicitándole que edite el nombre de la etiqueta. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Editar etiqueta con nombre de etiqueta actualizado](./images/edit-dialog.png)

El nombre de la etiqueta se ha actualizado correctamente y se le redirigirá a la pantalla de etiquetas, donde verá la etiqueta actualizada aparecer en la lista.

![Etiqueta actualizada para la categoría de etiqueta](./images/updated-tag-listed.png)

## Mover una etiqueta entre categorías {#move-tag}

Las etiquetas se pueden mover a otras categorías de etiquetas. Al mover una etiqueta, se mantiene la asociación de la etiqueta con cualquier objeto al que se aplique en ese momento.

Para mover una etiqueta existente, en la lista de categoría de etiqueta, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea mover. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Seleccionar **[!UICONTROL Editar]** en el menú desplegable.

![Acción de mover que se muestra en la lista desplegable](./images/move-action.png)

El **[!UICONTROL Mover etiqueta]** aparece un cuadro de diálogo que le solicita que seleccione la categoría de etiqueta a la que se debe mover la etiqueta seleccionada.

Puede desplazarse y seleccionar de la lista o, alternativamente, utilizar la función de búsqueda para introducir el nombre de la categoría. Cuando haya terminado, seleccione **[!UICONTROL Mover]**.

![Cuadro de diálogo Mover etiqueta con criterios de búsqueda para encontrar la categoría de etiqueta](./images/move-dialog.png)

La etiqueta se ha movido correctamente y se le redirigirá a la pantalla de etiquetas, donde verá la lista de etiquetas actualizada donde ya no aparecerá la etiqueta.

![Se ha actualizado la lista de etiquetas para la categoría de etiquetas actual](./images/current-tag-category.png)

La etiqueta aparecerá ahora en la categoría de etiqueta seleccionada anteriormente.

![Lista de etiquetas de la categoría de etiqueta seleccionada para mover la etiqueta](./images/moved-to-tag-category.png)

## Archivar una etiqueta {#archive-tag}

El estado de una etiqueta se puede cambiar entre activo y archivado. Las etiquetas archivadas no se eliminan de los objetos en los que ya se han aplicado, pero ya no se pueden aplicar a objetos nuevos. Para cada etiqueta, el mismo estado se refleja en todos los objetos. Esto es especialmente útil cuando desea mantener las asociaciones de etiqueta y objeto actuales pero no desea que la etiqueta se utilice en el futuro.

Para archivar una etiqueta existente, en la lista de categoría de etiqueta, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea archivar. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Seleccionar **[!UICONTROL Archivar]** en el menú desplegable.

![Acción de archivo que se muestra en la lista desplegable](./images/archive-action.png)

El **[!UICONTROL Archivar etiqueta]** aparece un cuadro de diálogo que le solicita que confirme el archivo de etiquetas. Seleccionar **[!UICONTROL Archivar]**.

![Archivar cuadro de diálogo de etiqueta solicitando confirmación](./images/archive-dialog.png)

La etiqueta se archiva correctamente y se le redirige a la pantalla de etiquetas. Verá que la lista de etiquetas actualizada ahora muestra el estado de la etiqueta como `Archived`.

![Se ha actualizado la lista de etiquetas de la categoría de etiquetas actual que muestra la etiqueta como archivada](./images/archive-status.png)

## Restaurar una etiqueta archivada {#restore-archived-tag}

Si desea aplicar una `Archived` a los objetos nuevos, la etiqueta debe estar en un `Active` estado. Restaurar una etiqueta archivada devolverá una etiqueta a su `Active` estado.

Para restaurar una etiqueta archivada, en la lista de categoría de etiqueta, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea restaurar. Un menú desplegable muestra los controles para restaurar o eliminar la etiqueta. Seleccionar **[!UICONTROL Restaurar]** en el menú desplegable.

![Acción de restauración que se muestra en la lista desplegable](./images/restore-action.png)

El **[!UICONTROL Restaurar etiqueta]** aparece un cuadro de diálogo que le solicita que confirme la restauración de etiquetas. Seleccionar **[!UICONTROL Restaurar]**.

![Cuadro de diálogo Restaurar etiqueta solicitando confirmación](./images/restore-dialog.png)

La etiqueta se ha restaurado correctamente y se le redirigirá a la pantalla de etiquetas. Verá que la lista de etiquetas actualizada ahora muestra el estado de la etiqueta como `Active`.

![Se ha actualizado la lista de etiquetas de la categoría de etiquetas actual que muestra la etiqueta como activa](./images/restored-active-status.png)

## Eliminar una etiqueta {#delete-tag}

>[!NOTE]
>
>Solo las etiquetas que están en un `Archived` estado y no están asociados a ningún objeto se pueden eliminar.

Si elimina una etiqueta, se eliminará por completo del sistema.

Para eliminar una etiqueta archivada, en la lista de categoría de etiqueta, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea eliminar. Un menú desplegable muestra los controles para restaurar o eliminar la etiqueta. Seleccionar **[!UICONTROL Eliminar]** en el menú desplegable.

![Eliminar acción que se muestra en la lista desplegable](./images/delete-action.png)

El **[!UICONTROL Eliminar etiqueta]** , solicitándole que confirme la eliminación de la etiqueta. Seleccione **[!UICONTROL Eliminar]**.

![Cuadro de diálogo Eliminar etiqueta solicitando confirmación](./images/delete-dialog.png)

La etiqueta de se ha eliminado correctamente y se le redirigirá a la pantalla de etiquetas. La etiqueta ya no aparece en la lista y se ha eliminado por completo.

![La lista de etiquetas actualizada para la categoría de etiquetas actual que muestra la etiqueta ya no aparece en la lista](./images/deleted-updated-list.png)

## Visualización de objetos etiquetados {#view-tagged}

Cada etiqueta tiene una página de detalles a la que se puede acceder desde el inventario de etiquetas. Esta página lista todos los objetos que actualmente tienen esa etiqueta aplicada, lo que permite a los usuarios ver objetos relacionados de diferentes aplicaciones y capacidades en una sola vista.

Para ver la lista de objetos etiquetados, busque la etiqueta dentro de una categoría de etiqueta y seleccione la etiqueta.

![Selección de etiquetas dentro de la categoría de etiquetas](./images/view-tag-selection.png)

El [!UICONTROL Objetos etiquetados] página, que muestra un inventario de objetos etiquetados.

![Inventario de objetos etiquetados](./images/tagged-objects.png)

## Pasos siguientes

Ya ha aprendido a administrar etiquetas. Para obtener una descripción general de alto nivel de las etiquetas en Experience Platform, consulte la [documentación de información general sobre etiquetas](../overview.md).
