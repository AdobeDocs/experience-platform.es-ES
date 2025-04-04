---
keywords: Experience Platform;inicio;temas populares;iu;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;explorar;clase;grupo de campos;tipo de datos;esquema;
solution: Experience Platform
title: Exploración de los recursos de esquema en la IU
description: Aprenda a explorar esquemas, clases, grupos de campos de esquema y tipos de datos existentes en la interfaz de usuario de Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Exploración de recursos de esquema en la IU

En Adobe Experience Platform, todos los recursos de esquema del Modelo de datos de experiencia (XDM) se almacenan en [!DNL Schema Library], incluidos los recursos estándar proporcionados por Adobe y los recursos personalizados definidos por su organización. En la interfaz de usuario de Experience Platform, puede ver la estructura y los campos de cualquier esquema, clase, grupo de campos o tipo de datos existente en [!DNL Schema Library]. Esto resulta especialmente útil a la hora de planificar y preparar la ingesta de datos, ya que la interfaz de usuario proporciona información sobre los tipos de datos esperados y los casos de uso de cada campo proporcionado por estos recursos XDM.

Este tutorial explica los pasos para explorar los esquemas, las clases, los grupos de campos y los tipos de datos existentes en la interfaz de usuario de Experience Platform.

## Búsqueda de un recurso de esquema {#lookup}

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. El área de trabajo [!UICONTROL Esquemas] proporciona una ficha **[!UICONTROL Examinar]** para explorar todos los esquemas de su organización, junto con fichas dedicadas adicionales para explorar **[!UICONTROL Clases]**, **[!UICONTROL Grupos de campos]**, **[!UICONTROL Tipos de datos]** y **[!UICONTROL Relaciones]** respectivamente.

![Espacio de trabajo de esquemas con varias fichas resaltadas.](../images/ui/explore/tabs.png)

El icono de filtro (![Imagen del icono de filtro](/help/images/icons/filter.png)) muestra los controles en el carril izquierdo para reducir los resultados de la lista. Los filtros de recursos están disponibles para esquemas y relaciones en las fichas **[!UICONTROL Examinar]** y **[!UICONTROL Relaciones]** respectivamente.

En la ficha [!UICONTROL Examinar] del área de trabajo [!UICONTROL Esquemas], puede filtrar el inventario de esquemas. Use la opción **[!UICONTROL Incluido en el perfil]** para mostrar solo los esquemas que se han habilitado para usar en [Perfil del cliente en tiempo real](../../profile/home.md). Utilice la opción **[!UICONTROL Mostrar esquemas ad hoc]** para filtrar la lista de esquemas creados con campos con espacio de nombres para su uso exclusivo en un único conjunto de datos.

![La ficha [!UICONTROL Esquemas] del área de trabajo [!UICONTROL Examinar] con el panel de filtros resaltado.](../images/ui/explore/filters.png)

En la ficha [!UICONTROL Relación] del área de trabajo [!UICONTROL Esquemas], puede filtrar la lista de relaciones en función de cuatro criterios. Los filtros incluyen [!UICONTROL esquema Source], [!UICONTROL esquema de destino], [!UICONTROL clase Source] y [!UICONTROL clase de destino]. La siguiente tabla proporciona una descripción de los filtros.

| Filtro | Descripción |
|-----------------------------------|------------|
| [!UICONTROL esquema de Source] | Para ver todas las relaciones en las que el esquema seleccionado sea el punto de partida o el &quot;origen&quot;, seleccione un esquema en el menú desplegable [!UICONTROL esquema de Source]. |
| [!UICONTROL Esquema de destino] | Para ver todas las relaciones en las que el esquema seleccionado sea el destino o el &quot;destino&quot;, seleccione un esquema en el menú desplegable [!UICONTROL Esquema de destino]. |
| [!UICONTROL Clase de Source] | Para filtrar relaciones basadas en la clase del esquema de inicio, seleccione una clase del menú desplegable [!UICONTROL Source class]. |
| [!UICONTROL Clase de destino] | Para mostrar las relaciones que terminan con esquemas de una clase específica, seleccione una clase en el menú desplegable [!UICONTROL Clase de destino]. |

{style="table-layout:auto"}

![Ficha Relaciones con la sección de filtros resaltada.](../images/ui/explore/relationships-filter.png)

También puede utilizar la barra de búsqueda para reducir aún más los resultados.

![La ficha Examinar del área de trabajo de esquemas con el campo de búsqueda resaltado.](../images/ui/explore/search.png)

Los recursos mostrados en los resultados de búsqueda se ordenan primero por coincidencias de título y luego por coincidencias de descripción. A su vez, cuanto más coincidan las palabras en cualquiera de estas categorías, más alto aparecerá el recurso en la lista.

Cuando haya encontrado el recurso que desea explorar, seleccione su nombre en la lista para ver su estructura en el lienzo.

## Exploración de un recurso XDM en el lienzo {#explore}

Una vez seleccionado un recurso, su estructura se abre en el lienzo.

![El lienzo del espacio de trabajo de tipos de datos que muestra el tipo de datos de Commerce.](../images/ui/explore/canvas.png)

Todos los campos de tipo de objeto que contienen subpropiedades se contraen de forma predeterminada la primera vez que aparecen en el lienzo. Para mostrar las subpropiedades de cualquier campo, seleccione el icono junto a su nombre.

![El lienzo del espacio de trabajo de tipos de datos con campos expandidos y subpropiedades resaltadas.](../images/ui/explore/field-expand.png)

### Indicador de clase y grupo de campos estándar {#standard-class-and-field-group-indicator}

