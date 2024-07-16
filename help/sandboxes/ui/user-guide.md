---
keywords: Experience Platform;inicio;temas populares;guía del usuario de zona protegida;guía del usuario de zona protegida
solution: Experience Platform
title: Guía de IU de Sandbox
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con los entornos limitados de la interfaz de usuario de Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 0db23e475d6546ebb886a56d5915d023ea215125
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 5%

---

# Guía de IU de Sandbox

Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con los entornos limitados de la interfaz de usuario de Adobe Experience Platform.

## Ver zonas protegidas

En la IU de Platform, selecciona **[!UICONTROL Zonas protegidas]** en el panel de navegación izquierdo y, a continuación, selecciona **[!UICONTROL Examinar]** para abrir el panel [!UICONTROL Zonas protegidas]. El panel enumera todos los entornos limitados disponibles para su organización, incluidos sus respectivos tipos (producción o desarrollo).

![view-sandboxes](../images/ui/view-sandboxes.png)

## Cambiar entre zonas protegidas

El indicador de zona protegida se encuentra en el encabezado superior de la interfaz de usuario de Platform y muestra el título de la zona protegida en la que se encuentra actualmente, su región y su tipo.

![indicador de espacio aislado](../images/ui/sandbox-indicator.png)

Para cambiar entre zonas protegidas, seleccione el indicador de la zona protegida y elija la zona protegida que desee en la lista desplegable.

![interfaz de conmutación](../images/ui/switcher-interface.png)

Una vez seleccionada una zona protegida, la pantalla se actualiza y se actualiza la zona protegida seleccionada.

![zona protegida conmutada](../images/ui/sandbox-switched.png)

## Creación de una zona protegida {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nombre de la zona protegida"
>abstract="El nombre de la zona protegida es el texto que se utiliza en el back-end para crear un ID único para esta zona protegida."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Título de la zona protegida"
>abstract="El título de la zona protegida es el nombre para mostrar que representa la zona protegida en menús y listas desplegables en toda la interfaz de usuario de Experience Platform."

