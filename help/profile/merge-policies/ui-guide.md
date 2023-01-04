---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;políticas de combinación;interfaz de usuario;interfaz de usuario;marca de tiempo solicitada;prioridad del conjunto de datos
title: Guía de la interfaz de usuario de políticas de combinación
type: Documentation
description: Al unir datos de varias fuentes en Experience Platform, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# Guía de la interfaz de usuario de políticas de combinación

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.

Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario (IU) de Adobe Experience Platform.

Para obtener más información sobre las políticas de combinación y su función en el Experience Platform, comience leyendo el [información general sobre políticas de combinación](overview.md).

## Primeros pasos

Esta guía requiere una comprensión práctica de varias [!DNL Experience Platform] características. Antes de seguir esta guía, consulte la documentación de los siguientes servicios:

* [Perfil del cliente en tiempo real](../home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Habilita el perfil del cliente en tiempo real al unir identidades de fuentes de datos dispares que se están incorporando en [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

## Ver directivas de combinación {#view-merge-policies}

Dentro de [!DNL Experience Platform] IU, puede empezar a trabajar con políticas de combinación seleccionando **[!UICONTROL Perfiles]** en el panel de navegación izquierdo y, a continuación, seleccione la **[!UICONTROL Combinar directivas]** pestaña . Esta ficha incluye una lista de todas las directivas de combinación existentes para su organización, así como detalles para cada directiva de combinación, incluido el nombre de la directiva, si la directiva de combinación es la directiva de combinación predeterminada y la clase de esquema a la que se relaciona la directiva de combinación.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/landing.png)

Para seleccionar qué detalles son visibles o para añadir columnas adicionales a la visualización, seleccione **[!UICONTROL Configurar columnas]** y haga clic en el nombre de una columna para agregarla o quitarla de la vista.

![](../images/merge-policies/adjust-view.png)

## Crear una directiva de combinación {#create-a-merge-policy}

Para crear una nueva directiva de combinación, seleccione **[!UICONTROL Crear directiva de combinación]** en la pestaña políticas de combinación para introducir el nuevo flujo de trabajo de directivas de combinación.

![Combinar la página de aterrizaje de directivas con el botón crear resaltado.](../images/merge-policies/create-new.png)

La variable **[!UICONTROL Nueva directiva de combinación]** flujo de trabajo, requiere que proporcione información importante para la nueva política de combinación mediante una serie de pasos guiados. Estos pasos se describen en las secciones siguientes.

![El nuevo flujo de trabajo de la política de combinación.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

El primer paso del flujo de trabajo le permite configurar la política de combinación proporcionando información básica. Esta información incluye:

* **[!UICONTROL Nombre]**: El nombre de la directiva de combinación debe ser descriptivo pero conciso.
* **[!UICONTROL Clase Schema]**: La clase de esquema XDM asociada a la directiva de combinación. Esto especifica la clase de esquema para la que se crea esta política de combinación. Las organizaciones pueden crear varias directivas de combinación por clase de esquema. Actualmente solo el [!UICONTROL Perfil individual XDM] La clase está disponible en la interfaz de usuario de . Puede obtener una vista previa del esquema de unión para la clase schema seleccionando **[!UICONTROL Ver esquema de unión]**. Para obtener más información, consulte la sección sobre [visualización del esquema de unión](#view-union-schema) esto sigue.
* **[!UICONTROL Vinculación de ID]**: Este campo define cómo determinar las identidades relacionadas de un cliente. Existen dos valores posibles para la vinculación de identidad y es importante comprender cómo afectará a los datos el tipo de vinculación de identidad que seleccione. Para obtener más información, consulte la [información general sobre políticas de combinación](overview.md).
   * **[!UICONTROL Ninguna]**: No realice ninguna vinculación de identidad.
   * **[!UICONTROL Gráfico privado]**: Realice la vinculación de identidad en función del gráfico de identidad privada.
* **[!UICONTROL Política de combinación predeterminada]**: Botón de alternancia que le permite seleccionar si esta directiva de combinación será o no la predeterminada para su organización. Si el selector está activado, aparece una advertencia que le solicita que confirme que desea cambiar la directiva de combinación predeterminada de su organización. Consulte la [información general sobre políticas de combinación](overview.md) para obtener más información sobre las directivas de combinación predeterminadas.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Política de combinación activa/perimetral]**: Botón de alternancia que permite seleccionar si esta directiva de combinación estará activa o no en Edge. Para garantizar que todos los consumidores de perfil trabajen con la misma vista en los bordes, las políticas de combinación se pueden marcar como activas en el borde. Para que un segmento se active en el perímetro (marcado como segmento perimetral), debe estar vinculado a una política de fusión que esté marcada como activo en el borde. Si un segmento es **not** vinculado a una política de combinación marcada como activa en Edge, el segmento no se marcará como activo en Edge y se marcará como segmento de flujo continuo. Además, cada simulador de pruebas de una organización solo puede tener **one** directiva de combinación activa en edge.

Una vez completados los campos obligatorios, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo.

![Una pantalla de configuración completa con el botón Siguiente resaltado.](../images/merge-policies/create-complete.png)

## [!UICONTROL Ver esquema de unión] {#view-union-schema}

Al crear o editar una directiva de combinación, puede ver el esquema de unión de la clase de esquema elegida seleccionando **[!UICONTROL Ver esquema de unión]**.

![](../images/merge-policies/view-union-schema.png)

Esto abre el [!UICONTROL Ver esquema de unión] , mostrando todos los esquemas de contribución, identidades y relaciones asociadas con el esquema de unión. Puede utilizar el cuadro de diálogo para explorar el esquema de unión del mismo modo que haría al acceder al [!UICONTROL Esquema de unión] en la ficha [!UICONTROL Perfiles] de la interfaz de usuario de Platform.

Para obtener información detallada sobre los esquemas de unión, incluido cómo interactuar con ellos en la variable [!UICONTROL Esquema de unión] o [!UICONTROL Ver esquema de unión] cuadro de diálogo que se muestra en el flujo de trabajo de políticas de combinación, visite [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleccionar conjuntos de datos de perfil] {#select-profile-datasets}

En el **[!UICONTROL Seleccionar conjuntos de datos de perfil]** , debe seleccionar **[!UICONTROL Método Merge]** que desea utilizar para la directiva de combinación. También se muestra en la pantalla el número total de [!UICONTROL Conjuntos de datos de perfil] en su organización que se relaciona con la clase de esquema seleccionada en la pantalla anterior.

Según el método de combinación que elija, todos los conjuntos de datos de perfil se combinarán en el orden en que se actualizaron por última vez (con marca de tiempo solicitada) o tendrá que seleccionar qué conjuntos de datos de perfil incluir en la política de combinación y el orden en que se fusionarán (prioridad del conjunto de datos).

Para obtener más información sobre los métodos de combinación, consulte la [información general sobre políticas de combinación](overview.md).

### Marca de tiempo solicitada {#timestamp-ordered-profile}

Selección **[!UICONTROL Marca de tiempo solicitada]** como método de combinación significa que los atributos de los conjuntos de datos actualizados más recientemente tendrán prioridad. Esto se aplica a todos los conjuntos de datos de perfil.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen mostrada) muestra el número total de conjuntos de datos de perfil que se incluirán.

![](../images/merge-policies/timestamp-ordered.png)

### Prioridad del conjunto de datos {#dataset-precedence-profile}

Selección **[!UICONTROL Prioridad del conjunto de datos]** como el método de combinación requiere que seleccione conjuntos de datos de perfil y que los priorice manualmente. Cada conjunto de datos enumerado también incluye el estado del último lote ingestado o muestra un aviso de que no se han introducido lotes en ese conjunto de datos.

Puede seleccionar hasta 50 conjuntos de datos de la lista de conjuntos de datos para incluirlos en la directiva de combinación.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen mostrada) muestra el número total de conjuntos de datos de perfil disponibles para su selección.

A medida que se seleccionan los conjuntos de datos, se añaden al **[!UICONTROL Seleccionar conjuntos de datos]** , lo que le permite arrastrar y soltar los conjuntos de datos y ordenarlos según su prioridad deseada. Como los conjuntos de datos se ajustan en la lista, el ordinal (1, 2, 3, etc.) situado junto al conjunto de datos se actualizará y mostrará la prioridad (1 teniendo en cuenta la prioridad más alta, luego 2, y después).

Al seleccionar un conjunto de datos también se actualiza la variable **[!UICONTROL Esquema de unión]** , que muestra los campos del esquema de unión en los que contribuye cada conjunto de datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Seleccionar conjuntos de datos de ExperienceEvent] {#select-experienceevent-datasets}

El siguiente paso del flujo de trabajo requiere que seleccione conjuntos de datos de ExperienceEvent . Esta pantalla está influenciada por el método de combinación seleccionado en la [[!UICONTROL Seleccionar conjuntos de datos de perfil]](#select-profile-datasets) en el Navegador.

### Marca de tiempo solicitada {#timestamp-ordered-experienceevent}

Si ha seleccionado **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para conjuntos de datos de perfil, los atributos de los conjuntos de datos de ExperienceEvent actualizados más recientemente también tendrán prioridad aquí.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen mostrada) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización que están relacionados con la clase de esquema seleccionada en la pantalla de configuración de la directiva de combinación.

![](../images/merge-policies/timestamp-experienceevent.png)

### Prioridad del conjunto de datos {#dataset-precedence-experienceevent}

Si ha seleccionado **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación para conjuntos de datos de perfil, deberá seleccionar conjuntos de datos de ExperienceEvent para incluirlos. Puede seleccionar hasta 50 conjuntos de datos de ExperienceEvent de la lista de conjuntos de datos.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen mostrada) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización que están relacionados con la clase de esquema seleccionada en la pantalla de configuración de la directiva de combinación.