Dentro del Editor de esquemas, las clases y los grupos de campos estándar (generados por Adobe) se indican con el icono de candado (![Un icono de candado.](/help/images/icons/lock-closed.png). El candado aparece en el carril izquierdo junto al nombre de la clase o del grupo de campos, así como junto a cualquier campo del diagrama de esquema que forme parte de un recurso generado por el sistema.

![Editor de esquemas con el icono de candado resaltado](../images/ui/explore/schema-editor-padlock-icon.png)

Consulte la documentación de [Agregar campos personalizados a grupos de campos estándar](./resources/schemas.md) para obtener instrucciones. No se puede editar una clase estándar.

### Campos generados por el sistema {#system-fields}

Algunos nombres de campo van precedidos de un guion bajo, como `_repo` y `_id`. Representan marcadores de posición para campos que el sistema generará y asignará automáticamente a medida que se incorporen los datos.

Como tal, la mayoría de estos campos deben excluirse de la estructura de los datos al ingerirlos en Experience Platform. La principal excepción a esta regla es el campo [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), en el cual todos los campos XDM creados en su organización deben tener un espacio de nombres.

### Tipos de datos {#data-types}

Para cada campo que se muestra en el lienzo, su tipo de datos correspondiente se muestra junto a su nombre, lo que indica de un vistazo el tipo de datos que ese campo espera para la ingesta.

![El tipo de datos de la dirección postal se muestra en el lienzo con los tipos de datos asociados resaltados.](../images/ui/explore/data-types.png)

Cualquier tipo de datos que se agregue entre corchetes (`[]`) representa una matriz de ese tipo de datos en particular. Por ejemplo, un tipo de datos de **[!UICONTROL Cadena]\[]** indica que el campo espera una matriz de valores de cadena. Un tipo de datos de **[!UICONTROL Elemento de pago]\[]** indica una matriz de objetos que se ajustan al tipo de datos de [!UICONTROL Elemento de pago].

Si un campo de matriz se basa en un tipo de objeto, puede seleccionar su icono en el lienzo para mostrar los atributos esperados para cada elemento de matriz.

![Objeto del lienzo con un campo de matriz resaltado y los atributos esperados para cada elemento de matriz mostrado.](../images/ui/explore/array-type.png)

### [!UICONTROL Propiedades de campo] {#field-properties}

Cuando selecciona el nombre de cualquier campo en el lienzo, el carril derecho se actualiza para mostrar detalles sobre ese campo en **[!UICONTROL Propiedades del campo]**. Esto puede incluir una descripción del caso de uso previsto del campo, los valores predeterminados, los patrones, los formatos, si el campo es obligatorio o no, y más.

![Campo seleccionado del tipo de datos Commerce con las propiedades de campo resaltadas.](../images/ui/explore/field-properties.png)

Si el campo que está inspeccionando es un campo de enumeración, el carril derecho también mostrará los valores aceptables que el campo espera recibir.

![Editor de esquemas con un campo seleccionado y valores de enumeración y nombres para mostrar resaltados en el carril de propiedades del campo.](../images/ui/explore/enum-field.png)

### Campos de identidad {#identity}

Al inspeccionar esquemas que contienen campos de identidad, estos campos se enumeran en el carril izquierdo bajo la clase o el grupo de campos que los proporciona al esquema. Seleccione el nombre del campo de identidad en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con que esté anidado.

Los campos de identidad se resaltan en el lienzo con un icono de huella digital (![Imagen de icono de huella digital](/help/images/icons/identity-service.png)). Si selecciona el nombre del campo de identidad, puede ver información adicional como el [área de nombres de identidad](../../identity-service/features/namespaces.md) y si el campo es o no la identidad principal del esquema.

![Editor de esquemas con la identidad del esquema resaltada en el carril izquierdo, el campo resaltado en el diagrama de esquema y el área de nombres de identidad resaltada en las propiedades del campo.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte la guía de [definición de campos de identidad](./fields/identity.md) para obtener más información sobre los campos de identidad y su relación con los servicios de Experience Platform descendentes.

### Campos de relación {#relationship}

Si está inspeccionando un esquema que contiene un campo de relación, el campo aparecerá en el carril izquierdo bajo **[!UICONTROL Relaciones]**. Seleccione el nombre del campo de relación en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con que esté anidado. Los campos de relación también se resaltan de forma exclusiva en el lienzo, mostrando el nombre del esquema de referencia al que está vinculado el campo. Para las organizaciones con capacidades B2B, se pueden escribir nombres de relación personalizados que se mostrarán en el lienzo en estos casos.

![Editor de esquemas con el campo de relación y Editar relación resaltados.](../images/ui/explore/relationship-field.png)

Para ver el área de nombres de identidad de la identidad principal del esquema de referencia, seleccione el campo de relación y, a continuación, **[!UICONTROL Editar relación]** en la barra lateral de [!UICONTROL Propiedades del campo]. Los parámetros de la relación se muestran en el cuadro de diálogo [!UICONTROL Editar relación] que aparece.

![Cuadro de diálogo Editar relación con los parámetros de relación mostrados.](../images/ui/explore/edit-relationship-dialog.png)

Consulte el tutorial sobre [creación de una relación en la interfaz de usuario](../tutorials/relationship-ui.md) para obtener más información sobre el uso de relaciones en esquemas XDM.

## Pasos siguientes

En este documento se explica cómo explorar los recursos XDM existentes en la interfaz de usuario de Experience Platform. Para obtener más información sobre las distintas características del área de trabajo [!UICONTROL Esquemas] y [!DNL Schema Editor], vea la información general sobre el área de trabajo [[!UICONTROL Esquemas]](./overview.md).
