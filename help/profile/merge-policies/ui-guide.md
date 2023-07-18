---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;políticas de combinación;IU;interfaz de usuario;marca de tiempo ordenada;prioridad de conjuntos de datos
title: Guía de IU de políticas de combinación
type: Documentation
description: Al unir datos de varias fuentes en Experience Platform, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada. Esta guía proporciona instrucciones paso a paso para trabajar con directivas de combinación mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2320'
ht-degree: 0%

---


# Guía de IU de políticas de combinación

Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.

Mediante las API de RESTful o la interfaz de usuario de, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con directivas de combinación mediante la interfaz de usuario (IU) de Adobe Experience Platform.

Para obtener más información sobre las políticas de combinación y su función dentro de Experience Platform, comience por leer la [resumen de políticas de combinación](overview.md).

## Primeros pasos

Esta guía requiere una comprensión práctica de varios aspectos importantes [!DNL Experience Platform] funciones. Antes de seguir esta guía, revise la documentación de los siguientes servicios:

* [Perfil del cliente en tiempo real](../home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Habilita el Perfil del cliente en tiempo real al unir identidades de fuentes de datos dispares a [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

## Ver políticas de combinación {#view-merge-policies}

Dentro de [!DNL Experience Platform] IU, puede empezar a trabajar con las políticas de combinación seleccionando **[!UICONTROL Perfiles]** en la navegación izquierda y, a continuación, seleccione la opción **[!UICONTROL Políticas de combinación]** pestaña. Esta pestaña incluye una lista de todas las políticas de combinación existentes para su organización, así como detalles para cada política de combinación, incluido el nombre de la política, si la política de combinación es o no la política de combinación predeterminada y la clase de esquema con la que se relaciona la política de combinación.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/landing.png)

Para seleccionar qué detalles están visibles o para agregar columnas adicionales a la visualización, seleccione **[!UICONTROL Configuración de columnas]** y haga clic en el nombre de una columna para añadirla o quitarla de la vista.

![](../images/merge-policies/adjust-view.png)

## Crear una política de combinación {#create-a-merge-policy}

Para crear una nueva política de combinación, seleccione **[!UICONTROL Crear política de combinación]** en la pestaña políticas de combinación para introducir el nuevo flujo de trabajo de políticas de combinación.

![Página de aterrizaje de políticas de combinación con el botón Crear resaltado.](../images/merge-policies/create-new.png)

El **[!UICONTROL Nueva política de combinación]** El flujo de trabajo de requiere que proporcione información importante para la nueva política de combinación a través de una serie de pasos guiados. Estos pasos se describen en las secciones siguientes.

![El nuevo flujo de trabajo de políticas de combinación.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

El primer paso del flujo de trabajo le permite configurar la política de combinación proporcionando información básica. Esta información incluye:

* **[!UICONTROL Nombre]**: el nombre de la política de combinación debe ser descriptivo pero conciso.
* **[!UICONTROL Clase de esquema]**: la clase de esquema XDM asociada a la política de combinación. Especifica la clase de esquema para la que se crea esta política de combinación. Las organizaciones pueden crear varias políticas de combinación por clase de esquema. Actualmente solo el [!UICONTROL Perfil individual de XDM] está disponible en la interfaz de usuario de. Puede obtener una vista previa del esquema de unión para la clase de esquema seleccionando **[!UICONTROL Ver esquema de unión]**. Para obtener más información, consulte la sección sobre [visualización del esquema de unión](#view-union-schema) que sigue.
* **[!UICONTROL Vinculación de ID]**: Este campo define cómo determinar las identidades relacionadas de un cliente. Existen dos valores posibles para la vinculación de identidad y es importante comprender cómo afectará a los datos el tipo de vinculación de identidad que seleccione. Para obtener más información, consulte la [resumen de políticas de combinación](overview.md).
   * **[!UICONTROL Ninguno]**: no realice ninguna vinculación de identidad.
   * **[!UICONTROL Gráfico privado]**: realice la vinculación de identidad en función del gráfico de identidad privado.
* **[!UICONTROL Política de combinación predeterminada]**: Botón de alternancia que le permite seleccionar si esta política de combinación será o no la predeterminada para su organización. Si el selector está activado, aparece una advertencia que le solicita que confirme que desea cambiar la política de combinación predeterminada de su organización. Consulte la [resumen de políticas de combinación](overview.md) para obtener más información sobre las políticas de combinación predeterminadas.
  ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Política de combinación activa en Edge]**: Botón de alternancia que le permite seleccionar si esta política de combinación estará activa o no en Edge. Para garantizar que todos los consumidores de perfiles trabajen con la misma vista en los bordes, las políticas de combinación se pueden marcar como activas en el borde. Para que una audiencia se active en Edge (marcada como audiencia Edge), debe estar vinculada a una política de combinación marcada como activa en Edge. Si una audiencia es **no** ligada a una política de combinación marcada como activa en edge, la audiencia no se marca como activa en edge y se marca como audiencia de flujo continuo. Además, cada zona protegida de una organización solo puede tener **uno** política de combinación activa en edge.

Una vez completados los campos obligatorios, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo.

![Una pantalla de configuración completa con el botón Siguiente resaltado.](../images/merge-policies/create-complete.png)

## [!UICONTROL Ver esquema de unión] {#view-union-schema}

Al crear o editar una política de combinación, puede ver el esquema de unión de la clase de esquema elegida seleccionando **[!UICONTROL Ver esquema de unión]**.

![](../images/merge-policies/view-union-schema.png)

Esto abre el [!UICONTROL Ver esquema de unión] , mostrando todos los esquemas, identidades y relaciones asociados con el esquema de unión. Puede utilizar el cuadro de diálogo para explorar el esquema de unión de la misma manera que lo haría accediendo al [!UICONTROL Esquema de unión] en la pestaña [!UICONTROL Perfiles] de la interfaz de usuario de Platform.

Para obtener información detallada sobre los esquemas de unión, incluido cómo interactuar con ellos en la [!UICONTROL Esquema de unión] o la pestaña [!UICONTROL Ver esquema de unión] que se muestra en el flujo de trabajo de las políticas de combinación, visite el [guía de IU del esquema de unión](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleccionar conjuntos de datos de perfil] {#select-profile-datasets}

En el **[!UICONTROL Seleccionar conjuntos de datos de perfil]** , debe seleccionar la opción **[!UICONTROL Método de combinación]** que desee utilizar para la política de combinación. También se muestra en la pantalla el número total de [!UICONTROL Conjuntos de datos de perfil] en su organización relacionadas con la clase de esquema seleccionada en la pantalla anterior.

Según el método de combinación que elija, todos los conjuntos de datos de perfil se combinarán en el orden en que se actualizaron por última vez (con la marca de tiempo ordenada) o tendrá que seleccionar qué conjuntos de datos de perfil incluir en la política de combinación y el orden en que combinarlos (prioridad de conjuntos de datos).

Para obtener más información sobre los métodos de combinación, consulte la [resumen de políticas de combinación](overview.md).

### Marca de tiempo solicitada {#timestamp-ordered-profile}

Seleccionar **[!UICONTROL Marca de tiempo solicitada]** ya que el método merge significa que los atributos de los conjuntos de datos actualizados más recientemente tendrán prioridad. Esto se aplica a todos los conjuntos de datos de perfil.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen que se muestra) muestra la cantidad total de conjuntos de datos de perfil que se incluirán.

![](../images/merge-policies/timestamp-ordered.png)

### Prioridad de conjuntos de datos {#dataset-precedence-profile}

Seleccionar **[!UICONTROL Prioridad de conjuntos de datos]** ya que el método de combinación requiere que seleccione Conjuntos de datos de perfil y que les dé prioridad manualmente. Cada conjunto de datos enumerado también incluye el estado del último lote introducido o muestra un aviso de que no se han introducido lotes en ese conjunto de datos.

Puede seleccionar hasta 50 conjuntos de datos de la lista de conjuntos de datos para incluirlos en la política de combinación.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen que se muestra) muestra el número total de conjuntos de datos de perfil disponibles para la selección.

A medida que se seleccionan los conjuntos de datos, se añaden a **[!UICONTROL Seleccionar conjuntos de datos]** , lo que le permite arrastrar y soltar los conjuntos de datos y ordenarlos según la prioridad que desee. A medida que los conjuntos de datos se ajustan en la lista, se actualiza el ordinal (1, 2, 3, etc.) junto al conjunto de datos, mostrando la prioridad (1 recibe la prioridad más alta, luego 2 y en adelante).

Al seleccionar un conjunto de datos, también se actualiza la **[!UICONTROL Esquema de unión]** , que muestra los campos del esquema de unión a los que cada conjunto de datos aporta datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte [guía de IU del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Seleccionar conjuntos de datos de ExperienceEvent] {#select-experienceevent-datasets}

El siguiente paso del flujo de trabajo requiere que seleccione conjuntos de datos de ExperienceEvent. En esta pantalla influye el método de combinación seleccionado en la [[!UICONTROL Seleccionar conjuntos de datos de perfil]](#select-profile-datasets) pantalla.

### Marca de tiempo solicitada {#timestamp-ordered-experienceevent}

Si ha seleccionado **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para conjuntos de datos de perfil, los atributos de los conjuntos de datos de ExperienceEvent actualizados más recientemente también tendrán prioridad aquí.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen que se muestra) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización relacionados con la clase de esquema seleccionada en la pantalla de configuración de la política de combinación.

![](../images/merge-policies/timestamp-experienceevent.png)

### Prioridad de conjuntos de datos {#dataset-precedence-experienceevent}

Si ha seleccionado **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación para conjuntos de datos de perfil, deberá seleccionar conjuntos de datos de ExperienceEvent para incluir. Puede seleccionar hasta 50 conjuntos de datos de ExperienceEvent en la lista de conjuntos de datos.

>[!NOTE]
>
>El número entre corchetes junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen que se muestra) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización relacionados con la clase de esquema seleccionada en la pantalla de configuración de la política de combinación.

Cuando se seleccionan conjuntos de datos, aparecen en el [!UICONTROL Seleccionar conjuntos de datos] sección.

Los conjuntos de datos de ExperienceEvent no se pueden ordenar manualmente; en su lugar, los atributos de los conjuntos de datos de ExperienceEvent se anexan a los conjuntos de datos de perfil si forman parte del mismo fragmento de perfil.

Al igual que seleccionar Conjuntos de datos de perfil, al seleccionar un conjunto de datos de ExperienceEvent también se actualiza la variable **[!UICONTROL Esquema de unión]** , que muestra los campos del esquema de unión a los que cada conjunto de datos aporta datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte [guía de IU del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Consulte] {#review}

El paso final del flujo de trabajo es revisar la política de combinación. El **[!UICONTROL Revisar]** Esta pantalla muestra información sobre la política de combinación, incluido el método de vinculación de ID seleccionado, el método de combinación seleccionado y los conjuntos de datos incluidos. (Para ver todos los conjuntos de datos de perfil o ExperienceEvent incluidos, seleccione el número de conjuntos de datos para expandir la lista desplegable).

También se incluye en la pantalla de revisión el **[!UICONTROL Previsualizar datos]** tabla que muestra registros de perfil de muestra mediante la política de combinación. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

Revise detenidamente la configuración de la política de combinación y previsualice los datos antes de seleccionar **[!UICONTROL Finalizar]** para completar el flujo de trabajo de creación.

### Marca de tiempo solicitada {#timestamp-ordered-review}

Si ha seleccionado **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para la política de combinación, la lista de conjuntos de datos de perfil incluye todos los conjuntos de datos que ha creado su organización en relación con la clase de esquema, en orden de marca de tiempo. La lista de conjuntos de datos de ExperienceEvent incluye todos los conjuntos de datos que su organización ha creado para la clase de esquema elegida y se adjuntarán a los conjuntos de datos de perfil.

El **[!UICONTROL Previsualizar datos]** La tabla muestra registros de perfil de muestra basados en un orden de marca de tiempo de los conjuntos de datos. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

![](../images/merge-policies/timestamp-review.png)

### Prioridad de conjuntos de datos {#dataset-precedence-review}

Si ha seleccionado **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación para la política de combinación, las listas de conjuntos de datos Profile y ExperienceEvent incluyen únicamente los conjuntos de datos Profile y ExperienceEvent que seleccionó durante el flujo de trabajo de creación, respectivamente. El orden de los conjuntos de datos de perfil debe coincidir con la prioridad especificada durante la creación. Si no es así, utilice el [!UICONTROL Atrás] para volver a los pasos anteriores del flujo de trabajo y ajustar la prioridad.

El **[!UICONTROL Previsualizar datos]** La tabla muestra registros de perfil de muestra que utilizan los conjuntos de datos seleccionados. Esto le permite obtener una vista previa del aspecto de un perfil de cliente antes de guardar la política de combinación.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista actualizada de políticas de combinación {#updated-list}

Después de completar el flujo de trabajo para crear una nueva política de combinación, vuelve al **[!UICONTROL Políticas de combinación]** pestaña. La lista de políticas de combinación para su organización debe incluir ahora la política de combinación que acaba de crear.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar una política de combinación

Desde el [!UICONTROL Políticas de combinación] , puede modificar una política de combinación existente creada para la [!DNL XDM Individual Profile] Seleccione la clase seleccionando la **[!UICONTROL Nombre de política]** para la política de combinación que desea editar.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/select-edit.png)

Si la variable **[!UICONTROL Editar política de combinación]** , puede realizar cambios en el nombre y en el [!UICONTROL Vinculación de ID] , así como cambiar si esta política es o no la política de combinación predeterminada para su organización.

Seleccionar **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo de la política de combinación y actualizar el método de combinación y los conjuntos de datos incluidos en la política de combinación.

![](../images/merge-policies/edit-screen.png)

Cuando haya realizado los cambios necesarios, revise la política de combinación y seleccione **[!UICONTROL Finalizar]** para guardar los cambios y volver al [!UICONTROL Políticas de combinación] pestaña.

>[!WARNING]
>
>Cambiar una política de combinación puede afectar a la segmentación y a los resultados del perfil, ya que alterará la forma en que se resuelven los conflictos de datos. Asegúrese de revisar cuidadosamente los cambios realizados en las políticas de combinación antes de guardarlas.

![](../images/merge-policies/edit-review.png)

## Infracciones de directiva de gobernanza de datos

Al crear o actualizar una política de combinación, se realiza una comprobación para determinar si la política de combinación infringe alguna de las políticas de uso de datos definidas por su organización. Las políticas de uso de datos forman parte de la gobernanza de datos de Adobe Experience Platform y son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en determinadas acciones [!DNL Platform] datos. Por ejemplo, si se utilizara una política de combinación para crear una audiencia que se activara en un destino de terceros y su organización tuviera una política de uso de datos que impidiera la exportación de datos específicos a terceros, usted recibiría un **[!UICONTROL Infracción de directiva de gobernanza de datos detectada]** al intentar guardar la política de combinación.

Esta notificación incluye una lista de las políticas de uso de datos que se han violado y le permite ver los detalles de la violación seleccionando una política de la lista. Al seleccionar una directiva infringida, la variable **[!UICONTROL Linaje de datos]** proporciona el motivo de la infracción y las activaciones afectadas, cada una de las cuales proporciona más detalles sobre cómo se ha infringido la política de uso de datos.

Para obtener más información sobre el rendimiento del control de datos en Adobe Experience Platform, comience por leer el [Resumen de gobernanza de datos](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Pasos siguientes

Ahora que ha creado y configurado políticas de combinación para su organización, puede utilizarlas para ajustar la vista de los perfiles de los clientes dentro de Platform y para crear audiencias a partir de los datos del perfil. Consulte la [resumen de segmentación](../../segmentation/home.md) para obtener más información sobre cómo crear y trabajar con audiencias con [!DNL Experience Platform] IU y API.
