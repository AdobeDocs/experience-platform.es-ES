---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Crear un esquema con el editor de esquemas
topic-legacy: tutorial
type: Tutorial
description: Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3532'
ht-degree: 0%

---

# Crear un esquema con el [!DNL Schema Editor]

La interfaz de usuario de Adobe Experience Platform le permite crear y administrar esquemas [!DNL Experience Data Model] (XDM) en un lienzo visual interactivo denominado [!DNL Schema Editor]. Este tutorial explica cómo crear un esquema con [!DNL Schema Editor].

>[!NOTE]
>
>Para fines de demostración, los pasos de este tutorial implican la creación de un esquema de ejemplo que describa los miembros de un programa de fidelidad de cliente. Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda que primero siga con la creación del esquema de ejemplo para conocer las capacidades de [!DNL Schema Editor].

Si prefiere componer un esquema utilizando la API [!DNL Schema Registry] en su lugar, comience leyendo la [[!DNL Schema Registry] guía para desarrolladores](../api/getting-started.md) antes de intentar el tutorial sobre la [creación de un esquema con la API](create-schema-api.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los distintos aspectos de Adobe Experience Platform implicados en la creación de esquemas. Antes de comenzar este tutorial, consulte la documentación de los siguientes conceptos:

* [[!DNL Experience Data Model (XDM)]](../home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../schema/composition.md) del esquema: Información general sobre esquemas XDM y sus componentes básicos, incluidas clases, mezclas, tipos de datos y campos.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Abra el espacio de trabajo [!UICONTROL Schemas] {#browse}

El espacio de trabajo [!UICONTROL Schemas] en la interfaz de usuario [!DNL Platform] proporciona una visualización del [!DNL Schema Library], lo que le permite ver y administrar los esquemas disponibles para su organización. El espacio de trabajo también incluye el [!DNL Schema Editor], el lienzo en el que puede componer un esquema a lo largo de este tutorial.

Después de iniciar sesión en [!DNL Experience Platform], seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo para abrir el espacio de trabajo **[!UICONTROL Schemas]**. La pestaña **[!UICONTROL Browse]** muestra una lista de esquemas (una representación del [!DNL Schema Library]) que puede ver y personalizar. La lista incluye el nombre, el tipo, la clase y el comportamiento (registro o serie temporal) en los que se basa el esquema, así como la fecha y la hora de la última modificación del esquema.

Consulte la guía [Exploración de los recursos XDM existentes en la interfaz de usuario](../ui/explore.md) para obtener más información.

## Crear y asignar un nombre a un esquema {#create}

Para empezar a componer un esquema, seleccione **[!UICONTROL Create schema]** en la esquina superior derecha del espacio de trabajo **[!UICONTROL Schemas]**. Aparece un menú desplegable que le ofrece la opción de elegir entre las clases principales [!UICONTROL XDM Individual Profile] y [!UICONTROL XDM ExperienceEvent]. Si estas clases no se adaptan a sus necesidades, también puede seleccionar **[!UICONTROL Browse]** para elegir entre otras clases disponibles o [crear una nueva clase](#create-new-class).

Para los fines de este tutorial, seleccione **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Dado que elige una clase XDM estándar en la que basar el esquema, aparece el cuadro de diálogo **[!UICONTROL Add mixin]**, que le permite empezar a añadir campos inmediatamente al esquema. Por ahora, seleccione **[!UICONTROL Cancel]** para salir del cuadro de diálogo.

![](../images/tutorials/create-schema/cancel-mixin.png)

Aparece el [!DNL Schema Editor]. Este es el lienzo sobre el que compondrá el esquema. Se crea automáticamente un esquema sin título en la sección **[!UICONTROL Structure]** del lienzo al llegar al editor, junto con los campos estándar incluidos en todos los esquemas basados en esa clase. La clase asignada para el esquema también se enumera en **[!UICONTROL Class]** en la sección **[!UICONTROL Composition]**.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Puede [cambiar la clase de un esquema](#change-class) en cualquier momento durante el proceso de composición inicial antes de guardar el esquema, pero esto debe hacerse con mucha precaución. Las mezclas solo son compatibles con ciertas clases y, por lo tanto, cambiar la clase restablecerá el lienzo y los campos que haya agregado.

Utilice los campos del lado derecho del editor para proporcionar un nombre para mostrar y una descripción opcional para el esquema. Una vez introducido un nombre, el lienzo se actualiza para reflejar el nuevo nombre del esquema.

![](../images/tutorials/create-schema/name_schema.png)

Hay que tener en cuenta varias consideraciones importantes a la hora de decidir un nombre para el esquema:

* Los nombres de esquema deben ser cortos y descriptivos para que el esquema se pueda encontrar fácilmente más adelante.
* Los nombres de esquema deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro. Por ejemplo, si su organización tiene programas de fidelidad separados para diferentes marcas, sería aconsejable nombrar al esquema &quot;Miembros de fidelidad de marca A&quot; para que sea más fácil distinguir de otros esquemas relacionados con la fidelidad que podría definir más adelante.
* También puede utilizar la descripción del esquema para proporcionar cualquier información contextual adicional relacionada con el esquema.

Este tutorial compone un esquema para introducir datos relacionados con los miembros de un programa de fidelidad y, por lo tanto, el esquema se denomina &quot;Miembros de fidelidad&quot;.

## Añadir una mezcla {#mixin}

Ahora puede empezar a añadir campos al esquema añadiendo mezclas. Una mezcla es un grupo de uno o más campos que a menudo se utilizan juntos para describir un concepto en particular. Este tutorial utiliza mezclas para describir los miembros del programa de fidelidad y capturar información clave como nombre, cumpleaños, número de teléfono, dirección, etc.

Para añadir una mezcla, seleccione **[!UICONTROL Add]** en la subsección **[!UICONTROL Mixins]**.

![](../images/tutorials/create-schema/add_mixin_button.png)

Aparece un nuevo cuadro de diálogo, que muestra una lista de las mezclas disponibles. Cada mezcla está destinada únicamente a utilizarse con una clase específica, por lo que el cuadro de diálogo sólo contiene mezclas compatibles con la clase seleccionada (en este caso, la clase [!DNL XDM Individual Profile]). Si está utilizando una clase XDM estándar, la lista de mezclas se ordenará de forma inteligente en función de la popularidad de uso.

![](../images/tutorials/create-schema/mixin-popularity.png)

La selección de una mezcla de la lista hace que aparezca en el carril derecho. Si lo desea, puede seleccionar varias mezclas, agregándolas a la lista en el carril derecho antes de confirmarlas. Además, aparece un icono en el lado derecho de la mezcla seleccionada actualmente, que permite previsualizar la estructura de los campos que proporciona.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Al previsualizar una mezcla, se proporciona una descripción detallada del esquema de la mezcla en el carril derecho. También puede navegar por los campos de la mezcla en el lienzo proporcionado. A medida que selecciona diferentes campos, el carril derecho se actualiza para mostrar detalles sobre el campo en cuestión. Seleccione **[!UICONTROL Back]** cuando haya terminado de obtener una vista previa para volver al cuadro de diálogo de selección de la mezcla.

![](../images/tutorials/create-schema/preview-mixin.png)

Para este tutorial, seleccione la mezcla **[!UICONTROL Demographic Details]** y, a continuación, seleccione **[!UICONTROL Add mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

El lienzo del esquema vuelve a aparecer. La sección **[!UICONTROL Mixins]** ahora enumera &quot;[!UICONTROL Demographic Details]&quot; y la sección **[!UICONTROL Structure]** incluye los campos contribuidos por la mezcla. Puede seleccionar el nombre de la mezcla en la sección **[!UICONTROL Mixins]** para resaltar los campos específicos que proporciona dentro del lienzo.

![](../images/tutorials/create-schema/person_details_structure.png)

Esta mezcla contribuye a varios campos bajo el nombre de nivel superior `person` con el tipo de datos &quot;[!UICONTROL Person]&quot;. Este grupo de campos describe información sobre un individuo, incluido el nombre, la fecha de nacimiento y el sexo.

>[!NOTE]
>
>Recuerde que los campos pueden utilizar tipos escalares (como cadena, entero, matriz o fecha), así como cualquier tipo de datos (un grupo de campos que representa un concepto común) definido dentro de [!DNL Schema Registry].

Observe que el campo `name` tiene un tipo de datos de &quot;[!UICONTROL Person name]&quot;, lo que significa que también describe un concepto común y contiene subcampos relacionados con nombres como nombre, apellido, título de cortesía y sufijo.

Seleccione los diferentes campos dentro del lienzo para mostrar los campos adicionales que contribuyen a la estructura del esquema.

## Añadir otra mezcla {#mixin-2}

Ahora puede repetir los mismos pasos para agregar otra mezcla. Cuando vea el cuadro de diálogo **[!UICONTROL Add mixin]** esta vez, observe que la mezcla &quot;[!UICONTROL Demographic Details]&quot; se ha atenuado y que la casilla de verificación situada junto a ella no se puede seleccionar. Esto evita que se dupliquen accidentalmente las mezclas que ya se han incluido en el esquema actual.

Para este tutorial, seleccione la mezcla &quot;[!DNL Personal Contact Details]&quot; en el cuadro de diálogo y, a continuación, seleccione **[!UICONTROL Add mixin]** para agregarla al esquema.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una vez añadido, el lienzo vuelve a aparecer. &quot;[!UICONTROL Personal Contact Details]&quot; ahora aparece en **[!UICONTROL Mixins]** en la sección **[!UICONTROL Composition]** y se han agregado campos para la dirección de inicio, el teléfono móvil y mucho más en **[!UICONTROL Structure]**.

Al igual que el campo `name` , los campos que acaba de añadir representan conceptos de varios campos. Por ejemplo, `homeAddress` tiene un tipo de datos de &quot;[!UICONTROL Postal address]&quot; y `mobilePhone` tiene un tipo de datos de &quot;[!UICONTROL Phone number]&quot;. Puede seleccionar cada uno de estos campos para expandirlos y ver los campos adicionales incluidos en el tipo de datos.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Defina una mezcla personalizada {#define-mixin}

El esquema &quot;[!UICONTROL Loyalty Members]&quot; está diseñado para capturar datos relacionados con los miembros de un programa de fidelidad, por lo que necesitará algunos campos específicos relacionados con la fidelidad.

Hay una mezcla estándar [!UICONTROL Loyalty Details] que puede agregar al esquema para capturar campos comunes relacionados con un programa de fidelidad. Aunque se le recomienda encarecidamente que utilice mezclas estándar para representar los conceptos capturados por sus esquemas, es posible que la estructura de la mezcla de fidelidad estándar no pueda capturar todos los datos relevantes para su programa de fidelidad en particular. En este escenario, puede elegir definir una nueva mezcla personalizada para capturar estos campos en su lugar.

Vuelva a abrir el cuadro de diálogo **[!UICONTROL Add Mixin]**, pero esta vez seleccione **[!UICONTROL Create New Mixin]** cerca de la parte superior. A continuación, se le pedirá que proporcione un nombre para mostrar y una descripción para su mezcla.

![](../images/tutorials/create-schema/mixin_create_new.png)

Como con los nombres de clase, el nombre de la mezcla debe ser corto y simple, describiendo lo que la mezcla contribuirá al esquema. Estas también son únicas, por lo que no podrá reutilizar el nombre y, por lo tanto, debe asegurarse de que sea lo suficientemente específico.

Para este tutorial, asigne un nombre a la nueva mezcla &quot;Detalles de lealtad&quot;.

Seleccione **[!UICONTROL Add mixin]** para volver a [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; debería aparecer en **[!UICONTROL Mixins]** en el lado izquierdo del lienzo, pero todavía no hay campos asociados a él y, por lo tanto, no aparecen campos nuevos en **[!UICONTROL Structure]**.

## Añadir campos a la mezcla {#mixin-fields}

Ahora que ha creado la mezcla &quot;Detalles de Lealtad&quot;, es hora de definir los campos que la mezcla contribuirá al esquema.

Para empezar, seleccione el nombre de la mezcla en la sección **[!UICONTROL Mixins]**. Una vez que haga esto, las propiedades de la mezcla aparecen en el lado derecho del editor y aparece un icono **plus (+)** junto al nombre del esquema en **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleccione el icono **plus (+)** situado junto a &quot;[!DNL Loyalty Members]&quot; para crear un nuevo nodo en la estructura. Este nodo (denominado `_tenantId` en este ejemplo) representa el ID de inquilino de la organización IMS, precedido por un guion bajo. La presencia del ID de inquilino indica que los campos que está agregando están contenidos en el espacio de nombres de su organización.

En otras palabras, los campos que agregue son únicos para su organización y se guardarán en [!DNL Schema Registry] en un área específica accesible solo para su organización. Los campos que defina siempre deben agregarse al espacio de nombres del inquilino para evitar conflictos con nombres de otras clases estándar, mezclas, tipos de datos y campos.

Dentro de ese nodo con espacio de nombres se encuentra &quot;[!UICONTROL New Field]&quot;. Este es el comienzo de la mezcla &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Con los controles del lado derecho del editor, comience creando un campo `loyalty` con el tipo &quot;[!UICONTROL Object]&quot; que se utilizará para incluir los campos relacionados con la lealtad. Cuando termine, seleccione **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Los cambios se aplican y aparece el objeto `loyalty` recién creado. Seleccione el icono **plus (+)** situado junto al objeto para añadir campos adicionales relacionados con la lealtad. Aparece un &quot;[!UICONTROL New Field]&quot; y la sección **[!UICONTROL Field properties]** está visible en el lado derecho del lienzo.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requiere la siguiente información:

* **[!UICONTROL Field Name]:** El nombre del campo, escrito en caso de camello. Ejemplo: loyaltyLevel
* **[!UICONTROL Display Name]:** El nombre del campo, escrito en el caso del título. Ejemplo: Nivel de fidelidad
* **[!UICONTROL Type]:** El tipo de datos del campo. Esto incluye tipos escalares básicos y cualquier tipo de datos definido en el [!DNL Schema Registry]. Ejemplos: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], etc.
* **[!UICONTROL Description]:** Se debe incluir una descripción opcional del campo, escrita en caso de sentencia, con un máximo de 200 caracteres.

El primer campo del objeto `Loyalty` será una cadena denominada `loyaltyId`. Al establecer el tipo del nuevo campo en &quot;[!UICONTROL String]&quot;, la sección **[!UICONTROL Field properties]** se rellena con varias opciones para aplicar restricciones, incluidos el valor predeterminado, el formato y la longitud máxima.

![](../images/tutorials/create-schema/string_constraints.png)

Hay diferentes opciones de restricción disponibles en función del tipo de datos seleccionado. Dado que `loyaltyId` será una dirección de correo electrónico, seleccione &quot;[!UICONTROL email]&quot; en el menú desplegable **[!UICONTROL Format]**. Seleccione **[!UICONTROL Apply]** para aplicar los cambios.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Añadir más campos a la mezcla {#mixin-fields-2}

Ahora que ha agregado el campo `loyaltyId`, puede agregar campos adicionales para capturar información relacionada con la lealtad, como:

* Puntos (entero)
* Miembro desde (fecha)

Para añadir cada campo al esquema, seleccione el icono **plus (+)** junto al objeto `loyalty` y rellene la información necesaria.

Cuando se complete, el objeto Lealtad contendrá campos para ID de fidelidad, puntos y desde entonces.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Añadir un campo de enumeración a la mezcla {#enum}

Al definir campos en [!DNL Schema Editor], hay algunas opciones adicionales que puede aplicar a tipos de campo básicos para proporcionar más restricciones en los datos que el campo puede contener. Los casos de uso de estas restricciones se explican en la siguiente tabla:

| Restricción | Descripción |
| --- | --- |
| [!UICONTROL Required] | Indica que el campo es necesario para la ingesta de datos. Cualquier dato cargado en un conjunto de datos basado en este esquema que no contenga este campo fallará tras la ingesta. |
| [!UICONTROL Array] | Indica que el campo contiene una matriz de valores, cada uno con el tipo de datos especificado. Por ejemplo, el uso de esta restricción en un campo con un tipo de datos de &quot;[!UICONTROL String]&quot; especifica que el campo contendrá una matriz de cadenas. |
| [!UICONTROL Enum] | Indica que este campo debe contener uno de los valores de una lista enumerada de valores posibles. |
| [!UICONTROL Identity] | Indica que este campo es de identidad. Más información sobre los campos de identidad se proporciona [más adelante en este tutorial](#identity-field). |
| [!UICONTROL Relationship] | Aunque las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. La restricción [!UICONTROL Relationship] indica que este campo hace referencia a la identidad principal de un esquema basado en una clase diferente, lo que implica una relación entre los dos esquemas. Consulte el tutorial sobre [definición de una relación](./relationship-ui.md) para obtener más información. |

>[!NOTE]
>
>Los campos requeridos, de identidad o de relación se muestran en el carril izquierdo, lo que permite localizar estos campos fácilmente independientemente de la complejidad del esquema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, el objeto [!DNL "loyalty"] del esquema requiere un nuevo campo de enumeración que describa el &quot;nivel de lealtad&quot; de un cliente, donde el valor solo puede ser una de las cuatro opciones posibles. Para añadir este campo al esquema, seleccione el icono **plus (+)** junto al objeto `loyalty` y rellene los campos obligatorios para **[!UICONTROL Field name]** y **[!UICONTROL Display name]**. Para **[!UICONTROL Type]**, seleccione &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Aparecen casillas de verificación adicionales para el campo después de que se haya seleccionado su tipo, incluidas las casillas de verificación **[!UICONTROL Array]**, **[!UICONTROL Enum]** y **[!UICONTROL Identity]**.

Active la casilla **[!UICONTROL Enum]** para abrir la sección **[!UICONTROL Enum values]** que aparece a continuación. Aquí puede introducir **[!UICONTROL Value]** (en camelCase) y **[!UICONTROL Label]** (un nombre opcional y fácil de leer en el caso del título) para cada nivel de lealtad aceptable.

Cuando haya completado todas las propiedades del campo, seleccione **[!UICONTROL Apply]** para agregar el campo &quot;[!DNL loyaltyLevel]&quot; al objeto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversión de un objeto de varios campos en un tipo de datos {#datatype}

El objeto `loyalty` ahora contiene varios campos específicos de lealtad y representa una estructura de datos común que podría resultar útil en otros esquemas. El [!DNL Schema Editor] permite aplicar fácilmente objetos de varios campos reutilizables convirtiendo la estructura de esos objetos en tipos de datos.

Los tipos de datos permiten el uso coherente de estructuras de varios campos y proporcionan más flexibilidad que una mezcla, ya que se pueden utilizar en cualquier lugar dentro de un esquema. Esto se hace estableciendo el valor **[!UICONTROL Type]** del campo en el valor de cualquier tipo de datos definido en [!DNL Schema Registry].

Para convertir el objeto `loyalty` en un tipo de datos, seleccione el campo `loyalty` en **[!UICONTROL Structure]** y, a continuación, seleccione **[!UICONTROL Convert to new data type]** en el lado derecho del editor, en **[!UICONTROL Field properties]**. Aparece una ventana emergente verde que confirma que el objeto se ha convertido correctamente.

![](../images/tutorials/create-schema/convert-data-type.png)

Ahora, al mirar en **[!UICONTROL Structure]**, puede ver que el campo `loyalty` tiene un tipo de datos &quot;[!DNL Loyalty]&quot; y que los campos tienen iconos de bloqueo pequeños junto a ellos, lo que indica que ya no son campos individuales sino parte de un tipo de datos de varios campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

En un esquema futuro, ahora se podría asignar un campo como tipo &quot;[!DNL Loyalty]&quot; y se incluirían automáticamente campos para ID, nivel de lealtad, miembro desde y puntos.

>[!NOTE]
>
>También puede crear y editar tipos de datos personalizados de forma independiente de la edición de esquemas. Consulte la guía sobre [creación y edición de tipos de datos](../ui/resources/data-types.md) para obtener más información.

## Buscar y filtrar campos de esquema

El esquema ahora contiene varias mezclas además de los campos proporcionados por su clase base. Al trabajar con esquemas más grandes, puede seleccionar las casillas de verificación situadas junto a los nombres de las mezclas en el carril izquierdo para filtrar los campos mostrados únicamente a los proporcionados por las mezclas que le interesen.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Si está buscando un campo específico en el esquema, también puede utilizar la barra de búsqueda para filtrar los campos mostrados por nombre, independientemente de la mezcla en la que se proporcionan.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La función de búsqueda tiene en cuenta los filtros de mezcla seleccionados al mostrar los campos coincidentes. Si una consulta de búsqueda no muestra los resultados esperados, es posible que tenga que verificar que no está filtrando ninguna mezcla relevante.

## Establecer un campo de esquema como campo de identidad {#identity-field}

La estructura de datos estándar que proporcionan los esquemas se puede aprovechar para identificar los datos que pertenecen al mismo individuo en múltiples fuentes, lo que permite varios casos de uso descendente como segmentación, informes, análisis de ciencia de datos, etc. Para unir datos en función de identidades individuales, los campos clave deben marcarse como campos [!UICONTROL Identity] dentro de los esquemas aplicables.

[!DNL Experience Platform] facilita la identificación de un campo de identidad mediante el uso de una  **[!UICONTROL Identity]** casilla de verificación en  [!DNL Schema Editor]. Sin embargo, debe determinar qué campo es el mejor candidato para utilizarlo como identidad, en función de la naturaleza de los datos.

Por ejemplo, puede haber miles de miembros del programa de fidelidad que pertenezcan al mismo &quot;nivel de fidelidad&quot;, pero cada miembro del programa de fidelidad tiene un `loyaltyId` único (que en este caso es la dirección de correo electrónico del miembro individual). El hecho de que `loyaltyId` sea un identificador único para cada miembro lo convierte en un buen candidato para un campo de identidad, mientras que `loyaltyLevel` no lo es.

>[!IMPORTANT]
>
>Los pasos que se describen a continuación abarcan cómo agregar un descriptor de identidad a un campo de esquema existente. Como alternativa a definir campos de identidad dentro de la estructura del propio esquema, también puede utilizar un campo `identityMap` para contener información de identidad en su lugar.
>
>Si planea utilizar `identityMap`, tenga en cuenta que anulará cualquier identidad principal que agregue al esquema directamente. Consulte la sección sobre `identityMap` en la [Guía básica de composición de esquema](../schema/composition.md#identityMap) para obtener más información.

En la sección **[!UICONTROL Structure]** del editor, seleccione el campo `loyaltyId` y la casilla **[!UICONTROL Identity]** aparece en **[!UICONTROL Field properties]**. Marque la casilla y la opción para establecerla como aparece el **[!UICONTROL Primary identity]**. Seleccione también este cuadro.

>[!NOTE]
>
>Cada esquema puede contener solo un campo de identidad principal. Una vez que se ha establecido un campo de esquema como identidad principal, recibirá un mensaje de error si más tarde intenta establecer otro campo de identidad en el esquema como principal.

A continuación, debe proporcionar un **[!UICONTROL Identity namespace]** de la lista de áreas de nombres predefinidas en la lista desplegable. Dado que `loyaltyId` es la dirección de correo electrónico del cliente, seleccione &quot;[!UICONTROL Email]&quot; en la lista desplegable. Seleccione **[!UICONTROL Apply]** para confirmar las actualizaciones del campo `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obtener una lista de áreas de nombres estándar y sus definiciones, consulte la [[!DNL Identity Service] documentación](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Después de aplicar el cambio, el icono de `loyaltyId` muestra un símbolo de huella digital, que indica que ahora es un campo de identidad.

![](../images/tutorials/create-schema/identity-applied.png)

Ahora todos los datos incorporados en el campo `loyaltyId` se utilizan para ayudar a identificar a ese individuo y unir una sola vista de ese cliente. Para obtener más información sobre cómo trabajar con identidades en [!DNL Experience Platform], consulte la documentación de [[!DNL Identity Service]](../../identity-service/home.md).

## Habilite el esquema para utilizarlo en [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) aprovecha los datos de identidad en  [!DNL Experience Platform] para proporcionar una vista holística de cada cliente individual. El servicio crea perfiles sólidos de 360° de atributos del cliente, así como cuentas con marca de tiempo de cada interacción que los clientes han tenido en cualquier sistema integrado con [!DNL Experience Platform].

Para que un esquema esté habilitado para utilizarse con [!DNL Real-time Customer Profile], debe tener una identidad principal definida. Recibirá un mensaje de error si intenta habilitar un esquema sin definir primero una identidad principal.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para habilitar el esquema &quot;Miembros de lealtad&quot; para su uso en [!DNL Profile], comience por seleccionar &quot;[!DNL Loyalty Members]&quot; en la sección **[!UICONTROL Structure]** del editor.

A la derecha del editor, se muestra información sobre el esquema, incluido su nombre para mostrar, descripción y tipo. Además de esta información, hay un botón de alternancia **[!UICONTROL Profile]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Seleccione **[!UICONTROL Profile]** y aparecerá una ventana emergente que le pedirá que confirme que desea habilitar el esquema para [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una vez que un esquema se ha habilitado para [!DNL Real-time Customer Profile] y se ha guardado, no se puede desactivar.

Seleccione **[!UICONTROL Enable]** para confirmar su elección. Puede volver a seleccionar la opción **[!UICONTROL Profile]** para deshabilitar el esquema si lo desea, pero una vez que el esquema se haya guardado mientras [!DNL Profile] está habilitado, ya no se puede deshabilitar.

## Pasos siguientes y recursos adicionales

Ahora que ha terminado de componer el esquema, puede ver el esquema completo en el lienzo. Seleccione **[!UICONTROL Save]** y el esquema se guardará en [!DNL Schema Library], lo que lo hace accesible desde [!DNL Schema Registry].

El nuevo esquema ahora se puede usar para introducir datos en [!DNL Platform]. Recuerde que una vez que el esquema se ha utilizado para introducir datos, solo se pueden realizar cambios aditivos. Consulte los [conceptos básicos de la composición de esquema](../schema/composition.md) para obtener más información sobre el control de versiones de esquemas.

Ahora puede seguir el tutorial sobre la [definición de una relación de esquema en la interfaz de usuario](./relationship-ui.md) para agregar un nuevo campo de relación al esquema &quot;Miembros de lealtad&quot;.

El esquema &quot;Miembros de lealtad&quot; también está disponible para su visualización y administración mediante la API [!DNL Schema Registry]. Para empezar a trabajar con la API, lea la [[!DNL Schema Registry API] guía para desarrolladores](../api/getting-started.md).

### Recursos de vídeo

>[!WARNING]
>
>La interfaz de usuario [!DNL Platform] que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

El siguiente vídeo muestra cómo crear un esquema simple en la interfaz de usuario [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

El siguiente vídeo pretende reforzar su comprensión del trabajo con mezclas y clases.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre el uso de [!DNL Schema Editor].

### Crear una nueva clase {#create-new-class}

[!DNL Experience Platform] proporciona la flexibilidad para definir un esquema basado en una clase que sea única para su organización. Para aprender a crear una nueva clase, consulte la guía sobre [creación y edición de clases en la interfaz de usuario](../ui/resources/classes.md#create).

### Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Las mezclas solo son compatibles con ciertas clases y, por lo tanto, cambiar la clase restablecerá el lienzo y los campos que haya agregado.

Para aprender a cambiar la clase de un esquema, consulte la guía sobre [administración de esquemas en la interfaz de usuario](../ui/resources/schemas.md).
