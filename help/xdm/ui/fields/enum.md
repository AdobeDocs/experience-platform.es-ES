---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enum;campo;
solution: Experience Platform
title: Definición de campos de enumeración y valores sugeridos en la IU
description: Obtenga información sobre cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario del Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# Defina enumeraciones y valores sugeridos en la interfaz de usuario {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enumeraciones y valores sugeridos"
>abstract="Un **Enumeración** restringe un campo de cadena para permitir la ingesta únicamente de datos que coincidan con un conjunto predefinido de valores. A cada restricción de enumeración se le puede asignar una **Nombre para mostrar** que rellena los menús desplegables de atributos en la interfaz de usuario de Segmentación. **Valores sugeridos** para un campo no restringen la ingesta y solo determinan los nombres para mostrar que se muestran en Segmentación. Si tiene varios esquemas que comparten un campo que pertenece a una clase o grupo de campos común y define diferentes enumeraciones o valores sugeridos para ese campo entre cada esquema, esos valores se combinan y se anexan en el esquema de unión."

En el Modelo de datos de experiencia (XDM), se puede dar a un campo de cadena un conjunto predefinido de valores aceptados o sugeridos para controlar mejor qué valores se incorporan a ese campo o cómo se comportará en la segmentación.

**[!UICONTROL Enumeraciones]** restringir los valores que se pueden introducir para un campo de cadena a un conjunto predefinido. Si intenta introducir datos en un campo de enumeración y el valor no coincide con ninguno de los definidos en su configuración, se denegará la ingesta.

A diferencia de las enumeraciones, la variable **[!UICONTROL Valores sugeridos]** permite a denotar un conjunto de valores recomendados para un campo de cadena que no restringen los valores que puede introducir. En su lugar, los valores sugeridos afectan a los valores predefinidos disponibles en la variable [IU de segmentación](../../../segmentation/ui/overview.md) al incluir el campo de cadena como atributo.

