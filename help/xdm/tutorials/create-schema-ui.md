---
keywords: Experience Platform;inicio;temas populares;iu;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Crear un esquema con el editor de esquemas
topic-legacy: tutorial
type: Tutorial
description: Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# Cree un esquema utilizando la variable [!DNL Schema Editor]

La interfaz de usuario de Adobe Experience Platform le permite crear y administrar [!DNL Experience Data Model] esquemas (XDM) en un lienzo visual interactivo denominado [!DNL Schema Editor]. Este tutorial explica cómo crear un esquema con el [!DNL Schema Editor].

>[!NOTE]
>
>Para fines de demostración, los pasos de este tutorial implican la creación de un esquema de ejemplo que describa los miembros de un programa de fidelidad de cliente. Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda que primero siga con la creación del esquema de ejemplo para conocer las capacidades de la variable [!DNL Schema Editor].

Si prefiere componer un esquema utilizando la variable [!DNL Schema Registry] En su lugar, comience leyendo la [[!DNL Schema Registry] guía para desarrolladores](../api/getting-started.md) antes de intentar el tutorial en [creación de un esquema con la API](create-schema-api.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los distintos aspectos de Adobe Experience Platform implicados en la creación de esquemas. Antes de comenzar este tutorial, consulte la documentación de los siguientes conceptos:

* [[!DNL Experience Data Model (XDM)]](../home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../schema/composition.md): Una descripción general de los esquemas XDM y sus componentes básicos, incluidas las clases, los grupos de campos de esquema, los tipos de datos y los campos individuales.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Abra el [!UICONTROL Esquemas] workspace {#browse}

La variable [!UICONTROL Esquemas] espacio de trabajo [!DNL Platform] La interfaz de usuario proporciona una visualización del [!DNL Schema Library], lo que le permite ver y administrar los esquemas disponibles para su organización. El espacio de trabajo también incluye la variable [!DNL Schema Editor], el lienzo en el que se puede componer un esquema a lo largo de este tutorial.

Tras iniciar sesión [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir **[!UICONTROL Esquemas]** espacio de trabajo. La variable **[!UICONTROL Examinar]** muestra una lista de esquemas (una representación del [!DNL Schema Library]) que puede ver y personalizar. La lista incluye el nombre, el tipo, la clase y el comportamiento (registro o serie temporal) en los que se basa el esquema, así como la fecha y la hora de la última modificación del esquema.

Consulte la guía de [exploración de recursos XDM existentes en la interfaz de usuario](../ui/explore.md) para obtener más información.

## Crear y asignar un nombre a un esquema {#create}

Para empezar a componer un esquema, seleccione **[!UICONTROL Crear esquema]** en la esquina superior derecha del **[!UICONTROL Esquemas]** espacio de trabajo. Aparece un menú desplegable que le ofrece la opción de elegir entre las clases principales [!UICONTROL Perfil individual XDM] y [!UICONTROL XDM ExperienceEvent]. Si estas clases no se ajustan a sus necesidades, también puede seleccionar **[!UICONTROL Examinar]** para elegir entre otras clases disponibles o [crear una nueva clase](#create-new-class).

Para los fines de este tutorial, seleccione **[!UICONTROL Perfil individual XDM]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Dado que eligió una clase XDM estándar en la que basar el esquema, la variable **[!UICONTROL Agregar grupo de campos]** , lo que le permite empezar a añadir campos inmediatamente al esquema. Por ahora, seleccione **[!UICONTROL Cancelar]** para salir del cuadro de diálogo.

![](../images/tutorials/create-schema/cancel-field-group.png)

La variable [!DNL Schema Editor] aparece. Este es el lienzo sobre el que compondrá el esquema. Se crea automáticamente un esquema sin título en la variable **[!UICONTROL Estructura]** del lienzo al llegar al editor, junto con los campos estándar incluidos en todos los esquemas basados en esa clase. La clase asignada para el esquema también aparece en **[!UICONTROL Clase]** en **[!UICONTROL Composición]** para obtener más información.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Puede [cambiar la clase de un esquema](#change-class) en cualquier momento durante el proceso de composición inicial antes de guardar el esquema, pero esto debe hacerse con mucha precaución. Los grupos de campos solo son compatibles con ciertas clases y, por lo tanto, al cambiar la clase se restablecerá el lienzo y los campos que haya agregado.

Utilice los campos del lado derecho del editor para proporcionar un nombre para mostrar y una descripción opcional para el esquema. Una vez introducido un nombre, el lienzo se actualiza para reflejar el nuevo nombre del esquema.

![](../images/tutorials/create-schema/name_schema.png)

Hay que tener en cuenta varias consideraciones importantes a la hora de decidir un nombre para el esquema:

* Los nombres de esquema deben ser cortos y descriptivos para que el esquema se pueda encontrar fácilmente más adelante.
* Los nombres de esquema deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro. Por ejemplo, si su organización tiene programas de fidelidad separados para diferentes marcas, sería aconsejable nombrar al esquema &quot;Miembros de fidelidad de marca A&quot; para que sea más fácil distinguir de otros esquemas relacionados con la fidelidad que podría definir más adelante.
* También puede utilizar la descripción del esquema para proporcionar cualquier información contextual adicional relacionada con el esquema.

Este tutorial compone un esquema para introducir datos relacionados con los miembros de un programa de fidelidad y, por lo tanto, el esquema se denomina &quot;Miembros de fidelidad&quot;.

## Agregar un grupo de campos {#field-group}

Ahora puede empezar a añadir campos al esquema añadiendo grupos de campos. Un grupo de campos es un grupo de uno o más campos que a menudo se utilizan juntos para describir un concepto en particular. Este tutorial utiliza grupos de campos para describir los miembros del programa de fidelidad y capturar información clave como nombre, cumpleaños, número de teléfono, dirección, etc.

Para añadir un grupo de campos, seleccione **[!UICONTROL Agregar]** en el **[!UICONTROL Grupos de campo]** subsección.

![](../images/tutorials/create-schema/add-field-group-button.png)

Aparece un nuevo cuadro de diálogo que muestra una lista de los grupos de campos disponibles. Cada grupo de campos solo está diseñado para utilizarse con una clase específica, por lo que el cuadro de diálogo solo enumera los grupos de campos compatibles con la clase seleccionada (en este caso, la variable [!DNL XDM Individual Profile] clase ). Si utiliza una clase XDM estándar, la lista de grupos de campos se ordenará de forma inteligente según la popularidad de uso.

![](../images/tutorials/create-schema/field-group-popularity.png)

Si se selecciona un grupo de campos de la lista, este aparecerá en el carril derecho. Si lo desea, puede seleccionar varios grupos de campos, agregándolos a la lista en el carril derecho antes de confirmarlos. Además, aparece un icono en el lado derecho del grupo de campos seleccionado que permite obtener una vista previa de la estructura de los campos que proporciona.

![](../images/tutorials/create-schema/preview-field-group-button.png)

Al obtener una vista previa de un grupo de campos, se proporciona una descripción detallada del esquema del grupo de campos en el carril derecho. También puede navegar por los campos del grupo de campos en el lienzo proporcionado. A medida que selecciona diferentes campos, el carril derecho se actualiza para mostrar detalles sobre el campo en cuestión. Select **[!UICONTROL Atrás]** cuando haya terminado de obtener la vista previa para volver al cuadro de diálogo de selección de grupos de campos.

![](../images/tutorials/create-schema/preview-field-group.png)

Para este tutorial, seleccione la **[!UICONTROL Detalles demográficos]** grupo de campos y, a continuación, seleccione **[!UICONTROL Agregar grupo de campos]**.

![](../images/tutorials/create-schema/demographic-details.png)

El lienzo del esquema vuelve a aparecer. La variable **[!UICONTROL Grupos de campo]** ahora enumera &quot;[!UICONTROL Detalles demográficos]&quot; y **[!UICONTROL Estructura]** incluye los campos contribuidos por el grupo de campos. Puede seleccionar el nombre del grupo de campos en la **[!UICONTROL Grupos de campo]** para resaltar los campos específicos que proporciona dentro del lienzo.

![](../images/tutorials/create-schema/demographic-details-structure.png)

Este grupo de campos contribuye con varios campos bajo el nombre de nivel superior `person` con el tipo de datos &quot;[!UICONTROL Persona]&quot;. Este grupo de campos describe información sobre un individuo, incluido el nombre, la fecha de nacimiento y el sexo.

>[!NOTE]
>
>Recuerde que los campos pueden utilizar tipos escalares (como cadena, entero, matriz o fecha), así como cualquier tipo de datos (un grupo de campos que representa un concepto común) definido dentro de la variable [!DNL Schema Registry].

Observe que la variable `name` El campo tiene un tipo de datos de &quot;[!UICONTROL Nombre de la persona]&quot;, lo que significa que también describe un concepto común y contiene subcampos relacionados con nombres como nombre, apellido, título de cortesía y sufijo.

Seleccione los diferentes campos dentro del lienzo para mostrar los campos adicionales que contribuyen a la estructura del esquema.

## Añadir otro grupo de campos {#field-group-2}

Ahora puede repetir los mismos pasos para agregar otro grupo de campos. Cuando vea la variable **[!UICONTROL Agregar grupo de campos]** esta vez, observe que la variable[!UICONTROL Detalles demográficos]&quot; grupo de campos se ha atenuado y la casilla que está junto a él no se puede seleccionar. Esto evita que se dupliquen accidentalmente los grupos de campos que ya se han incluido en el esquema actual.

Para este tutorial, seleccione la opción[!DNL Personal Contact Details]&quot; grupo de campos del cuadro de diálogo y, a continuación, seleccione **[!UICONTROL Agregar grupo de campos]** para agregarlo al esquema.

![](../images/tutorials/create-schema/personal-contact-details.png)

Una vez añadido, el lienzo vuelve a aparecer. &quot;[!UICONTROL Detalles de contacto personal]&quot; ahora aparece en **[!UICONTROL Grupos de campo]** en el **[!UICONTROL Composición]** , y se han añadido campos para la dirección principal, el teléfono móvil y mucho más en **[!UICONTROL Estructura]**.

Similar a la variable `name` , los campos que acaba de añadir representan conceptos de varios campos. Por ejemplo, `homeAddress` tiene un tipo de datos de &quot;[!UICONTROL Dirección postal]&quot; y `mobilePhone` tiene un tipo de datos de &quot;[!UICONTROL Número de teléfono]&quot;. Puede seleccionar cada uno de estos campos para expandirlos y ver los campos adicionales incluidos en el tipo de datos.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## Definir un grupo de campos personalizado {#define-field-group}

La variable[!UICONTROL Miembros de fidelidad]&quot; el esquema está diseñado para capturar datos relacionados con los miembros de un programa de fidelidad, por lo que requerirá algunos campos específicos relacionados con la fidelidad.

Hay una [!UICONTROL Detalles de fidelidad] grupo de campos que se puede agregar al esquema para capturar campos comunes relacionados con un programa de fidelidad. Aunque se le recomienda encarecidamente que utilice grupos de campos estándar para representar los conceptos capturados por los esquemas, es posible que la estructura del grupo de campos de lealtad estándar no pueda capturar todos los datos relevantes para su programa de fidelidad en particular. En esta situación, puede definir un nuevo grupo de campos personalizados para capturar estos campos.

Abra el **[!UICONTROL Agregar grupo de campos]** de nuevo, pero esta vez seleccione **[!UICONTROL Crear nuevo grupo de campos]** cerca de la parte superior. A continuación, se le pedirá que proporcione un nombre para mostrar y una descripción para su grupo de campos.

![](../images/tutorials/create-schema/create-new-field-group.png)

Al igual que con los nombres de clase, el nombre del grupo de campos debe ser corto y sencillo, describiendo lo que el grupo de campos contribuirá al esquema. Estas también son únicas, por lo que no podrá reutilizar el nombre y, por lo tanto, debe asegurarse de que sea lo suficientemente específico.

Para este tutorial, asigne al nuevo grupo de campos el nombre &quot;Detalles de lealtad&quot;.

Select **[!UICONTROL Agregar grupo de campos]** para volver a la [!DNL Schema Editor]. &quot;[!UICONTROL Detalles de fidelidad]&quot; debería aparecer en **[!UICONTROL Grupos de campo]** a la izquierda del lienzo, pero aún no hay campos asociados a él y, por lo tanto, no aparecen campos nuevos en **[!UICONTROL Estructura]**.

## Agregue campos al grupo de campos {#field-group-fields}

Ahora que ha creado el grupo de campos &quot;Detalles de lealtad&quot;, ha llegado el momento de definir los campos que el grupo de campos contribuirá al esquema.

Para empezar, seleccione el nombre del grupo de campos en la **[!UICONTROL Grupos de campo]** para obtener más información. Una vez hecho esto, las propiedades del grupo de campos aparecen en el lado derecho del editor y en una **plus (+)** aparece junto al nombre del esquema debajo de **[!UICONTROL Estructura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleccione el **plus (+)** junto a[!DNL Loyalty Members]&quot; para crear un nuevo nodo en la estructura. Este nodo (llamado `_tenantId` en este ejemplo) representa el ID de inquilino de la organización IMS, precedido por un guion bajo. La presencia del ID de inquilino indica que los campos que está agregando están contenidos en el espacio de nombres de su organización.

En otras palabras, los campos que agregue son exclusivos de su organización y se guardarán en la variable [!DNL Schema Registry] en un área específica accesible solo para su organización. Los campos que defina siempre deben agregarse al espacio de nombres del inquilino para evitar conflictos con nombres de otras clases estándar, grupos de campos, tipos de datos y campos.

Dentro de ese nodo espaciado con nombres se encuentra &quot;[!UICONTROL Campo nuevo]&quot;. Este es el comienzo del &quot;[!UICONTROL Detalles de fidelidad]&quot; grupo de campos.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Con los controles del lado derecho del editor, comience creando un `loyalty` campo con tipo &quot;[!UICONTROL Objeto]&quot; que se utilizará para incluir los campos relacionados con la lealtad. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Los cambios se aplican y el `loyalty` aparece. Seleccione el **plus (+)** junto al objeto para añadir campos adicionales relacionados con la lealtad. Un &quot;[!UICONTROL Campo nuevo]&quot; y **[!UICONTROL Propiedades del campo]** está visible en el lado derecho del lienzo.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requiere la siguiente información:

* **[!UICONTROL Nombre del campo]:** El nombre del campo, escrito en el caso del camello. Ejemplo: loyaltyLevel
* **[!UICONTROL Nombre para mostrar]:** El nombre del campo, escrito en el caso del título. Ejemplo: Nivel de fidelidad
* **[!UICONTROL Tipo]:** Tipo de datos del campo. Esto incluye tipos escalares básicos y cualquier tipo de datos definido en la variable [!DNL Schema Registry]. Ejemplos: [!UICONTROL Cadena], [!UICONTROL Número entero], [!UICONTROL Booleano], [!UICONTROL Persona], [!UICONTROL Dirección], [!UICONTROL Número de teléfono], etc.
* **[!UICONTROL Descripción]:** Se debe incluir una descripción opcional del campo, escrita en caso de sentencia, con un máximo de 200 caracteres.

El primer campo para la variable `Loyalty` el objeto será una cadena llamada `loyaltyId`. Al configurar el tipo del nuevo campo como &quot;[!UICONTROL Cadena]&quot;, **[!UICONTROL Propiedades del campo]** se rellena con varias opciones para la aplicación de restricciones, entre las que se incluyen el valor predeterminado, el formato y la longitud máxima.

![](../images/tutorials/create-schema/string_constraints.png)

Hay diferentes opciones de restricción disponibles en función del tipo de datos seleccionado. Since `loyaltyId` será una dirección de correo electrónico, seleccione &quot;[!UICONTROL email]&quot; de **[!UICONTROL Formato]** menú desplegable. Select **[!UICONTROL Aplicar]** para aplicar los cambios.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Añadir más campos al grupo de campos {#field-group-fields-2}

Ahora que ha añadido la variable `loyaltyId` , puede agregar campos adicionales para capturar información relacionada con la lealtad, como:

* Puntos (entero)
* Miembro desde (fecha)

Para añadir cada campo al esquema, seleccione la opción **plus (+)** junto al icono `loyalty` y rellene la información requerida.

Cuando se complete, el objeto Lealtad contendrá campos para ID de fidelidad, puntos y desde entonces.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Añadir un campo de enumeración al grupo de campos {#enum}

Al definir campos en la variable [!DNL Schema Editor], hay algunas opciones adicionales que se pueden aplicar a tipos de campo básicos para proporcionar más restricciones en los datos que el campo puede contener. Los casos de uso de estas restricciones se explican en la siguiente tabla:

| Restricción | Descripción |
| --- | --- |
| [!UICONTROL Requerido] | Indica que el campo es necesario para la ingesta de datos. Cualquier dato cargado en un conjunto de datos basado en este esquema que no contenga este campo fallará tras la ingesta. |
| [!UICONTROL Matriz] | Indica que el campo contiene una matriz de valores, cada uno con el tipo de datos especificado. Por ejemplo, si se utiliza esta restricción en un campo con un tipo de datos de &quot;[!UICONTROL Cadena]&quot; especifica que el campo contendrá una matriz de cadenas. |
| [!UICONTROL Enum] | Indica que este campo debe contener uno de los valores de una lista enumerada de valores posibles. |
| [!UICONTROL Identidad] | Indica que este campo es de identidad. Se proporciona más información sobre los campos de identidad [más adelante en este tutorial](#identity-field). |
| [!UICONTROL Relación] | Mientras que las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-Time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. La variable [!UICONTROL Relación] constraint indica que este campo hace referencia a la identidad principal de un esquema basado en una clase diferente, lo que implica una relación entre los dos esquemas. Consulte el tutorial en [definición de una relación](./relationship-ui.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Los campos requeridos, de identidad o de relación se muestran en el carril izquierdo, lo que permite localizar estos campos fácilmente independientemente de la complejidad del esquema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, la variable [!DNL "loyalty"] del esquema requiere un nuevo campo de enumeración que describa el &quot;nivel de lealtad&quot; de un cliente, donde el valor solo puede ser una de las cuatro opciones posibles. Para añadir este campo al esquema, seleccione el **plus (+)** junto a `loyalty` y rellene los campos obligatorios para **[!UICONTROL Nombre del campo]** y **[!UICONTROL Nombre para mostrar]**. Para **[!UICONTROL Tipo]**, seleccione &quot;[!UICONTROL Cadena]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Aparecen casillas de verificación adicionales para el campo una vez que se ha seleccionado su tipo, incluidas las casillas de verificación para **[!UICONTROL Matriz]**, **[!UICONTROL Enum]** y **[!UICONTROL Identidad]**.

Seleccione el **[!UICONTROL Enum]** para abrir la **[!UICONTROL Valores de enumeración]** a continuación. Aquí puede introducir el **[!UICONTROL Valor]** (en camelCase) y **[!UICONTROL Etiqueta]** (un nombre opcional y fácil de leer en el caso del título) para cada nivel de lealtad aceptable.

Cuando haya completado todas las propiedades del campo, seleccione **[!UICONTROL Aplicar]** para agregar el[!DNL loyaltyLevel]&quot; al `loyalty` objeto.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversión de un objeto de varios campos en un tipo de datos {#datatype}

La variable `loyalty` ahora contiene varios campos específicos de lealtad y representa una estructura de datos común que podría ser útil en otros esquemas. La variable [!DNL Schema Editor] permite aplicar fácilmente objetos de varios campos reutilizables convirtiendo la estructura de esos objetos en tipos de datos.

Los tipos de datos permiten el uso coherente de estructuras de varios campos y proporcionan más flexibilidad que un grupo de campos, ya que se pueden utilizar en cualquier lugar dentro de un esquema. Esto se hace estableciendo el **[!UICONTROL Tipo]** a la de cualquier tipo de datos definido en la variable [!DNL Schema Registry].

Para convertir la variable `loyalty` a un tipo de datos, seleccione `loyalty` campo bajo **[!UICONTROL Estructura]** y, a continuación, seleccione **[!UICONTROL Convertir en nuevo tipo de datos]** a la derecha del editor debajo de **[!UICONTROL Propiedades del campo]**. Aparece una ventana emergente verde que confirma que el objeto se ha convertido correctamente.

![](../images/tutorials/create-schema/convert-data-type.png)

Ahora, cuando se mira debajo **[!UICONTROL Estructura]**, puede ver que la variable `loyalty` El campo tiene un tipo de datos de &quot;[!DNL Loyalty]&quot; y los campos tienen iconos de bloqueo pequeños junto a ellos, lo que indica que ya no son campos individuales sino parte de un tipo de datos de varios campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

En un esquema futuro, ahora puede asignar un campo como &quot;[!DNL Loyalty]&quot; y automáticamente incluiría campos para ID, nivel de fidelidad, miembro desde y puntos.

>[!NOTE]
>
>También puede crear y editar tipos de datos personalizados de forma independiente de la edición de esquemas. Consulte la guía de [creación y edición de tipos de datos](../ui/resources/data-types.md) para obtener más información.

## Buscar y filtrar campos de esquema

El esquema ahora contiene varios grupos de campos además de los campos proporcionados por su clase base. Al trabajar con esquemas más grandes, puede seleccionar las casillas de verificación situadas junto a los nombres de los grupos de campos en el carril izquierdo para filtrar los campos mostrados únicamente a los proporcionados por los grupos de campos que le interesen.

![](../images/tutorials/create-schema/filter-by-field-group.png)

Si está buscando un campo específico en el esquema, también puede utilizar la barra de búsqueda para filtrar los campos mostrados por nombre, independientemente del grupo de campos en el que se proporcionen.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La función de búsqueda tiene en cuenta los filtros de grupo de campos seleccionados al mostrar los campos coincidentes. Si una consulta de búsqueda no muestra los resultados esperados, es posible que tenga que verificar que no está filtrando ningún grupo de campos relevante.

## Establecer un campo de esquema como campo de identidad {#identity-field}

La estructura de datos estándar que proporcionan los esquemas se puede aprovechar para identificar los datos que pertenecen al mismo individuo en múltiples fuentes, lo que permite varios casos de uso descendente como segmentación, informes, análisis de ciencia de datos, etc. Para unir datos en función de identidades individuales, los campos clave deben marcarse como [!UICONTROL Identidad] campos dentro de esquemas aplicables.

[!DNL Experience Platform] facilita la identificación de un campo de identidad mediante el uso de un **[!UICONTROL Identidad]** en la [!DNL Schema Editor]. Sin embargo, debe determinar qué campo es el mejor candidato para utilizarlo como identidad, en función de la naturaleza de los datos.

Por ejemplo, puede haber miles de miembros del programa de fidelidad que pertenezcan al mismo &quot;nivel de fidelidad&quot;, pero cada miembro del programa de fidelidad tiene un `loyaltyId` (que en este caso es la dirección de correo electrónico de cada miembro). El hecho de que `loyaltyId` es un identificador único para cada miembro lo convierte en un buen candidato para un campo de identidad, mientras que `loyaltyLevel` no.

>[!IMPORTANT]
>
>Los pasos que se describen a continuación abarcan cómo agregar un descriptor de identidad a un campo de esquema existente. Como alternativa a definir campos de identidad dentro de la estructura del propio esquema, también puede utilizar un `identityMap` para contener información de identidad en su lugar.
>
>Si planea usar `identityMap`, tenga en cuenta que anulará cualquier identidad principal que agregue al esquema directamente. Consulte la sección sobre `identityMap` en el [conceptos básicos de la guía de composición de esquemas](../schema/composition.md#identityMap) para obtener más información.

En el **[!UICONTROL Estructura]** del editor, seleccione `loyaltyId` y **[!UICONTROL Identidad]** la casilla de verificación aparece en **[!UICONTROL Propiedades del campo]**. Marque la casilla y la opción para establecerla como la **[!UICONTROL Identidad primaria]** aparece. Seleccione también este cuadro.

>[!NOTE]
>
>Cada esquema puede contener solo un campo de identidad principal. Una vez que se ha establecido un campo de esquema como identidad principal, recibirá un mensaje de error si más tarde intenta establecer otro campo de identidad en el esquema como principal.

A continuación, debe proporcionar una **[!UICONTROL Área de nombres de identidad]** en la lista de áreas de nombres predefinidas de la lista desplegable. Since `loyaltyId` es la dirección de correo electrónico del cliente, seleccione &quot;[!UICONTROL Correo electrónico]&quot; de la lista desplegable. Select **[!UICONTROL Aplicar]** para confirmar las actualizaciones de `loyaltyId` campo .

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obtener una lista de áreas de nombres estándar y sus definiciones, consulte la [[!DNL Identity Service] documentación](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Después de aplicar el cambio, aparece el icono para `loyaltyId` muestra un símbolo de huella digital que indica que ahora es un campo de identidad.

![](../images/tutorials/create-schema/identity-applied.png)

Ahora todos los datos incorporados a la variable `loyaltyId` se utilizará para ayudar a identificar a ese individuo y unir una sola vista de ese cliente. Para obtener más información sobre cómo trabajar con identidades en [!DNL Experience Platform], revise el [[!DNL Identity Service]](../../identity-service/home.md) documentación.

## Habilitar el esquema para utilizarlo en [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) aprovecha los datos de identidad en [!DNL Experience Platform] para proporcionar una vista holística de cada cliente individual. El servicio crea perfiles sólidos de 360° de atributos del cliente, así como cuentas con marca de tiempo de cada interacción que los clientes han tenido en cualquier sistema integrado con [!DNL Experience Platform].

Para que un esquema esté habilitado para su uso con [!DNL Real-Time Customer Profile], debe tener una identidad principal definida. Recibirá un mensaje de error si intenta habilitar un esquema sin definir primero una identidad principal.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para habilitar el esquema &quot;Miembros de lealtad&quot; para su uso en [!DNL Profile], comience por seleccionar &quot;[!DNL Loyalty Members]&quot; en el **[!UICONTROL Estructura]** del editor.

A la derecha del editor, se muestra información sobre el esquema, incluido su nombre para mostrar, descripción y tipo. Además de esta información, existe un **[!UICONTROL Perfil]** botón de alternancia.

![](../images/tutorials/create-schema/profile-toggle.png)

Select **[!UICONTROL Perfil]** y aparece una ventana emergente que le solicita que confirme que desea habilitar el esquema para [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una vez que se ha habilitado un esquema para [!DNL Real-Time Customer Profile] y guardadas, no se pueden deshabilitar.

Select **[!UICONTROL Habilitar]** para confirmar su elección. Puede seleccionar el **[!UICONTROL Perfil]** volver a alternar para deshabilitar el esquema si lo desea, pero una vez guardado el esquema mientras [!DNL Profile] está activada, ya no se puede desactivar.

## Pasos siguientes y recursos adicionales

Ahora que ha terminado de componer el esquema, puede ver el esquema completo en el lienzo. Select **[!UICONTROL Guardar]** y el esquema se guardará en la variable [!DNL Schema Library], lo que hace que el [!DNL Schema Registry].

El nuevo esquema ahora se puede usar para introducir datos en [!DNL Platform]. Recuerde que una vez que el esquema se ha utilizado para introducir datos, solo se pueden realizar cambios aditivos. Consulte la [conceptos básicos de la composición del esquema](../schema/composition.md) para obtener más información sobre el control de versiones de esquemas.

Ahora puede seguir el tutorial en [definición de una relación de esquema en la interfaz de usuario](./relationship-ui.md) para agregar un nuevo campo de relación al esquema &quot;Miembros de lealtad&quot;.

El esquema &quot;Miembros de lealtad&quot; también está disponible para su visualización y administración mediante la variable [!DNL Schema Registry] API. Para empezar a trabajar con la API, comience leyendo el [[!DNL Schema Registry API] guía para desarrolladores](../api/getting-started.md).

### Recursos de vídeo

>[!WARNING]
>
>La variable [!DNL Platform] La IU que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

El siguiente vídeo muestra cómo crear un esquema simple en la [!DNL Platform] IU.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

El siguiente vídeo pretende reforzar su comprensión del trabajo con grupos de campo y clases.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre el uso de la variable [!DNL Schema Editor].

### Crear una nueva clase {#create-new-class}

[!DNL Experience Platform] proporciona la flexibilidad para definir un esquema basado en una clase que sea única para su organización. Para aprender a crear una nueva clase, consulte la guía de [creación y edición de clases en la interfaz de usuario](../ui/resources/classes.md#create).

### Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Los grupos de campos solo son compatibles con ciertas clases y, por lo tanto, al cambiar la clase se restablecerá el lienzo y los campos que haya agregado.

Para aprender a cambiar la clase de un esquema, consulte la guía de [administración de esquemas en la interfaz de usuario](../ui/resources/schemas.md).
