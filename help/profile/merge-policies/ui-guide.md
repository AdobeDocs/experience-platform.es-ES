---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;políticas de combinación;interfaz de usuario;interfaz de usuario;marca de tiempo solicitada;prioridad del conjunto de datos
title: Guía de la interfaz de usuario de políticas de combinación
type: Documentation
description: Al unir datos de varias fuentes en Experience Platform, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: a6a49b4cf9c89b5c6b4679f36daede93590ffb3c
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 0%

---


# Guía de la interfaz de usuario de políticas de combinación

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.

Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario (IU) de Adobe Experience Platform.

Para obtener más información sobre las políticas de combinación y su función en el Experience Platform, lea en primer lugar la [información general sobre las políticas de combinación](overview.md).

## Primeros pasos

Esta guía requiere una comprensión práctica de varias funciones [!DNL Experience Platform] importantes. Antes de seguir esta guía, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Habilita el perfil del cliente en tiempo real al unir identidades de fuentes de datos dispares que se están incorporando en  [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

## Ver directivas de combinación {#view-merge-policies}

En la interfaz de usuario de [!DNL Experience Platform], puede empezar a trabajar con políticas de combinación seleccionando **[!UICONTROL Perfiles]** en la navegación izquierda y luego seleccionando la pestaña **[!UICONTROL Políticas de combinación]**. Esta ficha incluye una lista de todas las directivas de combinación existentes para su organización, así como detalles para cada directiva de combinación, incluido el nombre de la directiva, si la directiva de combinación es la directiva de combinación predeterminada y la clase de esquema a la que se relaciona la directiva de combinación.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/landing.png)

Para seleccionar qué detalles están visibles o para agregar columnas adicionales a la pantalla, seleccione **[!UICONTROL Configurar columnas]** y haga clic en el nombre de una columna para agregarla o quitarla de la vista.

![](../images/merge-policies/adjust-view.png)

## Crear una directiva de combinación {#create-a-merge-policy}

Para crear una nueva directiva de combinación, seleccione **[!UICONTROL Create merge policy]** en la pestaña políticas de combinación para entrar en el nuevo flujo de trabajo de políticas de combinación.

![Combinar la página de aterrizaje de directivas con el botón crear resaltado.](../images/merge-policies/create-new.png)

El flujo de trabajo **[!UICONTROL New merge policy]** requiere que proporcione información importante para la nueva política de combinación mediante una serie de pasos guiados. Estos pasos se describen en las secciones siguientes.

![El nuevo flujo de trabajo de la política de combinación.](../images/merge-policies/create.png)

## [!UICONTROL Configurar] {#configure}

El primer paso del flujo de trabajo le permite configurar la política de combinación proporcionando información básica. Esta información incluye:

