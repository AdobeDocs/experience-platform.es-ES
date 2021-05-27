---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;iu;espacio de trabajo;campo
solution: Experience Platform
title: Definición de campos XDM en la interfaz de usuario
description: Obtenga información sobre cómo definir campos XDM en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 4%

---

# Definición de campos XDM en la interfaz de usuario

El [!DNL Schema Editor] de la interfaz de usuario de Adobe Experience Platform le permite definir sus propios campos dentro de las clases personalizadas del Modelo de datos de experiencia (XDM) y los grupos de campos de esquema. Esta guía trata los pasos para definir los campos XDM en la interfaz de usuario, incluidas las opciones de configuración disponibles para cada tipo de campo.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema del Experience Platform y los [conceptos básicos de la composición del esquema](../../schema/composition.md) para conocer cómo las clases y los grupos de campos contribuyen a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial sobre [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las distintas capacidades de [!DNL Schema Editor].

## Seleccione un recurso para agregar campos a {#select-resource}

Para definir nuevos campos XDM en la interfaz de usuario, primero debe abrir un esquema dentro de [!DNL Schema Editor]. Según los esquemas que estén disponibles actualmente en el [!DNL Schema Library], puede elegir [crear un nuevo esquema](../resources/schemas.md#create) o [seleccionar un esquema existente para editar](../resources/schemas.md#edit).

Una vez que haya abierto el [!DNL Schema Editor], utilice el carril izquierdo para seleccionar la clase o el grupo de campos para el que desea definir los campos. Si el recurso es un recurso personalizado definido por su organización, los controles para agregar o editar campos aparecen en el lienzo. Estos controles aparecen junto al nombre del esquema, así como cualquier campo de tipo de objeto que se haya definido en la clase o grupo de campos seleccionados.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Si la clase o el grupo de campos que selecciona es un recurso principal proporcionado por Adobe, no se puede editar y, por lo tanto, no aparecerán los controles que se muestran arriba. Si el esquema al que desea agregar campos se basa en una clase XDM principal y no contiene ningún grupo de campos personalizados, puede [crear un nuevo grupo de campos](../resources/field-groups.md#create) para agregarlo al esquema en su lugar.

Para agregar un nuevo campo al recurso, seleccione el icono **plus (+)** situado junto al nombre del esquema en el lienzo o junto al campo de tipo de objeto en el que desea definir el campo.

![](../../images/ui/fields/overview/plus-icon.png)

## Definir un campo para un recurso {#define}

Después de seleccionar el icono **plus (+)**, aparece un **[!UICONTROL Nuevo campo]** en el lienzo, ubicado dentro de un objeto de nivel raíz que tiene un espacio de nombres con su ID de inquilino único (mostrado como `_tenantId` en el ejemplo siguiente). Todos los campos que se agregan a un esquema a través de clases personalizadas y grupos de campos se colocan automáticamente dentro de este espacio de nombres para evitar conflictos con otros campos procedentes de clases y grupos de campos proporcionados por Adobe.

![](../../images/ui/fields/overview/new-field.png)

En el carril derecho de **[!UICONTROL Field properties]**, puede configurar los detalles de los campos nuevos. Se requiere la siguiente información para cada campo:

| Propiedad Field | Descripción |
| --- | --- |
| [!UICONTROL Nombre del campo] | Un nombre único y descriptivo para el campo. Tenga en cuenta que el nombre del campo no se puede cambiar una vez guardado el esquema.<br><br>El nombre debería escribirse idealmente en camelCase. Puede contener caracteres alfanuméricos, guiones o guiones bajos, pero **no** puede comenzar con un guion bajo.<ul><li>**Correcto**:  `fieldName`</li><li>**Aceptable:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Incorrecto**:  `_fieldName`</li></ul> |
| [!UICONTROL Nombre para mostrar] | Nombre reconocible para el campo. |
| [!UICONTROL Tipo] | Tipo de datos que contendrá el campo. En este menú desplegable, puede seleccionar uno de los [tipos escalares estándar](../../schema/field-constraints.md) admitidos por XDM o uno de los [tipos de datos](../resources/data-types.md) de varios campos que se han definido anteriormente en [!DNL Schema Registry].<br><br>También puede seleccionar Búsqueda de tipo  **[!UICONTROL avanzada]** para buscar, filtrar tipos de datos existentes y localizar el tipo deseado con mayor facilidad. |

{style=&quot;table-layout:auto&quot;}

También puede proporcionar al campo una **[!UICONTROL Description]** legible en lenguaje natural para proporcionar más contexto en cuanto al caso de uso previsto del campo.

>[!NOTE]
>
>Según el **[!UICONTROL Type]** que haya seleccionado para el campo, pueden aparecer controles de configuración adicionales en el carril derecho. Consulte la sección sobre [propiedades de campo específicas del tipo](#type-specific-properties) para obtener más información sobre estos controles.
>
>El carril derecho también proporciona casillas de verificación para designar tipos de campo especiales. Consulte la sección sobre [tipos de campos especiales](#special) para obtener más información.

Una vez que haya terminado de configurar el campo, seleccione **[!UICONTROL Apply]**.

![](../../images/ui/fields/overview/field-details.png)

El lienzo se actualiza para mostrar el nombre y el tipo del campo, y el carril derecho muestra ahora la ruta del campo, además de sus otras propiedades.

![](../../images/ui/fields/overview/field-added.png)

Puede seguir los pasos anteriores para añadir más campos al esquema. Una vez guardado el esquema, sus grupos de clases base y de campos también se guardan si se han realizado cambios en ellos.

>[!NOTE]
>
>Los cambios que realice en los grupos de campos o en la clase de un esquema se reflejarán en todos los demás esquemas que los empleen.

## Propiedades de campo específicas del tipo {#type-specific-properties}

Al definir un nuevo campo, pueden aparecer opciones de configuración adicionales en el carril derecho en función del **[!UICONTROL Tipo]** que elija para el campo. La siguiente tabla describe estas propiedades de campo adicionales junto con sus tipos compatibles:

| Propiedad Field | Tipos compatibles | Descripción |
| --- | --- | --- |
| [!UICONTROL Valor predeterminado] | [!UICONTROL Cadena],  [!UICONTROL Doble],  [!UICONTROL Largo],  [!UICONTROL Entero],  [!UICONTROL Corto],  [!UICONTROL Byte],  [!UICONTROL Booleano] | Valor predeterminado que se asigna a este campo si no se proporciona ningún otro valor durante la ingesta. Este valor debe ajustarse al tipo seleccionado del campo. |
| [!UICONTROL Patrón] | [!UICONTROL Cadena] | Una [expresión regular](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) a la que debe ajustarse el valor de este campo para que se acepte durante la ingesta. |
| [!UICONTROL Formato] | [!UICONTROL Cadena] | Seleccione entre una lista de formatos predefinidos para cadenas a las que debe ajustarse el valor. Los formatos disponibles incluyen: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longitud mínima] | [!UICONTROL Cadena] | El número mínimo de caracteres que debe contener la cadena para que el valor se acepte durante la ingesta. |
| [!UICONTROL Longitud máxima] | [!UICONTROL Cadena] | El número máximo de caracteres que debe contener la cadena para que se acepte el valor durante la ingesta. |
| [!UICONTROL Valor mínimo] | [!UICONTROL Duplicada] | El valor mínimo para que se acepte el valor Double durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se acepta el valor . Al utilizar esta restricción, la restricción &quot;[!UICONTROL Exclusive Minimum value]&quot; debe dejarse en blanco. |
| [!UICONTROL Valor máximo] | [!UICONTROL Duplicada] | El valor máximo para el Double que se va a aceptar durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se acepta el valor . Al utilizar esta restricción, la restricción &quot;[!UICONTROL Exclusive maximum value]&quot; debe dejarse en blanco. |
| [!UICONTROL Valor mínimo exclusivo] | [!UICONTROL Duplicada] | El valor máximo para el Double que se va a aceptar durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se rechaza el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Minimum value]&quot; (no exclusiva) debe dejarse en blanco. |
| [!UICONTROL Valor máximo exclusivo] | [!UICONTROL Duplicada] | El valor máximo para el Double que se va a aceptar durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se rechaza el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Maximum value]&quot; (no exclusiva) debe dejarse en blanco. |

{style=&quot;table-layout:auto&quot;}

## Tipos de campos especiales {#special}

El carril derecho proporciona varias casillas de verificación para designar funciones especiales para el campo seleccionado. Los casos de uso de algunas de estas opciones implican consideraciones importantes con respecto a su estrategia de modelado de datos y a cómo pretende utilizar los servicios de Platform descendentes.

Para obtener más información sobre estos tipos especiales, consulte la siguiente documentación:

* [[!UICONTROL Requerido]](./required.md)
* [[!UICONTROL Matriz]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identidad]](./identity.md)  (solo disponible para campos de cadena)
* [[!UICONTROL Relación]](./relationship.md)  (solo disponible para campos de cadena)

Aunque técnicamente no es un tipo de campo especial, también se recomienda visitar la guía de [definición de campos de tipo de objeto](./object.md) para obtener más información sobre la definición de subcampos anidados si sus estructuras de esquema.

## Pasos siguientes

Esta guía proporciona información general sobre cómo definir campos XDM en la interfaz de usuario. Recuerde que los campos solo se pueden agregar a esquemas mediante el uso de clases y grupos de campos. Para obtener más información sobre cómo administrar estos recursos en la interfaz de usuario, consulte las guías sobre la creación y edición de [clases](../resources/classes.md) y [grupos de campos](../resources/field-groups.md).

Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL schemas] , consulte la información general del espacio de trabajo [[!UICONTROL Esquemas]](../overview.md).
