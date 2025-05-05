---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enum;campo;
solution: Experience Platform
title: Definición de campos de enumeración y valores sugeridos en la IU
description: Obtenga información sobre cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario de Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 8%

---

# Defina enumeraciones y valores sugeridos en la interfaz de usuario {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enumeraciones y valores sugeridos"
>abstract="Una **enumeración** restringe un campo de cadena para que solo permita la ingesta de datos que coincidan con un conjunto predefinido de valores. A cada restricción de enumeración se le puede asignar un **Nombre para mostrar** que rellena listas desplegables de atributos en la interfaz de usuario de segmentación. Los **valores sugeridos** para un campo no restringen la ingesta y solo determinan los nombres para mostrar que aparecen en la segmentación. Si tiene varios esquemas que comparten un campo que pertenece a una clase o grupo de campos común y define diferentes enumeraciones o valores sugeridos para ese campo entre cada esquema, esos valores se combinan y se añaden al esquema de unión."

En el Modelo de datos de experiencia (XDM), se puede dar a un campo de cadena un conjunto predefinido de valores aceptados o sugeridos para controlar mejor qué valores se incorporan a ese campo o cómo se comportará en la segmentación.

**[!UICONTROL Enumeraciones]** restringen los valores que se pueden introducir para un campo de cadena a un conjunto predefinido. Si intenta introducir datos en un campo de enumeración y el valor no coincide con ninguno de los definidos en su configuración, se denegará la ingesta.

A diferencia de las enumeraciones, la opción **[!UICONTROL Valores sugeridos]** permite denotar un conjunto de valores recomendados para un campo de cadena que no restringen los valores que puede introducir. En su lugar, los valores sugeridos afectan a los valores predefinidos disponibles en la [IU de segmentación](../../../segmentation/ui/overview.md) al incluir el campo de cadena como atributo.

Al [definir un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform y establecer el tipo en [!UICONTROL Cadena], se le da la opción de definir un [enum](#enum) o [valores sugeridos](#suggested-values) para ese campo.

![Imagen que muestra la opción Enumeración y valores sugeridos habilitada para un campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/enum-options-selected.png)

Este documento explica cómo definir enumeraciones y valores sugeridos en el área de trabajo de la interfaz de usuario de [!UICONTROL Schemas]. Para obtener información general rápida sobre las enumeraciones y los valores sugeridos, incluido cómo configurarlos en la interfaz de usuario y sus efectos descendentes, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3413676/?quality=12&learn=on&captions=spa)

## Definir una enumeración {#enum}

Seleccione **[!UICONTROL Enumeraciones y Valores sugeridos]**, luego seleccione **[!UICONTROL Enumeraciones]**. Aparecerán controles adicionales, que le permitirán especificar las restricciones de valor para la enumeración. Para agregar una restricción, seleccione **[!UICONTROL Agregar fila]**.

![Imagen que muestra la opción Enumeraciones seleccionada en la IU](../../images/ui/fields/enum/enum-add-row.png)

En la columna **[!UICONTROL Value]**, debe proporcionar el valor exacto al que desea restringir el campo. Opcionalmente, también puede proporcionar un **[!UICONTROL Nombre para mostrar]** fácil de usar para la restricción, lo que afecta a la forma en que se representará el valor en la segmentación.

Continúe usando **[!UICONTROL Agregar fila]** para agregar las restricciones deseadas y las etiquetas opcionales a la enumeración o seleccione el icono de eliminación (![Imagen del icono de eliminación](/help/images/icons/remove-circle.png)) junto a una fila agregada anteriormente para quitarla. Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/enum-confirm.png)

El lienzo se actualiza para reflejar los cambios. Cuando explore este esquema en el futuro, puede ver y editar las restricciones del campo de enumeración en el carril derecho.

## Definir valores sugeridos {#suggested-values}

Seleccione **[!UICONTROL Enumeraciones y valores sugeridos]**, luego seleccione **[!UICONTROL Valores sugeridos]** para que aparezcan controles adicionales. Desde aquí, seleccione **[!UICONTROL Agregar fila]** para empezar a agregar valores sugeridos.

![Imagen que muestra la opción Valores sugeridos seleccionada en la IU](../../images/ui/fields/enum/suggested-add-row.png)