* **[!UICONTROL Nombre]**: El nombre de la directiva de combinación debe ser descriptivo pero conciso.
* **[!UICONTROL Clase]** de esquema: La clase de esquema XDM asociada a la directiva de combinación. Esto especifica la clase de esquema para la que se crea esta política de combinación. Las organizaciones pueden crear varias directivas de combinación por clase de esquema. Actualmente solo la clase [!UICONTROL XDM Individual Profile] está disponible en la interfaz de usuario. Puede obtener una vista previa del esquema de unión para la clase de esquema seleccionando **[!UICONTROL View Union Schema]**. Para obtener más información, consulte la sección [visualización del esquema de unión](#view-union-schema) que se muestra a continuación.
* **[!UICONTROL Vinculación de ID]**: Este campo define cómo determinar las identidades relacionadas de un cliente. Existen dos valores posibles para la vinculación de identidad y es importante comprender cómo afectará a los datos el tipo de vinculación de identidad que seleccione. Para obtener más información, consulte [merge policy overview](overview.md).
   * **[!UICONTROL Ninguno]**: No realice ninguna vinculación de identidad.
   * **[!UICONTROL Gráfico]** privado: Realice la vinculación de identidad en función del gráfico de identidad privada.
* **[!UICONTROL Política]** de combinación predeterminada: Botón de alternancia que le permite seleccionar si esta directiva de combinación será o no la predeterminada para su organización. Si el selector está activado, aparece una advertencia que le solicita que confirme que desea cambiar la directiva de combinación predeterminada de su organización. Consulte la [información general de las directivas de combinación](overview.md) para obtener más información sobre las directivas de combinación predeterminadas.
   ![](../images/merge-policies/create-make-default.png)

Una vez completados los campos obligatorios, puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo.

![Una pantalla de configuración completa con el botón Siguiente resaltado.](../images/merge-policies/create-complete.png)

## [!UICONTROL Ver esquema de unión] {#view-union-schema}

Al crear o editar una directiva de combinación, puede ver el esquema de unión para la clase de esquema elegida seleccionando **[!UICONTROL View Union Schema]**.

![](../images/merge-policies/view-union-schema.png)

Se abrirá el cuadro de diálogo [!UICONTROL Ver esquema de unión], que muestra todos los esquemas de contribución, identidades y relaciones asociadas con el esquema de unión. Puede utilizar el cuadro de diálogo para explorar el esquema de unión del mismo modo que lo haría al acceder a la pestaña [!UICONTROL Union Schema] en la sección [!UICONTROL Profiles] de la interfaz de usuario de Platform.

Para obtener información detallada sobre los esquemas de unión, incluido cómo interactuar con ellos en la pestaña [!UICONTROL Union Schema] o en el cuadro de diálogo [!UICONTROL View Union Schema] que se muestra en el flujo de trabajo de políticas de combinación, visite la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleccionar conjuntos de datos de perfil] {#select-profile-datasets}

En la pantalla **[!UICONTROL Seleccionar conjuntos de datos de perfil]**, debe seleccionar el **[!UICONTROL Método de combinación]** que desea utilizar para la política de combinación. También se muestra en la pantalla el número total de [!UICONTROL Conjuntos de datos de perfil] en su organización que están relacionados con la clase de esquema seleccionada en la pantalla anterior.

Según el método de combinación que elija, todos los conjuntos de datos de perfil se combinarán en el orden en que se actualizaron por última vez (con marca de tiempo solicitada) o tendrá que seleccionar qué conjuntos de datos de perfil incluir en la política de combinación y el orden en que se fusionarán (prioridad del conjunto de datos).

Para obtener más información sobre los métodos de combinación, consulte [merge policy overview](overview.md).

### Marca de tiempo solicitada {#timestamp-ordered-profile}

Seleccionar **[!UICONTROL Marca de tiempo solicitada]** como método de combinación significa que los atributos de los conjuntos de datos actualizados más recientemente tendrán prioridad. Esto se aplica a todos los conjuntos de datos de perfil.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen mostrada) muestra el número total de conjuntos de datos de perfil que se incluirán.

![](../images/merge-policies/timestamp-ordered.png)

### Prioridad del conjunto de datos {#dataset-precedence-profile}

Si selecciona **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación, es necesario seleccionar conjuntos de datos de perfil y priorizarlos manualmente. Cada conjunto de datos enumerado también incluye el estado del último lote ingestado o muestra un aviso de que no se han introducido lotes en ese conjunto de datos.

Puede seleccionar hasta 50 conjuntos de datos de la lista de conjuntos de datos para incluirlos en la directiva de combinación.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de perfil]** (por ejemplo, `(37)` en la imagen mostrada) muestra el número total de conjuntos de datos de perfil disponibles para su selección.

A medida que se seleccionan los conjuntos de datos, estos se añaden a la sección **[!UICONTROL Select datasets]** , lo que permite arrastrar y soltar los conjuntos de datos y ordenarlos según la prioridad que desee. Como los conjuntos de datos se ajustan en la lista, el ordinal (1, 2, 3, etc.) situado junto al conjunto de datos se actualizará y mostrará la prioridad (1 teniendo en cuenta la prioridad más alta, luego 2, y después).