Cuándo [definición de un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform y establecer el tipo en [!UICONTROL Cadena], se le da la opción de definir un [enum](#enum) o [valores sugeridos](#suggested-values) para ese campo.

![Imagen que muestra la opción Enumeración y valores sugeridos habilitada para un campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/enum-options-selected.png)

Este documento explica cómo definir enumeraciones y valores sugeridos en [!UICONTROL Esquemas] Espacio de trabajo IU. Para obtener información general rápida sobre las enumeraciones y los valores sugeridos, incluido cómo configurarlos en la interfaz de usuario y sus efectos descendentes, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definir una enumeración {#enum}

Seleccionar **[!UICONTROL Enumeraciones y valores sugeridos]**, luego seleccione **[!UICONTROL Enumeraciones]**. Aparecerán controles adicionales, que le permitirán especificar las restricciones de valor para la enumeración. Para añadir una restricción, seleccione **[!UICONTROL Añadir fila]**.

![Imagen que muestra la opción Enumeraciones seleccionada en la IU](../../images/ui/fields/enum/enum-add-row.png)

En el **[!UICONTROL Valor]** , debe proporcionar el valor exacto al que desea restringir el campo. Si lo desea, puede proporcionar un **[!UICONTROL Nombre para mostrar]** también para la restricción, que afecta a cómo se representará el valor en la segmentación.

Continuar usando **[!UICONTROL Añadir fila]** para agregar las restricciones deseadas y las etiquetas opcionales a la enumeración o seleccione el icono eliminar (![Imagen del icono de eliminación](../../images/ui/fields/enum/remove-icon.png)) junto a una fila previamente agregada para quitarla. Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la IU](../../images/ui/fields/enum/enum-confirm.png)

El lienzo se actualiza para reflejar los cambios. Cuando explore este esquema en el futuro, puede ver y editar las restricciones del campo de enumeración en el carril derecho.

## Definir valores sugeridos {#suggested-values}

Seleccionar **[!UICONTROL Enumeraciones y valores sugeridos]**, luego seleccione **[!UICONTROL Valores sugeridos]** para que aparezcan controles adicionales. Desde aquí, seleccione **[!UICONTROL Añadir fila]** para empezar a añadir valores sugeridos.

![Imagen que muestra la opción Valores sugeridos seleccionada en la IU](../../images/ui/fields/enum/suggested-add-row.png)

En el **[!UICONTROL Nombre para mostrar]** , proporcione un nombre descriptivo para el valor tal como desea que aparezca en la interfaz de usuario de la segmentación. Para añadir más valores sugeridos, seleccione **[!UICONTROL Añadir fila]** de nuevo y repita el proceso según sea necesario. Para quitar una fila agregada anteriormente, seleccione ![el icono eliminar](../../images/ui/fields/enum/remove-icon.png) junto a la fila en cuestión.

Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la IU](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Los valores sugeridos actualizados de un campo tienen un retraso aproximado de cinco minutos que se reflejará en la interfaz de usuario de la segmentación.

### Administrar los valores sugeridos para los campos estándar

Algunos campos de componentes XDM estándar contienen sus propios valores sugeridos, como `eventType` desde el [[!UICONTROL ExperienceEvent de XDM] clase](../../classes/experienceevent.md). Aunque puede crear valores sugeridos adicionales para un campo estándar, no puede modificar ni eliminar ningún valor sugerido que no esté definido por su organización. Al ver un campo estándar en la interfaz de usuario, sus valores sugeridos se muestran, pero son de solo lectura.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la IU](../../images/ui/fields/enum/suggested-standard.png)

Para añadir nuevos valores sugeridos para un campo estándar, seleccione **[!UICONTROL Añadir fila]**. Para eliminar un valor sugerido que su organización añadió anteriormente, seleccione ![el icono eliminar](../../images/ui/fields/enum/remove-icon.png) junto a la fila en cuestión.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la IU](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Reglas de evolución para enumeraciones y valores sugeridos {#evolution}

Después de utilizar un esquema con un campo enum para introducir datos en Platform, cualquier cambio adicional realizado en la definición del esquema debe cumplir con los datos que ya están en el sistema. En general, los cambios realizados en un campo existente solo pueden realizar ese campo **menos** restrictivo. Un campo no puede ser más restrictivo de lo que ya es.

Cuando se trata de enumeraciones y valores sugeridos, las siguientes reglas se aplican después de la ingesta:

* Usted **LATA** agregue valores sugeridos para campos estándar y personalizados con valores sugeridos existentes.
* Usted **LATA** elimine los valores sugeridos de los campos personalizados con valores sugeridos existentes.
* Usted **LATA** agregar nuevos valores de enumeración para un campo de enumeración personalizado existente.
* Usted **LATA** cambie los valores de enumeración de un campo personalizado solo a valores sugeridos, o conviértalos en una cadena sin enumeración ni valores sugeridos. **Este modificador no se puede deshacer una vez aplicado.**
* Usted **NO PUEDE** elimine enumeraciones o valores sugeridos de los campos estándar.
* Usted **NO PUEDE** agregue valores enum a un campo sin valores enum existentes.
* Usted **NO PUEDE** elimine menos que todos los valores de enumeración existentes de un campo personalizado.
* Usted **NO PUEDE** cambie de valores sugeridos a una enumeración.

## Combinación de reglas para enumeraciones y valores sugeridos {#merging}

Si varios esquemas utilizan el mismo campo de enumeración con diferentes configuraciones y esos esquemas se incluyen en una unión, se aplican ciertas reglas cuando se trata de cómo se reconcilian las diferencias de enumeración. Las reglas exactas dependen de si los esquemas que hacen referencia al mismo campo estándar (como `eventType`) o si hacen referencia a la misma ruta de campo personalizada en diferentes grupos de campos.

Si hace referencia al mismo campo estándar:

* Cualquier valor sugerido adicional es **ANEXADO** en el sindicato.
* Las actualizaciones realizadas en los valores sugeridos para la misma clave de enumeración son **ACTUALIZADO** en el sindicato.

Si se hace referencia a la misma ruta de campo personalizado en grupos de campos diferentes:

* Cualquier valor sugerido adicional es **ANEXADO** en el sindicato.
* Si el mismo valor sugerido adicional se define en más de un esquema, esos valores son **COMBINADO** en el sindicato. En otras palabras, el mismo valor sugerido no aparecerá dos veces después de la combinación.

## Limitaciones de validación

Debido a las limitaciones actuales del sistema, hay dos casos en los que el sistema no valida una enumeración durante la ingesta:

1. La enumeración se define en un [campo de matriz](./array.md).
1. La enumeración se define en más de un nivel de profundidad en la jerarquía de esquemas.

## Pasos siguientes

En esta guía se explica cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario. Para obtener información sobre cómo administrar enumeraciones y valores sugeridos mediante la API de Registro de esquemas, consulte lo siguiente [tutorial](../../tutorials/suggested-values.md).

Para obtener información sobre cómo definir otros tipos de campos XDM en la variable [!DNL Schema Editor], consulte la información general sobre [definición de campos en la IU](./overview.md#special).
