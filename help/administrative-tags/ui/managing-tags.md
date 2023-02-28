---
keywords: Experience Platform;administración de etiquetas;etiquetas;
title: Administración de etiquetas administrativas
description: Este documento proporciona información sobre la administración de etiquetas administrativas en Adobe Experience Cloud
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Guía de administración de etiquetas

Las etiquetas permiten administrar las taxonomías de metadatos para clasificar los objetos empresariales y facilitar así la detección y la categorización. Las etiquetas pueden ayudar a identificar atributos taxonómicos importantes para las audiencias con las que trabajarán sus equipos, de modo que puedan encontrarlos más rápidamente y también agrupar audiencias comunes en un descriptor. Debe identificar categorías de etiquetas comunes, como regiones geográficas, unidades de negocio, líneas de productos, proyectos, equipos, intervalos de tiempo (trimestres, meses, años) o cualquier otra cosa que pueda ayudar a aplicar significado y facilitar la detección de audiencias para su equipo. 

## Crear una etiqueta {#create-tag}

Para crear una etiqueta nueva, seleccione **[!UICONTROL etiquetas]** en el panel de navegación izquierdo, seleccione la categoría de etiqueta que desee.

![Seleccionar una categoría de etiqueta](./images/tag-selection.png)

Select **[!UICONTROL Crear etiqueta]** para crear una etiqueta nueva.

![Crear una etiqueta nueva](./images/new-tag.png)

La variable **[!UICONTROL Crear etiqueta]** , solicitándole que introduzca un nombre de etiqueta único. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Crear etiqueta con nuevo nombre de etiqueta](./images/create-tag-dialog.png)

La nueva etiqueta se crea correctamente y se le redirige a la pantalla de etiquetas, donde verá que la etiqueta recién creada aparece en la lista.

![Etiqueta recién creada para la categoría de etiqueta](./images/new-tag-listed.png)

## Editar una etiqueta {#edit-tag}

Editar una etiqueta ayuda cuando hay errores ortográficos, actualizaciones de convención de nombres o actualizaciones de terminología. La edición de una etiqueta mantendrá la asociación de la etiqueta con cualquier objeto al que se haya aplicado actualmente.

Para editar una etiqueta existente, en la lista de categorías de etiquetas, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea editar. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Select **[!UICONTROL Editar]** en la lista desplegable .

![Acción Editar que se muestra en la lista desplegable](./images/edit-action.png)

La variable **[!UICONTROL Editar etiqueta]** , solicitándole que edite el nombre de la etiqueta. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Editar etiqueta con nombre de etiqueta actualizado](./images/edit-dialog.png)

El nombre de la etiqueta se actualiza correctamente y se le redirige a la pantalla de etiquetas, donde verá que la etiqueta actualizada aparece en la lista.

![Etiqueta actualizada para la categoría de etiqueta](./images/updated-tag-listed.png)

## Mover una etiqueta entre categorías {#move-tag}

Las etiquetas se pueden mover a otras categorías de etiquetas. Mover una etiqueta mantendrá la asociación de la etiqueta con cualquier objeto donde se aplique actualmente.

Para mover una etiqueta existente, en la lista de categorías de etiquetas, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea mover. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Select **[!UICONTROL Editar]** en la lista desplegable .

![Acción Mover que se muestra en la lista desplegable](./images/move-action.png)

La variable **[!UICONTROL Mover etiqueta]** , solicitándole que seleccione la categoría de etiqueta a la que se debe mover la etiqueta seleccionada.

Puede desplazarse y seleccionar desde la lista, o bien, utilizar la función de búsqueda para introducir el nombre de la categoría. Cuando haya terminado, seleccione **[!UICONTROL Mover]**.

![Mover el cuadro de diálogo de etiquetas con criterios de búsqueda para encontrar la categoría de etiquetas](./images/move-dialog.png)

La etiqueta se moverá correctamente y se le redirigirá a la pantalla de etiquetas, donde verá la lista de etiquetas actualizada, donde la etiqueta ya no aparecerá.

![Lista de etiquetas actualizada para la categoría de etiquetas actual](./images/current-tag-category.png)

La etiqueta ahora aparece en la categoría de etiqueta seleccionada anteriormente.

![Lista de etiquetas para la categoría de etiquetas seleccionada para mover la etiqueta](./images/moved-to-tag-category.png)

## Archivar una etiqueta {#archive-tag}

