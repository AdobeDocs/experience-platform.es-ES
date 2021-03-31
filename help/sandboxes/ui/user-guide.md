---
keywords: Experience Platform;inicio;temas populares;guía del usuario del entorno limitado;guía del entorno limitado
solution: Experience Platform
title: Guía de la interfaz de usuario del Simulador para pruebas
topic: Guía del usuario
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Guía de la interfaz de usuario del Simulador para pruebas

Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.

## Ver entornos limitados

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Sandboxes]** en el panel de navegación izquierdo para abrir el panel **[!UICONTROL Sandboxes]**. El tablero enumera todos los entornos limitados disponibles para su organización, incluido el tipo de entorno limitado (producción o desarrollo) y el estado (activo, creador, eliminado o fallido).

![](../images/ui/view-sandboxes.png)

## Cambiar entre entornos limitados

El control **sandbox switch** en la parte superior izquierda de la pantalla muestra el entorno limitado activo actualmente.

![](../images/ui/sandbox-switcher.png)

Para cambiar entre entornos limitados, seleccione el conmutador de simulador de pruebas y seleccione el simulador de pruebas que desee en la lista desplegable.

![](../images/ui/switcher-menu.png)

Una vez seleccionado un simulador de pruebas, la pantalla se actualiza con el simulador de pruebas seleccionado que ahora aparece en el simulador de pruebas.

![](../images/ui/switched.png)

## Sesiones para un simulador de pruebas

Puede navegar por la lista de entornos limitados disponibles mediante la función de búsqueda del menú del conmutador de entornos limitados. Escriba el nombre del simulador de pruebas al que desea acceder para filtrar por todos los entornos limitados disponibles para su organización.

![](../images/ui/sandbox-search.png)

## Crear un nuevo simulador de pruebas

>[!NOTE]
>
>La función Entornos aislados de producción múltiple está en fase beta.

Utilice el siguiente vídeo para obtener información general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear un nuevo simulador de pruebas, seleccione el botón **[!UICONTROL Create Sandbox]** en la parte superior derecha de la pantalla.

![](../images/ui/create-sandbox.png)

Aparece el cuadro de diálogo **[!UICONTROL Create Sandbox]**, que le solicita que proporcione un tipo, un título y un nombre para el simulador de pruebas. Si está creando un entorno limitado de desarrollo, seleccione **[!UICONTROL Development]** en el panel desplegable que aparece. Si está creando un entorno limitado de producción, seleccione **[!UICONTROL Production]**.

El título debe ser legible por el ser humano y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El nombre del simulador para pruebas es un identificador en minúsculas que se utiliza en las llamadas a la API y, por lo tanto, debe ser único y conciso. El nombre del simulador para pruebas solo debe contener caracteres alfanuméricos y guiones (`-`), debe comenzar con una letra y tener un máximo de 256 caracteres.

Cuando termine, seleccione **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

Una vez que haya terminado de crear el entorno limitado, actualice la página y aparecerá el nuevo entorno limitado en el panel **[!UICONTROL Sandboxes]** con el estado &quot;[!UICONTROL Creating]&quot;. El sistema tarda aproximadamente 15 minutos en aprovisionar nuevos entornos limitados, tras lo cual su estado cambia a &quot;[!UICONTROL Active]&quot;.

## Restablecer un simulador para pruebas

>[!NOTE]
>
>Puede restablecer cualquier entorno limitado de producción o desarrollo de su organización, excepto el entorno limitado de producción predeterminado.

Al restablecer un entorno limitado de producción o desarrollo, se eliminan todos los recursos asociados a dicho entorno limitado (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre del entorno limitado y los permisos asociados. Este simulador de pruebas &quot;limpio&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a él.

Seleccione el simulador de pruebas que desea restablecer de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Sandbox reset]**.

![](../images/ui/reset-sandbox.png)

Aparecerá un cuadro de diálogo que le pedirá que confirme su elección. Seleccione **[!UICONTROL Continue]** para continuar.

![](../images/ui/reset-confirm.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione **[!UICONTROL Reset]**

![](../images/ui/reset-final-confirm.png)

## Eliminación de un simulador para pruebas

>[!NOTE]
>
>Puede eliminar cualquier entorno limitado de producción o desarrollo de su organización, excepto el entorno limitado de producción predeterminado.

Al eliminar un entorno limitado de producción o desarrollo, se eliminan permanentemente todos los recursos asociados a dicho entorno limitado, incluidos los permisos.

Seleccione el simulador de pruebas que desee eliminar de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Delete]**.

![](../images/ui/delete-sandbox.png)

Aparecerá un cuadro de diálogo que le pedirá que confirme su elección. Seleccione **[!UICONTROL Continue]** para continuar.

![](../images/ui/delete-confirm.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione **[!UICONTROL Delete]**

![](../images/ui/delete-final-confirm.png)

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados dentro de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo administrar entornos limitados mediante la API de espacio aislado, consulte la [guía para desarrolladores de entornos limitados](../api/getting-started.md).