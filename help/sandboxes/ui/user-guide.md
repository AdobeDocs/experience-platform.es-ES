---
keywords: Experience Platform;inicio;temas populares;guía del usuario de zona protegida;guía del usuario de zona protegida
solution: Experience Platform
title: Guía de IU de Sandbox
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con los entornos limitados de la interfaz de usuario de Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Guía de IU de Sandbox

Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con los entornos limitados de la interfaz de usuario de Adobe Experience Platform.

## Ver zonas protegidas

En la IU de Platform, seleccione **[!UICONTROL Zonas protegidas]** en el panel de navegación izquierdo y seleccione **[!UICONTROL Examinar]** para abrir [!UICONTROL Zonas protegidas] panel. El panel enumera todos los entornos limitados disponibles para su organización, incluidos sus respectivos tipos (producción o desarrollo).

![view-sandboxes](../images/ui/view-sandboxes.png)

## Cambiar entre zonas protegidas

El indicador de zona protegida se encuentra en el encabezado superior de la interfaz de usuario de Platform y muestra el título de la zona protegida en la que se encuentra actualmente, su región y su tipo.

![sandbox-indicator](../images/ui/sandbox-indicator.png)

Para cambiar entre zonas protegidas, seleccione el indicador de la zona protegida y elija la zona protegida que desee en la lista desplegable.

![interfaz de conmutación](../images/ui/switcher-interface.png)

Una vez seleccionada una zona protegida, la pantalla se actualiza y se actualiza la zona protegida seleccionada.

![conmutado por zona protegida](../images/ui/sandbox-switched.png)

## Crear una nueva zona protegida {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nombre de zona protegida"
>abstract="El nombre de la zona protegida es el texto que se utiliza en el back-end para crear un ID único para esta zona protegida."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Título de zona protegida"
>abstract="El título de la zona protegida es el nombre para mostrar que representará la zona protegida en menús y desplegables a través de la interfaz de usuario de Experience Platform."

>[!NOTE]
>
>Cuando se crea una nueva zona protegida, primero debe agregarla al perfil del producto en [Adobe Admin Console](https://adminconsole.adobe.com/) antes de empezar a usar la nueva zona protegida. Consulte la documentación sobre [administración de permisos para un perfil de producto](../../access-control/ui/permissions.md) para obtener información sobre cómo aprovisionar una zona protegida en un perfil de producto.

Utilice el siguiente vídeo para obtener una descripción general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear una nueva zona protegida, seleccione **[!UICONTROL Crear zona protegida]** en la esquina superior derecha de la pantalla.

![create-sandbox](../images/ui/create-sandbox.png)

El **[!UICONTROL Crear zona protegida]** aparece el cuadro de diálogo. Si está creando una zona protegida de desarrollo, seleccione **[!UICONTROL Desarrollo]** en el panel desplegable. Para crear una nueva zona protegida de producción, seleccione **[!UICONTROL Producción]**.

![sandbox-type](../images/ui/sandbox-type.png)

Después de seleccionar el tipo, proporcione un nombre y un título a la zona protegida. El título debe ser legible en lenguaje natural y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El nombre de la zona protegida es un identificador en minúsculas para su uso en llamadas a la API y, por lo tanto, debe ser único y conciso. El nombre de la zona protegida debe comenzar con una letra, tener un máximo de 256 caracteres y constar solo de caracteres alfanuméricos y guiones (-).

Cuando termine, seleccione **[!UICONTROL Crear]**.

![sandbox-info](../images/ui/sandbox-info.png)

Una vez que haya terminado de crear la zona protegida, actualice la página y aparecerá la nueva zona protegida en la **[!UICONTROL Zonas protegidas]** panel con un estado de &quot;[!UICONTROL Creando]&quot;. El sistema tarda aproximadamente 30 segundos en aprovisionar las nuevas zonas protegidas, después de lo cual su estado cambia a &quot;[!UICONTROL Activo]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Restablecer una zona protegida

>[!WARNING]
>
>A continuación se muestra una lista de excepciones que pueden impedir el restablecimiento de la zona protegida de producción predeterminada o de una creada por el usuario: <ul><li>La zona protegida de producción predeterminada no se puede restablecer si Adobe Analytics también está utilizando el gráfico de identidades alojado en esta zona protegida para [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es) función.</li><li>La zona protegida de producción predeterminada no se puede restablecer si Adobe Audience Manager también está utilizando el gráfico de identidades alojado en esta zona protegida para [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).</li><li>La zona protegida de producción predeterminada no se puede restablecer si contiene datos para las funciones de CDA y PBD.</li><li>Una zona protegida de producción creada por el usuario que se utiliza para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de Audience se puede restablecer después de un mensaje de advertencia.</li></ul>

Al restablecer una zona protegida de producción o desarrollo, se eliminan todos los recursos asociados a ella (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre y los permisos asociados. Esta zona protegida &quot;limpia&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a ella.

Seleccione la zona protegida que desee restablecer en la lista de zonas protegidas. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Restablecimiento de zona protegida]**.

![restablecer](../images/ui/reset.png)

Aparecerá un cuadro de diálogo solicitándole que confirme su elección. Seleccionar **[!UICONTROL Continuar]** para continuar.

![reset-warning](../images/ui/reset-warning.png)

En la ventana de confirmación final, introduzca el nombre de la zona protegida en el cuadro de diálogo y seleccione **[!UICONTROL Restablecer]**.

![restablecer-confirmar](../images/ui/reset-confirm.png)

## Eliminación de una zona protegida

>[!WARNING]
>
>No puede eliminar la zona protegida de producción predeterminada. Sin embargo, cualquier zona protegida de producción creada por el usuario que se utilice para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service] se puede eliminar después de un mensaje de advertencia.

Al eliminar una zona protegida de producción o desarrollo, se eliminan permanentemente todos los recursos asociados a dicha zona protegida, incluidos los permisos.

Seleccione la zona protegida que desee eliminar de la lista de zonas protegidas. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Eliminar]**.

![eliminar](../images/ui/delete.png)

Aparecerá un cuadro de diálogo solicitándole que confirme su elección. Seleccionar **[!UICONTROL Continuar]** para continuar.

![delete-warning](../images/ui/delete-warning.png)

En la ventana de confirmación final, introduzca el nombre de la zona protegida en el cuadro de diálogo y seleccione  **[!UICONTROL Continuar]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo administrar entornos limitados mediante la API de entorno limitado, consulte la [guía para desarrolladores de sandbox](../api/getting-started.md).
