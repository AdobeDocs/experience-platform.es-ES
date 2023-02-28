---
keywords: Experience Platform;inicio;temas populares;etiquetas administrativas;etiquetas;
title: Información general sobre las etiquetas administrativas
description: Este documento proporciona información sobre las etiquetas administrativas en Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# Información general sobre etiquetas

Las etiquetas son una función de Adobe Experience Platform que permite a los administradores administrar las taxonomías de metadatos para clasificar objetos empresariales y facilitar así la detección y la categorización. Las etiquetas son metadatos que se pueden considerar como palabras clave que se pueden adjuntar a un segmento, conjunto de datos, recorrido u otros objetos para permitir que las búsquedas permitan encontrar ese objeto y objetos relacionados. Las etiquetas se clasifican en dos tipos: clasificado y sin categoría.

Para proporcionar más contexto y definir el propósito de una etiqueta, las categorías organizan las etiquetas en conjuntos útiles. Un administrador define qué etiquetas clasificadas están disponibles para que los usuarios las agreguen a los objetos. Las nuevas etiquetas que no contienen categorías también se pueden crear en línea en flujos de trabajo en los que se aplican etiquetas. Estas etiquetas aparecerán en la sección sin categoría del inventario de etiquetas. Tanto los administradores como los usuarios pueden aplicar las etiquetas, independientemente de quién las haya creado. Todos los tipos de etiquetas están disponibles para su selección al asignar a un objeto, buscar o filtrar.

## Terminología de etiquetas

El etiquetado implica los siguientes componentes:

| Terminología | Definición |
| --- | --- |
| Archivado | Estado de una etiqueta que mantiene las asociaciones actuales con objetos pero que restringe la aplicación de la etiqueta a objetos posteriores.  Las etiquetas archivadas están ocultas en el selector de etiquetas. |
| Objeto | Elemento de Experience Cloud al que se puede aplicar una etiqueta.  Ejemplos: Segmento, Recorrido, conjunto de datos. |
| Etiqueta | Las etiquetas son metadatos y se pueden considerar palabras clave que se pueden adjuntar a un segmento, conjunto de datos, recorrido u otros objetos para permitir que las búsquedas localicen ese objeto y los objetos relacionados. |
| Categoría de la etiqueta | Las categorías de etiquetas agrupan las etiquetas en conjuntos significativos para proporcionar un contexto bueno o describir el propósito de la etiqueta.  Los administradores administran las categorías y etiquetas de etiquetas dentro de las categorías. |
| Etiqueta sin categoría | Una etiqueta nueva que se crea en línea donde se aplican etiquetas. Cualquier usuario puede crear y aplicar estas etiquetas, pero no están vinculadas a una categoría.  Los administradores pueden mover estas etiquetas a una categoría para alinearlas con otras etiquetas similares. |

## Inventario de etiquetas

La administración de etiquetas y categorías de etiquetas mediante el inventario de etiquetas está disponible en la navegación del Experience Platform y Journey Optimizer. Los cambios en las etiquetas del inventario se reflejan en todos los objetos que admiten etiquetas. Todos los usuarios pueden acceder y examinar el inventario de etiquetas, pero la administración de etiquetas está limitada a los administradores de sistemas y productos.

El inventario de etiquetas tiene tres niveles de jerarquía, lo que permite a los usuarios administrar categorías de etiquetas, etiquetas dentro de una categoría y etiquetas individuales. Al administrar una etiqueta individual, los usuarios pueden ver y navegar a cualquier objeto donde se aplique esa etiqueta actualmente.

### Categorías de etiquetas

Las categorías agrupan las etiquetas en conjuntos significativos para proporcionar un contexto bueno o describir el propósito de la etiqueta. En cualquier etiqueta con una categoría, el nombre de la categoría seguido de dos puntos precede al nombre de la etiqueta.

Las siguientes acciones son posibles cuando se utilizan categorías de etiquetas:

* [Crear categoría de etiqueta](./ui/tags-categories.md#create-tag-category)
* [Editar categoría de etiqueta](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Eliminar categoría de etiqueta](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Administración de etiquetas dentro de una categoría

>[!NOTE]
>
>Para administrar las etiquetas de Experience Cloud, debe ser administrador del sistema o administrador de productos de Adobe Experience Platform para su organización, que tenga una suscripción a Experience Cloud.

Dentro de una categoría (o el grupo predeterminado &quot;Sin categoría&quot;), puede crear y administrar etiquetas. Las siguientes acciones son posibles al administrar etiquetas:

* [Crear una etiqueta](./ui/managing-tags.md#create-a-tag-create-tag)
* [Editar una etiqueta](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Mover una etiqueta entre categorías](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archivar una etiqueta](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restaurar una etiqueta archivada](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Eliminar una etiqueta](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Ver objetos etiquetados](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
