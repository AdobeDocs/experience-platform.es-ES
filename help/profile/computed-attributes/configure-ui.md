---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Configuración de un campo de atributo calculado
topic-legacy: guide
type: Documentation
description: Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando una mezcla para añadir el campo a un esquema existente o seleccionando un campo que ya haya definido dentro de un esquema.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---


# (Alpha) Configuración de un campo de atributo calculado en la interfaz de usuario

>[!IMPORTANT]
>
>La funcionalidad de atributo computado está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando una mezcla para añadir el campo a un esquema existente o seleccionando un campo que ya haya definido dentro de un esquema.

>[!NOTE]
>
>Los atributos calculados no se pueden agregar a campos dentro de mezclas definidas por Adobe. El campo debe estar dentro del espacio de nombres `tenant` , lo que significa que debe ser un campo que defina y agregue a un esquema.

Para definir correctamente un campo de atributo calculado, el esquema debe estar habilitado para [!DNL Profile] y aparecer como parte del esquema de unión para la clase en la que se basa el esquema. Para obtener más información sobre los esquemas y uniones habilitados para [!DNL Profile], consulte la sección de la [!DNL Schema Registry] guía para desarrolladores en [habilitación de un esquema para Perfil y visualización de esquemas de unión](../../xdm/api/getting-started.md). También se recomienda revisar la sección [sobre las uniones](../../xdm/schema/composition.md) en la documentación básica de la composición del esquema.

El flujo de trabajo de este tutorial utiliza un esquema habilitado para [!DNL Profile] y sigue los pasos para definir una nueva mezcla que contenga el campo de atributo calculado y garantizar que sea el área de nombres correcta. Si ya tiene un campo en el área de nombres correcta dentro de un esquema habilitado para perfil, puede continuar directamente con el paso para [crear un atributo calculado](#create-a-computed-attribute).

## Ver un esquema

Los pasos siguientes utilizan la interfaz de usuario de Adobe Experience Platform para localizar un esquema, añadir una mezcla y definir un campo. Si prefiere utilizar la API [!DNL Schema Registry], consulte la [Guía para desarrolladores del Registro de Esquemas](../../xdm/api/getting-started.md) para ver los pasos sobre cómo crear una mezcla, agregar una mezcla a un esquema y habilitar un esquema para usar con [!DNL Real-time Customer Profile].

En la interfaz de usuario, haga clic en **[!UICONTROL Schemas]** en el carril izquierdo y utilice la barra de búsqueda de la pestaña **[!UICONTROL Browse]** para encontrar rápidamente el esquema que desea actualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Una vez que haya localizado el esquema, haga clic en su nombre para abrir el [!DNL Schema Editor] donde puede realizar modificaciones en el esquema.

![](../images/computed-attributes/Schema-Editor.png)

## Crear una mezcla

Para crear una nueva mezcla, haga clic en **[!UICONTROL Add]** junto a **[!UICONTROL Mixins]** en la sección **[!UICONTROL Composition]** a la izquierda del editor. Esto abre el cuadro de diálogo **[!UICONTROL Add mixin]** donde puede ver las mezclas existentes. Haga clic en el botón de opción **[!UICONTROL Create new mixin]** para definir la nueva mezcla.

Asigne un nombre y una descripción a la mezcla y haga clic en **[!UICONTROL Add mixin]** cuando termine.

![](../images/computed-attributes/Add-mixin.png)

## Añadir un campo de atributo calculado al esquema

La nueva mezcla debe aparecer ahora en la sección &quot;[!UICONTROL Mixins]&quot; de &quot;[!UICONTROL Composition]&quot;. Haga clic en el nombre de la mezcla y aparecerán varios botones **[!UICONTROL Add field]** en la sección **[!UICONTROL Structure]** del editor.

Seleccione **[!UICONTROL Add field]** junto al nombre del esquema para añadir un campo de nivel superior o puede seleccionar añadir el campo en cualquier lugar dentro del esquema que prefiera.

Después de hacer clic en **[!UICONTROL Add field]** se abre un nuevo objeto, denominado para su ID de inquilino, que muestra que el campo se encuentra en el área de nombres correcta. Dentro de ese objeto, aparece un **[!UICONTROL New field]**. Esto se hace si el campo donde se va a definir el atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configuración del campo

Mediante la sección **[!UICONTROL Field properties]** en el lado derecho del editor, proporcione la información necesaria para el nuevo campo, incluido su nombre, nombre para mostrar y tipo.

>[!NOTE]
>
>El tipo del campo debe ser del mismo tipo que el valor del atributo calculado. Por ejemplo, si el valor del atributo calculado es una cadena, el campo que se está definiendo en el esquema debe ser una cadena.

Cuando termine, haga clic en **[!UICONTROL Apply]** y el nombre del campo, así como su tipo, aparecerán en la sección **[!UICONTROL Structure]** del editor.

![](../images/computed-attributes/Apply.png)

## Habilitar esquema para [!DNL Profile]

Antes de continuar, asegúrese de que el esquema se ha habilitado para [!DNL Profile]. Haga clic en el nombre del esquema en la sección **[!UICONTROL Structure]** del editor para que aparezca la pestaña **[!UICONTROL Schema Properties]**. Si el control deslizante **[!UICONTROL Profile]** está en azul, el esquema se ha habilitado para [!DNL Profile].

>[!NOTE]
>
>No se puede deshacer la activación de un esquema para [!DNL Profile], por lo que si hace clic en el control deslizante una vez activado, no tendrá que arriesgarse a desactivarlo.

![](../images/computed-attributes/Profile.png)

Ahora puede hacer clic en **[!UICONTROL Save]** para guardar el esquema actualizado y continuar con el resto del tutorial utilizando la API .

## Pasos siguientes

Ahora que ha creado un campo en el que se almacenará el valor de atributo calculado, puede crear el atributo calculado utilizando el extremo de API `/computedattributes`. Para ver los pasos detallados para crear un atributo calculado en la API, siga los pasos que se proporcionan en la [guía de extremo de la API de atributos calculados](ca-api.md).