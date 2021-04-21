---
keywords: Experience Platform;inicio;temas populares;guía del usuario del entorno limitado;guía del entorno limitado
solution: Experience Platform
title: Guía de la interfaz de usuario del Simulador para pruebas
topic-legacy: user guide
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '608'
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

Utilice el siguiente vídeo para obtener información general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear un nuevo simulador de pruebas en la interfaz de usuario, seleccione el botón **[!UICONTROL Create Sandbox]** en la parte superior derecha de la pantalla.

![](../images/ui/create-sandbox.png)

Aparece el cuadro de diálogo **[!UICONTROL Create Sandbox]**, que le solicita que proporcione un título y un nombre para mostrar para el simulador de pruebas. El **título de visualización** está diseñado para ser legible por el usuario y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El simulador de pruebas **[!UICONTROL Name]** es un identificador en minúsculas que se utiliza en las llamadas a la API y, por lo tanto, debe ser único y conciso. El simulador de pruebas **[!UICONTROL Name]** solo debe contener caracteres alfanuméricos y guiones **(-)**, debe comenzar con una letra y tener un máximo de 256 caracteres.

Cuando termine, seleccione **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Como está restringido a la creación de tipos de entornos limitados que no sean de producción solamente, la opción **[!UICONTROL type]** está bloqueada en &quot;No de producción&quot; y no se puede manipular.

Una vez que haya terminado de crear el entorno limitado, actualice la página y aparecerá el nuevo entorno limitado en el panel **[!UICONTROL Sandboxes]** con el estado &quot;[!UICONTROL Creating]&quot;. El sistema tarda aproximadamente 15 minutos en aprovisionar nuevos entornos limitados, tras lo cual su estado cambia a &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Restablecer un simulador para pruebas

>[!NOTE]
>
>Esta funcionalidad solo está disponible para entornos limitados que no sean de producción. No se pueden restablecer los entornos limitados de producción.

Al restablecer un simulador para pruebas que no sean de producción, se eliminan todos los recursos asociados a ese simulador para pruebas (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre del simulador para pruebas y los permisos asociados. Este simulador de pruebas &quot;limpio&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a él.

Para restablecer un simulador para pruebas en la interfaz de usuario, seleccione **[!UICONTROL Sandboxes]** en la barra de navegación izquierda y, a continuación, seleccione el simulador para pruebas que desea restablecer. En el cuadro de diálogo que aparece en el lado derecho de la pantalla, seleccione **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox.png)

Aparecerá un cuadro de diálogo que le pedirá que confirme su elección. Seleccione **[!UICONTROL Reset]** para continuar.

![](../images/ui/reset-confirm.png)

Aparece un mensaje de confirmación y el estado del entorno limitado cambia a &quot;**[!UICONTROL Resetting]&quot;**. Una vez que el sistema lo haya aprovisionado, su estado se actualizará a **&quot;[!UICONTROL Active]&quot;** o **&quot;[!UICONTROL Failed]&quot;**.

![](../images/ui/resetting.png)

## Eliminación de un simulador para pruebas

>[!NOTE]
>
>Esta funcionalidad solo está disponible para entornos limitados que no sean de producción. Los entornos limitados de producción no se pueden eliminar.

Al eliminar permanentemente un simulador para pruebas que no sean de producción, se eliminan todos los recursos asociados con ese simulador para pruebas, incluidos los permisos.

Para eliminar un simulador para pruebas en la interfaz de usuario, seleccione **[!UICONTROL Sandboxes]** en la barra de navegación izquierda y, a continuación, seleccione el simulador para pruebas que desea eliminar. En el cuadro de diálogo que aparece en el lado derecho de la pantalla, seleccione **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox.png)

Aparecerá un cuadro de diálogo que le pedirá que confirme su elección. Seleccione **[!UICONTROL Delete]** para continuar.

![](../images/ui/delete-confirm.png)

Aparece un mensaje de confirmación y el simulador de pruebas se elimina del espacio de trabajo **[!UICONTROL Sandboxes]**.

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados dentro de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo administrar entornos limitados mediante la API de espacio aislado, consulte la [guía para desarrolladores de entornos limitados](../api/getting-started.md).
