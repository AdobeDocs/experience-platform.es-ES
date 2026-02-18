---
solution: Experience Platform
title: Guía de IU de Audiences
description: Composición de audiencia en la interfaz de usuario de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar audiencias para su organización.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 66084e9847cca7ce6afd6a5b8c67689c9deef580
workflow-type: tm+mt
source-wordcount: '2293'
ht-degree: 16%

---

# Guía de IU de composición de audiencia

>[!BEGINSHADEBOX]

Si es cliente de Adobe Journey Optimizer, lea la [guía de introducción a la composición de audiencias](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/audience-orchestration/get-started-audience-orchestration.html?lang=es) en la documentación de Adobe Journey Optimizer para obtener más información sobre cómo trabajar con la composición de audiencias en ese contexto.

>[!ENDSHADEBOX]

>[!AVAILABILITY]
>
>Para utilizar esta función, debe tener los siguientes permisos:
>
>- Administrar segmentos
>- Administrar perfiles
>- Administrar políticas de combinación
>
>Encontrará más información sobre los permisos de Experience Platform en la [descripción general del control de acceso](../../access-control/home.md#permissions).

>[!NOTE]
>
>Esta guía explica cómo crear audiencias mediante Composición de audiencias. Para aprender a crear audiencias a través de las definiciones de segmentos mediante el Generador de segmentos, lea la [guía de la interfaz de usuario del Generador de segmentos](./segment-builder.md).

Composición de audiencia proporciona un espacio de trabajo para crear y editar audiencias, utilizando bloques que se utilizan para representar diferentes acciones.

![Interfaz de usuario de composición de audiencia.](../images/ui/audience-composition/audience-composition.png)

Para cambiar los detalles de la composición, incluidos el título y la descripción, seleccione el botón ![controles deslizantes](/help/images/icons/properties.png).

Aparece la ventana emergente **[!UICONTROL Composition properties]**. Puede insertar detalles de la composición, incluidos el título y la descripción aquí.

![Se muestra la ventana emergente de propiedades de composición.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Si **no** le asigna un título a la composición, tendrá un título de &quot;Composición&quot; seguido de la fecha y hora de creación de forma predeterminada. Además, cada composición **debe** tener su propio nombre único.

Después de actualizar los detalles de la composición, seleccione **[!UICONTROL Save]** para confirmar estas actualizaciones. El lienzo de composición de audiencia vuelve a aparecer.

El lienzo de composición de audiencias se compone de cuatro tipos diferentes de bloques: **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclude]](#exclude-block)**, **[[!UICONTROL Rank]](#rank-block)** y **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_audience"
>title="Bloque de público"
>abstract="El bloque Público le permite añadir los subpúblicos que desee utilizar para componer el nuevo público."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_merge_types"
>title="Tipos de combinación"
>abstract="Los tipos de combinación determinan cómo se combinan los subpúblicos seleccionados. Los valores admitidos son unión, intersección y superposición de exclusión."

El tipo de bloque **[!UICONTROL Audience]** le permite agregar las subaudiencias que desea utilizar para crear su nueva audiencia mayor. De forma predeterminada, se incluye un bloque **[!UICONTROL Audience]** en la parte superior del lienzo de composición.

Al seleccionar el bloque **[!UICONTROL Audience]**, el carril derecho muestra controles para etiquetar la audiencia, agregar audiencias al bloque y crear reglas personalizadas para el bloque de audiencia.

>[!NOTE]
>
>Puede agregar audiencias **o** para crear una regla personalizada. Estas dos funcionalidades **no se pueden** usar juntas.

![Se muestran los detalles del bloque de audiencia.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Add audience] {#add-audience}

Para añadir audiencias al bloque Audiencia. seleccione **[!UICONTROL Add Audience]**.

![El botón Agregar audiencia está resaltado.](../images/ui/audience-composition/select-add-audience.png)

>[!IMPORTANT]
>
>Tenga en cuenta que solo aparecerán **1&rbrace; audiencias definidas mediante la política de combinación predeterminada.**
>
>Además, solo se pueden usar **audiencias publicadas** creadas con el Generador de segmentos. Las audiencias creadas con Composición de audiencias y audiencias generadas externamente están disponibles **no**.

Aparecerá una lista de audiencias. Seleccione las audiencias que desee incluir, seguidas de **[!UICONTROL Add]** para anexarlas al bloque de audiencias.

![Aparece una lista de audiencias. Puede seleccionar la audiencia que desea agregar en este cuadro de diálogo.](../images/ui/audience-composition/select-audience.png)

Las audiencias seleccionadas aparecerán ahora dentro del carril derecho cuando se seleccione el bloque **[!UICONTROL Audience]**. Desde aquí puede cambiar el tipo de combinación de las audiencias combinadas.

![Se resaltan los posibles tipos de combinación de las audiencias.](../images/ui/audience-composition/merge-types.png)

| Tipo de combinación | Descripción |
| ---------- | ----------- |
| [!UICONTROL Union] | Las audiencias se combinan en una sola audiencia. Sería el equivalente de una operación O. |
| [!UICONTROL Intersection] | Las audiencias se combinan y solo se agregan las audiencias que se comparten en **todas**. Esto sería el equivalente de una operación AND. |
| [!UICONTROL Exclude overlap] | Las audiencias se combinan y solo se agregan las audiencias que se comparten en **una, pero no todas**. Esto sería el equivalente de una operación XOR. |

### [!UICONTROL Build rule] {#build-rule}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rule_builder"
>title="Generador de segmentos"
>abstract="Puede usar el Generador de segmentos para añadir una regla personalizada para su composición."

Para agregar una regla personalizada al bloque Audiencia, seleccione **[!UICONTROL Build rule]**.

![El botón Generar regla está resaltado.](../images/ui/audience-composition/select-build-rule.png)

Aparecerá el Generador de segmentos. Puede usar el Generador de segmentos para crear una regla personalizada para la audiencia que seguirá. Encontrará más información sobre el uso del Generador de segmentos en la [guía del Generador de segmentos](./segment-builder.md).

![Se muestra la interfaz de usuario del Generador de segmentos.](../images/ui/audience-composition/segment-builder.png)

Después de agregar una regla personalizada, seleccione **[!UICONTROL Save]** para agregar la regla a su audiencia.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Exclude] {#exclude-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude"
>title="Excluir bloque"
>abstract="El bloque Excluir permite excluir de la composición públicos o atributos especificados."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_type"
>title="Tipo de exclusión"
>abstract="Puede excluir perfiles pertenecientes a un público específico (Excluir por público) o excluir perfiles en función de un atributo específico (Excluir por atributo)."

El tipo de bloque **[!UICONTROL Exclude]** le permite excluir una subaudiencia o atributos especificados de la nueva audiencia mayor.

Para agregar un bloque **[!UICONTROL Exclude]**, seleccione el icono **+**, seguido de **[!UICONTROL Exclude]**.

![Se ha seleccionado la opción Excluir.](../images/ui/audience-composition/add-exclude-block.png)

Se agrega el bloque **[!UICONTROL Exclude]**. Cuando se selecciona este bloque, los detalles sobre la exclusión aparecen en el carril derecho. Esto incluye la etiqueta del bloque y el tipo de exclusión. Puede excluir [por audiencia](#exclude-audience) o [por atributo](#exclude-attribute).

![Bloque Exclude, que resalta los dos tipos de exclusión disponibles.](../images/ui/audience-composition/exclude.png)

### Excluir por audiencia {#exclude-audience}

Si excluye por audiencia, puede seleccionar la audiencia que desea excluir seleccionando **[!UICONTROL Add Audience]**.

![El botón [!UICONTROL Add audience] está seleccionado, lo que le permite elegir la audiencia que desea excluir.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>Solo se pueden usar las **audiencias publicadas** creadas mediante el Generador de segmentos. Las audiencias creadas con Composición de audiencias y audiencias generadas externamente están disponibles **no**.

Aparecerá una lista de audiencias. Seleccione **[!UICONTROL Add]** para agregar la audiencia que desee excluir al bloque de exclusión.

![Aparece una lista de audiencias. Puede seleccionar la audiencia que desea agregar en este cuadro de diálogo.](../images/ui/audience-composition/select-audience.png)

### Excluir por atributo {#exclude-attribute}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_attribute"
>title="Excluir por atributo"
>abstract="Cuando excluye por atributo, puede excluir perfiles específicos de la aparición en la composición en función de los atributos seleccionados."

Si excluye por atributo, puede seleccionar qué atributos desea excluir seleccionando el icono ![filter](/help/images/icons/project-edit.png) dentro de la sección **[!UICONTROL Exclusion rule]**. Excluir el atributo permite excluir cualquier perfil que contenga este atributo de la audiencia resultante.

![La sección de atributos está resaltada y muestra dónde seleccionar para elegir el atributo que se excluirá.](../images/ui/audience-composition/exclude-attribute.png)

Aparecerá una lista de atributos de perfil. Seleccione el tipo de atributo que desea excluir, seguido de **[!UICONTROL Select]** para agregarlo al bloque de exclusión.

![Se muestra una lista de atributos.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>Al excluir por atributo, solo puede especificar **un** valor que excluir. El uso de cualquier tipo de separador, como una coma o un punto y coma, solo hará que se excluya ese valor exacto. Por ejemplo, si establece el valor como `red, blue`, se excluirá el término `red, blue` del atributo, pero **no** se excluirá el término `red` o `blue`.

## [!UICONTROL Enrich] {#enrich-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich"
>title="Enriquecimiento del bloque"
>abstract="El bloque Enriquecer le permite enriquecer el público con atributos adicionales procedentes de los conjuntos de datos de Adobe Experience Platform."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_dataset"
>title="Conjunto de datos de enriquecimiento"
>abstract="El conjunto de datos de enriquecimiento contiene los datos que desea asociar con la composición."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_criteria"
>title="Criterios de enriquecimiento"
>abstract="Los criterios de enriquecimiento incluyen la clave de unión de origen y la clave de unión del conjunto de datos de enriquecimiento. Estas dos claves reconcilian el conjunto de datos de origen y el conjunto de datos de enriquecimiento."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_attributes"
>title="Atributos de enriquecimiento"
>abstract="Los atributos de enriquecimiento son los atributos que desea asociar con la composición."

>[!IMPORTANT]
>
>En este momento, los atributos de enriquecimiento **solo** se pueden usar en escenarios de Adobe Journey Optimizer descendentes.

El tipo de bloque **[!UICONTROL Enrich]** le permite enriquecer su audiencia con atributos adicionales de un conjunto de datos. Puede utilizar estos atributos en casos de uso de personalización.

Para agregar un bloque **[!UICONTROL Enrich]**, seleccione el icono **+**, seguido de **[!UICONTROL Enrich]**.

![La opción [!UICONTROL Enrich] está seleccionada.](../images/ui/audience-composition/add-enrich-block.png)

Se agrega el bloque **[!UICONTROL Enrich]**. Cuando se selecciona este bloque, los detalles sobre el enriquecimiento aparecen en el carril derecho. Esto incluye la etiqueta del bloque y el conjunto de datos de enriquecimiento.

Para seleccionar el conjunto de datos con el que enriquecer la audiencia, seleccione el icono ![filter](/help/images/icons/project-edit.png).

![El botón de filtro está resaltado. Si selecciona esta opción, accederá a la ventana emergente [!UICONTROL Select dataset].](../images/ui/audience-composition/enrich-select-dataset.png)

Aparece la ventana emergente **[!UICONTROL Select dataset]**. Seleccione el conjunto de datos que desee agregar para el enriquecimiento, seguido de **[!UICONTROL Select]** para agregar el conjunto de datos para el enriquecimiento.

![El conjunto de datos elegido está seleccionado.](../images/ui/audience-composition/select-dataset.png)

>[!IMPORTANT]
>
>El conjunto de datos seleccionado **debe** cumplir con los siguientes criterios:
>
>- El conjunto de datos **debe** ser de tipo de registro.
>   - El conjunto de datos **no puede** ser de tipo de evento, generado por el sistema o marcado para el perfil.
>- El conjunto de datos **debe** tener 1 GB o menos.

La sección **[!UICONTROL Enrichment criteria]** aparece ahora en el carril derecho. En esta sección, puede seleccionar **[!UICONTROL Source join key]** y **[!UICONTROL Enrichment dataset join key]**, lo que le permite vincular el conjunto de datos de enriquecimiento con la audiencia que está intentando crear.

![El área [!UICONTROL Enrichment criteria] está resaltada.](../images/ui/audience-composition/enrichment-criteria.png)

Para seleccionar **[!UICONTROL Source join key]**, seleccione el icono ![filtro](/help/images/icons/project-edit.png).

Aparece la ventana emergente **[!UICONTROL Select a profile attribute]**. Seleccione el atributo de perfil que desee utilizar como clave de unión de origen, seguido de **[!UICONTROL Select]** para elegir ese atributo como clave de unión de origen.

![El atributo que desea usar como clave de combinación de origen está resaltado.](../images/ui/audience-composition/select-source-join-key.png)

Para seleccionar **[!UICONTROL Enrichment dataset join key]**, seleccione el icono ![filtro](/help/images/icons/project-edit.png).

Aparece la ventana emergente **[!UICONTROL Enrichment attributes]**. Seleccione el atributo que desee usar como clave de unión del conjunto de datos de enriquecimiento, seguido de **[!UICONTROL Select]** para elegir ese atributo como clave de unión del conjunto de datos de enriquecimiento.

![El atributo que desea usar como clave de unión del conjunto de datos de enriquecimiento está resaltado.](../images/ui/audience-composition/select-enrichment-dataset-join-key.png)

Ahora que ha agregado ambas claves de unión, aparece la sección **[!UICONTROL Enrichment attributes]**. Ahora puede añadir el atributo con el que desee mejorar la audiencia. Para agregar estos atributos, seleccione **[!UICONTROL Add attribute]**.

Aparece la ventana emergente **[!UICONTROL Enrichment attributes]**. Puede seleccionar los atributos del conjunto de datos con los que enriquecer la audiencia, seguidos de **[!UICONTROL Select]** para agregarlos a la audiencia.

![Los atributos de enriquecimiento que desea agregar están resaltados.](../images/ui/audience-composition/select-enrichment-attribute.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Rank] {#rank-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_ranking"
>title="Bloque de clasificación"
>abstract="El bloque Clasificación le permite clasificar perfiles según un atributo específico e incluirlos en su composición. "

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rank_profilelimit_text"
>title="Añadir límite de perfil"
>abstract="La opción Añadir límite de perfil permite especificar un número máximo de perfiles que incluir como parte del proceso de clasificación."

El tipo de bloque **[!UICONTROL Rank]** le permite clasificar y ordenar perfiles en función de un atributo especificado e incluir estos perfiles clasificados en la composición.

Para agregar un bloque **[!UICONTROL Rank]**, seleccione el icono **+**, seguido de **[!UICONTROL Rank]**.

![La opción Clasificación está seleccionada.](../images/ui/audience-composition/add-rank-block.png)

Al seleccionar el bloque, los detalles sobre la clasificación se muestran en el carril derecho, incluida la etiqueta del bloque, el atributo por el que clasificar, el orden de clasificación y una opción para limitar el número de perfiles que clasificar.

![Se resalta el bloque de clasificación, así como los detalles del bloque de clasificación.](../images/ui/audience-composition/rank.png)

Para seleccionar por qué atributo clasificar las audiencias, seleccione el icono ![filter](/help/images/icons/project-edit.png).

![El icono de filtro está resaltado y muestra lo que debe seleccionar para tener acceso a la pantalla de selección de atributos de perfil.](../images/ui/audience-composition/select-rank-attribute.png)

Aparecerá una lista de atributos de perfil. En esta ventana emergente, puede seleccionar el tipo de atributo por el que desea clasificar la audiencia. Seleccione **[!UICONTROL Select]** para agregarlo a su bloque de clasificación. Tenga en cuenta que el atributo seleccionado **solamente** puede ser números.

![Se muestra una lista de atributos.](../images/ui/audience-composition/rank-attribute.png)

Después de seleccionar el atributo, puede seleccionar el orden por el que desea clasificarlo. Puede ser ascendente (de menor a mayor) o descendente (de mayor a menor).

Además, puede limitar el número de perfiles devueltos habilitando la opción **[!UICONTROL Add profile limit]**. Cuando esta opción está habilitada, puede establecer el número máximo de perfiles devueltos dentro del campo **[!UICONTROL Included profiles]**.

![Se ha resaltado la opción Agregar límite de perfil, que le permite limitar el número de perfiles devueltos.](../images/ui/audience-composition/add-profile-limit-rank.png)

## [!UICONTROL Split] {#split-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split"
>title="Bloque de división"
>abstract="El bloque División le permite dividir la composición en varias rutas. "

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_type"
>title="Tipo de división"
>abstract="Puede dividir la composición por división de porcentaje o de atributo. La división porcentual divide aleatoriamente los perfiles en varias rutas. La división Atributo le permite dividir los perfiles según un atributo específico."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_otherprofiles_text"
>title="Otros perfiles"
>abstract="La opción Otros perfiles le permite crear una ruta adicional con los perfiles restantes que no coinciden con ninguna de las condiciones especificadas de las otras rutas."

>[!NOTE]
>
>Para usar el bloque **[!UICONTROL Split]**, usted **debe** tener al menos 10 perfiles en su audiencia.

El tipo de bloque **[!UICONTROL Split]** le permite dividir la nueva audiencia en varias subaudiencias. Puede dividir esta audiencia según el porcentaje o por un atributo.

Para agregar un bloque **[!UICONTROL Split]**, seleccione el icono **+**, seguido de **[!UICONTROL Split]**.

![Se ha seleccionado la opción Dividir.](../images/ui/audience-composition/add-split-block.png)

Al dividir la audiencia, puede hacerlo por porcentaje o por atributo.

### Dividido por porcentaje {#split-percentage}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_percentage"
>title="Dividido por porcentaje"
>abstract="El público se puede dividir aleatoriamente en varios públicos en función del número de rutas y porcentajes proporcionados."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_persistent"
>title="División persistente"
>abstract="Puede hacer que la división porcentual sea persistente habilitando esta opción y seleccionando un espacio de nombres de identidad."

Al dividir por porcentaje, las audiencias se dividirán aleatoriamente en función del número de rutas y porcentajes proporcionados.

![Se resalta la división porcentual.](../images/ui/audience-composition/split-by-percentage.png)

También puede proporcionar una identidad, lo que haría que la división basada en porcentajes fuera persistente. Los tipos de identidad disponibles incluyen todas las áreas de nombres de identidad disponibles en su organización.

![La casilla de verificación Dividir por identidad está resaltada. Además, se resalta la lista desplegable que le permite seleccionar con la identidad para dividir.](../images/ui/audience-composition/split-by-identity.png)

### Dividir por atributo {#split-attribute}

Al dividir por atributo, las audiencias se dividen según los atributos proporcionados. Para seleccionar el atributo por el que dividir, seleccione el bloque **[!UICONTROL Split]**, seguido del icono ![filter](/help/images/icons/project-edit.png).

![Se ha seleccionado el botón de filtro, que muestra cómo filtrar por atributo.](../images/ui/audience-composition/split-by-attribute.png)

Aparecerá una lista de atributos de perfil. Seleccione el tipo de atributo, seguido de **[!UICONTROL Select]** para agregarlo al bloque dividido.

![Se muestra una lista de atributos.](../images/ui/audience-composition/select-attribute.png)

Después de seleccionar el atributo, puede elegir qué perfiles pertenecerán a cada subaudiencia agregando los valores dentro del campo **[!UICONTROL Values]**.

![Se agregan los valores por los que desea dividir los atributos.](../images/ui/audience-composition/attribute-split-values.png)

Además, puede habilitar la opción **[!UICONTROL Other profiles]** para crear una subaudiencia que incluya todos los perfiles no seleccionados.

![Se ha resaltado la opción Otros perfiles.](../images/ui/audience-composition/split-other-profiles.png)

## Publicar el público {#publish}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_publish"
>title="Publicación"
>abstract="Puede publicar la composición para crear los públicos resultantes en Adobe Experience Platform."

>[!IMPORTANT]
>
>Al publicar la composición de audiencia, tenga en cuenta que puede tardar hasta 48 horas en evaluarse y activarse para su uso en servicios descendentes como un destino de Real-Time CDP o un canal de Adobe Journey Optimizer.

Después de crear la composición, puede guardarla y publicarla seleccionando **[!UICONTROL Publish]**.

![El botón Publicar aparece resaltado y muestra cómo guardar y publicar la composición.](../images/ui/audience-composition/publish.png)

Si se produce algún error al crear la audiencia, aparece una alerta que le permite saber cómo resolver el problema.

![El botón Publicar aparece resaltado y muestra cómo guardar y publicar la composición.](../images/ui/audience-composition/audience-alert.png)

## Próximos pasos

Composición de audiencia proporciona un flujo de trabajo enriquecido que le permite crear composiciones a partir de los distintos tipos de bloques. Para obtener más información acerca de otras partes de la interfaz de usuario del servicio de segmentación, lea la [Guía del usuario del servicio de segmentación](./overview.md).
