---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear esquemas
solution: Experience Platform
title: Crear un esquema con el editor de esquemas
topic-legacy: tutorial
type: Tutorial
description: Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '3754'
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
   * [Aspectos básicos de la composición](../schema/composition.md) del esquema: Una descripción general de los esquemas XDM y sus componentes básicos, incluidas las clases, los grupos de campos de esquema, los tipos de datos y los campos individuales.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Abra el espacio de trabajo [!UICONTROL Esquemas] {#browse}

El espacio de trabajo [!UICONTROL Esquemas] en la interfaz de usuario [!DNL Platform] proporciona una visualización del [!DNL Schema Library], lo que le permite ver y administrar los esquemas disponibles para su organización. El espacio de trabajo también incluye el [!DNL Schema Editor], el lienzo en el que puede componer un esquema a lo largo de este tutorial.

Después de iniciar sesión en [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir el espacio de trabajo **[!UICONTROL Esquemas]**. La pestaña **[!UICONTROL Browse]** muestra una lista de esquemas (una representación del [!DNL Schema Library]) que puede ver y personalizar. La lista incluye el nombre, el tipo, la clase y el comportamiento (registro o serie temporal) en los que se basa el esquema, así como la fecha y la hora de la última modificación del esquema.

Consulte la guía [Exploración de los recursos XDM existentes en la interfaz de usuario](../ui/explore.md) para obtener más información.

## Crear y asignar un nombre a un esquema {#create}

Para empezar a componer un esquema, seleccione **[!UICONTROL Create schema]** en la esquina superior derecha del espacio de trabajo **[!UICONTROL schemas]**. Aparece un menú desplegable que le ofrece la opción de elegir entre las clases principales [!UICONTROL XDM Individual Profile] y [!UICONTROL XDM ExperienceEvent]. Si estas clases no se adaptan a sus necesidades, también puede seleccionar **[!UICONTROL Browse]** para elegir entre otras clases disponibles o [crear una nueva clase](#create-new-class).

Para los fines de este tutorial, seleccione **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Dado que elige una clase XDM estándar en la que se basa el esquema, aparece el cuadro de diálogo **[!UICONTROL Add field group]**, que le permite empezar a añadir campos inmediatamente al esquema. Por ahora, seleccione **[!UICONTROL Cancelar]** para salir del cuadro de diálogo.

![](../images/tutorials/create-schema/cancel-field-group.png)

Aparece el [!DNL Schema Editor]. Este es el lienzo sobre el que compondrá el esquema. Se crea automáticamente un esquema sin título en la sección **[!UICONTROL Structure]** del lienzo al llegar al editor, junto con los campos estándar incluidos en todos los esquemas basados en esa clase. La clase asignada para el esquema también se enumera en **[!UICONTROL Clase]** en la sección **[!UICONTROL Composición]**.

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

Para agregar un grupo de campos, seleccione **[!UICONTROL Add]** en la subsección **[!UICONTROL Field groups]**.

![](../images/tutorials/create-schema/add-field-group-button.png)

Aparece un nuevo cuadro de diálogo que muestra una lista de los grupos de campos disponibles. Cada grupo de campos solo está diseñado para utilizarse con una clase específica, por lo que el cuadro de diálogo solo enumera los grupos de campos compatibles con la clase seleccionada (en este caso, la clase [!DNL XDM Individual Profile] ). Si utiliza una clase XDM estándar, la lista de grupos de campos se ordenará de forma inteligente según la popularidad de uso.

![](../images/tutorials/create-schema/field-group-popularity.png)

Si se selecciona un grupo de campos de la lista, este aparecerá en el carril derecho. Si lo desea, puede seleccionar varios grupos de campos, agregándolos a la lista en el carril derecho antes de confirmarlos. Además, aparece un icono en el lado derecho del grupo de campos seleccionado que permite obtener una vista previa de la estructura de los campos que proporciona.

![](../images/tutorials/create-schema/preview-field-group-button.png)

Al obtener una vista previa de un grupo de campos, se proporciona una descripción detallada del esquema del grupo de campos en el carril derecho. También puede navegar por los campos del grupo de campos en el lienzo proporcionado. A medida que selecciona diferentes campos, el carril derecho se actualiza para mostrar detalles sobre el campo en cuestión. Seleccione **[!UICONTROL Back]** cuando haya terminado de obtener una vista previa para volver al cuadro de diálogo de selección del grupo de campos.

![](../images/tutorials/create-schema/preview-field-group.png)

Para este tutorial, seleccione el grupo de campos **[!UICONTROL Demographic Details]** y, a continuación, seleccione **[!UICONTROL Add field group]**.

![](../images/tutorials/create-schema/demographic-details.png)

El lienzo del esquema vuelve a aparecer. La sección **[!UICONTROL Field groups]** ahora enumera &quot;[!UICONTROL Demographic Details]&quot; y la sección **[!UICONTROL Structure]** incluye los campos aportados por el grupo de campos. Puede seleccionar el nombre del grupo de campos en la sección **[!UICONTROL Field groups]** para resaltar los campos específicos que proporciona dentro del lienzo.

![](../images/tutorials/create-schema/demographic-details-structure.png)

Este grupo de campos contribuye con varios campos bajo el nombre de nivel superior `person` con el tipo de datos &quot;[!UICONTROL Persona]&quot;. Este grupo de campos describe información sobre un individuo, incluido el nombre, la fecha de nacimiento y el sexo.

>[!NOTE]
>
>Recuerde que los campos pueden utilizar tipos escalares (como cadena, entero, matriz o fecha), así como cualquier tipo de datos (un grupo de campos que representa un concepto común) definido dentro de [!DNL Schema Registry].

Observe que el campo `name` tiene un tipo de datos de &quot;[!UICONTROL Person name]&quot;, lo que significa que también describe un concepto común y contiene subcampos relacionados con los nombres, como nombre, apellidos, título de cortesía y sufijo.

Seleccione los diferentes campos dentro del lienzo para mostrar los campos adicionales que contribuyen a la estructura del esquema.

## Agregar otro grupo de campos {#field-group-2}

Ahora puede repetir los mismos pasos para agregar otro grupo de campos. Cuando vea el cuadro de diálogo **[!UICONTROL Agregar grupo de campos]** esta vez, observe que el grupo de campos &quot;[!UICONTROL Detalles demográficos]&quot; se ha atenuado y la casilla de verificación situada junto a él no se puede seleccionar. Esto evita que se dupliquen accidentalmente los grupos de campos que ya se han incluido en el esquema actual.

Para este tutorial, seleccione el grupo de campos &quot;[!DNL Personal Contact Details]&quot; en el cuadro de diálogo y, a continuación, seleccione **[!UICONTROL Add field group]** para agregarlo al esquema.

![](../images/tutorials/create-schema/personal-contact-details.png)

Una vez añadido, el lienzo vuelve a aparecer. &quot;[!UICONTROL Detalles de contacto personal]&quot; ahora aparece en **[!UICONTROL Grupos de campo]** en la sección **[!UICONTROL Composición]**, y se han agregado campos para dirección de inicio, teléfono móvil y más en **[!UICONTROL Estructura]**.

Al igual que el campo `name` , los campos que acaba de añadir representan conceptos de varios campos. Por ejemplo, `homeAddress` tiene un tipo de datos de &quot;[!UICONTROL Dirección postal]&quot; y `mobilePhone` tiene un tipo de datos de &quot;[!UICONTROL Número de teléfono]&quot;. Puede seleccionar cada uno de estos campos para expandirlos y ver los campos adicionales incluidos en el tipo de datos.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## Definir un grupo de campos personalizado {#define-field-group}

El esquema &quot;[!UICONTROL Loyalty Members]&quot; está diseñado para capturar datos relacionados con los miembros de un programa de fidelidad, por lo que se necesitarán algunos campos específicos relacionados con la fidelidad.

Hay un grupo de campos [!UICONTROL Detalles de lealtad] estándar que puede agregar al esquema para capturar campos comunes relacionados con un programa de fidelidad. Aunque se le recomienda encarecidamente que utilice grupos de campos estándar para representar los conceptos capturados por los esquemas, es posible que la estructura del grupo de campos de lealtad estándar no pueda capturar todos los datos relevantes para su programa de fidelidad en particular. En esta situación, puede definir un nuevo grupo de campos personalizados para capturar estos campos.

Vuelva a abrir el cuadro de diálogo **[!UICONTROL Agregar grupo de campos]**, pero esta vez seleccione **[!UICONTROL Crear nuevo grupo de campos]** cerca de la parte superior. A continuación, se le pedirá que proporcione un nombre para mostrar y una descripción para su grupo de campos.

![](../images/tutorials/create-schema/create-new-field-group.png)

Al igual que con los nombres de clase, el nombre del grupo de campos debe ser corto y sencillo, describiendo lo que el grupo de campos contribuirá al esquema. Estas también son únicas, por lo que no podrá reutilizar el nombre y, por lo tanto, debe asegurarse de que sea lo suficientemente específico.

Para este tutorial, asigne al nuevo grupo de campos el nombre &quot;Detalles de lealtad&quot;.

Seleccione **[!UICONTROL Add field group]** para volver al [!DNL Schema Editor]. &quot;[!UICONTROL Detalles de lealtad]&quot; debería aparecer ahora en **[!UICONTROL Grupos de campos]** en el lado izquierdo del lienzo, pero aún no hay campos asociados a él y, por lo tanto, no aparecen campos nuevos en **[!UICONTROL Estructura]**.

## Agregar campos al grupo de campos {#field-group-fields}

Ahora que ha creado el grupo de campos &quot;Detalles de lealtad&quot;, ha llegado el momento de definir los campos que el grupo de campos contribuirá al esquema.

Para empezar, seleccione el nombre del grupo de campos en la sección **[!UICONTROL Field groups]**. Una vez hecho esto, las propiedades del grupo de campos aparecen en el lado derecho del editor y aparece un icono **plus (+)** junto al nombre del esquema en **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleccione el icono **plus (+)** situado junto a &quot;[!DNL Loyalty Members]&quot; para crear un nuevo nodo en la estructura. Este nodo (denominado `_tenantId` en este ejemplo) representa el ID de inquilino de la organización IMS, precedido por un guion bajo. La presencia del ID de inquilino indica que los campos que está agregando están contenidos en el espacio de nombres de su organización.

En otras palabras, los campos que agregue son únicos para su organización y se guardarán en [!DNL Schema Registry] en un área específica accesible solo para su organización. Los campos que defina siempre deben agregarse al espacio de nombres del inquilino para evitar conflictos con nombres de otras clases estándar, grupos de campos, tipos de datos y campos.

Dentro de ese nodo con espacio de nombres hay un &quot;[!UICONTROL Nuevo campo]&quot;. Este es el principio del grupo de campos &quot;[!UICONTROL Detalles de lealtad]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Con los controles del lado derecho del editor, comience creando un campo `loyalty` con el tipo &quot;[!UICONTROL Object]&quot; que se utilizará para incluir los campos relacionados con la lealtad. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Los cambios se aplican y aparece el objeto `loyalty` recién creado. Seleccione el icono **plus (+)** situado junto al objeto para añadir campos adicionales relacionados con la lealtad. Aparece un &quot;[!UICONTROL Nuevo campo]&quot; y la sección **[!UICONTROL Propiedades del campo]** está visible en el lado derecho del lienzo.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requiere la siguiente información:

* **[!UICONTROL Nombre] del campo:** el nombre del campo, escrito en el caso del camello. Ejemplo: loyaltyLevel
* **[!UICONTROL Nombre para mostrar]:** el nombre del campo, escrito en el caso del título. Ejemplo: Nivel de fidelidad
* **[!UICONTROL Tipo]:** el tipo de datos del campo. Esto incluye tipos escalares básicos y cualquier tipo de datos definido en el [!DNL Schema Registry]. Ejemplos: [!UICONTROL Cadena], [!UICONTROL Entero], [!UICONTROL Booleano], [!UICONTROL Persona], [!UICONTROL Dirección], [!UICONTROL Número de teléfono], etc.
* **[!UICONTROL Descripción]:** Se debe incluir una descripción opcional del campo, escrita en caso de sentencia, con un máximo de 200 caracteres.

El primer campo del objeto `Loyalty` será una cadena denominada `loyaltyId`. Al establecer el tipo del nuevo campo en &quot;[!UICONTROL String]&quot;, la sección **[!UICONTROL Field properties]** se rellena con varias opciones para aplicar restricciones, incluidos el valor predeterminado, el formato y la longitud máxima.

![](../images/tutorials/create-schema/string_constraints.png)

Hay diferentes opciones de restricción disponibles en función del tipo de datos seleccionado. Dado que `loyaltyId` será una dirección de correo electrónico, seleccione &quot;[!UICONTROL email]&quot; en el menú desplegable **[!UICONTROL Formato]**. Seleccione **[!UICONTROL Aplicar]** para aplicar los cambios.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Agregar más campos al grupo de campos {#field-group-fields-2}

Ahora que ha agregado el campo `loyaltyId`, puede agregar campos adicionales para capturar información relacionada con la lealtad, como:

* Puntos (entero)
* Miembro desde (fecha)

Para añadir cada campo al esquema, seleccione el icono **plus (+)** junto al objeto `loyalty` y rellene la información necesaria.

Cuando se complete, el objeto Lealtad contendrá campos para ID de fidelidad, puntos y desde entonces.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Añadir un campo de enumeración al grupo de campos {#enum}

Al definir campos en [!DNL Schema Editor], hay algunas opciones adicionales que puede aplicar a tipos de campo básicos para proporcionar más restricciones en los datos que el campo puede contener. Los casos de uso de estas restricciones se explican en la siguiente tabla:

| Restricción | Descripción |
| --- | --- |
| [!UICONTROL Requerido] | Indica que el campo es necesario para la ingesta de datos. Cualquier dato cargado en un conjunto de datos basado en este esquema que no contenga este campo fallará tras la ingesta. |
| [!UICONTROL Matriz] | Indica que el campo contiene una matriz de valores, cada uno con el tipo de datos especificado. Por ejemplo, el uso de esta restricción en un campo con un tipo de datos de &quot;[!UICONTROL String]&quot; especifica que el campo contendrá una matriz de cadenas. |
| [!UICONTROL Enum] | Indica que este campo debe contener uno de los valores de una lista enumerada de valores posibles. |
| [!UICONTROL Identidad] | Indica que este campo es de identidad. Más información sobre los campos de identidad se proporciona [más adelante en este tutorial](#identity-field). |
| [!UICONTROL Relación] | Aunque las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. La restricción [!UICONTROL Relationship] indica que este campo hace referencia a la identidad principal de un esquema basado en una clase diferente, lo que implica una relación entre los dos esquemas. Consulte el tutorial sobre [definición de una relación](./relationship-ui.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Los campos requeridos, de identidad o de relación se muestran en el carril izquierdo, lo que permite localizar estos campos fácilmente independientemente de la complejidad del esquema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, el objeto [!DNL "loyalty"] del esquema requiere un nuevo campo de enumeración que describa el &quot;nivel de lealtad&quot; de un cliente, donde el valor solo puede ser una de las cuatro opciones posibles. Para añadir este campo al esquema, seleccione el icono **plus (+)** junto al objeto `loyalty` y rellene los campos obligatorios para **[!UICONTROL Field name]** y **[!UICONTROL Display name]**. Para **[!UICONTROL Type]**, seleccione &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Después de seleccionar su tipo, aparecen casillas de verificación adicionales para el campo, incluidas las casillas de verificación **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Active la casilla **[!UICONTROL Enum]** para abrir la sección **[!UICONTROL Enum values]** que aparece a continuación. Aquí puede introducir el **[!UICONTROL Value]** (en camelCase) y la **[!UICONTROL Label]** (un nombre opcional y fácil de leer en el caso del título) para cada nivel de lealtad aceptable.

Cuando haya completado todas las propiedades del campo, seleccione **[!UICONTROL Apply]** para agregar el campo &quot;[!DNL loyaltyLevel]&quot; al objeto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversión de un objeto de varios campos en un tipo de datos {#datatype}

El objeto `loyalty` ahora contiene varios campos específicos de lealtad y representa una estructura de datos común que podría resultar útil en otros esquemas. El [!DNL Schema Editor] permite aplicar fácilmente objetos de varios campos reutilizables convirtiendo la estructura de esos objetos en tipos de datos.

Los tipos de datos permiten el uso coherente de estructuras de varios campos y proporcionan más flexibilidad que un grupo de campos, ya que se pueden utilizar en cualquier lugar dentro de un esquema. Esto se hace estableciendo el valor **[!UICONTROL Type]** del campo en el valor de cualquier tipo de datos definido en [!DNL Schema Registry].

Para convertir el objeto `loyalty` en un tipo de datos, seleccione el campo `loyalty` en **[!UICONTROL Estructura]** y, a continuación, seleccione **[!UICONTROL Convertir en nuevo tipo de datos]** en el lado derecho del editor, en **[!UICONTROL Propiedades del campo]**. Aparece una ventana emergente verde que confirma que el objeto se ha convertido correctamente.

![](../images/tutorials/create-schema/convert-data-type.png)

Ahora, al mirar en **[!UICONTROL Structure]**, puede ver que el campo `loyalty` tiene un tipo de datos &quot;[!DNL Loyalty]&quot; y que los campos tienen iconos de bloqueo pequeños junto a ellos, lo que indica que ya no son campos individuales sino parte de un tipo de datos de varios campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

En un esquema futuro, ahora se podría asignar un campo como tipo &quot;[!DNL Loyalty]&quot; y se incluirían automáticamente campos para ID, nivel de lealtad, miembro desde y puntos.

>[!NOTE]
>
>También puede crear y editar tipos de datos personalizados de forma independiente de la edición de esquemas. Consulte la guía sobre [creación y edición de tipos de datos](../ui/resources/data-types.md) para obtener más información.

## Buscar y filtrar campos de esquema

El esquema ahora contiene varios grupos de campos además de los campos proporcionados por su clase base. Al trabajar con esquemas más grandes, puede seleccionar las casillas de verificación situadas junto a los nombres de los grupos de campos en el carril izquierdo para filtrar los campos mostrados únicamente a los proporcionados por los grupos de campos que le interesen.

![](../images/tutorials/create-schema/filter-by-field-group.png)

Si está buscando un campo específico en el esquema, también puede utilizar la barra de búsqueda para filtrar los campos mostrados por nombre, independientemente del grupo de campos en el que se proporcionen.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La función de búsqueda tiene en cuenta los filtros de grupo de campos seleccionados al mostrar los campos coincidentes. Si una consulta de búsqueda no muestra los resultados esperados, es posible que tenga que verificar que no está filtrando ningún grupo de campos relevante.

## Establecer un campo de esquema como campo de identidad {#identity-field}

La estructura de datos estándar que proporcionan los esquemas se puede aprovechar para identificar los datos que pertenecen al mismo individuo en múltiples fuentes, lo que permite varios casos de uso descendente como segmentación, informes, análisis de ciencia de datos, etc. Para unir datos en función de identidades individuales, los campos clave deben marcarse como campos [!UICONTROL Identity] dentro de los esquemas aplicables.

[!DNL Experience Platform] facilita la identificación de un campo de identidad mediante el uso de una casilla de verificación  **** Identityen  [!DNL Schema Editor]. Sin embargo, debe determinar qué campo es el mejor candidato para utilizarlo como identidad, en función de la naturaleza de los datos.

Por ejemplo, puede haber miles de miembros del programa de fidelidad que pertenezcan al mismo &quot;nivel de fidelidad&quot;, pero cada miembro del programa de fidelidad tiene un `loyaltyId` único (que en este caso es la dirección de correo electrónico del miembro individual). El hecho de que `loyaltyId` sea un identificador único para cada miembro lo convierte en un buen candidato para un campo de identidad, mientras que `loyaltyLevel` no lo es.

>[!IMPORTANT]
>
>Los pasos que se describen a continuación abarcan cómo agregar un descriptor de identidad a un campo de esquema existente. Como alternativa a definir campos de identidad dentro de la estructura del propio esquema, también puede utilizar un campo `identityMap` para contener información de identidad en su lugar.
>
>Si planea utilizar `identityMap`, tenga en cuenta que anulará cualquier identidad principal que agregue al esquema directamente. Consulte la sección sobre `identityMap` en la [Guía básica de composición de esquema](../schema/composition.md#identityMap) para obtener más información.

En la sección **[!UICONTROL Structure]** del editor, seleccione el campo `loyaltyId` y la casilla **[!UICONTROL Identity]** aparece en **[!UICONTROL Field properties]**. Marque la casilla y la opción para establecerla como aparece la **[!UICONTROL Primary identity]**. Seleccione también este cuadro.

>[!NOTE]
>
>Cada esquema puede contener solo un campo de identidad principal. Una vez que se ha establecido un campo de esquema como identidad principal, recibirá un mensaje de error si más tarde intenta establecer otro campo de identidad en el esquema como principal.

A continuación, debe proporcionar un **[!UICONTROL espacio de nombres de identidad]** de la lista de espacios de nombres predefinidos de la lista desplegable. Dado que `loyaltyId` es la dirección de correo electrónico del cliente, seleccione &quot;[!UICONTROL Correo electrónico]&quot; en la lista desplegable. Seleccione **[!UICONTROL Apply]** para confirmar las actualizaciones del campo `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obtener una lista de áreas de nombres estándar y sus definiciones, consulte la [[!DNL Identity Service] documentación](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Después de aplicar el cambio, el icono de `loyaltyId` muestra un símbolo de huella digital, que indica que ahora es un campo de identidad.

![](../images/tutorials/create-schema/identity-applied.png)

Ahora todos los datos incorporados en el campo `loyaltyId` se utilizan para ayudar a identificar a ese individuo y unir una sola vista de ese cliente. Para obtener más información sobre cómo trabajar con identidades en [!DNL Experience Platform], consulte la documentación de [[!DNL Identity Service]](../../identity-service/home.md).

## Habilitar el esquema para utilizarlo en [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) aprovecha los datos de identidad en  [!DNL Experience Platform] para proporcionar una vista holística de cada cliente individual. El servicio crea perfiles sólidos de 360° de atributos del cliente, así como cuentas con marca de tiempo de cada interacción que los clientes han tenido en cualquier sistema integrado con [!DNL Experience Platform].

Para que un esquema esté habilitado para utilizarse con [!DNL Real-time Customer Profile], debe tener una identidad principal definida. Recibirá un mensaje de error si intenta habilitar un esquema sin definir primero una identidad principal.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para habilitar el esquema &quot;Miembros de lealtad&quot; para su uso en [!DNL Profile], comience por seleccionar &quot;[!DNL Loyalty Members]&quot; en la sección **[!UICONTROL Estructura]** del editor.

A la derecha del editor, se muestra información sobre el esquema, incluido su nombre para mostrar, descripción y tipo. Además de esta información, hay un botón de alternancia **[!UICONTROL Profile]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Seleccione **[!UICONTROL Perfil]** y aparecerá una ventana emergente para pedirle que confirme que desea habilitar el esquema para [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una vez que un esquema se ha habilitado para [!DNL Real-time Customer Profile] y se ha guardado, no se puede desactivar.

Seleccione **[!UICONTROL Enable]** para confirmar su elección. Puede seleccionar de nuevo la opción **[!UICONTROL Profile]** para deshabilitar el esquema si lo desea, pero una vez que el esquema se ha guardado mientras [!DNL Profile] está habilitado, ya no se puede deshabilitar.

## Pasos siguientes y recursos adicionales

Ahora que ha terminado de componer el esquema, puede ver el esquema completo en el lienzo. Seleccione **[!UICONTROL Save]** y el esquema se guardará en [!DNL Schema Library], de modo que el [!DNL Schema Registry] pueda acceder a él.

El nuevo esquema ahora se puede usar para introducir datos en [!DNL Platform]. Recuerde que una vez que el esquema se ha utilizado para introducir datos, solo se pueden realizar cambios aditivos. Consulte los [conceptos básicos de la composición de esquema](../schema/composition.md) para obtener más información sobre el control de versiones de esquemas.

Ahora puede seguir el tutorial sobre la [definición de una relación de esquema en la interfaz de usuario](./relationship-ui.md) para agregar un nuevo campo de relación al esquema &quot;Miembros de lealtad&quot;.

El esquema &quot;Miembros de lealtad&quot; también está disponible para su visualización y administración mediante la API [!DNL Schema Registry]. Para empezar a trabajar con la API, lea la [[!DNL Schema Registry API] guía para desarrolladores](../api/getting-started.md).

### Recursos de vídeo

>[!WARNING]
>
>La interfaz de usuario [!DNL Platform] que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

El siguiente vídeo muestra cómo crear un esquema simple en la interfaz de usuario [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

El siguiente vídeo pretende reforzar su comprensión del trabajo con grupos de campo y clases.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre el uso de [!DNL Schema Editor].

### Crear una nueva clase {#create-new-class}

[!DNL Experience Platform] proporciona la flexibilidad para definir un esquema basado en una clase que sea única para su organización. Para aprender a crear una nueva clase, consulte la guía sobre [creación y edición de clases en la interfaz de usuario](../ui/resources/classes.md#create).

### Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Los grupos de campos solo son compatibles con ciertas clases y, por lo tanto, al cambiar la clase se restablecerá el lienzo y los campos que haya agregado.

Para aprender a cambiar la clase de un esquema, consulte la guía sobre [administración de esquemas en la interfaz de usuario](../ui/resources/schemas.md).
