---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;campo;
solution: Experience Platform
title: Definición de campos XDM en la IU
description: Obtenga información sobre cómo definir campos XDM en la interfaz de usuario de Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---

# Definición de campos XDM en la IU

[!DNL Schema Editor] en la interfaz de usuario de Adobe Experience Platform le permite definir sus propios campos dentro de clases personalizadas de modelo de datos de experiencia (XDM) y grupos de campos de esquema. Esta guía explica los pasos para definir campos XDM en la interfaz de usuario de, incluidas las opciones de configuración disponibles para cada tipo de campo.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [descripción general de XDM](../../home.md) para obtener una introducción del papel de XDM en el ecosistema de Experience Platform y los [conceptos básicos de la composición de esquemas](../../schema/composition.md) para conocer cómo las clases y los grupos de campos contribuyen a los campos en los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda que también siga el tutorial sobre [maquetar un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas funcionalidades de [!DNL Schema Editor].

## Seleccione un recurso al que añadir campos {#select-resource}

Para definir nuevos campos XDM en la interfaz de usuario, primero debe abrir un esquema dentro de [!DNL Schema Editor]. Según los esquemas que estén disponibles actualmente en [!DNL Schema Library], puede elegir [crear un nuevo esquema](../resources/schemas.md#create) o [seleccionar un esquema existente para editar](../resources/schemas.md#edit).

Una vez que tenga [!DNL Schema Editor] abierto, los controles para agregar campos aparecerán en el lienzo. Estos controles aparecen junto al nombre del esquema, así como cualquier campo de tipo de objeto que se haya definido en la clase o grupo de campos seleccionado.

![Editor de esquemas con los iconos de adición resaltados.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Si intenta agregar un campo a un objeto proporcionado por un grupo de campos estándar, ese grupo de campos se convertirá en un grupo de campos personalizado y el grupo de campos original dejará de estar disponible. Consulte la sección sobre [agregar campos a grupos de campos estándar](../resources/schemas.md#custom-fields-for-standard-groups) en la guía de IU de esquemas para obtener más información.

Para agregar un nuevo campo al recurso, seleccione el icono **más (+)** junto al nombre del esquema en el lienzo o junto al campo de tipo de objeto en el que desea definir el campo.

![Editor de esquemas con un icono de agregar resaltado.](../../images/ui/fields/overview/plus-icon.png)

Dependiendo de si agrega un campo directamente a un esquema o a su clase constituyente y a los grupos de campos, los pasos necesarios para agregar el campo variarán. El resto de este documento se centra en cómo configurar las propiedades de un campo independientemente de dónde aparezca en el esquema. Para obtener más información sobre las diferentes formas en que se pueden añadir campos a un esquema, consulte las siguientes secciones en la guía de la IU de esquemas:

* [Adición de campos a grupos de campos](../resources/schemas.md#add-fields)
* [Añadir campos directamente a un esquema](../resources/schemas.md#add-individual-fields)

## Definir las propiedades de un campo {#define}

Después de seleccionar el icono **más (+)**, aparece un marcador de posición **[!UICONTROL Campo sin título]** en el lienzo.

![Editor de esquemas con un nuevo campo sin título resaltado.](../../images/ui/fields/overview/new-field.png)

En el carril derecho bajo **[!UICONTROL Propiedades del campo]**, puede configurar los detalles del nuevo campo. Se requiere la siguiente información para cada campo:

| Propiedad de campo | Descripción |
| --- | --- |
| [!UICONTROL Nombre de campo] | Un nombre único y descriptivo para el campo. Tenga en cuenta que el nombre del campo no se puede cambiar una vez guardado el esquema. Este valor se usa para identificar y hacer referencia al campo en el código y en otras aplicaciones de flujo descendente<br><br>Idealmente, el nombre debería escribirse en camelCase. Puede contener caracteres alfanuméricos o guiones bajos, pero **no puede** comenzar con un guion bajo.<ul><li>**Correcto**: `fieldName`</li><li>**Aceptable:** `field_name2`, `fieldName_3`</li><li>**Incorrecto**: `_fieldName`</li></ul> |
| [!UICONTROL Nombre para mostrar] | Un nombre para mostrar para el campo. Este es el nombre que se utilizará para representar el campo en el lienzo del Editor de esquemas. El nombre de campo se puede cambiar al nombre para mostrar mediante [display name toggle](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Tipo] | Tipo de datos que contendrá el campo. Desde este menú desplegable, puede seleccionar uno de los [tipos escalares estándar](../../schema/field-constraints.md) compatibles con XDM, o uno de los [tipos de datos](../resources/data-types.md) de varios campos que se han definido previamente en [!DNL Schema Registry].<br>Nota: si selecciona el tipo de datos Map, aparecerá la propiedad [!UICONTROL Map value type].<br><br>También puede seleccionar **[!UICONTROL Búsqueda de tipo avanzada]** para buscar y filtrar los tipos de datos existentes y encontrar el tipo deseado con mayor facilidad. |
| [!UICONTROL Asignar tipo de valor] | Este valor es necesario si selecciona [!UICONTROL Map] como tipo de datos para el campo. Los valores disponibles para el mapa son [!UICONTROL String] y [!UICONTROL Integer]. Seleccione un valor de la lista desplegable de opciones disponibles.<br>Para obtener más información acerca de [propiedades de campo específicas del tipo](#type-specific-properties), consulte la descripción general de definir campos. |

{style="table-layout:auto"}

También puede proporcionar una descripción y notas para cada campo. Utilice el campo **[!UICONTROL Descripción]** para agregar contexto y describir la funcionalidad del tipo de datos de asignación. Esto contribuye al mantenimiento y a la legibilidad de la implementación. También puede agregar notas para complementar la descripción inicial. Esto debería ofrecer información más granular y específica para ayudar a los desarrolladores a comprender, mantener y utilizar el mapa de forma eficaz en el contexto de la base de código. |


>[!NOTE]
>
>Según el **[!UICONTROL Tipo]** que seleccionó para el campo, pueden aparecer controles de configuración adicionales en el carril derecho. Consulte la sección sobre [propiedades de campo específicas del tipo](#type-specific-properties) para obtener más información sobre estos controles.
>
>El carril derecho también proporciona casillas de verificación para designar tipos de campo especiales. Consulte la sección sobre [tipos de campo especiales](#special) para obtener más información.

Una vez que haya terminado de configurar el campo, seleccione **[!UICONTROL Aplicar]**.

![La sección [!UICONTROL Propiedades de campo] del Editor de esquemas está resaltada.](../../images/ui/fields/overview/field-details.png)

El lienzo se actualiza para mostrar el campo recién agregado, ubicado dentro de un objeto que tiene un espacio de nombres con respecto a su ID de inquilino único (mostrado como `_tenantId` en el ejemplo siguiente). Todos los campos personalizados que se agregan a un esquema se colocan automáticamente dentro de este espacio de nombres para evitar conflictos con otros campos de clases y grupos de campos proporcionados por Adobe. El carril derecho ahora enumera la ruta del campo además de sus otras propiedades.

![Se resalta un nuevo campo en el diagrama de esquema y su ruta correspondiente en la sección [!UICONTROL Propiedades del campo].](../../images/ui/fields/overview/field-added.png)

Puede seguir siguiendo los pasos anteriores para agregar más campos al esquema. Una vez guardado el esquema, su clase base y los grupos de campos también se guardan si se han realizado cambios en ellos.

>[!NOTE]
>
>Cualquier cambio que realice en los grupos de campos o en la clase de un esquema se reflejará en todos los demás esquemas que los utilicen.

## Propiedades de campo específicas del tipo {#type-specific-properties}

Al definir un nuevo campo, pueden aparecer opciones de configuración adicionales en el carril derecho según el **[!UICONTROL Tipo]** que elija para el campo. En la tabla siguiente se describen estas propiedades de campo adicionales junto con sus tipos compatibles:

| Propiedad de campo | Tipos compatibles | Descripción |
| --- | --- | --- |
| [!UICONTROL Asignar tipo de valor] | [!UICONTROL Mapa] | La propiedad [!UICONTROL Map value type] solo aparece en la interfaz de usuario si selecciona el valor Map en las opciones desplegables de [!UICONTROL Type]. Puede seleccionar entre los tipos de valor Cadena y Entero para el Mapa.<br>![Editor de esquemas con los campos Tipo y Tipo de valor de asignación resaltados.](../../images/ui/fields/overview/map-type.png "Editor de esquemas con los campos Tipo y Tipo de valor de asignación resaltados."){width="100" zoomable="yes"}<br>Nota: todos los tipos de datos de asignación creados mediante la API que no sean de tipo String ni Integer se muestran como un tipo de datos &#39;[!UICONTROL Complex]&#39;. No puede crear tipos de datos &#39;[!UICONTROL Complex]&#39; a través de la interfaz de usuario. |
| [!UICONTROL Patrón] | [!UICONTROL Cadena] | Una [expresión regular](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) a la que debe ajustarse el valor de este campo para que se acepte durante la ingesta. |
| [!UICONTROL Formato] | [!UICONTROL Cadena] | Seleccione de una lista de formatos predefinidos para cadenas con los que debe ajustarse el valor. Los formatos disponibles incluyen: <ul><li>[[!UICONTROL fecha-hora]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL correo electrónico]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL nombre de host]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL puntero json]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longitud mínima] | [!UICONTROL Cadena] | Número mínimo de caracteres que debe contener la cadena para que el valor se acepte durante la ingesta. |
| [!UICONTROL Longitud máxima] | [!UICONTROL Cadena] | Número máximo de caracteres que debe contener la cadena para que el valor se acepte durante la ingesta. |
| [!UICONTROL Valor mínimo] | [!UICONTROL Doble] | El valor mínimo de Double que se aceptará durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se acepta el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Valor mínimo exclusivo]&quot; debe dejarse en blanco. |
| [!UICONTROL Valor máximo] | [!UICONTROL Doble] | El valor máximo de Double que se aceptará durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se acepta el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Valor máximo exclusivo]&quot; debe dejarse en blanco. |
| [!UICONTROL Valor mínimo exclusivo] | [!UICONTROL Doble] | El valor máximo de Double que se aceptará durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se rechaza el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Minimum value]&quot; (no exclusiva) debe dejarse en blanco. |
| [!UICONTROL Valor máximo exclusivo] | [!UICONTROL Doble] | El valor máximo de Double que se aceptará durante la ingesta. Si el valor introducido coincide exactamente con el introducido aquí, se rechaza el valor. Al utilizar esta restricción, la restricción &quot;[!UICONTROL Valor máximo]&quot; (no exclusivo) debe dejarse en blanco. |

{style="table-layout:auto"}

## Tipos de campo especiales {#special}

El carril derecho proporciona varias casillas de verificación para designar funciones especiales para el campo seleccionado. Los casos de uso de algunas de estas opciones implican consideraciones importantes sobre su estrategia de modelado de datos y cómo desea utilizar los servicios de Experience Platform descendentes.

Para obtener más información sobre estos tipos especiales, consulte la siguiente documentación:

* [Mapa](./map.md)
* [[!UICONTROL Requerido]](./required.md)
* [[!UICONTROL Matriz]](./array.md)
* [[!UICONTROL Enumeración]](./enum.md)
* [[!UICONTROL Identidad]](./identity.md) (disponible solo para campos de cadena)
* [[!UICONTROL Relación]](./relationship.md) (disponible solo para campos de cadena)

Aunque técnicamente no es un tipo de campo especial, también se recomienda que visite la guía de [definición de campos de tipo de objeto](./object.md) para obtener más información sobre la definición de subcampos anidados si sus estructuras de esquema.

## Pasos siguientes

Esta guía proporciona información general sobre cómo definir campos XDM en la interfaz de usuario. Recuerde que los campos solo se pueden agregar a esquemas mediante el uso de clases y grupos de campos. Para obtener más información sobre cómo administrar estos recursos en la interfaz de usuario, consulte las guías sobre la creación y edición de [clases](../resources/classes.md) y [grupos de campos](../resources/field-groups.md).

Para obtener más información sobre las capacidades del área de trabajo [!UICONTROL Esquemas], consulte la descripción general del área de trabajo [[!UICONTROL Esquemas]](../overview.md).
