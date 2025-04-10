---
title: Guía de IU de políticas de combinación
type: Documentation
description: Aprenda a trabajar con políticas de combinación mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 2%

---


# Guía de la IU de las políticas de combinación

Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Experience Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.

Mediante las API de RESTful o la interfaz de usuario de, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con directivas de combinación mediante la interfaz de usuario (IU) de Adobe Experience Platform.

Para obtener más información sobre las políticas de combinación y su función en Experience Platform, lea la [descripción general de las políticas de combinación](overview.md).

## Introducción

Esta guía requiere una comprensión práctica de varias características importantes de [!DNL Experience Platform]. Antes de seguir esta guía, revise la documentación de los siguientes servicios:

* [Perfil del cliente en tiempo real](../home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): habilita el perfil del cliente en tiempo real al unir identidades de diferentes fuentes de datos que se están ingiriendo en [!DNL Experience Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.

## Ver políticas de combinación {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Política de combinación no encontrada"
>abstract="Esto significa que Experience Platform no ha podido encontrar la política de combinación solicitada. Para resolver este error, pruebe una de las siguientes soluciones:<ul><li>Asegúrese de que el ID de la política de combinación correcto aparece en la dirección URL.</li><li>Asegúrese de que tiene la combinación correcta de organización y zona protegida para la política de combinación a la que intenta acceder.</li></ul>"

En la interfaz de usuario de [!DNL Experience Platform], puede empezar a trabajar con directivas de combinación seleccionando **[!UICONTROL Perfiles]** en el panel de navegación izquierdo y, a continuación, la pestaña **[!UICONTROL Políticas de combinación]**.

Esta pestaña incluye una lista de todas las políticas de combinación existentes para su organización, así como detalles para cada política de combinación, incluido el nombre de la política, si la política de combinación es o no la política de combinación predeterminada y la clase de esquema con la que se relaciona la política de combinación.

![Se muestra la página de exploración de las políticas de combinación.](../images/merge-policies/landing.png)

Para seleccionar qué detalles están visibles o para agregar columnas adicionales a la pantalla, seleccione ![el icono de configuración de columna](../../images/icons/column-settings.png) y seleccione un nombre de columna para agregarlo o quitarlo de la vista.

![Se muestran las opciones disponibles para personalizar la página de exploración de la directiva de combinación.](../images/merge-policies/adjust-view.png)

## Crear una política de combinación {#create-a-merge-policy}

Para crear una nueva política de combinación, seleccione **[!UICONTROL Crear política de combinación]** en la ficha políticas de combinación para introducir el nuevo flujo de trabajo de la política de combinación.

![Página de aterrizaje de políticas de combinación con el botón Crear resaltado.](../images/merge-policies/create-new.png)

El flujo de trabajo **[!UICONTROL Nueva política de combinación]** requiere que proporcione información importante para la nueva política de combinación mediante una serie de pasos guiados. Estos pasos se describen en las secciones siguientes.

![El nuevo flujo de trabajo de la política de combinación.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

El primer paso del flujo de trabajo le permite configurar la política de combinación proporcionando información básica. Esta información incluye:

* **[!UICONTROL Nombre]**: el nombre de la política de combinación debe ser descriptivo pero conciso.
* **[!UICONTROL Clase de esquema]**: La clase de esquema XDM asociada a la política de combinación. Especifica la clase de esquema para la que se crea esta política de combinación. Las organizaciones pueden crear varias políticas de combinación por clase de esquema. Actualmente, solo la clase [!UICONTROL XDM Individual Profile] está disponible en la interfaz de usuario. Puede obtener una vista previa del esquema de unión para la clase de esquema seleccionando **[!UICONTROL Ver esquema de unión]**. Para obtener más información, vea la sección sobre [ver el esquema de unión](#view-union-schema) que sigue.
* **[!UICONTROL Vinculación de ID]**: este campo define cómo determinar las identidades relacionadas de un cliente. Existen dos valores posibles para la vinculación de identidad y es importante comprender cómo afectará a los datos el tipo de vinculación de identidad que seleccione. Para obtener más información, consulte la [descripción general de las políticas de combinación](overview.md).
   * **[!UICONTROL Ninguno]**: no realice ninguna vinculación de identidad.
   * **[!UICONTROL Gráfico privado]**: realice la vinculación de identidad en función de su gráfico de identidad privado.
* **[!UICONTROL Política de combinación predeterminada]**: Botón de alternancia que le permite seleccionar si esta política de combinación será o no la predeterminada para su organización. Si el selector está activado, aparece una advertencia que le solicita que confirme que desea cambiar la política de combinación predeterminada de su organización. Consulte la [descripción general de las políticas de combinación](overview.md) para obtener más información sobre las políticas de combinación predeterminadas.
  ![Una ventana emergente que explica lo que sucede cuando la política de combinación se establece como política de combinación predeterminada.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Política de combinación activa en Edge]**: Un botón de alternancia que le permite seleccionar si esta política de combinación estará activa o no en Edge. Para garantizar que todos los consumidores de perfiles trabajen con la misma vista en los bordes, las políticas de combinación se pueden marcar como activas en el borde. Para que una audiencia se active en Edge (marcada como audiencia Edge), debe estar vinculada a una política de combinación marcada como activa en Edge. Si una audiencia **no** está vinculada a una política de combinación marcada como activa en Edge, la audiencia no se marca como activa en Edge y se marca como una audiencia de flujo continuo. Además, cada zona protegida de una organización solo puede tener **una** política de combinación activa en Edge.

Una vez completados los campos obligatorios, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo.

![Se completó la configuración de la pantalla con el botón Siguiente resaltado.](../images/merge-policies/create-complete.png)

## [!UICONTROL Ver esquema de unión] {#view-union-schema}

Al crear o editar una política de combinación, puede ver el esquema de unión de la clase de esquema elegida seleccionando **[!UICONTROL Ver esquema de unión]**.

![El botón &quot;Ver esquema de unión&quot; está resaltado en el nuevo flujo de trabajo de la política de combinación.](../images/merge-policies/view-union-schema.png)

Esto abre el cuadro de diálogo [!UICONTROL Ver esquema de unión], que muestra todos los esquemas, identidades y relaciones asociados con el esquema de unión. Puede usar el cuadro de diálogo para explorar el esquema de unión de la misma manera que lo haría si accediera a la pestaña [!UICONTROL Esquema de unión] en la sección [!UICONTROL Perfiles] de la interfaz de usuario de Experience Platform.

Para obtener información detallada sobre los esquemas de unión, incluido cómo interactuar con ellos en la pestaña [!UICONTROL Esquema de unión] o el cuadro de diálogo [!UICONTROL Ver esquema de unión] que se muestra en el flujo de trabajo de las políticas de combinación, visite la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md).

![Cuadro de diálogo Ver esquema de unión.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleccionar conjuntos de datos de perfil] {#select-profile-datasets}

En la pantalla **[!UICONTROL Seleccionar conjuntos de datos de perfil]**, debe seleccionar el **[!UICONTROL método de combinación]** que desee usar en la política de combinación. En la pantalla también se muestra el número total de [!UICONTROL conjuntos de datos de perfil] de su organización relacionados con la clase de esquema que se seleccionó en la pantalla anterior.

Según el método de combinación que elija, todos los conjuntos de datos de perfil se combinarán en el orden en que se actualizaron por última vez (con la marca de tiempo ordenada) o tendrá que seleccionar qué conjuntos de datos de perfil incluir en la política de combinación y el orden en que combinarlos (prioridad de conjuntos de datos).

Para obtener más información sobre los métodos de combinación, consulte la [descripción general de las políticas de combinación](overview.md).

>[!BEGINTABS]

>[!TAB Marca de tiempo solicitada]

Si se selecciona **[!UICONTROL Marca de tiempo ordenada]** como método de combinación, los atributos de los conjuntos de datos actualizados más recientemente tendrán prioridad. Esto se aplica a todos los conjuntos de datos de perfil.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen que se muestra) muestra el número total de conjuntos de datos de perfil que se incluirán.

![Imagen que muestra el método de combinación ordenado con marca de tiempo seleccionado.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Prioridad de conjuntos de datos]

Si selecciona **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación, deberá seleccionar Conjuntos de datos de perfil y priorizarlos manualmente. Cada conjunto de datos enumerado también incluye el estado del último lote introducido o muestra un aviso de que no se han introducido lotes en ese conjunto de datos.

Puede seleccionar hasta 50 conjuntos de datos de la lista de conjuntos de datos para incluirlos en la política de combinación.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen mostrada) muestra el número total de conjuntos de datos de perfil disponibles para su selección.

A medida que se seleccionan los conjuntos de datos, se agregan a la sección **[!UICONTROL Seleccionar conjuntos de datos]**, lo que le permite arrastrar y soltar los conjuntos de datos y ordenarlos según la prioridad que desee. A medida que los conjuntos de datos se ajustan en la lista, se actualiza el ordinal (1, 2, 3, etc.) junto al conjunto de datos, mostrando la prioridad (1 recibe la prioridad más alta, luego 2 y en adelante).

Al seleccionar un conjunto de datos, también se actualiza la sección **[!UICONTROL Esquema de unión]**, que muestra los campos del esquema de unión a los que cada conjunto de datos aporta datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones de la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md)