>[!NOTE]
>
>La creación de una nueva zona protegida requiere que la agregue a una función en [[!UICONTROL Permisos]](../../access-control/abac/ui/permissions.md) para poder empezar a utilizarla. Para obtener información sobre cómo aprovisionar una zona protegida para una función, consulte la documentación de [administración de zonas protegidas para una función](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

Utilice el siguiente vídeo para obtener una descripción general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear una nueva zona protegida, seleccione **[!UICONTROL Crear zona protegida]** en la esquina superior derecha de la pantalla.

![create-sandbox](../images/ui/create-sandbox.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear zona protegida]**. Si está creando una zona protegida de desarrollo, seleccione **[!UICONTROL Desarrollo]** en el panel desplegable. Para crear una nueva zona protegida de producción, seleccione **[!UICONTROL Producción]**.

![tipo de zona protegida](../images/ui/sandbox-type.png)

Después de seleccionar el tipo, proporcione un nombre y un título a la zona protegida. El título debe ser legible en lenguaje natural y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El nombre de la zona protegida es un identificador en minúsculas para su uso en llamadas a la API y, por lo tanto, debe ser único y conciso. El nombre de la zona protegida debe comenzar con una letra, tener un máximo de 256 caracteres y constar solo de caracteres alfanuméricos y guiones (-).

Cuando termine, seleccione **[!UICONTROL Crear]**.

![información de zona protegida](../images/ui/sandbox-info.png)

Una vez que haya terminado de crear la zona protegida, actualice la página y aparecerá la nueva zona protegida en el panel **[!UICONTROL Zonas protegidas]** con el estado &quot;[!UICONTROL Creando]&quot;. El sistema tarda aproximadamente 30 segundos en aprovisionar las nuevas zonas protegidas, después de lo cual su estado cambia a &quot;[!UICONTROL Activo]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Restablecer una zona protegida

>[!WARNING]
>
>A continuación se muestra una lista de excepciones que pueden impedir el restablecimiento de la zona protegida de producción predeterminada o de una creada por el usuario:
>* No se puede restablecer la zona protegida de producción predeterminada si Adobe Analytics también está usando el gráfico de identidades alojado en esta zona protegida para la característica [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es).
>* No se puede restablecer la zona protegida de producción predeterminada si Adobe Audience Manager también está usando el gráfico de identidades alojado en la zona protegida para [destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).
>* La zona protegida de producción predeterminada no se puede restablecer si contiene datos para las funciones de CDA y PBD.
>* Una zona protegida de producción creada por el usuario que se utiliza para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de Audience se puede restablecer después de un mensaje de advertencia.
>* Antes de iniciar el restablecimiento de una zona protegida, se le pedirá que elimine sus composiciones manualmente para asegurarse de que los datos de audiencia asociados se limpien correctamente.

### Eliminar composiciones de audiencia

La composición de audiencias no está integrada actualmente con la capacidad de restablecimiento de la zona protegida, por lo que las audiencias deberán eliminarse manualmente antes de realizar el restablecimiento de la zona protegida.

Seleccione **[!UICONTROL Audiencias]** en el panel de navegación izquierdo y luego seleccione **[!UICONTROL Composiciones]**.

![La ficha [!UICONTROL Composiciones] del área de trabajo de [!UICONTROL Audiencias].](../images/ui/audiences.png)

A continuación, seleccione los puntos suspensivos (`...`) junto a la primera audiencia y luego seleccione **[!UICONTROL Eliminar]**.

![Menú de audiencia que resalta la opción [!UICONTROL Eliminar].](../images/ui/delete-composition.png)

Se mostrará una confirmación de la eliminación correcta y volverá a la ficha **[!UICONTROL Composiciones]**.

Repita los pasos anteriores con todas las composiciones. Se eliminarán todas las audiencias del inventario de audiencias. Una vez eliminadas todas las audiencias, puede seguir restableciendo la zona protegida.

### Restablecimiento de una zona protegida

Al restablecer una zona protegida de producción o desarrollo, se eliminan todos los recursos asociados a ella (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre y los permisos asociados. Esta zona protegida &quot;limpia&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a ella.

Seleccione la zona protegida que desee restablecer en la lista de zonas protegidas. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Restablecimiento de espacio aislado]**.

![restablecer](../images/ui/reset.png)

Aparecerá un cuadro de diálogo solicitándole que confirme su elección. Seleccione **[!UICONTROL Continuar]** para continuar.

![advertencia de restablecimiento](../images/ui/reset-warning.png)

En la ventana de confirmación final, escriba el nombre de la zona protegida en el cuadro de diálogo y seleccione **[!UICONTROL Restablecer]**.

![restablecer-confirmar](../images/ui/reset-confirm.png)

## Eliminación de una zona protegida

>[!WARNING]
>
>No puede eliminar la zona protegida de producción predeterminada. Sin embargo, cualquier zona protegida de producción creada por el usuario que se utilice para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service] se puede eliminar después de un mensaje de advertencia.

Al eliminar una zona protegida de producción o desarrollo, se eliminan permanentemente todos los recursos asociados a dicha zona protegida, incluidos los permisos.

Seleccione la zona protegida que desee eliminar de la lista de zonas protegidas. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Eliminar]**.

![eliminar](../images/ui/delete.png)

Aparecerá un cuadro de diálogo solicitándole que confirme su elección. Seleccione **[!UICONTROL Continuar]** para continuar.

![eliminar-advertencia](../images/ui/delete-warning.png)

En la ventana de confirmación final, escriba el nombre de la zona protegida en el cuadro de diálogo y seleccione **[!UICONTROL Continuar]**.

![eliminar-confirmar](../images/ui/delete-confirm.png)

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo administrar zonas protegidas mediante la API de zonas protegidas, consulte la [guía para desarrolladores de zonas protegidas](../api/getting-started.md).