El estado de una etiqueta se puede cambiar entre activo y archivado. Las etiquetas archivadas no se eliminan de los objetos en los que ya se han aplicado, pero ya no se pueden aplicar a nuevos objetos. Para cada etiqueta, el mismo estado se refleja en todos los objetos. Esto resulta especialmente útil cuando desea mantener asociaciones de objetos de etiqueta actuales, pero no desea que la etiqueta se utilice en el futuro.

Para archivar una etiqueta existente, en la lista de categorías de etiquetas, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea archivar. Un menú desplegable muestra los controles para editar, mover o archivar la etiqueta. Select **[!UICONTROL Archivo]** en la lista desplegable .

![Acción Archivar que se muestra en la lista desplegable](./images/archive-action.png)

La variable **[!UICONTROL Archivar etiqueta]** , solicitándole que confirme el archivo de etiquetas. Select **[!UICONTROL Archivo]**.

![Cuadro de diálogo Archivar etiqueta solicitar confirmación](./images/archive-dialog.png)

La etiqueta se archiva correctamente y se le redirige a la pantalla de etiquetas. Verá que la lista de etiquetas actualizada ahora muestra el estado de la etiqueta como `Archived`.

![Se ha actualizado la lista de etiquetas de la categoría de etiquetas actual que muestra la etiqueta como archivada](./images/archive-status.png)

## Restaurar una etiqueta archivada {#restore-archived-tag}

Si desea aplicar una `Archived` a nuevos objetos, la etiqueta debe estar en un `Active` estado. Al restaurar una etiqueta archivada, se devolverá una etiqueta a su `Active` estado.

Para restaurar una etiqueta archivada, en la lista de categorías de etiquetas, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea restaurar. Un menú desplegable muestra los controles para restaurar o eliminar la etiqueta. Select **[!UICONTROL Restaurar]** en la lista desplegable .

![Acción Restaurar que se muestra en la lista desplegable](./images/restore-action.png)

La variable **[!UICONTROL Restaurar etiqueta]** , solicitándole que confirme la restauración de etiquetas. Select **[!UICONTROL Restaurar]**.

![Cuadro de diálogo Restaurar etiqueta solicitando confirmación](./images/restore-dialog.png)

La etiqueta se restaura correctamente y se le redirige a la pantalla de etiquetas. Verá que la lista de etiquetas actualizada ahora muestra el estado de la etiqueta como `Active`.

![Se ha actualizado la lista de etiquetas de la categoría de etiquetas actual que muestra la etiqueta como activa](./images/restored-active-status.png)

## Eliminar una etiqueta {#delete-tag}

>[!NOTE]
>
>Solo las etiquetas que se encuentran en una `Archived` y no están asociados a ningún objeto.

Al eliminar una etiqueta, ésta se eliminará del sistema por completo.

Para eliminar una etiqueta archivada, en la lista de categorías de etiquetas, seleccione los puntos suspensivos (`...`) junto al nombre de la etiqueta que desea eliminar. Un menú desplegable muestra los controles para restaurar o eliminar la etiqueta. Select **[!UICONTROL Eliminar]** en la lista desplegable .

![Acción Eliminar que se muestra en la lista desplegable](./images/delete-action.png)

La variable **[!UICONTROL Eliminar etiqueta]** , pidiéndole que confirme la eliminación de la etiqueta. Seleccione **[!UICONTROL Eliminar]**.

![Cuadro de diálogo Eliminar etiqueta que solicita confirmación](./images/delete-dialog.png)

La etiqueta se elimina correctamente y se le redirige a la pantalla de etiquetas. La etiqueta ya no aparece en la lista y se ha eliminado por completo.

![La lista de etiquetas actualizada para la categoría de etiquetas actual que muestra la etiqueta ya no aparece en la lista](./images/deleted-updated-list.png)

## Visualización de objetos etiquetados {#view-tagged}

Cada etiqueta tiene una página de detalles a la que se puede acceder desde el inventario de etiquetas. Esta página enumera todos los objetos que actualmente tienen esa etiqueta aplicada, lo que permite a los usuarios ver objetos relacionados de distintas aplicaciones y capacidades en una sola vista.

Para ver la lista de objetos etiquetados, busque la etiqueta dentro de una categoría de etiquetas y seleccione la etiqueta .

![Selección de etiquetas dentro de la categoría de etiquetas](./images/view-tag-selection.png)

La variable [!UICONTROL Objetos etiquetados] , mostrando un inventario de objetos etiquetados.

![Inventario de objetos etiquetados](./images/tagged-objects.png)

## Pasos siguientes

Ya ha aprendido a administrar etiquetas. Para obtener una descripción general de alto nivel de las etiquetas en Experience Platform, consulte la [documentación general de etiquetas](../overview.md).