![Imagen que muestra la prioridad del conjunto de datos que se está seleccionando, junto con la configuración correspondiente que debe elegir si esa opción está seleccionada.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Seleccionar conjuntos de datos de ExperienceEvent] {#select-experienceevent-datasets}

El siguiente paso del flujo de trabajo requiere que seleccione conjuntos de datos de ExperienceEvent. En esta pantalla influye el método de combinación seleccionado en la pantalla [[!UICONTROL Seleccionar conjuntos de datos de perfil]](#select-profile-datasets).

>[!BEGINTABS]

>[!TAB Marca de tiempo solicitada]

Si seleccionó **[!UICONTROL Marca de tiempo ordenada]** como método de combinación para conjuntos de datos de perfil, los atributos de los conjuntos de datos de ExperienceEvent actualizados más recientemente también tendrán prioridad aquí.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL conjuntos de datos de ExperienceEvent]** (por ejemplo, `(1)` en la imagen que se muestra) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización relacionados con la clase de esquema que seleccionó en la pantalla de configuración de la política de combinación.

![Se muestra el número total de conjuntos de datos de ExperienceEvent que pueden relacionarse con la clase de esquema.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Prioridad de conjuntos de datos]

Si seleccionó **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación para los conjuntos de datos de perfil, deberá seleccionar los conjuntos de datos de ExperienceEvent que desea incluir. Puede seleccionar hasta 50 conjuntos de datos de ExperienceEvent en la lista de conjuntos de datos.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL conjuntos de datos de ExperienceEvent]** (por ejemplo, `(1)` en la imagen que se muestra) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización relacionados con la clase de esquema que seleccionó en la pantalla de configuración de la política de combinación.