A medida que se seleccionan los conjuntos de datos, aparecen en la variable [!UICONTROL Seleccionar conjuntos de datos] para obtener más información.

Los conjuntos de datos de ExperienceEvent no se pueden ordenar manualmente, sino que los atributos de los conjuntos de datos de ExperienceEvent se anexan a los conjuntos de datos de perfil si forman parte del mismo fragmento de perfil.

De forma similar a seleccionar conjuntos de datos de perfil, al seleccionar un conjunto de datos de ExperienceEvent también se actualiza la variable **[!UICONTROL Esquema de unión]** , que muestra los campos del esquema de unión en los que contribuye cada conjunto de datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Revisión] {#review}

El último paso del flujo de trabajo es revisar la política de combinación. La variable **[!UICONTROL Consulte]** la pantalla muestra información sobre la directiva de combinación, incluido el método de vinculación de ID seleccionado, el método de combinación seleccionado y los conjuntos de datos incluidos. (Para ver todos los conjuntos de datos de Perfil o ExperienceEvent incluidos, seleccione el número de conjuntos de datos que desea expandir en la lista desplegable).

También se incluye en la pantalla de revisión el **[!UICONTROL Vista previa de datos]** tabla que muestra registros de perfil de ejemplo utilizando la directiva de combinación. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

Asegúrese de revisar la configuración de la directiva de combinación y obtener una vista previa de los datos con cuidado antes de seleccionar **[!UICONTROL Finalizar]** para completar el flujo de trabajo de creación.

### Marca de tiempo solicitada {#timestamp-ordered-review}

Si ha seleccionado **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para la política de combinación, la lista de conjuntos de datos de perfil incluye todos los conjuntos de datos que su organización ha creado relacionados con la clase de esquema, en orden de marca de tiempo. La lista de conjuntos de datos de ExperienceEvent incluye todos los conjuntos de datos que su organización ha creado para la clase de esquema elegida y se adjuntarán a los conjuntos de datos de perfil.

La variable **[!UICONTROL Vista previa de datos]** la tabla muestra registros de perfil de ejemplo basados en un orden de marca de tiempo de los conjuntos de datos. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

![](../images/merge-policies/timestamp-review.png)

### Prioridad del conjunto de datos {#dataset-precedence-review}

Si ha seleccionado **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación para la política de combinación, las listas de conjuntos de datos de Profile y ExperienceEvent incluyen solo los conjuntos de datos de Profile y ExperienceEvent que seleccionó durante el flujo de trabajo de creación, respectivamente. El orden de los conjuntos de datos de perfil debe coincidir con la prioridad especificada durante la creación. Si no es así, use el [!UICONTROL Atrás] para volver a los pasos anteriores del flujo de trabajo y ajustar la prioridad.

La variable **[!UICONTROL Vista previa de datos]** la tabla muestra registros de perfil de ejemplo utilizando los conjuntos de datos seleccionados. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista actualizada de directivas de combinación {#updated-list}

Después de completar el flujo de trabajo para crear una nueva política de combinación, volverá a la **[!UICONTROL Combinar directivas]** pestaña . La lista de directivas de combinación para su organización debe incluir ahora la directiva de combinación que acaba de crear.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar una directiva de combinación

En el [!UICONTROL Combinar directivas] , puede modificar una política de combinación existente creada para la [!DNL XDM Individual Profile] seleccionando la **[!UICONTROL Nombre de la directiva]** para la política de combinación que desee editar.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/select-edit.png)

Cuando la variable **[!UICONTROL Editar directiva de combinación]** , puede realizar cambios en el nombre y [!UICONTROL Vinculación de ID] , así como cambiar si esta directiva es o no la directiva de combinación predeterminada para su organización.

Select **[!UICONTROL Siguiente]** para continuar a través del flujo de trabajo de la directiva de combinación para actualizar el método de combinación y los conjuntos de datos incluidos en la directiva de combinación.

![](../images/merge-policies/edit-screen.png)

Una vez que haya realizado los cambios necesarios, revise la directiva de combinación y seleccione **[!UICONTROL Finalizar]** para guardar los cambios y volver a la [!UICONTROL Combinar directivas] pestaña .

>[!WARNING]
>
>Cambiar una política de combinación puede afectar a la segmentación y a los resultados de perfil, ya que alterará la forma en que se resuelven los conflictos de datos. Asegúrese de revisar cuidadosamente los cambios en las directivas de combinación antes de guardarlos.

![](../images/merge-policies/edit-review.png)

## Infracción de la política de control de datos

Al crear o actualizar una directiva de combinación, se realiza una comprobación para determinar si la directiva de combinación infringe alguna de las políticas de uso de datos definidas por su organización. Las políticas de uso de datos forman parte de la Administración de datos de Adobe Experience Platform y son reglas que describen los tipos de acciones de marketing que puede realizar, o de las que se le restringe, en relación con determinadas [!DNL Platform] datos. Por ejemplo, si se utilizara una directiva de combinación para crear un segmento que se activara en un destino de terceros y su organización tuviera una directiva de uso de datos que impidiera la exportación de datos específicos a terceros, recibirá una **[!UICONTROL Se ha detectado una violación de la política de control de datos]** al intentar guardar la directiva de combinación.

Esta notificación incluye una lista de las políticas de uso de datos que se han infringido y le permite ver los detalles de la infracción seleccionando una directiva en la lista. Al seleccionar una directiva violada, la variable **[!UICONTROL Línea de datos]** proporciona el motivo de la infracción y las activaciones afectadas, cada una de las cuales proporciona más detalles sobre cómo se ha violado la política de uso de datos.

Para obtener más información sobre cómo se realiza el control de datos en Adobe Experience Platform, lea la [Información general sobre la administración de datos](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Pasos siguientes

Ahora que ha creado y configurado directivas de combinación para su organización, puede utilizarlas para ajustar la vista de los perfiles de cliente dentro de Platform y para crear segmentos de audiencia a partir de los datos de perfil. Consulte la [información general sobre segmentación](../../segmentation/home.md) para obtener más información sobre cómo crear y trabajar con segmentos mediante la variable [!DNL Experience Platform] IU y API.
