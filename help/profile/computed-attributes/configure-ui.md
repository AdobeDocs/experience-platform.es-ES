---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Cómo configurar un campo de atributo calculado
topic: guía
type: Documentación
description: Los atributos calculados son funciones que se utilizan para acumulados datos de nivel de evento en atributos de nivel de perfil. Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear con una mezcla para agregar el campo a un esquema existente o seleccionando un campo que ya haya definido en un esquema.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# (Alfa) Configure un campo de atributo calculado en la interfaz de usuario

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear con una mezcla para agregar el campo a un esquema existente o seleccionando un campo que ya haya definido en un esquema.

>[!NOTE]
>
>No se pueden agregar atributos calculados a los campos dentro de mezclas definidas por Adobe. El campo debe estar dentro de la Área de nombres `tenant`, lo que significa que debe ser un campo que usted defina y agregue a un esquema.

Para definir correctamente un campo de atributo calculado, el esquema debe habilitarse para [!DNL Profile] y aparecer como parte del esquema de unión para la clase en la que se basa el esquema. Para obtener más información sobre esquemas y uniones habilitados para [!DNL Profile], consulte la sección de la [!DNL Schema Registry] guía para desarrolladores en [habilitación de un esquema para Perfil y visualización de esquemas de unión](../../xdm/api/getting-started.md). También se recomienda revisar la [sección sobre uniones](../../xdm/schema/composition.md) en la documentación básica de la composición de esquema.

El flujo de trabajo de este tutorial utiliza un esquema habilitado para [!DNL Profile] y sigue los pasos para definir una nueva combinación que contenga el campo de atributo calculado y garantizar que sea la Área de nombres correcta. Si ya tiene un campo que se encuentra en la Área de nombres correcta dentro de un esquema habilitado para Perfil, puede continuar directamente con el paso para [crear un atributo calculado](#create-a-computed-attribute).

## Vista de un esquema

Los pasos siguientes utilizan la interfaz de usuario de Adobe Experience Platform para localizar un esquema, agregar una mezcla y definir un campo. Si prefiere utilizar la API [!DNL Schema Registry], consulte la [guía para desarrolladores del Registro de Esquemas](../../xdm/api/getting-started.md) para ver los pasos sobre cómo crear una mezcla, agregar una mezcla a un esquema y habilitar un esquema para su uso con [!DNL Real-time Customer Profile].

En la interfaz de usuario, haga clic en **[!UICONTROL Esquemas]** en el carril izquierdo y utilice la barra de búsqueda de la ficha **[!UICONTROL Examinar]** para encontrar rápidamente el esquema que desea actualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Una vez que haya localizado el esquema, haga clic en su nombre para abrir el [!DNL Schema Editor] donde puede realizar modificaciones en el esquema.

![](../images/computed-attributes/Schema-Editor.png)

## Crear una mezcla

Para crear una nueva mezcla, haga clic en **[!UICONTROL Añadir]** al lado de **[!UICONTROL Mezclas]** en la sección **[!UICONTROL Composición]** a la izquierda del editor. Esto abre el cuadro de diálogo **[!UICONTROL Añadir mezcla]** donde puede ver las mezclas existentes. Haga clic en el botón de radio para **[!UICONTROL Crear nueva mezcla]** para definir la nueva mezcla.

Asigne un nombre y una descripción a la mezcla y haga clic en **[!UICONTROL Añadir mezcla]** cuando finalice.

![](../images/computed-attributes/Add-mixin.png)

## Añadir un campo de atributo calculado en el esquema

La nueva mezcla debe aparecer ahora en la sección &quot;[!UICONTROL Mezclas]&quot; en &quot;[!UICONTROL Composición]&quot;. Haga clic en el nombre de la mezcla y aparecerán varios botones **[!UICONTROL Añadir campo]** en la sección **[!UICONTROL Estructura]** del editor.

Seleccione **[!UICONTROL Añadir campo]** junto al nombre del esquema para agregar un campo de nivel superior, o puede seleccionar agregar el campo en cualquier lugar dentro del esquema que prefiera.

Después de hacer clic en **[!UICONTROL Añadir campo]**, se abre un nuevo objeto, denominado para su ID de inquilino, que muestra que el campo está en la Área de nombres correcta. Dentro de ese objeto, aparece un **[!UICONTROL nuevo campo]**. Esto sucede si el campo en el que se va a definir el atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configurar el campo

Mediante la sección **[!UICONTROL Propiedades del campo]** a la derecha del editor, proporcione la información necesaria para el nuevo campo, incluido su nombre, nombre para mostrar y tipo.

>[!NOTE]
>
>El tipo del campo debe ser del mismo tipo que el valor del atributo calculado. Por ejemplo, si el valor del atributo calculado es una cadena, el campo que se está definiendo en el esquema debe ser una cadena.

Cuando termine, haga clic en **[!UICONTROL Aplicar]** y el nombre del campo, así como su tipo, aparecerán en la sección **[!UICONTROL Estructura]** del editor.

![](../images/computed-attributes/Apply.png)

## Habilitar esquema para [!DNL Profile]

Antes de continuar, asegúrese de que el esquema se haya habilitado para [!DNL Profile]. Haga clic en el nombre del esquema en la sección **[!UICONTROL Estructura]** del editor para que aparezca la ficha **[!UICONTROL Propiedades del Esquema]**. Si el deslizador **[!UICONTROL Perfil]** es azul, el esquema se ha habilitado para [!DNL Profile].

>[!NOTE]
>
>No se puede deshacer la activación de un esquema para [!DNL Profile], por lo que si hace clic en el control deslizante una vez que se ha habilitado, no tendrá que correr el riesgo de deshabilitarlo.

![](../images/computed-attributes/Profile.png)

Ahora puede hacer clic en **[!UICONTROL Guardar]** para guardar el esquema actualizado y continuar con el resto del tutorial usando la API.

## Pasos siguientes

Ahora que ha creado un campo en el que se almacenará el valor de atributo calculado, puede crear el atributo calculado mediante el extremo de API `/computedattributes`. Para ver los pasos detallados para crear un atributo calculado en la API, siga los pasos que se proporcionan en la [guía de extremo de la API de atributos calculados](ca-api.md).