Cuando se seleccionan los conjuntos de datos, aparecen en la sección [!UICONTROL Seleccionar conjuntos de datos].

Los conjuntos de datos de ExperienceEvent no se pueden ordenar manualmente; en su lugar, los atributos de los conjuntos de datos de ExperienceEvent se anexan a los conjuntos de datos de perfil si forman parte del mismo fragmento de perfil.

De forma similar a seleccionar Conjuntos de datos de perfil, al seleccionar un conjunto de datos de ExperienceEvent también se actualiza la sección **[!UICONTROL Esquema de unión]**, que muestra los campos del esquema de unión a los que cada conjunto de datos aporta datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones de la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md).

![Se muestran los conjuntos de datos de ExperienceEvent seleccionables.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Revisar] {#review}

El paso final del flujo de trabajo es revisar la política de combinación. La pantalla **[!UICONTROL Revisar]** muestra información sobre la política de combinación, incluido el método de vinculación de ID seleccionado, el método de combinación seleccionado y los conjuntos de datos incluidos. (Para ver todos los conjuntos de datos de perfil o ExperienceEvent incluidos, seleccione el número de conjuntos de datos para expandir la lista desplegable).

También se incluye en la pantalla de revisión la tabla **[!UICONTROL Vista previa de datos]** que muestra registros de perfil de muestra mediante la política de combinación. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

Asegúrese de revisar cuidadosamente la configuración de la política de combinación y obtener una vista previa de los datos antes de seleccionar **[!UICONTROL Finalizar]** para completar el flujo de trabajo de creación.

>[!BEGINTABS]

>[!TAB Marca de tiempo solicitada]

Si seleccionó **[!UICONTROL Timestamp ordered]** como método de combinación para la directiva de combinación, la lista de conjuntos de datos de perfil incluye todos los conjuntos de datos que ha creado su organización en relación con la clase de esquema, en orden de marca de tiempo. La lista de conjuntos de datos de ExperienceEvent incluye todos los conjuntos de datos que su organización ha creado para la clase de esquema elegida y se adjuntarán a los conjuntos de datos de perfil.

La tabla **[!UICONTROL Vista previa de datos]** muestra registros de perfil de muestra basados en el orden de marca de tiempo de los conjuntos de datos. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

Seleccione **[!UICONTROL Finalizar]** para crear su nueva política de combinación.

![Se muestra la página de revisión. Esta página le permite revisar los detalles de la directiva de combinación recién creada.](../images/merge-policies/timestamp-review.png)

>[!TAB Prioridad de conjuntos de datos]

Si seleccionó **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación para la directiva de combinación, las listas de conjuntos de datos de Perfil y ExperienceEvent incluyen únicamente los conjuntos de datos de Perfil y ExperienceEvent que seleccionó durante el flujo de trabajo de creación, respectivamente. El orden de los conjuntos de datos de perfil debe coincidir con la prioridad especificada durante la creación. Si no es así, use el botón [!UICONTROL Atrás] para volver a los pasos anteriores del flujo de trabajo y ajustar la prioridad.

La tabla **[!UICONTROL Vista previa de datos]** muestra registros de perfil de muestra usando los conjuntos de datos seleccionados. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

Seleccione **[!UICONTROL Finalizar]** para crear su nueva política de combinación.

![Se muestra la página de revisión. Esta página le permite revisar los detalles de la directiva de combinación recién creada.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Editar una política de combinación {#edit}

En la ficha [!UICONTROL Políticas de combinación], puede modificar una política de combinación existente creada para la clase [!DNL XDM Individual Profile] seleccionando el **[!UICONTROL nombre de la directiva]** para la política de combinación que desee editar.

Cuando aparezca la pantalla **[!UICONTROL Editar política de combinación]**, puede realizar cambios en el nombre y en el método [!UICONTROL vinculación de ID], así como cambiar si esta política es o no la política de combinación predeterminada para su organización.

Seleccione **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo de la política de combinación y actualizar el método de combinación y los conjuntos de datos incluidos en la política de combinación.

![Se muestra el flujo de trabajo de editar política de combinación.](../images/merge-policies/edit-screen.png)

Una vez que haya realizado los cambios necesarios, revise la política de combinación y seleccione **[!UICONTROL Finalizar]** para guardar los cambios y volver a la pestaña [!UICONTROL Políticas de combinación].

>[!WARNING]
>
>Cambiar una política de combinación puede afectar a la segmentación y a los resultados del perfil, ya que alterará la forma en que se resuelven los conflictos de datos. Asegúrese de revisar cuidadosamente los cambios realizados en las políticas de combinación antes de guardarlas.

![Se muestra la página de revisión del flujo de trabajo de la directiva de edición.](../images/merge-policies/edit-review.png)

## Infracciones de directiva de gobernanza de datos

Al crear o actualizar una política de combinación, se realiza una comprobación para determinar si la política de combinación infringe alguna de las políticas de uso de datos definidas por su organización. Las políticas de uso de datos forman parte de Adobe Experience Platform Data Governance y son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en datos específicos de [!DNL Experience Platform].

Por ejemplo, si se ha utilizado una política de combinación para crear una audiencia que se activó en un destino de terceros y su organización tenía una política de uso de datos que impedía la exportación de datos específicos a terceros, recibirá una **[!UICONTROL notificación de infracción de la política de gobernanza de datos detectada]** al intentar guardar la política de combinación.

Esta notificación incluye una lista de las políticas de uso de datos que se han violado y le permite ver los detalles de la violación seleccionando una política de la lista. Al seleccionar una directiva infringida, la pestaña **[!UICONTROL Linaje de datos]** proporciona el motivo de la infracción y las activaciones afectadas, y cada una proporciona más detalles sobre cómo se ha violado la directiva de uso de datos.

Para obtener más información sobre el rendimiento del control de datos en Adobe Experience Platform, lea la [Información general sobre el control de datos](../../data-governance/home.md).

## Pasos siguientes

Ahora que ha creado y configurado políticas de combinación para su organización, puede utilizarlas para ajustar la vista de los perfiles de los clientes en Experience Platform y para crear audiencias a partir de los datos del perfil. Consulte la [descripción general de la segmentación](../../segmentation/home.md) para obtener más información sobre cómo crear y trabajar con audiencias mediante la IU y las API de [!DNL Experience Platform].