En la columna **[!UICONTROL Nombre para mostrar]**, proporcione un nombre descriptivo para el valor tal como desea que aparezca en la interfaz de usuario de la segmentación. Para agregar más valores sugeridos, vuelva a seleccionar **[!UICONTROL Agregar fila]** y repita el proceso según sea necesario. Para quitar una fila agregada anteriormente, seleccione ![el icono Eliminar](/help/images/icons/remove-circle.png) que se encuentra junto a la fila en cuestión.

Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Los valores sugeridos actualizados de un campo tienen un retraso aproximado de cinco minutos que se reflejará en la interfaz de usuario de la segmentación.

### Administrar los valores sugeridos para los campos estándar

Algunos campos de componentes XDM estándar contienen sus propios valores sugeridos, como `eventType` de la clase [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md). Aunque puede crear valores sugeridos adicionales para un campo estándar, no puede modificar ni eliminar ningún valor sugerido que no esté definido por su organización. Al ver un campo estándar en la interfaz de usuario, sus valores sugeridos se muestran, pero son de solo lectura.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-standard.png)

Para agregar nuevos valores sugeridos para un campo estándar, seleccione **[!UICONTROL Agregar fila]**. Para quitar un valor sugerido que su organización agregó anteriormente, seleccione ![el icono Eliminar](/help/images/icons/remove-circle.png) junto a la fila en cuestión.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Reglas de evolución para enumeraciones y valores sugeridos {#evolution}

Después de utilizar un esquema con un campo enum para introducir datos en Experience Platform, cualquier cambio adicional realizado en la definición del esquema debe cumplir con los datos que ya están en el sistema. En general, los cambios realizados en un campo existente solo pueden hacer que el campo **less** sea restrictivo. Un campo no puede ser más restrictivo de lo que ya es.

Cuando se trata de enumeraciones y valores sugeridos, las siguientes reglas se aplican después de la ingesta:

* Usted **PUEDE** agregar valores sugeridos para campos estándar y personalizados con valores sugeridos existentes.
* Usted **PUEDE** quitar valores sugeridos de los campos personalizados con valores sugeridos existentes.
* Usted **PUEDE** agregar nuevos valores de enumeración para un campo de enumeración personalizado existente.
* Usted **CAN** cambia los valores de enumeración de un campo personalizado a valores sugeridos solamente, o lo convierte a una cadena sin enumeración ni valores sugeridos. **Este modificador no se puede deshacer una vez aplicado.**
* Usted **NO PUEDE** eliminar enumeraciones o valores sugeridos de los campos estándar.
* Usted **NO** puede agregar valores de enumeración a un campo sin enumeración existente.
* Usted **NO PUEDE** eliminar menos de todos los valores de enumeración existentes para un campo personalizado.
* Usted **NO PUEDE** cambiar de valores sugeridos a una enumeración.

## Combinación de reglas para enumeraciones y valores sugeridos {#merging}

Si varios esquemas utilizan el mismo campo de enumeración con diferentes configuraciones y esos esquemas se incluyen en una unión, se aplican ciertas reglas cuando se trata de cómo se reconcilian las diferencias de enumeración. Las reglas exactas dependen de si los esquemas que hacen referencia al mismo campo estándar (como `eventType`) o si hacen referencia a la misma ruta de campo personalizada en diferentes grupos de campos.

Si hace referencia al mismo campo estándar:

* Cualquier valor sugerido adicional es **APPENDED** en la unión.
* Las actualizaciones realizadas en los valores sugeridos para la misma clave de enumeración son **UPDATED** en la unión.

Si se hace referencia a la misma ruta de campo personalizado en grupos de campos diferentes:

* Cualquier valor sugerido adicional es **APPENDED** en la unión.
* Si el mismo valor sugerido adicional se define en más de un esquema, esos valores son **MERGED** en la unión. En otras palabras, el mismo valor sugerido no aparecerá dos veces después de la combinación.

## Limitaciones de validación

Debido a las limitaciones actuales del sistema, hay dos casos en los que el sistema no valida una enumeración durante la ingesta:

1. La enumeración se define en un [campo de matriz](./array.md).
1. La enumeración se define en más de un nivel de profundidad en la jerarquía de esquemas.

## Pasos siguientes

En esta guía se explica cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario. Para obtener información sobre cómo administrar enumeraciones y valores sugeridos mediante la API de Registro de esquemas, consulte el siguiente [tutorial](../../tutorials/suggested-values.md).

Para obtener información sobre cómo definir otros tipos de campos XDM en [!DNL Schema Editor], consulte la descripción general de [definición de campos en la interfaz de usuario](./overview.md#special).
