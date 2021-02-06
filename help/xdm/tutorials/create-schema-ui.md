---
keywords: Experience Platform;inicio;temas populares;ui;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquema;editor de Esquemas;esquema;Esquema;esquemas;Esquemas;crear
solution: Experience Platform
title: Creación de un Esquema con el Editor de Esquemas
topic: tutorial
type: Tutorial
description: Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '3600'
ht-degree: 0%

---


# Crear un esquema con el [!DNL Schema Editor]

La interfaz de usuario de Adobe Experience Platform le permite crear y administrar esquemas [!DNL Experience Data Model] (XDM) en un lienzo visual interactivo denominado [!DNL Schema Editor]. Este tutorial explica cómo crear un esquema con el [!DNL Schema Editor].

>[!NOTE]
>
>Para demostraciones, los pasos de este tutorial incluyen la creación de un esquema de ejemplo que describe a los miembros de un programa de lealtad del cliente. Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda que primero siga con la creación del esquema de ejemplo para conocer las capacidades del [!DNL Schema Editor].

Si prefiere componer un esquema con la API [!DNL Schema Registry] en su lugar, lea la [[!DNL Schema Registry] guía para desarrolladores](../api/getting-started.md) antes de intentar el tutorial sobre [la creación de un esquema con la API](create-schema-api.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos aspectos de Adobe Experience Platform relacionados con la creación de esquemas. Antes de comenzar este tutorial, consulte la documentación de los siguientes conceptos:

* [[!DNL Experience Data Model (XDM)]](../home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../schema/composition.md) de esquemas: Información general sobre los esquemas XDM y sus componentes, incluidas clases, mezclas, tipos de datos y campos.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Abra el espacio de trabajo [!UICONTROL Esquemas] {#browse}

El espacio de trabajo [!UICONTROL Esquemas] de la [!DNL Platform] interfaz de usuario proporciona una visualización del [!DNL Schema Library], lo que le permite administrar en vista los esquemas disponibles para su organización. El espacio de trabajo también incluye el [!DNL Schema Editor] lienzo en el que puede componer un esquema a lo largo de este tutorial.

Después de iniciar sesión en [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en la navegación izquierda para abrir el espacio de trabajo **[!UICONTROL Esquemas]**. La ficha **[!UICONTROL Examinar]** muestra una lista de esquemas (una representación de [!DNL Schema Library]) que puede vista y personalizar. La lista incluye el nombre, el tipo, la clase y el comportamiento (registro o serie temporal) en los que se basa el esquema, así como la fecha y la hora en que se modificó el esquema por última vez.

Consulte la guía sobre [exploración de recursos XDM existentes en la interfaz de usuario](../ui/explore.md) para obtener más información.

## Crear y asignar un nombre a un esquema {#create}

Para empezar a componer un esquema, seleccione **[!UICONTROL Crear esquema]** en la esquina superior derecha del espacio de trabajo **[!UICONTROL Esquemas]**. Aparece un menú desplegable que le ofrece la opción de elegir entre las clases principales [!UICONTROL Perfil individual XDM] y [!UICONTROL EventoExperienciaXDM]. Si estas clases no se ajustan a sus necesidades, también puede seleccionar **[!UICONTROL Examinar]** para elegir entre otras clases disponibles o [crear una nueva clase](#create-new-class).

Para los fines de este tutorial, seleccione **[!UICONTROL Perfil individual XDM]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Aparece el [!DNL Schema Editor]. Este es el lienzo sobre el cual compondrás tu esquema. Como eligió una clase XDM estándar en la que basar el esquema, se crea automáticamente un esquema sin título en la sección **[!UICONTROL Estructura]** del lienzo al llegar al editor, junto con los campos estándar incluidos en todos los esquemas basados en esa clase. La clase asignada para el esquema también se encuentra en la sección **[!UICONTROL Clase]** de **[!UICONTROL Composición]**.

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

Para agregar una mezcla, seleccione **[!UICONTROL Añadir]** en la subsección **[!UICONTROL Mezclas]**.

![](../images/tutorials/create-schema/add_mixin_button.png)

Aparece un nuevo cuadro de diálogo, que muestra una lista de mezclas disponibles. Cada mezcla está destinada únicamente a utilizarse con una clase específica, por lo que el cuadro de diálogo sólo lista mezclas compatibles con la clase seleccionada (en este caso, la clase [!DNL XDM Individual Profile]). Si utiliza una clase XDM estándar, la lista de mezclas se ordenará de forma inteligente en función de la popularidad del uso.

![](../images/tutorials/create-schema/mixin-popularity.png)

La selección de una mezcla de la lista hace que aparezca en el carril derecho. Puede seleccionar varias mezclas si lo desea, agregando cada una a la lista en el carril derecho antes de confirmar. Además, aparece un icono en el lado derecho de la mezcla seleccionada que le permite realizar una previsualización de la estructura de los campos que proporciona.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Al previsualizar una mezcla, se proporciona una descripción detallada del esquema de la mezcla en el carril derecho. También puede navegar por los campos de la mezcla en el lienzo proporcionado. Al seleccionar campos diferentes, se actualiza el carril correcto para mostrar detalles sobre el campo en cuestión. Seleccione **[!UICONTROL Atrás]** cuando termine de obtener una vista previa para volver al cuadro de diálogo de selección de mezcla.

![](../images/tutorials/create-schema/preview-mixin.png)

Para este tutorial, seleccione la mezcla **[!UICONTROL Detalles demográficos]** y, a continuación, seleccione **[!UICONTROL Añadir mezcla]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

El lienzo del esquema vuelve a aparecer. La sección **[!UICONTROL Mezclas]** ahora lista &quot;[!UICONTROL Detalles demográficos]&quot; y la sección **[!UICONTROL Estructura]** incluye los campos que aporta la mezcla. Puede seleccionar el nombre de la mezcla en la sección **[!UICONTROL Mezclas]** para resaltar los campos específicos que proporciona dentro del lienzo.

![](../images/tutorials/create-schema/person_details_structure.png)

Esta combinación aporta varios campos bajo el nombre de nivel superior `person` con el tipo de datos &quot;[!UICONTROL Persona]&quot;. Este grupo de campos describe información sobre un individuo, incluido el nombre, la fecha de nacimiento y el sexo.

>[!NOTE]
>
>Recuerde que los campos pueden utilizar tipos escalares (como cadena, entero, matriz o fecha), así como cualquier tipo de datos (un grupo de campos que representa un concepto común) definido dentro de [!DNL Schema Registry].

Observe que el campo `name` tiene un tipo de datos de &quot;[!UICONTROL Nombre de la persona]&quot;, lo que significa que también describe un concepto común y contiene subcampos relacionados con los nombres, como nombre, apellidos, título de cortesía y sufijo.

Seleccione los diferentes campos dentro del lienzo para mostrar los campos adicionales que contribuyen a la estructura de esquema.

## Añadir otra mezcla {#mixin-2}

Ahora puede repetir los mismos pasos para agregar otra mezcla. Cuando vista el cuadro de diálogo **[!UICONTROL Añadir mezcla]** esta vez, tenga en cuenta que la mezcla &quot;[!UICONTROL Detalles demográficos]&quot; se ha atenuado y que la casilla de verificación situada junto a él no se puede seleccionar. Esto evita que usted duplique accidentalmente las mezclas que ya ha incluido en el esquema actual.

Para este tutorial, seleccione la mezcla &quot;[!DNL Personal Contact Details]&quot; en el cuadro de diálogo y, a continuación, seleccione **[!UICONTROL Añadir mezcla]** para agregarla al esquema.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una vez agregado, el lienzo vuelve a aparecer. &quot;[!UICONTROL Detalles de contacto personal]&quot; ahora se encuentra en **[!UICONTROL Mezclas]** en la sección **[!UICONTROL Composición]**, y se han agregado campos para dirección doméstica, teléfono móvil y más en **[!UICONTROL Estructura]**.

Al igual que el campo `name`, los campos que acaba de agregar representan conceptos de varios campos. Por ejemplo, `homeAddress` tiene un tipo de datos de &quot;[!UICONTROL dirección postal]&quot; y `mobilePhone` tiene un tipo de datos de &quot;[!UICONTROL número de teléfono]&quot;. Puede seleccionar cada uno de estos campos para expandirlos y ver los campos adicionales incluidos en el tipo de datos.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definir una nueva mezcla {#define-mixin}

El esquema &quot;[!UICONTROL Miembros de lealtad]&quot; tiene el propósito de capturar datos relacionados con los miembros de un programa de lealtad, por lo que requerirá algunos campos específicos relacionados con la lealtad. No hay mezclas estándar disponibles que contengan los campos necesarios, por lo tanto deberá definir una nueva mezcla.

Esta vez, cuando abra el cuadro de diálogo **[!UICONTROL Añadir mezcla]**, seleccione **[!UICONTROL Crear nueva mezcla]**. Luego se le pedirá que proporcione un nombre para mostrar y una descripción para la mezcla.

![](../images/tutorials/create-schema/mixin_create_new.png)

Al igual que con los nombres de clase, el nombre de la mezcla debe ser corto y simple, describiendo lo que la mezcla contribuirá al esquema. Estos también son únicos, por lo que no podrá reutilizar el nombre y, por lo tanto, debe asegurarse de que sea lo suficientemente específico.

Para este tutorial, asigne un nombre a la nueva combinación &quot;Detalles de lealtad&quot;.

Seleccione **[!UICONTROL Añadir mezcla]** para volver a [!DNL Schema Editor]. &quot;[!UICONTROL Detalles de lealtad]&quot; debe aparecer ahora en **[!UICONTROL Mezclas]** en el lado izquierdo del lienzo, pero aún no hay campos asociados a él y, por lo tanto, no aparecen nuevos campos en **[!UICONTROL Estructura]**.

## Añadir campos a la mezcla {#mixin-fields}

Ahora que ha creado la mezcla &quot;Detalles de Lealtad&quot;, es hora de definir los campos que la mezcla contribuirá al esquema.

Para comenzar, seleccione el nombre de la mezcla en la sección **[!UICONTROL Mezclas]**. Una vez hecho esto, las propiedades de la mezcla aparecen en la parte derecha del editor y aparece un icono **más (+)** junto al nombre del esquema en **[!UICONTROL Estructura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleccione el icono **más (+)** junto a &quot;[!DNL Loyalty Members]&quot; para crear un nuevo nodo en la estructura. Este nodo (denominado `_tenantId` en este ejemplo) representa la ID de inquilino de la organización de IMS, precedida por un guion bajo. La presencia de la ID de inquilino indica que los campos que está agregando están contenidos en la Área de nombres de su organización.

En otras palabras, los campos que está agregando son exclusivos de su organización y se guardarán en [!DNL Schema Registry] en un área específica a la que solo pueda acceder su organización. Los campos que defina siempre deben agregarse a la Área de nombres del inquilino para evitar conflictos con nombres de otras clases estándar, mezclas, tipos de datos y campos.

Dentro de ese nodo con espacio de nombres hay un &quot;[!UICONTROL Nuevo campo]&quot;. Este es el comienzo de la mezcla &quot;[!UICONTROL Detalles de lealtad]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Con los controles del lado derecho del editor, cree un campo `loyalty` de inicio con el tipo &quot;[!UICONTROL Object]&quot; que se utilizará para mantener los campos relacionados con la lealtad. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Los cambios se aplican y aparece el objeto `loyalty` recién creado. Seleccione el icono **más (+)** junto al objeto para agregar campos adicionales relacionados con la lealtad. Aparece un &quot;[!UICONTROL Nuevo campo]&quot; y la sección **[!UICONTROL Propiedades del campo]** está visible en el lado derecho del lienzo.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requiere la siguiente información:

* **[!UICONTROL Nombre] del campo:** El nombre del campo, escrito en caso de camello. Ejemplo: loyaltyLevel
* **[!UICONTROL Nombre] para mostrar:** el nombre del campo, escrito en el caso del título. Ejemplo: Nivel de fidelidad
* **[!UICONTROL Tipo]:** El tipo de datos del campo. Esto incluye tipos escalares básicos y cualquier tipo de datos definido en [!DNL Schema Registry]. Ejemplos: [!UICONTROL Cadena], [!UICONTROL Entero], [!UICONTROL Boolean], [!UICONTROL Persona], [!UICONTROL Dirección], [!UICONTROL Número de teléfono], etc.
* **[!UICONTROL Descripción]:** Se debe incluir una descripción opcional del campo, escrita en caso de sentencia, con un máximo de 200 caracteres.

El primer campo del objeto `Loyalty` será una cadena llamada `loyaltyId`. Al establecer el tipo del nuevo campo en &quot;[!UICONTROL String]&quot;, la sección **[!UICONTROL Propiedades del campo]** se llena con varias opciones para aplicar restricciones, incluido el valor predeterminado, el formato y la longitud máxima.

![](../images/tutorials/create-schema/string_constraints.png)

Hay diferentes opciones de restricción disponibles según el tipo de datos seleccionado. Dado que `loyaltyId` será una dirección de correo electrónico, seleccione &quot;[!UICONTROL correo electrónico]&quot; en el menú desplegable **[!UICONTROL Formato]**. Seleccione **[!UICONTROL Aplicar]** para aplicar los cambios.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Añadir más campos a la mezcla {#mixin-fields-2}

Ahora que ha agregado el campo `loyaltyId`, puede agregar campos adicionales para capturar información relacionada con la lealtad como:

* Puntos (entero)
* Miembro desde (fecha)

Para agregar cada campo al esquema, seleccione el icono **más (+)** junto al objeto `loyalty` y rellene la información requerida.

Una vez completado, el objeto Lealtad contendrá campos para ID de lealtad, puntos y elementos desde los que se obtuvo.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Añadir un campo de enumeración a la mezcla {#enum}

Al definir campos en [!DNL Schema Editor], existen algunas opciones adicionales que puede aplicar a los tipos de campo básicos para proporcionar restricciones adicionales en los datos que el campo puede contener. Los casos de uso de estas restricciones se explican en la siguiente tabla:

| Restricción | Descripción |
| --- | --- |
| [!UICONTROL Requerido] | Indica que el campo es obligatorio para la ingesta de datos. Cualquier dato cargado en un conjunto de datos basado en este esquema que no contenga este campo fallará durante la ingestión. |
| [!UICONTROL Matriz] | Indica que el campo contiene una matriz de valores, cada uno con el tipo de datos especificado. Por ejemplo, si se utiliza esta restricción en un campo con un tipo de datos &quot;[!UICONTROL String]&quot;, se especifica que el campo contendrá una matriz de cadenas. |
| [!UICONTROL Enum] | Indica que este campo debe contener uno de los valores de una lista enumerada de valores posibles. |
| [!UICONTROL Identidad] | Indica que este campo es un campo de identidad. Más información sobre los campos de identidad se proporciona [más adelante en este tutorial](#identity-field). |
| [!UICONTROL Relación] | Aunque las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. La restricción [!UICONTROL Relationship] indica que este campo hace referencia a la identidad principal de un esquema basado en una clase diferente, lo que implica una relación entre los dos esquemas. Consulte el tutorial sobre [definición de una relación](./relationship-ui.md) para obtener más información. |

>[!NOTE]
>
>Todos los campos obligatorios, de identidad o de relación se muestran en el carril izquierdo, lo que permite localizar estos campos fácilmente independientemente de la complejidad del esquema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, el objeto [!DNL "loyalty"] del esquema requiere un nuevo campo de enumeración que describa el &quot;nivel de lealtad&quot; de un cliente, donde el valor sólo puede ser una de las cuatro opciones posibles. Para agregar este campo al esquema, seleccione el icono **más (+)** junto al objeto `loyalty` y rellene los campos obligatorios para **[!UICONTROL Nombre del campo]** y **[!UICONTROL Nombre para mostrar]**. Para **[!UICONTROL Tipo]**, seleccione &quot;[!UICONTROL Cadena]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Aparecerán casillas de verificación adicionales para el campo después de que se haya seleccionado su tipo, incluidas las casillas de verificación para **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Seleccione la casilla **[!UICONTROL Enum]** para abrir la sección **[!UICONTROL Enum values]** a continuación. Aquí puede introducir el **[!UICONTROL valor]** (en camelCase) y **[!UICONTROL etiqueta]** (un nombre opcional y fácil de leer en el caso del título) para cada nivel de lealtad aceptable.

Cuando haya completado todas las propiedades del campo, seleccione **[!UICONTROL Aplicar]** para agregar el campo &quot;[!DNL loyaltyLevel]&quot; al objeto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversión de un objeto de varios campos en un tipo de datos {#datatype}

El objeto `loyalty` ahora contiene varios campos específicos de lealtad y representa una estructura de datos común que podría ser útil en otros esquemas. El [!DNL Schema Editor] permite aplicar fácilmente objetos de varios campos reutilizables mediante la conversión de la estructura de esos objetos en tipos de datos.

Los tipos de datos permiten el uso coherente de estructuras de varios campos y proporcionan más flexibilidad que una mezcla, ya que se pueden utilizar en cualquier lugar dentro de un esquema. Esto se realiza estableciendo el valor **[!UICONTROL Type]** del campo en el valor de cualquier tipo de datos definido en [!DNL Schema Registry].

Para convertir el objeto `loyalty` en un tipo de datos, seleccione el campo `loyalty` en **[!UICONTROL Estructura]** y, a continuación, seleccione **[!UICONTROL Convertir en nuevo tipo de datos]** en el lado derecho del editor en **[!UICONTROL Propiedades del campo]**. Aparece una ventana emergente verde que confirma que el objeto se ha convertido correctamente.

![](../images/tutorials/create-schema/convert-data-type.png)

Ahora, cuando consulta en **[!UICONTROL Estructura]**, puede ver que el campo `loyalty` tiene un tipo de datos &quot;[!DNL Loyalty]&quot; y que los campos tienen iconos de bloqueo pequeños junto a ellos, lo que indica que ya no son campos individuales sino que forman parte de un tipo de datos de varios campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

En un esquema futuro, ahora se puede asignar un campo como tipo &quot;[!DNL Loyalty]&quot; y se incluirán automáticamente campos para ID, nivel de lealtad, miembro desde y puntos.

>[!NOTE]
>
>También puede crear y editar tipos de datos personalizados independientemente de la edición de esquemas. Consulte la guía sobre [creación y edición de tipos de datos](../ui/resources/data-types.md) para obtener más información.

## Buscar y filtrar campos de esquema

El esquema ahora contiene varias mezclas además de los campos proporcionados por su clase base. Al trabajar con esquemas más grandes, puede seleccionar las casillas de verificación situadas junto a los nombres de las mezclas en el carril izquierdo para filtrar los campos mostrados únicamente a los proporcionados por las mezclas que le interesen.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Si busca un campo específico en el esquema, también puede utilizar la barra de búsqueda para filtrar los campos mostrados por nombre, independientemente de la mezcla en la que se proporcionen.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La función de búsqueda tiene en cuenta cualquier filtros de mezcla seleccionado al mostrar los campos coincidentes. Si una consulta de búsqueda no muestra los resultados esperados, es posible que tenga que comprobar con doble que no está filtrando ninguna mezcla relevante.

## Establecer un campo de esquema como campo de identidad {#identity-field}

La estructura de datos estándar que proporcionan los esquemas se puede aprovechar para identificar los datos que pertenecen a la misma persona en múltiples fuentes, permitiendo diversos casos de uso descendente como segmentación, sistema de informes, análisis de la ciencia de datos, etc. Para poder unir datos en función de identidades individuales, los campos clave deben marcarse como campos [!UICONTROL Identidad] dentro de los esquemas aplicables.

[!DNL Experience Platform] facilita la identificación de un campo de identidad mediante el uso de una casilla de verificación  **** Identidad en la  [!DNL Schema Editor]. Sin embargo, debe determinar qué campo es el mejor candidato para utilizar como identidad, en función de la naturaleza de los datos.

Por ejemplo, puede haber miles de miembros del programa de lealtad que pertenecen al mismo &quot;nivel de lealtad&quot;, pero cada miembro del programa de lealtad tiene un `loyaltyId` único (que en este caso es la dirección de correo electrónico del miembro individual). El hecho de que `loyaltyId` sea un identificador único para cada miembro lo convierte en un buen candidato para un campo de identidad, mientras que `loyaltyLevel` no lo es.

>[!IMPORTANT]
>
>Los pasos que se describen a continuación explican cómo agregar un descriptor de identidad a un campo de esquema existente. Como alternativa a definir campos de identidad dentro de la estructura del esquema mismo, también puede utilizar un campo `identityMap` para contener información de identidad.
>
>Si planea utilizar `identityMap`, tenga en cuenta que anulará cualquier identidad principal que agregue directamente al esquema. Consulte la sección sobre `identityMap` en la [guía básica de composición de esquema](../schema/composition.md#identityMap) para obtener más información.

En la sección **[!UICONTROL Estructura]** del editor, seleccione el campo `loyaltyId` y la casilla **[!UICONTROL Identidad]** aparece en **[!UICONTROL Propiedades del campo]**. Marque la casilla y la opción para establecerla como **[!UICONTROL Identidad principal]** aparece. Seleccione también este cuadro.

>[!NOTE]
>
>Cada esquema puede contener sólo un campo de identidad principal. Una vez que un campo de esquema se haya establecido como identidad principal, recibirá un mensaje de error si posteriormente intenta establecer otro campo de identidad en el esquema como principal.

A continuación, debe proporcionar una **[!UICONTROL Área de nombres de identidad]** desde la lista de Áreas de nombres predefinidas en el menú desplegable. Dado que `loyaltyId` es la dirección de correo electrónico del cliente, seleccione &quot;[!UICONTROL Correo electrónico]&quot; en la lista desplegable. Seleccione **[!UICONTROL Aplicar]** para confirmar las actualizaciones en el campo `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obtener una lista de las Áreas de nombres estándar y sus definiciones, consulte la [[!DNL Identity Service] documentación](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Después de aplicar el cambio, el icono para `loyaltyId` muestra un símbolo de huella digital, que indica que ahora es un campo de identidad.

![](../images/tutorials/create-schema/identity-applied.png)

Ahora, todos los datos ingestados en el campo `loyaltyId` se utilizarán para identificar a esa persona y unir una sola vista de ese cliente. Para obtener más información sobre cómo trabajar con identidades en [!DNL Experience Platform], consulte la documentación de [[!DNL Identity Service]](../../identity-service/home.md).

## Habilitar el esquema para su uso en [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) aprovecha los datos de identidad  [!DNL Experience Platform] para proporcionar una vista holística de cada cliente individual. El servicio crea sólidos perfiles de 360° de atributos del cliente, así como cuentas con marca de hora de cada interacción que los clientes han tenido en cualquier sistema integrado con [!DNL Experience Platform].

Para que un esquema se pueda habilitar para su uso con [!DNL Real-time Customer Profile], debe tener una identidad principal definida. Recibirá un mensaje de error si intenta habilitar un esquema sin definir primero una identidad principal.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para habilitar el esquema &quot;Miembros de lealtad&quot; para su uso en [!DNL Profile], comience por seleccionar &quot;[!DNL Loyalty Members]&quot; en la sección **[!UICONTROL Estructura]** del editor.

A la derecha del editor, se muestra información sobre el esquema, incluido su nombre para mostrar, descripción y tipo. Además de esta información, existe un botón de alternancia **[!UICONTROL Perfil]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Seleccione **[!UICONTROL Perfil]** y aparecerá una ventana emergente, pidiéndole que confirme que desea habilitar el esquema para [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una vez que un esquema se ha habilitado para [!DNL Real-time Customer Profile] y guardado, no se puede deshabilitar.

Seleccione **[!UICONTROL Habilitar]** para confirmar su elección. Puede seleccionar el **[!UICONTROL Perfil]** de nuevo para deshabilitar el esquema si lo desea, pero una vez guardado el esquema mientras [!DNL Profile] está habilitado, ya no se puede deshabilitar.

## Próximos pasos y recursos adicionales

Ahora que ha terminado de componer el esquema, puede ver el esquema completo en el lienzo. Seleccione **[!UICONTROL Guardar]** y el esquema se guardará en [!DNL Schema Library], lo que lo hará accesible desde [!DNL Schema Registry].

El nuevo esquema ahora se puede usar para ingestar datos en [!DNL Platform]. Recuerde que una vez que el esquema se ha utilizado para ingestar datos, sólo se pueden realizar cambios aditivos. Consulte los [conceptos básicos de la composición de esquema](../schema/composition.md) para obtener más información sobre el control de versiones de esquema.

Ahora puede seguir el tutorial sobre [definición de una relación de esquema en la IU](./relationship-ui.md) para agregar un nuevo campo de relación al esquema &quot;Miembros de lealtad&quot;.

El esquema &quot;Miembros de lealtad&quot; también está disponible para su visualización y administración mediante la API [!DNL Schema Registry]. Para empezar a trabajar con la API, lea la [[!DNL Schema Registry API] guía para desarrolladores](../api/getting-started.md) para comenzar a trabajar con ella.

### Recursos de vídeo

>[!WARNING]
>
>La [!DNL Platform] IU que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

El siguiente vídeo muestra cómo crear un esquema simple en la interfaz de usuario [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

El siguiente vídeo pretende reforzar su comprensión del trabajo con mezclas y clases.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre el uso de [!DNL Schema Editor].

### Crear una nueva clase {#create-new-class}

[!DNL Experience Platform] proporciona la flexibilidad necesaria para definir un esquema basado en una clase exclusiva de su organización. Para obtener información sobre cómo crear una nueva clase, consulte la guía sobre [creación y edición de clases en la interfaz de usuario](../ui/resources/classes.md#create).

### Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Las mezclas solo son compatibles con determinadas clases y, por lo tanto, si se cambia la clase, se restablecerán el lienzo y los campos que se hayan agregado.

Para obtener información sobre cómo cambiar la clase de un esquema, consulte la guía sobre [administración de esquemas en la interfaz de usuario](../ui/resources/schemas.md).