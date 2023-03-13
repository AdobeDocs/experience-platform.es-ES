---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía de usuario;guía de iu;guía de iu de audiencias;generador de audiencias;audiencia;audiencias;guía de iu de audiencias;
solution: Experience Platform
title: Guía de IU de Audiences
description: El Generador de audiencias en la IU de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar audiencias para su organización.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guía de IU de Audience Builder

>[!IMPORTANT]
>
>El Generador de audiencias se encuentra actualmente en la versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

El Generador de audiencias proporciona un espacio de trabajo para crear y editar audiencias, utilizando bloques que se utilizan para representar diferentes acciones.

![La interfaz de usuario de Audience Builder.](../images/ui/audience-builder/audience-builder.png)

El lienzo de composición de audiencia se compone de cinco tipos diferentes de bloques: **[[!UICONTROL Audiencia]](#audience-block)**, **[[!UICONTROL Excluir]](#exclude-block)**, **[[!UICONTROL Unirse]](#join-block)**, **[[!UICONTROL Rango]](#rank-block)**, y **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audiencia ] {#audience-block}

El **[!UICONTROL Audiencia]** el tipo de bloque le permite añadir las subaudiencias que desea para componer su nueva audiencia más grande. De forma predeterminada, una **[!UICONTROL Audiencia]** El bloque de se incluye en la parte superior del lienzo de composición.

Al seleccionar la variable **[!UICONTROL Audiencia]** , el carril derecho muestra controles para etiquetar y añadir audiencias al bloque.

![Se muestran los detalles del bloque Audiencia.](../images/ui/audience-builder/select-audience.png)

Después de seleccionar **[!UICONTROL Añadir audiencia]**, aparecerá una lista de audiencias. Seleccione las audiencias que desee incluir, seguidas de **[!UICONTROL Añadir]** para anexarlas al bloque de audiencia.

![Aparecerá una lista de audiencias. Puede seleccionar la audiencia que desea agregar en este cuadro de diálogo.](../images/ui/audience-builder/select-audience.png)

Las audiencias seleccionadas aparecerán ahora en el carril derecho cuando el **[!UICONTROL Audiencia]** El bloque está seleccionado. Desde aquí puede cambiar el tipo de combinación de las audiencias combinadas.

![Se resaltan los posibles tipos de combinación de las audiencias.](../images/ui/audience-builder/merge-types.png)

| Tipo de combinación | Descripción |
| ---------- | ----------- |
| [!UICONTROL Union] | Las audiencias se combinan en una sola audiencia. Sería el equivalente de una operación O. |
| [!UICONTROL Intersección] | Las audiencias se combinan, y solo se comparten las audiencias en **todo** de ellos que se van a añadir. Esto sería el equivalente de una operación AND. |
| [!UICONTROL Excluir superposición] | Las audiencias se combinan, y solo se comparten las audiencias en **uno, pero no todos** de ellos que se van a añadir. Esto sería el equivalente de una operación XOR. |

## [!UICONTROL Excluir] {#exclude-block}

El **[!UICONTROL Excluir]** el tipo de bloque le permite excluir subaudiencias o atributos especificados de la nueva audiencia más grande.

Para agregar un **[!UICONTROL Excluir]** , seleccione la **+** icono, seguido de **[!UICONTROL Excluir]**.

![La opción Excluir está seleccionada.](../images/ui/audience-builder/add-exclude-block.png)

El **[!UICONTROL Excluir]** se ha añadido un bloque de. Cuando se selecciona este bloque, los detalles sobre la exclusión aparecen en el carril derecho. Esto incluye la etiqueta del bloque y el tipo de exclusión. Puede excluir [por audiencia](#exclude-audience) o [por atributo](#exclude-attribute).

![El bloque Exclude, que resalta los dos tipos diferentes de exclusión disponibles.](../images/ui/audience-builder/exclude.png)

### Excluir por audiencia {#exclude-audience}

Si excluye por audiencia, puede seleccionar qué audiencias desea excluir seleccionando **[!UICONTROL Añadir audiencia]**.

![El botón Add audience está seleccionado, lo que le permite elegir qué audiencia desea excluir.](../images/ui/audience-builder/add-excluded-audience.png)

Aparecerá una lista de audiencias. Seleccionar **[!UICONTROL Añadir]** para añadir las audiencias que desee excluir al bloque de exclusión.

![Aparecerá una lista de audiencias. Puede seleccionar la audiencia que desea agregar en este cuadro de diálogo.](../images/ui/audience-builder/select-audience.png)

### Excluir por atributo {#exclude-attribute}

Si excluye por atributo, puede seleccionar qué atributos desea excluir seleccionando la variable ![filter](../images/ui/audience-builder/filter-attribute.png) dentro de la **[!UICONTROL Regla de exclusión]** sección.

![La sección de atributos aparece resaltada y muestra dónde seleccionar para elegir el atributo que desea excluir.](../images/ui/audience-builder/exclude-attribute.png)

Aparecerá una lista de atributos de perfil. Seleccione el tipo de atributo que desea excluir, seguido de **[!UICONTROL Seleccionar]** para añadirlos al bloque de exclusión.

![Se muestra una lista de atributos.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Unirse] {#join-block}

El **[!UICONTROL Unirse]** el tipo de bloque permite añadir audiencias externas de conjuntos de datos que Adobe Experience Platform aún no ha procesado.

Para agregar un **[!UICONTROL Unirse]** , seleccione la **+** icono, seguido de **[!UICONTROL Unirse]**.

![La opción Join está seleccionada.](../images/ui/audience-builder/add-join-block.png)

Al seleccionar el bloque, los detalles sobre la unión se muestran en el carril derecho, incluida la etiqueta del bloque y la opción para agregar audiencias al conjunto de datos enriquecido.

![El bloque de combinación se resalta, incluidos los detalles sobre el bloque de combinación.](../images/ui/audience-builder/join.png)

Después de seleccionar **[!UICONTROL Añadir audiencia]**, aparecerá una lista de audiencias. Seleccione las audiencias que desee incluir, seguidas de **[!UICONTROL Añadir]** para añadirlos al bloque de unión.

![Aparecerá una lista de audiencias. Puede seleccionar la audiencia que desea agregar en este cuadro de diálogo.](../images/ui/audience-builder/select-audience.png)

Las audiencias seleccionadas aparecerán ahora en el carril derecho cuando el **[!UICONTROL Unirse]** El bloque está seleccionado.

![Se muestran las audiencias que se añadieron como parte de la unión.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Rango] {#rank-block}

El **[!UICONTROL Rango]** el tipo de bloque le permite clasificar y ordenar las audiencias antes de que se publique la nueva audiencia.

Para agregar un **[!UICONTROL Rango]** , seleccione la **+** icono, seguido de **[!UICONTROL Rango]**.

![La opción Rank está seleccionada.](../images/ui/audience-builder/add-rank-block.png)

Al seleccionar el bloque, los detalles sobre la clasificación se muestran en el carril derecho, incluida la etiqueta del bloque, el atributo por el que clasificar, el orden de clasificación y una opción para limitar el número de perfiles que clasificar.

![Se resaltará el bloque de clasificación, así como los detalles del bloque de clasificación.](../images/ui/audience-builder/rank.png)

Para seleccionar por qué atributo clasificar las audiencias, seleccione el ![filter](../images/ui/audience-builder/filter-attribute.png) icono.

![El icono de filtro se resalta y muestra lo que debe seleccionar para acceder a la pantalla de selección de atributos de perfil.](../images/ui/audience-builder/select-rank-attribute.png)

Aparecerá una lista de atributos de perfil. En esta ventana emergente, puede seleccionar el tipo de atributo por el que desea clasificar la audiencia. Seleccionar **[!UICONTROL Seleccionar]** para añadirlo a su bloque de clasificación. Tenga en cuenta que el atributo seleccionado **solamente** ser de tipo `int`.

![Se muestra una lista de atributos.](../images/ui/audience-builder/select-attribute.png)

Después de seleccionar el atributo, puede seleccionar el orden por el que desea clasificarlo. Puede ser ascendente (de menor a mayor) o descendente (de mayor a menor).

Además, puede limitar el número de audiencias que devuelve habilitando la variable **[!UICONTROL Añadir límite de perfil]** alternar. Cuando esta opción está habilitada, puede establecer el número máximo de audiencias devueltas dentro de la variable **[!UICONTROL Perfiles incluidos]** field.

![Se resalta la opción Add profile limit, que permite limitar el número de audiencias devueltas.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

El **[!UICONTROL Split]** el tipo de bloque le permite dividir la nueva audiencia en varias subaudiencias. Puede dividir esta audiencia según el porcentaje o por un atributo.

Para agregar un **[!UICONTROL Split]** , seleccione la **+** icono, seguido de **[!UICONTROL Split]**.

![La opción Split está seleccionada.](../images/ui/audience-builder/add-split-block.png)

### Dividido por porcentaje {#split-percentage}

Al dividir por porcentaje, las audiencias se dividirán aleatoriamente en función del número de rutas y porcentajes proporcionados.

Por ejemplo, puede tener tres rutas, cada una con un porcentaje diferente de perfiles.

![Se muestra el desglose en número de audiencias guardadas y porcentajes.](../images/ui/audience-builder/percentages.png)

Además, puede marcar una de las audiencias divididas como grupo de control.

![La opción de grupo de control está activada. Esto permite marcar una de las audiencias divididas como grupo de control.](../images/ui/audience-builder/control-group.png)

### Dividir por atributo {#split-attribute}

Al dividir por atributo, las audiencias se dividen según los atributos proporcionados. Para seleccionar el atributo por el que dividir, seleccione **[!UICONTROL Split]** bloque, seguido de la variable ![filter](../images/ui/audience-builder/filter-attribute.png) icono.

![Se selecciona el botón de filtro, que muestra cómo filtrar por atributo.](../images/ui/audience-builder/select-attribute-split.png)

Aparecerá una lista de atributos de perfil. Seleccione el tipo de atributo, seguido de **[!UICONTROL Seleccionar]** para añadirlo a su bloque de división.

![Se muestra una lista de atributos.](../images/ui/audience-builder/select-attribute.png)

Después de seleccionar el atributo, puede elegir qué perfiles pertenecen a cada subaudiencia añadiendo los valores dentro de la variable **[!UICONTROL Valores]** field.

![Se añaden los valores por los que desea dividir los atributos.](../images/ui/audience-builder/attribute-split-values.png)

Además, puede habilitar la variable **[!UICONTROL Otros perfiles]** active esta opción para crear una subaudiencia que incluya todos los perfiles no seleccionados.

![Se resaltará la opción Otros perfiles.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publicación de la audiencia

Una vez maquetada la audiencia, puede guardarla y publicarla seleccionando **[!UICONTROL Publish]**.

![El botón Publicar aparece resaltado y muestra cómo guardar y publicar la audiencia.](../images/ui/audience-builder/publish-audience.png)

Si se produce algún error al crear la audiencia, aparece una alerta que le permite saber cómo resolver el problema.

![El botón Publicar aparece resaltado y muestra cómo guardar y publicar la audiencia.](../images/ui/audience-builder/audience-alert.png)

## Pasos siguientes

El Generador de audiencias proporciona un flujo de trabajo enriquecido que le permite crear audiencias a partir de los diferentes tipos de bloques. Para obtener más información acerca de otras partes de la interfaz de usuario del servicio de segmentación, lea la [Guía del usuario del servicio de segmentación](./overview.md).
