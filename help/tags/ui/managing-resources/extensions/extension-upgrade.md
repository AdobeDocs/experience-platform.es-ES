---
title: Actualizaciones de extensiones
description: Descubra cómo las actualizaciones de extensión se empaquetan y representan en el catálogo de extensiones.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 97%

---

# Actualizaciones de extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Los desarrolladores de extensiones añaden continuamente nuevas funciones a sus extensiones y suelen corregir errores. Estas actualizaciones se incluyen en las versiones nuevas de una extensión y se pueden descargar en el catálogo de extensiones como actualizaciones.

## Catálogo de extensiones

Cuando un desarrollador de extensiones ha proporcionado una nueva versión de la extensión, esa nueva versión está disponible en el catálogo de extensiones. El catálogo solo muestra la versión más reciente de una extensión. No puede instalar ninguna versión de extensión distinta a `latest`.

Al instalar una extensión en su propiedad, se instala la versión disponible actualmente y la propiedad conserva esa versión concreta a partir de ese momento, incluso si se añaden versiones más recientes al catálogo.

## Notificaciones de actualización

Cuando haya instalado una extensión en su propiedad y en el catálogo aparezca una versión más reciente, en la tarjeta de la extensión aparece un botón de [!UICONTROL actualizar] al abrir la página Extensiones instaladas.

También aparece un aviso al editar recursos proporcionados por esa extensión.

## Las actualizaciones son permanentes

Si desea actualizar a una versión más reciente disponible en el catálogo, debe instalar esa actualización por su cuenta. Una actualización es un “cambio” que debe añadirse a una biblioteca, probarse y publicarse antes de que afecte a las etiquetas implementadas.

Las actualizaciones no deben realizarse a la ligera. No debe actualizar a menos que esté preparado para probar la nueva extensión y esté listo para implementarla. Una vez que la actualización se haya añadido a su propiedad, debe incluirse en todas las bibliotecas. Toda biblioteca que no incluya la extensión actualizada produce errores de compilación.

Actualmente no es posible sustituir la extensión por una versión anterior. Una vez que la haya actualizado (independientemente de si publica o no), la nueva versión de la extensión ha llegado a su propiedad para quedarse.

## Proceso de actualización

La instalación de una actualización es casi igual que instalar la extensión por primera vez.

1. Seleccione **[!UICONTROL Actualizar]** para ir a la pantalla [!UICONTROL Configuración de la extensión].
1. Aplique cualquier cambio de configuración que desee.
1. Seleccione **[!UICONTROL Guardar]**.

La actualización no comienza hasta que pulse **[!UICONTROL Guardar]**. Antes de ello, puede seleccionar [!UICONTROL Cancelar] y permanecer en la versión instalada. Cuando se selecciona **[!UICONTROL Guardar]** ya no hay vuelta atrás.

Las actualizaciones de extensión no están permitidas si tiene una biblioteca en el estado `Approved` o `Submitted`. Esto se debe a que la siguiente compilación debe incluir la nueva versión de la extensión. Para una biblioteca con el estado `Approved` o `Submitted`, la siguiente compilación es la versión de producción. Esa compilación no funcionará correctamente ya que no contiene la versión más reciente, por lo que el flujo de trabajo consiste en publicar o rechazar bibliotecas en el estado `Approved` o `Submitted` _antes_ de actualizar la extensión.

## Publicación de una actualización

Una vez instalada la extensión actualizada en la propiedad, debe incluirla en todas las bibliotecas a partir de ese momento. Se muestra un mensaje de error de compilación en cualquier biblioteca que no la incluya.

Aparte de esto, añadir la extensión actualizada a la biblioteca es lo mismo que [añadir cualquier otro cambio](../../publishing/libraries.md) a una biblioteca.

Desde la pantalla [!UICONTROL Editar biblioteca], puede utilizar el botón [!UICONTROL Añadir todos los recursos modificados] o puede utilizar el botón [!UICONTROL Añadir un recurso] y seleccionar la extensión actualizada por su cuenta.

>[!TIP]
>
>Los desarrolladores de extensiones pueden añadir nuevos elementos de configuración a sus vistas de extensión para activar nuevas funciones. Si ve errores de compilación después de actualizar a una nueva versión de la extensión (y ha aislado los errores en esa compilación), lo primero que debe hacer es ir a la página “Configure” de la extensión y asegurarse de usar Save (aunque no haya cambiado nada). A continuación, añada el nuevo cambio a la biblioteca e intente volver a compilarlo.

Cuando haya añadido la actualización de la extensión a la biblioteca, puede seguir los pasos descritos en [flujo de publicación](../../publishing/publishing-flow.md) para publicar la biblioteca en Producción.
