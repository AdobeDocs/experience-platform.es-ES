---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Configuración de un campo de atributo calculado
type: Documentation
description: Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando un grupo de campos de esquema para añadir el campo a un esquema existente o seleccionando un campo que ya haya definido dentro de un esquema.
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha) Configuración de un campo de atributo calculado en la interfaz de usuario

>[!IMPORTANT]
>
>La funcionalidad de atributo computado está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear utilizando un grupo de campos de esquema para añadir el campo a un esquema existente o seleccionando un campo que ya haya definido dentro de un esquema.

>[!NOTE]
>
>Los atributos calculados no se pueden agregar a campos dentro de grupos de campos definidos por el Adobe. El campo debe estar dentro de la variable `tenant` namespace, lo que significa que debe ser un campo que defina y añada a un esquema.

Para definir correctamente un campo de atributo calculado, el esquema debe estar habilitado para [!DNL Profile] y aparecen como parte del esquema de unión para la clase en la que se basa el esquema. Para obtener más información, consulte [!DNL Profile]-esquemas y uniones habilitados, revise la sección del [!DNL Schema Registry] guía para desarrolladores [activación de un esquema para Perfil y visualización de esquemas de unión](../../xdm/api/getting-started.md). También se recomienda revisar la [sección sobre sindicatos](../../xdm/schema/composition.md) en la documentación básica de composición de esquema.

El flujo de trabajo de este tutorial utiliza un [!DNL Profile]-enabled schema y sigue los pasos para definir un nuevo grupo de campos que contenga el campo de atributo calculado y asegurarse de que sea el área de nombres correcta. Si ya tiene un campo en el área de nombres correcta dentro de un esquema habilitado para perfil, puede continuar directamente con el paso para [creación de un atributo calculado](#create-a-computed-attribute).

## Ver un esquema

Los pasos siguientes utilizan la interfaz de usuario de Adobe Experience Platform para localizar un esquema, agregar un grupo de campos y definir un campo. Si prefiere usar la variable [!DNL Schema Registry] API, consulte la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md) para ver los pasos sobre cómo crear un grupo de campos, agregar un grupo de campos a un esquema y habilitar un esquema para utilizarlo con [!DNL Real-Time Customer Profile].

En la interfaz de usuario, haga clic en **[!UICONTROL Esquemas]** en el carril izquierdo y utilice la barra de búsqueda de la **[!UICONTROL Examinar]** para encontrar rápidamente el esquema que desea actualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Una vez que haya localizado el esquema, haga clic en su nombre para abrir el [!DNL Schema Editor] donde puede realizar modificaciones en el esquema.

![](../images/computed-attributes/Schema-Editor.png)

## Creación de un grupo de campos

Para crear un nuevo grupo de campos, haga clic en **[!UICONTROL Agregar]** junto a **[!UICONTROL Grupos de campo]** en el **[!UICONTROL Composición]** a la izquierda del editor. Esto abre el **[!UICONTROL Agregar grupo de campos]** cuadro de diálogo donde puede ver los grupos de campos existentes. Haga clic en el botón de opción para **[!UICONTROL Crear nuevo grupo de campos]** para definir el nuevo grupo de campos.

Asigne un nombre y una descripción al grupo de campos y haga clic en **[!UICONTROL Agregar grupo de campos]** cuando se complete.

![](../images/computed-attributes/Add-field-group.png)

## Añadir un campo de atributo calculado al esquema

El nuevo grupo de campos debería aparecer en la sección[!UICONTROL Grupos de campo]&quot; en &quot;[!UICONTROL Composición]&quot;. Haga clic en el nombre del grupo de campos y en varios **[!UICONTROL Añadir campo]** aparecerán en el **[!UICONTROL Estructura]** del editor.

Select **[!UICONTROL Añadir campo]** junto al nombre del esquema para añadir un campo de nivel superior, o puede seleccionar añadir el campo en cualquier lugar dentro del esquema que prefiera.

Después de hacer clic en **[!UICONTROL Añadir campo]** se abre un nuevo objeto, denominado para su ID de inquilino, que muestra que el campo está en el espacio de nombres correcto. Dentro de ese objeto, una **[!UICONTROL Campo nuevo]** aparece. Esto se hace si el campo donde se va a definir el atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configuración del campo

Al usar la variable **[!UICONTROL Propiedades del campo]** a la derecha del editor, proporcione la información necesaria para el nuevo campo, incluido su nombre, nombre para mostrar y tipo.

>[!NOTE]
>
>El tipo del campo debe ser del mismo tipo que el valor del atributo calculado. Por ejemplo, si el valor del atributo calculado es una cadena, el campo que se está definiendo en el esquema debe ser una cadena.

Cuando termine, haga clic en **[!UICONTROL Aplicar]** y el nombre del campo, así como su tipo, aparecerán en la variable **[!UICONTROL Estructura]** del editor.

![](../images/computed-attributes/Apply.png)

## Habilitar esquema para [!DNL Profile]

Antes de continuar, asegúrese de que el esquema se ha habilitado para [!DNL Profile]. Haga clic en el nombre del esquema en la **[!UICONTROL Estructura]** del editor para que **[!UICONTROL Propiedades del esquema]** se abre. Si la variable **[!UICONTROL Perfil]** el control deslizante es azul, el esquema se ha habilitado para [!DNL Profile].

>[!NOTE]
>
>Activación de un esquema para [!DNL Profile] no se puede deshacer, por lo que si hace clic en el control deslizante una vez activado, no tendrá que arriesgarse a desactivarlo.

![](../images/computed-attributes/Profile.png)

Ahora puede hacer clic en **[!UICONTROL Guardar]** para guardar el esquema actualizado y continuar con el resto del tutorial utilizando la API .

## Pasos siguientes

Ahora que ha creado un campo en el que se almacenará el valor de atributo calculado, puede crear el atributo calculado utilizando la variable `/computedattributes` extremo de API. Para ver los pasos detallados para crear un atributo calculado en la API, siga los pasos que se proporcionan en la [guía de extremo de API de atributos calculados](ca-api.md).