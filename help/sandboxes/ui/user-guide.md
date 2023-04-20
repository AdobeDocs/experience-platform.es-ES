---
keywords: Experience Platform;inicio;temas populares;guía del usuario del entorno limitado;guía del entorno limitado
solution: Experience Platform
title: Guía de la interfaz de usuario del Simulador para pruebas
description: Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 8%

---

# Guía de la interfaz de usuario del Simulador para pruebas

Este documento proporciona pasos sobre cómo realizar varias operaciones relacionadas con entornos limitados en la interfaz de usuario de Adobe Experience Platform.

## Ver entornos limitados

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sandboxes]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Examinar]** para abrir el [!UICONTROL Sandboxes] tablero. El tablero enumera todos los entornos limitados disponibles para su organización, incluidos sus respectivos tipos (producción o desarrollo).

![entornos limitados de vista](../images/ui/view-sandboxes.png)

## Cambiar entre entornos limitados

El indicador del simulador de pruebas está situado en el encabezado superior de la interfaz de usuario de Platform y muestra el título del simulador de pruebas en el que se encuentra, su región y su tipo.

![indicador de entorno limitado](../images/ui/sandbox-indicator.png)

Para cambiar entre entornos limitados, seleccione el indicador del entorno limitado y seleccione el entorno limitado que desee en la lista desplegable.

![interfaz del conmutador](../images/ui/switcher-interface.png)

Una vez seleccionado un simulador para pruebas, la pantalla se actualiza y actualiza al simulador para pruebas seleccionado.

![cambio de entorno limitado](../images/ui/sandbox-switched.png)

## Crear un nuevo simulador de pruebas {#create}

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
>Cuando se crea un nuevo simulador para pruebas, primero debe agregar ese nuevo simulador para pruebas al perfil del producto en [Adobe Admin Console](https://adminconsole.adobe.com/) antes de empezar a usar el nuevo simulador de pruebas. Consulte la documentación sobre [administración de permisos para un perfil de producto](../../access-control/ui/permissions.md) para obtener información sobre cómo aprovisionar un entorno limitado a un perfil de producto.

Utilice el siguiente vídeo para obtener información general rápida sobre cómo utilizar entornos limitados en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para crear un nuevo simulador de pruebas, seleccione **[!UICONTROL Crear entorno limitado]** en la esquina superior derecha de la pantalla.

![create-sandbox](../images/ui/create-sandbox.png)

La variable **[!UICONTROL Crear entorno limitado]** aparece en el cuadro de diálogo. Si está creando un entorno limitado de desarrollo, seleccione **[!UICONTROL Desarrollo]** en el panel desplegable. Para crear un nuevo simulador para pruebas de producción, seleccione **[!UICONTROL Producción]**.

![tipo de entorno limitado](../images/ui/sandbox-type.png)

Después de seleccionar el tipo, proporcione un nombre y un título al simulador de pruebas. El título debe ser legible por el ser humano y debe ser lo suficientemente descriptivo como para ser fácilmente identificable. El nombre del simulador para pruebas es un identificador en minúsculas que se utiliza en las llamadas a la API y, por lo tanto, debe ser único y conciso. El nombre del simulador para pruebas debe comenzar con una letra, tener un máximo de 256 caracteres y constar únicamente de caracteres alfanuméricos y guiones (-).

Cuando termine, seleccione **[!UICONTROL Crear]**.

![sandbox-info](../images/ui/sandbox-info.png)

Una vez que haya terminado de crear el simulador de pruebas, actualice la página y aparecerá el nuevo simulador de pruebas en la **[!UICONTROL Sandboxes]** panel con el estado &quot;[!UICONTROL Creación]&quot;. Los nuevos entornos limitados tardan aproximadamente 30 segundos en ser aprovisionados por el sistema, tras lo cual su estado cambia a &quot;[!UICONTROL Activo]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Restablecer un simulador para pruebas

>[!WARNING]
>
>A continuación se muestra una lista de excepciones que pueden impedir que restablezca el entorno limitado de producción predeterminado o un entorno limitado de producción creado por el usuario: <ul><li>No se puede restablecer el simulador para pruebas de producción predeterminado si Adobe Analytics también está utilizando el gráfico de identidad alojado en el simulador para pruebas [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es) función.</li><li>No se puede restablecer el simulador para pruebas de producción predeterminado si Adobe Audience Manager también está utilizando el gráfico de identidad alojado en el simulador para pruebas [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).</li><li>No se puede restablecer el entorno limitado de producción predeterminado si contiene datos para las funciones CDA y PBD.</li><li>Un simulador para pruebas de producción creado por el usuario que se utiliza para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de audiencia se puede restablecer tras un mensaje de advertencia.</li></ul>

Al restablecer un entorno limitado de producción o desarrollo, se eliminan todos los recursos asociados a dicho entorno limitado (esquemas, conjuntos de datos, etc.), al tiempo que se mantienen el nombre del entorno limitado y los permisos asociados. Este simulador de pruebas &quot;limpio&quot; sigue estando disponible con el mismo nombre para los usuarios que tienen acceso a él.

Seleccione el simulador de pruebas que desea restablecer de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Restablecimiento de Sandbox]**.

![reset](../images/ui/reset.png)

Aparece un cuadro de diálogo que le solicita que confirme su elección. Select **[!UICONTROL Continuar]** para continuar.

![reset-warning](../images/ui/reset-warning.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione **[!UICONTROL Restablecer]**.

![reset-confirm](../images/ui/reset-confirm.png)

## Eliminación de un simulador para pruebas

>[!WARNING]
>
>No se puede eliminar el entorno limitado de producción predeterminado. Sin embargo, cualquier simulador para pruebas de producción creado por el usuario que se use para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service] se puede eliminar después de un mensaje de advertencia.

Al eliminar un entorno limitado de producción o desarrollo, se eliminan permanentemente todos los recursos asociados a dicho entorno limitado, incluidos los permisos.

Seleccione el simulador de pruebas que desee eliminar de la lista de entornos limitados. En el panel de navegación derecho que aparece, seleccione **[!UICONTROL Eliminar]**.

![delete](../images/ui/delete.png)

Aparece un cuadro de diálogo que le solicita que confirme su elección. Select **[!UICONTROL Continuar]** para continuar.

![delete-warning](../images/ui/delete-warning.png)

En la ventana de confirmación final, introduzca el nombre del simulador de pruebas en el cuadro de diálogo y seleccione  **[!UICONTROL Continuar]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Pasos siguientes

Este documento muestra cómo administrar entornos limitados dentro de la interfaz de usuario del Experience Platform. Para obtener información sobre cómo administrar entornos limitados mediante la API de espacio aislado, consulte la [guía para desarrolladores de sandbox](../api/getting-started.md).
