---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Crear un esquema con el editor de esquemas.
topic: tutorials
description: Este tutorial trata los pasos para crear un esquema con el Editor de Esquemas en Experience Platform.
translation-type: tm+mt
source-git-commit: ed1f2fdac0f9c977d11c867327c084353c1bcd0f
workflow-type: tm+mt
source-wordcount: '3528'
ht-degree: 0%

---


# Cree un esquema con la variable [!DNL Schema Editor]

La interfaz de usuario de Adobe Experience Platform le permite crear y administrar esquemas [!DNL Experience Data Model] (XDM) en un lienzo visual interactivo denominado [!DNL Schema Editor]. En este tutorial se explica cómo crear un esquema con el [!DNL Schema Editor].

>[!NOTE]
>
>Para demostraciones, los pasos de este tutorial incluyen la creación de un esquema de ejemplo que describe a los miembros de un programa de lealtad del cliente. Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda que primero siga la creación del esquema de ejemplo para conocer las funciones del [!DNL Schema Editor].

Si prefiere componer un esquema con la [!DNL Schema Registry] API en su lugar, consulte la guía [[!DNL Schema Registry] del](../api/getting-started.md) desarrollador antes de intentar el tutorial sobre la [creación de un esquema con la API](create-schema-api.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos aspectos de Adobe Experience Platform relacionados con la creación de esquemas. Antes de comenzar este tutorial, consulte la documentación de los siguientes conceptos:

* [[!Modelo de datos de experiencia DNL (XDM)]](../home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Información general sobre los esquemas XDM y sus componentes, incluidas clases, mezclas, tipos de datos y campos.
* [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Examinar esquemas existentes en el espacio de trabajo [!UICONTROL Esquemas] {#browse}

El espacio de trabajo [!UICONTROL Esquemas] de la [!DNL Platform] interfaz de usuario proporciona una visualización de la [!DNL Schema Library], lo que le permite administrar vistas de los esquemas disponibles para su organización. El espacio de trabajo también incluye el [!DNL Schema Editor], el lienzo en el que puede componer un esquema a lo largo de este tutorial.

Después de iniciar sesión [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir el espacio de trabajo de **[!UICONTROL Esquemas]** . La ficha **[!UICONTROL Examinar]** muestra una lista de esquemas (una representación del [!DNL Schema Library]) que se pueden vista y personalizar. La lista incluye el nombre, el tipo, la clase y el comportamiento (registro o serie temporal) en los que se basa el esquema, así como la fecha y la hora en que se modificó el esquema por última vez.

Seleccione el icono de filtro situado junto a la barra de búsqueda para utilizar las capacidades de filtrado de todos los recursos del Registro, incluidos los tipos de datos, las clases y las mezclas. También puede filtrar en función de si los recursos son propiedad de Adobe o de su organización, y si se han habilitado para su uso en [!DNL Real-time Customer Profile].

![](../images/tutorials/create-schema/schemas_filter.png)

## Crear y asignar un nombre a un esquema {#create}

Para empezar a componer un esquema, seleccione **[!UICONTROL Crear Esquema]** en la esquina superior derecha del espacio de trabajo de **[!UICONTROL Esquemas]** . Aparece un menú desplegable que le ofrece la opción de elegir entre las clases principales [!UICONTROL XDM Individual Perfil] y [!UICONTROL XDM ExperienceEvent], o de examinar otras clases disponibles. Para los fines de este tutorial, seleccione Perfil **[!UICONTROL individual]** XDM.

![](../images/tutorials/create-schema/create_schema_button.png)

Aparece [!DNL Schema Editor] . Este es el lienzo sobre el cual compondrás tu esquema. Al llegar al editor, se crea automáticamente un esquema sin título en la sección **[!UICONTROL Estructura]** del lienzo, junto con los campos estándar incluidos en todos los esquemas basados en la clase de Perfil [!UICONTROL individual] XDM. La clase asignada para el esquema se muestra en **[!UICONTROL Clase]** en la sección **[!UICONTROL Composición]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Puede [cambiar la clase de un esquema](#change-class) en cualquier momento durante el proceso de composición inicial antes de guardar el esquema, pero esto debe hacerse con extrema precaución. Las mezclas solo son compatibles con determinadas clases y, por lo tanto, si se cambia la clase, se restablecerán el lienzo y los campos que se hayan agregado.

Utilice los campos del lado derecho del editor para proporcionar un nombre para mostrar y una descripción opcional del esquema. Una vez introducido un nombre, el lienzo se actualiza para reflejar el nuevo nombre del esquema.

![](../images/tutorials/create-schema/name_schema.png)

A la hora de decidir un nombre para el esquema, hay que tener en cuenta varias consideraciones importantes:

* Los nombres de los esquemas deben ser cortos y descriptivos para que el esquema pueda encontrarse más adelante.
* Los nombres de los esquemas deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro. Por ejemplo: si su organización tiene programas de lealtad separados para diferentes marcas, sería aconsejable nombrar a su esquema &quot;Miembros de lealtad de la marca A&quot; para que sea más fácil distinguir de otros esquemas relacionados con la lealtad que pueda definir más adelante.
* También puede utilizar la descripción del esquema para proporcionar cualquier información contextual adicional relacionada con el esquema.

Este tutorial contiene un esquema para ingestar datos relacionados con los miembros de un programa de lealtad y, por lo tanto, el esquema se denomina &quot;Miembros de lealtad&quot;.

## Añadir una mezcla {#mixin}

Ahora puede empezar a agregar campos al esquema agregando mezclas. Una mezcla es un grupo de uno o más campos que se utilizan a menudo juntos para describir un concepto en particular. Este tutorial utiliza mezclas para describir los miembros del programa de lealtad y capturar información clave como nombre, cumpleaños, número de teléfono, dirección, etc.

Para agregar una mezcla, seleccione **[!UICONTROL Añadir]** en la subsección **[!UICONTROL Mezclas]** .

![](../images/tutorials/create-schema/add_mixin_button.png)

Aparece un nuevo cuadro de diálogo, que muestra una lista de mezclas disponibles. Cada mezcla está destinada únicamente a utilizarse con una clase específica, por lo que el cuadro de diálogo sólo lista mezclas compatibles con la clase seleccionada (en este caso, la [!DNL XDM Individual Profile] clase).

La selección de una mezcla de la lista hace que aparezca en el carril derecho. Además, aparece un icono en el lado derecho de la mezcla seleccionada que permite la previsualización de la estructura de los campos que proporciona. Seleccione la mezcla Detalles **[!UICONTROL de persona de]** Perfil y, a continuación, seleccione **[!UICONTROL Añadir mezcla]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

El lienzo del esquema vuelve a aparecer. La sección **[!UICONTROL Mezclas]** ahora lista &quot;Detalles[!UICONTROL de persona de]Perfil&quot; y la sección **[!UICONTROL Estructura]** incluye los campos que la mezcla ha contribuido. Puede seleccionar el nombre de la mezcla en la sección **[!UICONTROL Mezclas]** para resaltar los campos específicos que proporciona dentro del lienzo.

![](../images/tutorials/create-schema/person_details_structure.png)

Esta combinación aporta varios campos bajo el nombre de nivel superior &quot;[!UICONTROL persona]&quot; con el tipo de datos &quot;[!UICONTROL Persona]&quot;. Este grupo de campos describe información sobre un individuo, incluido el nombre, la fecha de nacimiento y el sexo.

>[!NOTE]
>
>Recuerde que los campos pueden utilizar tipos escalares (como cadena, entero, matriz o fecha), así como cualquier tipo de datos (un grupo de campos que representa un concepto común) definido dentro del [!DNL Schema Registry].

Observe que el campo &quot;[!UICONTROL nombre]&quot; tiene un tipo de datos de &quot;nombrecompleto&quot;, lo que significa que también describe un concepto común y contiene subcampos relacionados con el nombre, como nombre, apellidos, título de cortesía y sufijo.

Seleccione los distintos campos dentro del lienzo para ver los campos adicionales que contribuyen a la estructura de esquema.

## Añadir otra mezcla {#mixin-2}

Ahora puede repetir los mismos pasos para agregar otra mezcla. Cuando esta vez vista el cuadro de diálogo **[!UICONTROL Añadir mezcla]** , observe que la combinación &quot;Detalles[!UICONTROL de persona de]Perfil&quot; se ha atenuado y que el botón de radio que se encuentra junto a él no se puede seleccionar. Esto evita que usted duplique accidentalmente las mezclas que ya ha incluido en el esquema actual.

Ahora puede agregar &quot;[!DNL Profile Personal Details" mixin] desde el cuadro de diálogo.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una vez agregado, el lienzo vuelve a aparecer. &quot;Datos[!UICONTROL personales de]Perfil&quot; ahora aparece en **[!UICONTROL Mezclas]** en la sección **[!UICONTROL Composición]** , y los campos para la dirección doméstica, el teléfono móvil y más se han agregado en **[!UICONTROL Estructura]**.

De forma similar al campo &quot;[!UICONTROL nombre]&quot;, los campos que acaba de agregar representan conceptos de varios campos. Por ejemplo, &quot;[!UICONTROL homeAddress]&quot; tiene un tipo de datos de &quot;[!UICONTROL Address]&quot; y &quot;[!UICONTROL mobilePhone]&quot; tiene un tipo de datos de &quot;[!UICONTROL Phone Number]&quot;. Puede seleccionar cada uno de estos campos para expandirlos y ver los campos adicionales incluidos en el tipo de datos.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definir una nueva mezcla {#define-mixin}

El esquema &quot;Miembros[!UICONTROL de la]lealtad&quot; pretende capturar datos relacionados con los miembros de un programa de lealtad, por lo que requerirá algunos campos específicos relacionados con la lealtad. No hay mezclas estándar disponibles que contengan los campos necesarios, por lo tanto deberá definir una nueva mezcla.

Esta vez, cuando abra el cuadro de diálogo *[!UICONTROL Añadir mezcla]* , seleccione **[!UICONTROL Crear nueva combinación]**. Luego se le pedirá que proporcione un **[!UICONTROL Nombre]** para mostrar y una **[!UICONTROL Descripción]** para la mezcla.

![](../images/tutorials/create-schema/mixin_create_new.png)

Al igual que con los nombres de clase, el nombre de la mezcla debe ser corto y simple, describiendo lo que la mezcla contribuirá al esquema. Estos también son únicos, por lo que no podrá reutilizar el nombre y, por lo tanto, debe asegurarse de que sea lo suficientemente específico.

Para este tutorial, asigne a la nueva combinación el nombre &quot;Detalles[!UICONTROL de]lealtad&quot;.

Seleccione **[!UICONTROL Añadir mezcla]** para volver a la [!DNL Schema Editor]. &quot;Detalles[!UICONTROL de]lealtad&quot; debería aparecer ahora en **[!UICONTROL Mezclas]** en la parte izquierda del lienzo, pero todavía no hay campos asociados a él y por lo tanto no aparecen campos nuevos en **[!UICONTROL Estructura]**.

## Añadir campos a la mezcla {#mixin-fields}

Ahora que ha creado la combinación de &quot;Detalles[!UICONTROL de]Lealtad&quot;, es hora de definir los campos en los que la mezcla contribuirá al esquema.

Para comenzar, seleccione el nombre de la mezcla en la sección **[!UICONTROL Mezclas]** . Una vez realizado esto, las propiedades de la mezcla aparecen en la parte derecha del editor y aparece un botón **[!UICONTROL Añadir campo]** junto al nombre del esquema en **[!UICONTROL Estructura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleccione **[!UICONTROL Añadir campo]** junto a &quot;[!DNL Loyalty Members]&quot; para crear un nuevo nodo en la estructura. Este nodo (denominado &quot;_inquilinoId&quot; en este ejemplo) representa el ID de inquilino de la organización de IMS, precedido de un guion bajo. La presencia de la ID de inquilino indica que los campos que está agregando están contenidos en la Área de nombres de su organización.

En otras palabras, los campos que está agregando son exclusivos de su organización y se van a guardar en el [!DNL Schema Registry] en un área específica a la que solo pueda acceder su organización. Los campos que defina siempre deben agregarse a la Área de nombres del inquilino para evitar conflictos con nombres de otras clases estándar, mezclas, tipos de datos y campos.

Dentro de ese nodo con espacio de nombres hay un &quot;[!UICONTROL nuevo campo]&quot;. Este es el comienzo de la combinación de &quot;Detalles[!UICONTROL de]Lealtad&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Con los controles del lado derecho del editor, cree un inicio mediante la creación de un campo &quot;[!DNL loyalty]&quot; con el tipo &quot;[!UICONTROL Objeto]&quot; que se utilizará para mantener los campos relacionados con la lealtad. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Los cambios se aplican y aparece el objeto &quot;[!DNL loyalty]&quot; recién creado. Seleccione **[!UICONTROL Añadir campo]** junto al objeto para agregar campos adicionales relacionados con la lealtad. Aparece un &quot;[!UICONTROL Nuevo campo]&quot; y la sección Propiedades **[!UICONTROL del]** campo está visible en la parte derecha del lienzo.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requiere la siguiente información:

* **[!UICONTROL Nombre]del campo:** Nombre del campo, escrito en caso de camello. Ejemplo: loyaltyLevel
* **[!UICONTROL Nombre]para mostrar:** Nombre del campo, escrito en caso de título. Ejemplo: Nivel de fidelidad
* **[!UICONTROL Tipo]:** Tipo de datos del campo. Esto incluye los tipos escalares básicos y cualquier tipo de datos definido en el [!DNL Schema Registry]. Ejemplos: [!UICONTROL cadena], [!UICONTROL entero], [!UICONTROL booleano], [!UICONTROL Persona], [!UICONTROL Dirección], Número de teléfono, etc.
* **[!UICONTROL Descripción]:** Se debe incluir una descripción opcional del campo, escrita en caso de sentencia, con un máximo de 200 caracteres.

El primer campo del [!DNL Loyalty] objeto será una cadena llamada &quot;[!DNL loyaltyId]&quot;. Al establecer el tipo del nuevo campo en &quot;[!UICONTROL Cadena]&quot;, la sección Propiedades **[!UICONTROL del]** campo se llena con varias opciones para aplicar restricciones, como Valor **** predeterminado, **[!UICONTROL Formato]** y Longitud **** máxima.

![](../images/tutorials/create-schema/string_constraints.png)

Hay diferentes opciones de restricción disponibles según el tipo de datos seleccionado. Como &quot;[!DNL loyaltyId]&quot; será una dirección de correo electrónico, seleccione &quot;[!UICONTROL correo electrónico]&quot; en el menú desplegable **[!UICONTROL Formato]** . Seleccione **[!UICONTROL Aplicar]** para aplicar los cambios.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Añadir más campos a la mezcla {#mixin-fields-2}

Ahora que ha agregado el campo &quot;[!DNL loyaltyId]&quot;, puede agregar campos adicionales para capturar información relacionada con la lealtad como:

* Puntos (entero)
* Miembro desde (fecha)

Para agregar cada campo, seleccione **[!UICONTROL Añadir campo]** en el objeto loyalty y rellene la información requerida.

Una vez completado, el objeto Lealtad contendrá campos para ID de lealtad, puntos y elementos desde los que se obtuvo.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Añadir un campo de enumeración a la mezcla {#enum}

Al definir los campos en el [!DNL Schema Editor], hay algunas opciones adicionales que puede aplicar a los tipos de campo básicos para proporcionar restricciones adicionales en los datos que el campo puede contener. Los casos de uso de estas restricciones se explican en la siguiente tabla:

| Restricción | Descripción |
| --- | --- |
| [!UICONTROL Requerido] | Indica que el campo es obligatorio para la ingesta de datos. Cualquier dato cargado en un conjunto de datos basado en este esquema que no contenga este campo fallará durante la ingestión. |
| [!UICONTROL Matriz] | Indica que el campo contiene una matriz de valores, cada uno con el tipo de datos especificado. Por ejemplo, si se utiliza esta restricción en un campo con un tipo de datos de &quot;[!UICONTROL String]&quot;, se especifica que el campo contendrá una matriz de cadenas. |
| [!UICONTROL Enum] | Indica que este campo debe contener uno de los valores de una lista enumerada de valores posibles. |
| [!UICONTROL Identidad] | Indica que este campo es un campo de identidad. Más información sobre los campos de identidad se proporciona [más adelante en este tutorial](#identity-field). |
| [!UICONTROL Relación] | Aunque las relaciones de esquema pueden inferirse mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto sólo se aplica a esquemas que comparten la misma clase. La restricción [!UICONTROL Relación] indica que este campo hace referencia a la identidad principal de un esquema basado en una clase diferente, lo que implica una relación entre los dos esquemas. Consulte el tutorial sobre la [definición de una relación](./relationship-ui.md) para obtener más información. |

Para este tutorial, el [!DNL "loyalty"] objeto del esquema requiere un nuevo campo de enumeración que describe el &quot;nivel de lealtad&quot; de un cliente, donde el valor sólo puede ser una de las cuatro opciones posibles. Para agregar este campo al esquema, seleccione **[!UICONTROL Añadir campo]** al lado del objeto &quot;[!DNL loyalty]&quot; y rellene los campos requeridos para el nombre **[!UICONTROL del]** campo y el nombre **** para mostrar. Para **[!UICONTROL Tipo]**, seleccione &quot;[!UICONTROL Cadena]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Aparecerán casillas de verificación adicionales para el campo después de que se haya seleccionado su tipo, incluidas las casillas de verificación para **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Seleccione la casilla **[!UICONTROL Enum]** para abrir la sección Valores **** Enum que aparece a continuación. Aquí puede introducir el **[!UICONTROL valor]** (en camelCase) y la **[!UICONTROL etiqueta]** (un nombre opcional y fácil de leer en el caso del título) para cada nivel de lealtad aceptable.

Cuando haya completado todas las propiedades del campo, seleccione **[!UICONTROL Aplicar]** para agregar el campo &quot;[!DNL loyaltyLevel]&quot; al objeto &quot;[!DNL loyalty]&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversión de un objeto de varios campos en un tipo de datos {#datatype}

El objeto &quot;[!DNL loyalty]&quot; ahora contiene varios campos específicos de lealtad y representa una estructura de datos común que podría ser útil en otros esquemas. Esto [!DNL Schema Editor] le permite aplicar fácilmente objetos de varios campos reutilizables mediante la conversión de la estructura de dichos objetos en tipos de datos.

Los tipos de datos permiten el uso coherente de estructuras de varios campos y proporcionan más flexibilidad que una mezcla, ya que se pueden utilizar en cualquier lugar dentro de un esquema. Esto se lleva a cabo estableciendo el valor **[!UICONTROL Tipo]** del campo en el valor de cualquier tipo de datos definido en el [!DNL Schema Registry].

Para convertir el objeto &quot;[!DNL loyalty]&quot; en un tipo de datos, seleccione el campo &quot;[!DNL loyalty]&quot; en **[!UICONTROL Estructura]** y, a continuación, seleccione **[!UICONTROL Convertir en nuevo tipo]** de datos en el lado derecho del editor en Propiedades **[!UICONTROL de]** campo. Aparece una ventana emergente verde que confirma que el objeto se ha convertido correctamente.

![](../images/tutorials/create-schema/convert-data-type.png)

Ahora, cuando se observa en **[!UICONTROL Estructura]**, se puede ver que el campo &quot;[!DNL loyalty]&quot; tiene un tipo de datos &quot;[!DNL Loyalty]&quot; y que los campos tienen pequeños iconos de bloqueo junto a ellos, lo que indica que ya no son campos individuales sino que forman parte de un tipo de datos de varios campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

En un esquema futuro, ahora se puede asignar un campo al **[!UICONTROL Tipo]** de &quot;[!DNL Loyalty]&quot; y se incluirán automáticamente campos para ID, nivel de lealtad, miembro desde y puntos.

## Definición de un campo de esquema como campo de identidad {#identity-field}

La estructura de datos estándar que proporcionan los esquemas se puede aprovechar para identificar los datos que pertenecen a la misma persona en múltiples fuentes, permitiendo diversos casos de uso descendente como segmentación, sistema de informes, análisis de la ciencia de datos, etc. Para poder unir datos en función de identidades individuales, los campos clave deben marcarse como campos de &quot;[!UICONTROL Identidad]&quot; dentro de los esquemas aplicables.

[!DNL Experience Platform] facilita la identificación de un campo de identidad mediante el uso de una casilla de verificación **[!UICONTROL Identidad]** en la [!DNL Schema Editor]. Sin embargo, debe determinar qué campo es el mejor candidato para utilizar como identidad, en función de la naturaleza de los datos.

Por ejemplo, puede haber miles de miembros del programa de lealtad pertenecientes al mismo &quot;nivel de lealtad&quot;, pero cada miembro del programa de lealtad tiene un &quot;[!DNL loyaltyId]&quot; único (que en este caso es la dirección de correo electrónico del miembro individual). El hecho de que &quot;[!DNL loyaltyId]&quot; sea un identificador único para cada miembro lo convierte en un buen candidato para un campo de identidad, mientras que &quot;nivel de lealtad&quot; no lo es.

>[!IMPORTANT]
>
>Los pasos que se describen a continuación explican cómo agregar un descriptor de identidad a un campo de esquema existente. Como alternativa a definir campos de identidad dentro de la estructura del esquema mismo, también puede utilizar un `identityMap` campo para contener información de identidad.
>
>Si planea usar `identityMap`, tenga en cuenta que anulará cualquier identidad principal que agregue directamente al esquema. Consulte la sección sobre `identityMap` los [conceptos básicos de la guía](../schema/composition.md#identityMap) de composición de esquemas para obtener más información.

En la sección **[!UICONTROL Estructura]** del editor, seleccione el campo &quot;[!DNL loyaltyId]&quot; y la casilla de verificación **[!UICONTROL Identidad]** aparece en Propiedades **** del campo. Marque la casilla y la opción para establecer esto como la identidad **** principal aparece. Seleccione también este cuadro.

A continuación, debe proporcionar una Área de nombres **[!UICONTROL de]** identidad a partir de la lista de Áreas de nombres predefinidas en el menú desplegable. Como &quot;[!DNL loyaltyId]&quot; es la dirección de correo electrónico del cliente, seleccione &quot;[!UICONTROL Correo electrónico]&quot; en el menú desplegable. Seleccione **[!UICONTROL Aplicar]** para confirmar las actualizaciones en el campo &quot;[!DNL loyaltyId]&quot;.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obtener una lista de las Áreas de nombres estándar y sus definiciones, consulte la documentación [del servicio de](../../identity-service/troubleshooting-guide.md#standard-namespaces)identidad.

Ahora todos los datos ingestados en el campo &quot;[!DNL loyaltyId]&quot; se utilizarán para identificar a esa persona y unir una sola vista de ese cliente.

>[!NOTE]
>
>Una vez que un campo de esquema se haya establecido como identidad principal, recibirá un mensaje de error si posteriormente intenta establecer otro campo del esquema como principal. Cada esquema puede contener sólo un campo de identidad principal.

Para obtener más información sobre cómo trabajar con identidades en [!DNL Experience Platform], consulte la documentación de [[!DNL Identity Service]](../../identity-service/home.md) .

## Habilitar el esquema para utilizarlo en [!DNL Real-time Customer Profile] {#profile}

[[!DNL Perfil del cliente en tiempo real]](../../profile/home.md) aprovecha los datos de identidad en [!DNL Experience Platform] para proporcionar una vista holística de cada cliente individual. El servicio crea sólidos perfiles de 360° de atributos del cliente, así como cuentas con marca de hora de cada interacción que los clientes han tenido en cualquier sistema integrado con [!DNL Experience Platform].

Para que un esquema se pueda utilizar con [!DNL Real-time Customer Profile], debe tener una identidad principal definida. Recibirá un mensaje de error si intenta habilitar un esquema sin definir primero una identidad principal.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para habilitar el esquema &quot;Miembros de lealtad&quot; para su uso en [!DNL Profile], seleccione &quot;[!DNL Loyalty Members]&quot; en la sección **[!UICONTROL Estructura]** del editor.

A la derecha del editor, se muestra información sobre el esquema, incluido su nombre para mostrar, descripción y tipo. Además de esta información, hay un botón de alternancia de **[!UICONTROL Perfil]** .

![](../images/tutorials/create-schema/profile-toggle.png)

Seleccione el **[!UICONTROL Perfil]** y aparecerá una ventana emergente para pedirle que confirme que desea habilitar el esquema para [!DNL Profile].

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Una vez que un esquema se ha habilitado [!DNL Real-time Customer Profile] y guardado, no se puede deshabilitar.

Seleccione **[!UICONTROL Habilitar]** para confirmar su elección. Puede volver a seleccionar la opción de **[!UICONTROL Perfil]** para deshabilitar el esquema si lo desea, pero una vez que el esquema se ha guardado mientras [!DNL Profile] está activado, ya no se puede deshabilitar.

## Próximos pasos y recursos adicionales

Ahora que ha terminado de componer un esquema &quot;Miembros de la lealtad&quot;, puede ver el esquema completo en el lienzo. Seleccione **[!UICONTROL Guardar]** y el esquema se guardará en el [!DNL Schema Library]archivo, lo que lo hará accesible para el [!DNL Schema Registry].

El nuevo esquema ahora se puede utilizar para ingerir datos en [!DNL Platform]. Recuerde que una vez que el esquema se ha utilizado para ingestar datos, sólo se pueden realizar cambios aditivos. Consulte los [conceptos básicos de la composición](../schema/composition.md) de esquema para obtener más información sobre el control de versiones de esquemas.

Ahora puede seguir el tutorial sobre la [definición de una relación de esquema en la interfaz de usuario](./relationship-ui.md) para agregar un nuevo campo de relación al esquema &quot;Miembros de lealtad&quot;.

El esquema &quot;Miembros de lealtad&quot; también está disponible para su visualización y administración mediante la [!DNL Schema Registry] API. Para empezar a trabajar con la API, lea la guía [[!DNL Schema Registry API] del](../api/getting-started.md)desarrollador para inicio.

### Recursos de vídeo

>[!WARNING]
>
>La interfaz de usuario que [!DNL Platform] se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

El siguiente vídeo muestra cómo crear un esquema sencillo en la [!DNL Platform] interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

El siguiente vídeo pretende reforzar su comprensión del trabajo con mezclas y clases.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apéndice

Las siguientes secciones proporcionan información adicional sobre el uso del [!DNL Schema Editor].

### Create a new class {#create-new-class}

[!DNL Experience Platform] proporciona la flexibilidad necesaria para definir un esquema basado en una clase exclusiva de su organización.

En el espacio de trabajo **[!UICONTROL Esquemas]** , seleccione **[!UICONTROL Crear esquema]** y, a continuación, seleccione **[!UICONTROL Examinar]** en el menú desplegable.

![](../images/tutorials/create-schema/browse-classes.png)

Aparece un cuadro de diálogo que le permite seleccionar entre una lista de clases disponibles. En la parte superior del cuadro de diálogo, seleccione **[!UICONTROL Crear nueva clase]**. A continuación, puede asignar a la nueva clase un nombre **[!UICONTROL para]** mostrar (un nombre corto, descriptivo, único y práctico para la clase), una **[!UICONTROL descripción]** y un **[!UICONTROL comportamiento]** (&quot;[!UICONTROL registro]&quot; o &quot;serie[!UICONTROL temporal]&quot;) para los datos que el esquema definirá.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>Cuando cree un esquema que implemente una clase definida por su organización, recuerde que las mezclas están disponibles para su uso únicamente con clases compatibles. Como la clase que ha definido es nueva, no hay mezclas compatibles en el cuadro de diálogo *Añadir mezcla* . En su lugar, deberá seleccionar **[!UICONTROL Crear nueva mezcla]** y definir una mezcla para utilizarla con esa clase. La próxima vez que componga un esquema que implemente la nueva clase, la mezcla que definió aparecerá en la lista y estará disponible para su uso.

### Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Las mezclas solo son compatibles con determinadas clases y, por lo tanto, si se cambia la clase, se restablecerán el lienzo y los campos que se hayan agregado.

Para reasignar una clase, seleccione **[!UICONTROL Asignar]** en el lado izquierdo del lienzo.

![](../images/tutorials/create-schema/assign_class_button.png)

Aparece un cuadro de diálogo que muestra una lista de todas las clases disponibles, incluidas las definidas por su organización (el propietario es &quot;[!UICONTROL Cliente]&quot;) y las clases estándar definidas por Adobe.

Seleccione una clase de la lista para mostrar su descripción en el lado derecho del cuadro de diálogo. También puede seleccionar Estructura **[!UICONTROL de clases de]** Previsualización para ver los campos y metadatos asociados a la clase. Seleccione **[!UICONTROL Asignar clase]** para continuar.

![](../images/tutorials/create-schema/assign_class.png)

Se abre un nuevo cuadro de diálogo en el que se le solicita que confirme que desea asignar una nueva clase. Seleccione **[!UICONTROL Asignar]** para confirmar.

![](../images/tutorials/create-schema/assign-confirm.png)

Después de confirmar el cambio de clase, se restablecerá el lienzo y se perderá todo el progreso de la composición.