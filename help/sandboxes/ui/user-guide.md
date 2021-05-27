---
keywords: Experience Platform;inicio;temas populares;guía del usuario del entorno limitado;guía del entorno limitado
solution: Experience Platform
title: Guía de la interfaz de usuario del Simulador para pruebas
topic-legacy: user guide
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 8c1c7b6b01b55bd15c492b0f62d280c1e9a98070
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Guía de la interfaz de usuario del Simulador para pruebas

Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.

## Ver entornos limitados

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sandboxes]** en el panel de navegación izquierdo para abrir el tablero [!UICONTROL Sandboxes]. El tablero enumera todos los entornos limitados disponibles para su organización, incluido el tipo de entorno limitado (producción o desarrollo) y el estado (activo, creador, eliminado o fallido).

![](../images/ui/view-sandboxes.png)

## Cambiar entre entornos limitados

El control **sandbox switch** en la parte superior izquierda de la pantalla muestra el entorno limitado activo actualmente.

![](../images/ui/sandbox-switcher.png)

Para cambiar entre entornos limitados, seleccione el conmutador de simulador de pruebas y seleccione el simulador de pruebas que desee en la lista desplegable.

![](../images/ui/switcher-menu.png)

Una vez seleccionado un simulador de pruebas, la pantalla se actualiza con el simulador de pruebas seleccionado que ahora aparece en el simulador de pruebas.

![](../images/ui/switched.png)

## Buscar un simulador de pruebas

Puede navegar por la lista de entornos limitados disponibles mediante la función de búsqueda del menú del conmutador de entornos limitados. Escriba el nombre del simulador de pruebas al que desea acceder para filtrar por todos los entornos limitados disponibles para su organización.

![](../images/ui/sandbox-search.png)

## Crear un nuevo simulador de pruebas

Utilice el siguiente vídeo para obtener información general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear un nuevo entorno limitado, seleccione **[!UICONTROL Crear entorno limitado]** en la esquina superior derecha de la pantalla.

![crear](../images/ui/create.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear entorno limitado]**. Si está creando un entorno limitado de desarrollo, seleccione **[!UICONTROL Desarrollo]** en el panel desplegable. Para crear un nuevo entorno limitado de producción, seleccione **[!UICONTROL Producción]**.

![type](../images/ui/type.png)

Después de seleccionar el tipo, proporcione un nombre y un título al simulador de pruebas. El título debe ser legible por el ser humano y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El nombre del simulador para pruebas es un identificador en minúsculas que se utiliza en las llamadas a la API y, por lo tanto, debe ser único y conciso. El nombre del simulador para pruebas debe comenzar con una letra, tener un máximo de 256 caracteres y constar únicamente de caracteres alfanuméricos y guiones (-).

Cuando termine, seleccione **[!UICONTROL Crear]**.

![información](../images/ui/info.png)

Una vez que haya terminado de crear el simulador para pruebas, actualice la página y aparecerá el nuevo simulador para pruebas en el tablero **[!UICONTROL Sandboxes]** con el estado &quot;[!UICONTROL Creating]&quot;. El sistema tarda aproximadamente 30 segundos en aprovisionar nuevos entornos limitados, tras lo cual su estado cambia a &quot;[!UICONTROL Activo]&quot;.

## Restablecer un simulador para pruebas

>[!IMPORTANT]
>
>No se puede restablecer el entorno limitado de producción predeterminado si Adobe Analytics también está utilizando el gráfico de identidad alojado en él para la función [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) o si Adobe Audience Manager también está utilizando el gráfico de identidad alojado en él para la función [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) . Tampoco se pueden restablecer los entornos limitados de producción que se utilizan para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de audiencia.

Al restablecer un entorno limitado de producción o desarrollo, se eliminan todos los recursos asociados a dicho entorno limitado (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre del entorno limitado y los permisos asociados. Este simulador de pruebas &quot;limpio&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a él.

Seleccione el simulador de pruebas que desea restablecer de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Sandbox reset]**.

![reset](../images/ui/reset.png)

Aparece un cuadro de diálogo que le solicita que confirme su elección. Seleccione **[!UICONTROL Continue]** para continuar.

![reset-warning](../images/ui/reset-warning.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione **[!UICONTROL Reset]**

![reset-confirm](../images/ui/reset-confirm.png)

## Eliminación de un simulador para pruebas

>[!IMPORTANT]
>
>El entorno limitado de producción predeterminado no se puede eliminar y los entornos limitados de producción que se utilizan para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de audiencia tampoco se pueden eliminar.

Al eliminar un entorno limitado de producción o desarrollo, se eliminan permanentemente todos los recursos asociados a dicho entorno limitado, incluidos los permisos.

Seleccione el simulador de pruebas que desee eliminar de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Eliminar]**.

![delete](../images/ui/delete.png)

Aparece un cuadro de diálogo que le solicita que confirme su elección. Seleccione **[!UICONTROL Continue]** para continuar.

![delete-warning](../images/ui/delete-warning.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione **[!UICONTROL Continue]**

![delete-confirm](../images/ui/delete-confirm.png)

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados dentro de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo administrar entornos limitados mediante la API de espacio aislado, consulte la [guía para desarrolladores de entornos limitados](../api/getting-started.md).