Al seleccionar un conjunto de datos, también se actualiza la sección **[!UICONTROL Union schema]**, que muestra los campos del esquema de unión en los que cada conjunto de datos contribuye con los datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Seleccionar conjuntos de datos de ExperienceEvent] {#select-experienceevent-datasets}

El siguiente paso del flujo de trabajo requiere que seleccione conjuntos de datos de ExperienceEvent . Esta pantalla está influenciada por el método de combinación que seleccionó en la pantalla [[!UICONTROL Seleccionar conjuntos de datos de perfil]](#select-profile-datasets).

### Marca de tiempo solicitada {#timestamp-ordered-experienceevent}

Si seleccionó **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para conjuntos de datos de perfil, los atributos de los conjuntos de datos de ExperienceEvent actualizados más recientemente también tendrán prioridad aquí.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen mostrada) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización que están relacionados con la clase de esquema seleccionada en la pantalla de configuración de la directiva de combinación.

![](../images/merge-policies/timestamp-experienceevent.png)

### Prioridad del conjunto de datos {#dataset-precedence-experienceevent}

Si seleccionó **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación para los conjuntos de datos de perfil, deberá seleccionar los conjuntos de datos de ExperienceEvent para incluirlos. Puede seleccionar hasta 50 conjuntos de datos de ExperienceEvent de la lista de conjuntos de datos.

>[!NOTE]
>
>El número entre corchetes situado junto a **[!UICONTROL Conjuntos de datos de ExperienceEvent]** (por ejemplo, `(20)` en la imagen mostrada) muestra el número total de conjuntos de datos de ExperienceEvent creados por su organización que están relacionados con la clase de esquema seleccionada en la pantalla de configuración de la directiva de combinación.

Como los conjuntos de datos están seleccionados, aparecen en la sección [!UICONTROL Seleccionar conjuntos de datos].

Los conjuntos de datos de ExperienceEvent no se pueden ordenar manualmente, sino que los atributos de los conjuntos de datos de ExperienceEvent se anexan a los conjuntos de datos de perfil si forman parte del mismo fragmento de perfil.

De forma similar a la selección de conjuntos de datos de perfil, al seleccionar un conjunto de datos de ExperienceEvent también se actualiza la sección **[!UICONTROL Union schema]**, que muestra los campos del esquema de unión en el que cada conjunto de datos contribuye con los datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Consulte] {#review}

El último paso del flujo de trabajo es revisar la política de combinación. La pantalla **[!UICONTROL Revisar]** muestra información sobre la política de combinación, incluido el método de vinculación de ID seleccionado, el método de combinación seleccionado y los conjuntos de datos incluidos. (Para ver todos los conjuntos de datos de Perfil o ExperienceEvent incluidos, seleccione el número de conjuntos de datos que desea expandir en la lista desplegable).

También se incluye en la pantalla de revisión la tabla **[!UICONTROL Preview data]** que muestra registros de perfil de muestra mediante la política de combinación. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

Asegúrese de revisar la configuración de la directiva de combinación y obtener una vista previa de los datos cuidadosamente antes de seleccionar **[!UICONTROL Finish]** para completar el flujo de trabajo de creación.

### Marca de tiempo solicitada {#timestamp-ordered-review}

Si seleccionó **[!UICONTROL Timestamp ordered]** como método de combinación para la política de combinación, la lista de conjuntos de datos de perfil incluye todos los conjuntos de datos creados por la organización relacionados con la clase de esquema, en orden de marca de tiempo. La lista de conjuntos de datos de ExperienceEvent incluye todos los conjuntos de datos que su organización ha creado para la clase de esquema elegida y se adjuntarán a los conjuntos de datos de perfil.

La tabla **[!UICONTROL Preview data]** muestra registros de perfil de muestra basados en un orden de marca de tiempo de los conjuntos de datos. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

![](../images/merge-policies/timestamp-review.png)

### Prioridad del conjunto de datos {#dataset-precedence-review}

Si seleccionó **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación para la política de combinación, las listas de conjuntos de datos de Perfil y ExperienceEvent incluyen solo los conjuntos de datos de Perfil y ExperienceEvent que seleccionó durante el flujo de trabajo de creación, respectivamente. El orden de los conjuntos de datos de perfil debe coincidir con la prioridad especificada durante la creación. Si no es así, utilice el botón [!UICONTROL Back] para volver a los pasos anteriores del flujo de trabajo y ajustar la prioridad.

La tabla **[!UICONTROL Preview data]** muestra registros de perfil de muestra utilizando los conjuntos de datos seleccionados. Esto le permite obtener una vista previa del aspecto de un perfil del cliente antes de guardar la directiva de combinación.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista actualizada de directivas de combinación {#updated-list}

Después de completar el flujo de trabajo para crear una nueva política de combinación, volverá a la pestaña **[!UICONTROL Políticas de combinación]**. La lista de directivas de combinación para su organización debe incluir ahora la directiva de combinación que acaba de crear.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar una directiva de combinación

Desde la pestaña [!UICONTROL Merge Policies], puede modificar una política de combinación existente creada para la clase [!DNL XDM Individual Profile] seleccionando el **[!UICONTROL Policy name]** para la política de combinación que desee editar.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/select-edit.png)

Cuando aparece la pantalla **[!UICONTROL Edit merge policy]**, puede realizar cambios en el método name y [!UICONTROL ID stitching], así como cambiar si esta directiva es o no la directiva de combinación predeterminada para su organización.

Seleccione **[!UICONTROL Next]** para continuar a través del flujo de trabajo de la directiva de combinación para actualizar el método de combinación y los conjuntos de datos incluidos en la directiva de combinación.

![](../images/merge-policies/edit-screen.png)

Una vez que haya realizado los cambios necesarios, revise la directiva de combinación y seleccione **[!UICONTROL Finish]** para guardar los cambios y volver a la pestaña [!UICONTROL Merge policy].

>[!WARNING]
>
>Cambiar una política de combinación puede afectar a la segmentación y a los resultados de perfil, ya que alterará la forma en que se resuelven los conflictos de datos. Asegúrese de revisar cuidadosamente los cambios en las directivas de combinación antes de guardarlos.

![](../images/merge-policies/edit-review.png)

## Infracción de la política de control de datos

Al crear o actualizar una directiva de combinación, se realiza una comprobación para determinar si la directiva de combinación infringe alguna de las políticas de uso de datos definidas por su organización. Las políticas de uso de datos forman parte de Adobe Experience Platform [!DNL Data Governance] y son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, con datos específicos de [!DNL Platform]. Por ejemplo, si se utilizó una directiva de combinación para crear un segmento que se activó en un destino de terceros y la organización tenía una directiva de uso de datos que impedía la exportación de datos específicos a terceros, recibiría una notificación **[!UICONTROL de infracción de directiva de control de datos detectada]** al intentar guardar la directiva de combinación.

Esta notificación incluye una lista de las políticas de uso de datos que se han infringido y le permite ver los detalles de la infracción seleccionando una directiva en la lista. Al seleccionar una directiva violada, la pestaña **[!UICONTROL Data lineage]** proporciona el motivo de la infracción y las activaciones afectadas, cada una de las cuales proporciona más detalles sobre cómo se ha violado la directiva de uso de datos.

Para obtener más información sobre cómo se realiza el control de datos dentro de Adobe Experience Platform, lea en primer lugar la [información general sobre el control de datos](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Pasos siguientes

Ahora que ha creado y configurado directivas de combinación para su organización, puede utilizarlas para ajustar la vista de los perfiles de cliente dentro de Platform y para crear segmentos de audiencia a partir de los datos de perfil. Consulte la [información general de segmentación](../../segmentation/home.md) para obtener más información sobre cómo crear y trabajar con segmentos mediante la interfaz de usuario y las API de [!DNL Experience Platform].
