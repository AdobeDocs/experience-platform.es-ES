---
keywords: Experience Platform;inicio;temas populares;Unified tags;tags;
title: Información general sobre etiquetas unificadas (beta)
description: Este documento proporciona información sobre las etiquetas unificadas en Adobe Experience Platform
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Resumen de etiquetas unificadas (beta)

>[!IMPORTANT]
>
>Las etiquetas unificadas están en versión beta. Si desea dejar comentarios, haga clic en el botón en la parte superior de la página de administración de etiquetas.

Las etiquetas son una función de Adobe Experience Platform que permite a los administradores administrar taxonomías de metadatos para clasificar objetos empresariales y facilitar así la detección y la categorización. Las etiquetas son metadatos que se pueden considerar como palabras clave que se pueden adjuntar a un segmento, conjunto de datos, recorrido u otros objetos para permitir búsquedas y encontrar ese objeto y los objetos relacionados. Las etiquetas se clasifican en dos tipos: por categorías y sin clasificar.

Para proporcionar más contexto y definir el propósito de una etiqueta, las categorías organizan las etiquetas en conjuntos útiles. Un administrador define qué etiquetas clasificadas están disponibles para que los usuarios las agreguen a objetos. También se pueden crear nuevas etiquetas que no contengan categorías en línea en los flujos de trabajo donde se aplican las etiquetas. Estas etiquetas se mostrarán en la sección sin clasificar del inventario de etiquetas. Tanto los administradores como los usuarios pueden aplicar las etiquetas, independientemente de quién las haya creado. Todos los tipos de etiquetas están disponibles para su selección al asignarlas a un objeto, al realizar búsquedas o al filtrar.

## Terminología de etiquetas

El etiquetado incluye los siguientes componentes:

| Terminología | Definición |
| --- | --- |
| Archivado | Estado de una etiqueta que mantiene las asociaciones actuales con objetos, pero que restringe la aplicación de la etiqueta a otros objetos.  Las etiquetas archivadas se ocultan al selector de etiquetas. |
| Objeto | Un elemento de Experience Cloud al que se puede aplicar una etiqueta.  Ejemplos: Segmento, Recorrido, Conjunto de datos. |
| Etiqueta | Las etiquetas son metadatos y se pueden considerar como palabras clave que se pueden adjuntar a un segmento, conjunto de datos, recorrido u otros objetos para permitir búsquedas y encontrar ese objeto y los objetos relacionados. |
| Categoría de etiqueta | Las categorías de etiquetas agrupan las etiquetas en conjuntos significativos para proporcionar el bueno contexto o describir el propósito de la etiqueta.  Los administradores administran las categorías de etiquetas y las etiquetas dentro de las categorías. |
| Etiqueta sin categoría | Una etiqueta nueva que se crea en línea donde se aplican las etiquetas. Cualquier usuario puede crear y aplicar estas etiquetas, pero no están enlazadas a una categoría.  Los administradores pueden mover estas etiquetas a una categoría para alinearlas con otras etiquetas similares. |

## Inventario de etiquetas

La administración de etiquetas y categorías de etiquetas mediante el inventario de etiquetas está disponible en la navegación de Experience Platform y Journey Optimizer. Los cambios en las etiquetas del inventario se reflejan en todos los objetos que admiten etiquetas. Todos los usuarios pueden acceder y examinar el inventario de etiquetas, pero la administración de etiquetas se limita a los administradores de sistemas y productos.

El inventario de etiquetas tiene tres niveles de jerarquía, lo que permite a los usuarios administrar las categorías de etiquetas, las etiquetas dentro de una categoría y las etiquetas individuales. Al administrar una etiqueta individual, los usuarios pueden ver y navegar a cualquier objeto donde se aplique actualmente esa etiqueta.

### Categorías de etiquetas

Las categorías agrupan las etiquetas en conjuntos significativos para proporcionar el bueno contexto o describir el propósito de la etiqueta. En cualquier etiqueta con una categoría, el nombre de la categoría seguido de dos puntos precede al nombre de la etiqueta.

Las siguientes acciones son posibles al utilizar categorías de etiquetas:

* [Crear categoría de etiqueta](./ui/tags-categories.md#create-tag-category)
* [Editar categoría de etiqueta](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Eliminar categoría de etiqueta](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Administración de etiquetas dentro de una categoría

>[!NOTE]
>
>Para administrar etiquetas para Experience Cloud, debe ser administrador del sistema o de productos para Adobe Experience Platform en su organización, que está suscrita a Experience Cloud.

Dentro de una categoría (o del grupo predeterminado &quot;Sin categoría&quot;), puede crear y administrar etiquetas. Las siguientes acciones son posibles al administrar etiquetas:

* [Crear una etiqueta](./ui/managing-tags.md#create-a-tag-create-tag)
* [Edición de una etiqueta](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Mover una etiqueta entre categorías](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archivar una etiqueta](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restaurar una etiqueta archivada](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Eliminar una etiqueta](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Ver objetos etiquetados](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
