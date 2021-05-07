---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;políticas de combinación;interfaz de usuario;interfaz de usuario;marca de tiempo solicitada;prioridad del conjunto de datos
title: Guía de la interfaz de usuario de políticas de combinación
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2879'
ht-degree: 0%

---

# Guía de la interfaz de usuario de políticas de combinación

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.

Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente. Cuando los datos de múltiples fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;soltero&quot; mientras que el otro indica que el cliente está &quot;casado&quot;), la política de combinación determina qué información incluir en el perfil del individuo.

Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario (IU) de Adobe Experience Platform.

Si prefiere trabajar con políticas de combinación utilizando la API [!DNL Real-time Customer Profile], siga las instrucciones descritas en la [guía de API de políticas de combinación](../api/merge-policies.md).

## Primeros pasos

Esta guía requiere una comprensión práctica de varias funciones [!DNL Experience Platform] importantes. Antes de seguir esta guía o usar las API de perfil, revise la documentación de los siguientes servicios:

* [Perfil](../home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Habilita el perfil del cliente en tiempo real al unir identidades de fuentes de datos dispares que se están incorporando en  [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

## Métodos de combinación {#merge-methods}

Cada fragmento de perfil contiene información para una sola identidad del número total de identidades que podría existir para un individuo. Al combinar esos datos para formar un perfil de cliente, existe la posibilidad de que esa información entre en conflicto y se debe especificar la prioridad. La selección de un método de combinación le permite especificar qué atributos del conjunto de datos priorizar si se produce un conflicto de combinación entre conjuntos de datos.

Hay dos métodos de combinación disponibles para las directivas de combinación. A continuación se resumen cada uno de estos métodos y se proporcionan detalles adicionales en las secciones siguientes:

* **[!UICONTROL Timestamp ordered]:** En caso de conflicto, se da prioridad al fragmento de perfil que se actualizó más recientemente.
   * **Marcas de hora personalizadas:** [!UICONTROL Timestamp ordered]  también admite marcas de hora personalizadas que tienen prioridad sobre las marcas de hora del sistema al combinar datos en el mismo conjunto de datos (varias identidades) o entre conjuntos de datos. Para obtener más información, consulte la sección sobre [uso de marcas de hora personalizadas](#custom-timestamps).
* **[!UICONTROL Dataset precedence]:** En caso de conflicto, asigne prioridad a los fragmentos de perfil según el conjunto de datos del que procedan. Al seleccionar esta opción, debe elegir los conjuntos de datos relacionados y su orden de prioridad.

### Marca de tiempo solicitada {#timestamp-ordered}

A medida que los registros de perfil se incorporan al Experience Platform, se obtiene una marca de tiempo del sistema en el momento de la ingesta y se agrega al registro. Cuando se selecciona **[!UICONTROL Timestamp ordered]** como método de combinación para una directiva de combinación, los perfiles se combinan en función de la marca de tiempo del sistema. En otras palabras, la combinación se realiza en función de la marca de tiempo para cuando el registro se incorporó a Platform.

#### Uso de marcas de hora personalizadas {#custom-timestamps}

En ocasiones puede haber casos de uso en los que sea necesario proporcionar una marca de tiempo personalizada y en los que la política de combinación respete la marca de tiempo personalizada en lugar de la marca de tiempo del sistema. Algunos ejemplos de esto son rellenar los datos o garantizar el orden correcto de los eventos si los registros se introducen de forma desordenada.

Para utilizar una marca de tiempo personalizada, el grupo de campos de esquema **[!UICONTROL External Source System Audit Details]** debe agregarse al esquema de perfil. Una vez añadida, la marca de tiempo personalizada se puede rellenar con el campo `lastUpdatedDate` . Cuando se ingesta un registro con el campo `lastUpdatedDate` rellenado, el Experience Platform utilizará ese campo para combinar registros entre conjuntos de datos. Si `lastUpdatedDate` no está presente o no se rellena, Platform seguirá usando la marca de tiempo del sistema.

>[!NOTE]
>
>Debe asegurarse de que la marca de tiempo `lastUpdatedDate` se rellene al ingerir una actualización en el mismo registro.

La siguiente captura de pantalla muestra los campos del grupo de campos [!UICONTROL External Source System Audit Details]. Para obtener instrucciones paso a paso sobre cómo trabajar con esquemas mediante la interfaz de usuario de Platform, incluido cómo añadir grupos de campos a esquemas, visite el [tutorial para crear un esquema con la IU](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-field-group.png)

Para trabajar con marcas de hora personalizadas mediante la API, consulte la sección [guía de extremo de directivas de combinación sobre el uso de marcas de hora personalizadas](../api/merge-policies.md#custom-timestamps).

### Prioridad del conjunto de datos {#dataset-precedence}

Cuando se selecciona **[!UICONTROL Dataset precedence]** como método de combinación para una política de combinación, se puede dar prioridad a los fragmentos de perfil en función del conjunto de datos del que proceden. Un caso de uso de ejemplo sería si su organización tuviera información presente en un conjunto de datos que es preferible o de confianza sobre los datos de otro conjunto de datos.

Para crear una directiva de combinación utilizando **[!UICONTROL Dataset precedence]**, debe seleccionar los conjuntos de datos de Perfil y ExperienceEvent que se incluyen y, a continuación, puede ordenar manualmente los conjuntos de datos de Perfil para que tengan prioridad. Una vez seleccionados y ordenados los conjuntos de datos, se asignará la prioridad más alta al conjunto de datos superior, el segundo será el segundo más alto, y así sucesivamente.

## [!UICONTROL ID stitching] {#id-stitching}

La vinculación de identidad ([!UICONTROL ID stitching]) es el proceso de identificación de fragmentos de datos y de combinación para formar un registro de perfil completo. Para ayudar a ilustrar los diferentes comportamientos de vinculación, considere un cliente único que interactúa con una marca utilizando dos direcciones de correo electrónico diferentes.

* **[!UICONTROL None]:** Cuando se selecciona esta opción, los ID no se vinculan. Cuando se produce la segmentación, las identidades que pueden pertenecer a la misma persona no se vinculan y la segmentación solo tendrá en cuenta los atributos adjuntos a cada ID individual al determinar si un cliente cumple los requisitos para pertenecer a un segmento. Esto podría hacer que un único cliente tenga varios perfiles y cada perfil cumpla los requisitos para segmentos diferentes, lo que resultaría en que se envíen varios mensajes de marketing al mismo cliente.
* **[!UICONTROL Private graph]:** Cuando se selecciona el gráfico privado, se vinculan varias identidades relacionadas con la misma persona. Esto hace que el cliente tenga un solo perfil y permite que la segmentación tenga en cuenta múltiples atributos de varias identidades relacionadas al determinar la calificación del segmento. En este escenario, es probable que el cliente tenga un solo perfil, cumpla los requisitos de un segmento en función de la combinación de atributos entre identidades y reciba solo un mensaje de marketing.

Para obtener más información sobre las identidades y su función en la generación de perfiles y segmentos, lea por favor la [descripción general del servicio de identidad](../../identity-service/home.md).

## Directiva de combinación predeterminada {#default-merge-policy}

Una organización puede crear una directiva de combinación predeterminada para que la utilice su organización al combinar fragmentos de perfil. Esto permite a los usuarios seleccionar fácilmente la directiva predeterminada al realizar acciones en el Experience Platform, como ver perfiles de clientes o crear segmentos. En la mayoría de los casos, a menos que se especifique otra directiva de combinación, se utilizará la directiva de combinación predeterminada.

Cada organización puede crear varias políticas de combinación relacionadas con una sola clase de esquema XDM, pero solo puede declararse una política de combinación predeterminada para cada clase. Por ejemplo, su organización podría tener una directiva de combinación predeterminada relacionada con la clase [!DNL XDM Individual Profile] y una directiva de combinación predeterminada diferente para una clase de inventario de productos personalizada.

Si crea una nueva directiva de combinación y la establece como predeterminada, el sistema actualizará automáticamente la directiva de combinación predeterminada anterior para que ya no sea la predeterminada.

>[!WARNING]
>
>Los recuentos de perfiles y los segmentos con una política de combinación predeterminada asociada existente pueden verse afectados. Cualquier segmento que tenga aplicada una directiva de combinación predeterminada se actualizará a la nueva directiva de combinación predeterminada.

## Ver directivas de combinación {#view-merge-policies}

En la interfaz de usuario [!DNL Experience Platform], puede empezar a trabajar con políticas de combinación seleccionando **[!UICONTROL Profiles]** en la navegación izquierda y luego la pestaña **[!UICONTROL Merge Policies]**. Esta ficha incluye una lista de todas las directivas de combinación existentes para su organización, así como detalles para cada directiva de combinación, incluido el nombre de la directiva, si la directiva de combinación es la directiva de combinación predeterminada y la clase de esquema a la que se relaciona la directiva de combinación.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/landing.png)

Para seleccionar qué detalles están visibles o para agregar columnas adicionales a la pantalla, seleccione **[!UICONTROL Configure columns]** y haga clic en el nombre de una columna para agregarla o quitarla de la vista.

![](../images/merge-policies/adjust-view.png)

## Crear una directiva de combinación {#create-a-merge-policy}

Para crear una nueva directiva de combinación, seleccione **[!UICONTROL Create merge policy]** en la pestaña políticas de combinación.

![Combinar la página de aterrizaje de directivas con el botón crear resaltado.](../images/merge-policies/create-new.png)

En la pantalla del flujo de trabajo **[!UICONTROL New merge policy]**, puede proporcionar información importante para la nueva política de combinación mediante una serie de pasos guiados.

![El nuevo flujo de trabajo de la política de combinación.](../images/merge-policies/create.png)

### [!UICONTROL Configure] {#configure}

El primer paso del flujo de trabajo le permite configurar la política de combinación proporcionando información básica. Esta información incluye:

* **[!UICONTROL Name]**: El nombre de la directiva de combinación debe ser descriptivo pero conciso.
* **[!UICONTROL Schema class]**: La clase de esquema XDM asociada a la directiva de combinación. Esto especifica la clase de esquema para la que se crea esta política de combinación. Las organizaciones pueden crear varias directivas de combinación por clase de esquema. Actualmente solo la clase [!UICONTROL XDM Individual Profile] está disponible en la interfaz de usuario. Puede obtener una vista previa del esquema de unión para la clase de esquema seleccionando **[!UICONTROL View Union Schema]**. Para obtener más información, consulte la sección [visualización del esquema de unión](#view-union-schema) que se muestra a continuación.
* **[!UICONTROL ID stitching]**: Este campo define cómo determinar las identidades relacionadas de un cliente. Consulte la sección sobre la [vinculación de ID](#id-stitching) anterior en esta guía para obtener más información. Hay dos valores posibles:
   * **[!UICONTROL None]**: No realice ninguna vinculación de identidad.
   * **[!UICONTROL Private Graph]**: Realice la vinculación de identidad en función del gráfico de identidad privada.
* **[!UICONTROL Default merge policy]**: Botón de alternancia que le permite seleccionar si esta directiva de combinación será o no la predeterminada para su organización. Si el selector está activado, aparece una advertencia que le solicita que confirme que desea cambiar la directiva de combinación predeterminada de su organización. Consulte la sección sobre [políticas de combinación predeterminadas](#default-merge-policy) en esta guía para obtener más información.
   ![](../images/merge-policies/create-make-default.png)

Una vez completados los campos obligatorios, puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo.

![Una pantalla de configuración completa con el botón Siguiente resaltado.](../images/merge-policies/create-complete.png)

#### [!UICONTROL View Union Schema] {#view-union-schema}

Al crear o editar una directiva de combinación, puede ver el esquema de unión para la clase de esquema elegida seleccionando **[!UICONTROL View Union Schema]**.

![](../images/merge-policies/view-union-schema.png)

Se abrirá el cuadro de diálogo [!UICONTROL View Union Schema], que muestra todos los esquemas de contribución, identidades y relaciones asociadas con el esquema de unión. Puede utilizar el cuadro de diálogo para explorar el esquema de unión del mismo modo que lo haría al acceder a la pestaña [!UICONTROL Union Schema] en la sección [!UICONTROL Profiles] de la interfaz de usuario de Platform.

Para obtener información detallada sobre los esquemas de unión, incluido cómo interactuar con ellos en la pestaña [!UICONTROL Union Schema] o en el cuadro de diálogo [!UICONTROL View Union Schema] que se muestra en el flujo de trabajo de políticas de combinación, visite la [guía de la interfaz de usuario del esquema de unión](union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Select Profile datasets] {#select-profile-datasets}

En la pantalla **[!UICONTROL Select Profile datasets]**, debe seleccionar el **[!UICONTROL Merge method]** que desea utilizar para la directiva de combinación. También se muestra en la pantalla el número total de [!UICONTROL Profile datasets] en la organización que están relacionados con la clase de esquema seleccionada en la pantalla anterior.

Según el método de combinación que elija, todos los conjuntos de datos de perfil se combinarán en el orden en que se actualizaron por última vez (con marca de tiempo solicitada) o tendrá que seleccionar qué conjuntos de datos de perfil incluir en la política de combinación y el orden en que se fusionarán (prioridad del conjunto de datos). Para obtener más información sobre los métodos de combinación, consulte la sección [merge methods](#merge-methods) proporcionada anteriormente en este documento.

#### Marca de tiempo solicitada {#timestamp-ordered-profile}

Si selecciona **[!UICONTROL Timestamp ordered]** como método de combinación, los atributos de los conjuntos de datos actualizados más recientemente tendrán prioridad. Esto se aplica a todos los conjuntos de datos de perfil.

![](../images/merge-policies/timestamp-ordered.png)

#### Prioridad del conjunto de datos {#dataset-precedence-profile}

Para seleccionar **[!UICONTROL Dataset precedence]** como método de combinación es necesario seleccionar conjuntos de datos de perfil y priorizarlos manualmente. Cada conjunto de datos enumerado también incluye el estado del último lote ingestado o muestra un aviso de que no se han introducido lotes en ese conjunto de datos.

Puede seleccionar hasta 50 conjuntos de datos de la lista de conjuntos de datos para incluirlos en la directiva de combinación. A medida que se seleccionan los conjuntos de datos, se añaden a la sección **[!UICONTROL Select datasets]** , lo que permite arrastrar y soltar los conjuntos de datos y ordenarlos según la prioridad que desee. Como los conjuntos de datos se ajustan en la lista, el ordinal (1, 2, 3, etc.) situado junto al conjunto de datos se actualizará y mostrará la prioridad (1 teniendo en cuenta la prioridad más alta, luego 2, y después).

Al seleccionar un conjunto de datos también se actualiza la sección **[!UICONTROL Union schema]**, que muestra los campos del esquema de unión en los que contribuye cada conjunto de datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

El siguiente paso del flujo de trabajo requiere que seleccione conjuntos de datos de ExperienceEvent . Esta pantalla está influenciada por el método de combinación seleccionado en la pantalla [[!UICONTROL Select Profile datasets]](#select-profile-datasets).

También se muestra en esta pantalla el número total de **[!UICONTROL ExperienceEvent datasets]** creados por la organización en relación con la clase de esquema seleccionada en la pantalla de configuración de la directiva de combinación.

#### Marca de tiempo solicitada {#timestamp-ordered-experienceevent}

Si seleccionó **[!UICONTROL Timestamp ordered]** como método de combinación para conjuntos de datos de perfil, los atributos de los conjuntos de datos de ExperienceEvent actualizados más recientemente también tendrán prioridad aquí.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Prioridad del conjunto de datos {#dataset-precedence-experienceevent}

Si seleccionó **[!UICONTROL Dataset precedence]** como método de combinación para conjuntos de datos de perfil, deberá seleccionar conjuntos de datos de ExperienceEvent para incluirlos. Puede seleccionar hasta 50 conjuntos de datos de ExperienceEvent de la lista de conjuntos de datos. Como los conjuntos de datos están seleccionados, aparecen en la sección [!UICONTROL Select datasets].

Los conjuntos de datos de ExperienceEvent no se pueden ordenar manualmente, sino que los atributos de los conjuntos de datos de ExperienceEvent se anexan a los conjuntos de datos de perfil si forman parte del mismo fragmento de perfil.

De forma similar a seleccionar conjuntos de datos de perfil, al seleccionar un conjunto de datos de ExperienceEvent también se actualiza la sección **[!UICONTROL Union schema]**, que muestra los campos del esquema de unión en los que contribuye cada conjunto de datos. Para obtener más información sobre los esquemas de unión, incluido cómo interactuar con las visualizaciones en la interfaz de usuario, consulte la [guía de la interfaz de usuario del esquema de unión](union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Review] {#review}

El último paso del flujo de trabajo es revisar la política de combinación. La pantalla **[!UICONTROL Review]** muestra el nombre de la nueva directiva de combinación, la clase de esquema en la que se basa, la opción [!UICONTROL ID stitching] que seleccionó, así como el método de combinación y los conjuntos de datos incluidos en la directiva de combinación. Para ver todos los conjuntos de datos de Perfil o ExperienceEvent incluidos, seleccione el número de conjuntos de datos que desea expandir en la lista desplegable.

Asegúrese de revisar la política de combinación cuidadosamente antes de seleccionar **[!UICONTROL Finish]** para completar el flujo de trabajo de creación.

#### Marca de tiempo solicitada {#timestamp-ordered-review}

Si seleccionó **[!UICONTROL Timestamp ordered]** como método de combinación para la directiva de combinación, la lista de conjuntos de datos de perfil incluye todos los conjuntos de datos que su organización ha creado relacionados con la clase de esquema, en orden de marca de tiempo. La lista de conjuntos de datos de ExperienceEvent incluye todos los conjuntos de datos que su organización ha creado para la clase de esquema elegida y se adjuntarán a los conjuntos de datos de perfil.

![](../images/merge-policies/timestamp-review.png)

#### Prioridad del conjunto de datos {#dataset-precedence-review}

Si seleccionó **[!UICONTROL Dataset precedence]** como método de combinación para la política de combinación, las listas de conjuntos de datos de Profile y ExperienceEvent incluyen solo los conjuntos de datos de Profile y ExperienceEvent que seleccionó durante el flujo de trabajo de creación, respectivamente. El orden de los conjuntos de datos de perfil debe coincidir con la prioridad especificada durante la creación. Si no es así, utilice el botón [!UICONTROL Back] para volver a los pasos anteriores del flujo de trabajo y ajustar la prioridad.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista actualizada de directivas de combinación {#updated-list}

Después de completar el flujo de trabajo para crear una nueva política de combinación, volverá a la pestaña **[!UICONTROL Merge Policies]**. La lista de directivas de combinación para su organización debe incluir ahora la directiva de combinación que acaba de crear.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar una directiva de combinación

Desde la pestaña [!UICONTROL Merge Policies], puede modificar una política de combinación existente creada para la clase [!DNL XDM Individual Profile] seleccionando la **[!UICONTROL Policy name]** para la política de combinación que desee editar.

![Página de aterrizaje de políticas de combinación](../images/merge-policies/select-edit.png)

Cuando aparece la pantalla **[!UICONTROL Edit merge policy]**, puede realizar cambios en el nombre y en [!UICONTROL ID stitching], así como cambiar si esta directiva es la directiva de combinación predeterminada para su organización.

Seleccione **[!UICONTROL Next]** para continuar a través del flujo de trabajo de la directiva de combinación para actualizar el método de combinación y los conjuntos de datos incluidos en la directiva de combinación.

![](../images/merge-policies/edit-screen.png)

Una vez que haya realizado los cambios necesarios, revise la directiva de combinación y seleccione **[!UICONTROL Finish]** para volver a la pestaña **[!UICONTROL Merge policies]**.

>[!WARNING]
>
>Cambiar una política de combinación puede afectar a la segmentación y a los resultados de perfil, ya que alterará la forma en que se resuelven los conflictos de datos.

![](../images/merge-policies/edit-review.png)

## Infracción de la política de control de datos

Al crear o actualizar una directiva de combinación, se realiza una comprobación para determinar si la directiva de combinación infringe alguna de las políticas de uso de datos definidas por su organización. Las políticas de uso de datos forman parte de Adobe Experience Platform [!DNL Data Governance] y son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, con datos específicos de [!DNL Platform]. Por ejemplo, si se utilizó una directiva de combinación para crear un segmento que se activó en un destino de terceros y la organización tenía una directiva de uso de datos que impedía la exportación de datos específicos a terceros, recibirá una notificación **[!UICONTROL Data governance policy violation detected]** al intentar guardar la directiva de combinación.

Esta notificación incluye una lista de las políticas de uso de datos que se han infringido y le permite ver los detalles de la infracción seleccionando una directiva en la lista. Al seleccionar una directiva violada, la pestaña **[!UICONTROL Data lineage]** proporciona el motivo de la infracción y las activaciones afectadas, y cada una proporciona más detalles sobre cómo se ha violado la directiva de uso de datos.

Para obtener más información sobre cómo se realiza el control de datos dentro de Adobe Experience Platform, lea en primer lugar la [información general sobre el control de datos](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Pasos siguientes

Ahora que ha creado y configurado directivas de combinación para su organización, puede utilizarlas para ajustar la vista de los perfiles de cliente dentro de Platform y para crear segmentos de audiencia a partir de los datos de perfil. Consulte [Información general de segmentación](../../segmentation/home.md) para obtener más información sobre cómo crear y trabajar con segmentos mediante la interfaz de usuario y las API de [!DNL Experience Platform].
