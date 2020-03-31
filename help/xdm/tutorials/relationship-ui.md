---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir una relación entre dos esquemas mediante el Editor de Esquemas de Esquema
topic: tutorials
translation-type: tm+mt
source-git-commit: f8c34d84e30ae14c3936c2e32ee84a2fcd3abdc3

---


# Definir una relación entre dos esquemas mediante el Editor de Esquemas

La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en distintos canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas del Modelo de datos de experiencia (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes.

Este documento proporciona un tutorial para definir una relación uno a uno entre dos esquemas definidos por su organización mediante el Editor de Esquemas en la interfaz de usuario de la plataforma de experiencia. Para ver los pasos sobre la definición de relaciones de esquema mediante la API, consulte el tutorial sobre la [definición de una relación mediante la API](relationship-api.md)del Registro de Esquema.

## Primeros pasos

Este tutorial requiere un conocimiento práctico del sistema XDM y del editor de Esquema en la interfaz de usuario de la plataforma de experiencia. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en la plataforma](../home.md)de experiencias: Información general sobre XDM y su implementación en la plataforma de experiencias.
* [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema con el Editor](create-schema-ui.md)de Esquemas: Un tutorial sobre los conceptos básicos del trabajo con el Editor de Esquemas.

## Definir un esquema de origen y destino

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre los miembros del programa de lealtad de una organización (definido en un esquema de &quot;miembros de la lealtad&quot;) y sus hoteles favoritos (definido en un esquema de &quot;hoteles&quot;).

Las relaciones de Esquema están representadas por un esquema **de** origen que tiene un campo que hace referencia a otro campo dentro de un esquema **de** destino. En los pasos siguientes, &quot;Miembros de la Lealtad&quot; será el esquema de origen, mientras que &quot;Hoteles&quot; actuará como el esquema de destino.

Con fines de referencia, las siguientes secciones describen la estructura de cada esquema utilizado en este tutorial antes de definir una relación.

### esquema de miembros de lealtad

El esquema de origen &quot;Miembros de lealtad&quot; es el esquema que se creó en el tutorial para [crear un esquema en la interfaz de usuario](create-schema-ui.md). Incluye un objeto &quot;loyalty&quot; bajo su Área de nombres &quot;\_tenantId&quot;, que incluye varios campos específicos de lealtad. Uno de estos campos, &quot;loyaltyId&quot;, sirve como identidad principal para el esquema en la Área de nombres &quot;Email&quot;. Como se muestra en Propiedades _de_ Esquema, este esquema se ha habilitado para su uso en Perfil [de clientes en tiempo](../../profile/home.md)real.

![](../images/tutorials/relationship/loyalty-members.png)

### esquema de hoteles

El esquema de destino &quot;Hoteles&quot; contiene campos que describen un hotel, incluyen su dirección, marca, número de habitaciones y clasificación por estrellas. El campo &quot;hotelId&quot; sirve como identidad principal para el esquema bajo la Área de nombres &quot;ECID&quot;. A diferencia de &quot;Miembros de lealtad&quot;, este esquema no se ha habilitado para el Perfil del cliente en tiempo real.

![](../images/tutorials/relationship/hotels.png)

## Crear una mezcla de relación

>[!NOTE] Este paso solo es necesario si el esquema de origen no tiene un campo de tipo de cadena dedicado para utilizarlo como referencia a otro esquema. Si este campo ya está definido en el esquema de origen, vaya al siguiente paso para [definir un campo](#relationship-field)de relación.

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo específico para utilizarlo como referencia al esquema de destino. Puede agregar este campo al esquema de origen creando una nueva mezcla.

Para Inicio, haga clic en **Añadir** en la sección _Mezclas_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Aparecerá el cuadro de diálogo _Añadir mezcla_ . Desde aquí, haga clic en **Crear nueva combinación**. En los campos de texto que aparecen, introduzca un nombre para mostrar y una descripción para la nueva combinación. Haga clic en **Añadir mezcla** cuando termine.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

El lienzo vuelve a aparecer con &quot;Relación de lealtad&quot; en la sección _Mezclas_ . Haga clic en el nombre de la mezcla y, a continuación, haga clic en **Añadir campo** junto al campo de nivel raíz &quot;Miembros de lealtad&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo campo en el lienzo bajo la Área de nombres &quot;\_inquilinoId&quot;. En Propiedades __ del campo, proporcione un nombre de campo y un nombre para mostrar para el campo y defina su tipo en &quot;Cadena&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, haga clic en **Aplicar**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El campo &quot;loyaltyRelationship&quot; actualizado aparece en el lienzo. Haga clic en **Guardar** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

Una vez definido el esquema de origen, puede designarlo como un campo de relación.

Haga clic en el campo de referencia en el lienzo y, a continuación, desplácese hacia abajo en Propiedades _del_ campo hasta que aparezca la casilla de verificación **Relación** . Seleccione la casilla de verificación para mostrar los parámetros necesarios para configurar un campo de relación.

![](../images/tutorials/relationship/relationship-checkbox.png)

Haga clic en el menú desplegable del Esquema **de** referencia y seleccione el esquema de destino de la relación (&quot;Hoteles&quot; en este ejemplo). Si el esquema de destino está habilitado para la unión, el campo Área de nombres **de identidad de** referencia se establece automáticamente en la Área de nombres de la identidad principal del esquema de destino. Si el esquema no tiene definida una identidad principal, debe seleccionar manualmente la Área de nombres que va a utilizar en el menú desplegable. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

El campo aparece como una relación en el lienzo, mostrando el nombre y la Área de nombres de identidad de referencia del esquema de destino. Haga clic en **Guardar** para guardar los cambios y completar el flujo de trabajo.

![](../images/tutorials/relationship/relationship-save.png)

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente una relación uno a uno entre dos esquemas con el Editor de Esquemas. Para ver los pasos sobre cómo definir relaciones mediante la API, consulte el tutorial sobre la [definición de una relación mediante la API](relationship-api.md)del Registro de Esquema.