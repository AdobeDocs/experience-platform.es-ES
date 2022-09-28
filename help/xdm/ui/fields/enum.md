---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enumeración;campo
solution: Experience Platform
title: Definir campos de enumeración y valores sugeridos en la interfaz de usuario
description: Obtenga información sobre cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: e515e32588991e468429c9256533732d04a4339f
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Definir enumeraciones y valores sugeridos en la interfaz de usuario {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="enumeraciones y valores sugeridos"
>abstract="Un **Enum** restringe un campo de cadena para que solo permita la ingesta de datos que coincidan con un conjunto predefinido de valores. A cada restricción se le puede asignar una **Nombre para mostrar** que rellena listas desplegables de atributos en la interfaz de usuario de segmentación. **Valores sugeridos** para un campo no restrinja la ingesta y solo determine los nombres para mostrar que se muestran en Segmentación. Si tiene varios esquemas que comparten un campo que pertenece a una clase o grupo de campos común y define diferentes enumeraciones o valores sugeridos para ese campo entre cada esquema, esos valores se combinan y se añaden al esquema de unión."

En Experience Data Model (XDM), se puede dar a un campo de cadena un conjunto predefinido de valores aceptados o sugeridos para controlar mejor qué valores se introducen en ese campo o cómo se comportarán en la segmentación.

Un **enum** restringe los valores que se pueden introducir para un campo de cadena a un conjunto predefinido. Si intenta introducir datos en un campo de enumeración y el valor no coincide con ninguno de los definidos en su configuración, se denegará la ingesta.

A diferencia de las enumeraciones, agregue **valores sugeridos** a un campo de cadena no restringe los valores que puede introducir. En su lugar, los valores sugeridos afectan a los valores predefinidos disponibles en la variable [Interfaz de usuario de segmentación](../../../segmentation/ui/overview.md) al incluir el campo de cadena como atributo.

When [definición de un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform y estableciendo el tipo en [!UICONTROL Cadena], se le da la opción de definir un [enum](#enum) o [valores sugeridos](#suggested-values) para ese campo.

![Imagen que muestra la opción Enum y valores sugeridos activada para un campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/enum-options-selected.png)

## Definir una enumeración {#enum}

Select **[!UICONTROL enumeraciones y valores sugeridos]** y, a continuación, seleccione **[!UICONTROL Números]**. Aparecen controles adicionales que permiten especificar las restricciones de valor de la enumeración. Para añadir una restricción, seleccione **[!UICONTROL Añadir fila]**.

![Imagen que muestra la opción enumeraciones seleccionada en la interfaz de usuario](../../images/ui/fields/enum/enum-add-row.png)

En el **[!UICONTROL Valor]** , debe proporcionar el valor exacto al que desea restringir el campo. Opcionalmente, puede proporcionar un **[!UICONTROL Nombre para mostrar]** también para la restricción, que afecta a cómo se representará el valor en la segmentación.

Continúe utilizando **[!UICONTROL Añadir fila]** para añadir las restricciones deseadas y las etiquetas opcionales a la enumeración, o seleccione el icono eliminar (![Imagen del icono de eliminación](../../images/ui/fields/enum/remove-icon.png)) junto a una fila agregada anteriormente para eliminarla. Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/enum-confirm.png)

El lienzo se actualiza para reflejar los cambios. Cuando explore este esquema en el futuro, puede ver y editar las restricciones del campo de enumeración dentro del carril derecho.

## Definir valores sugeridos {#suggested-values}

Select **[!UICONTROL enumeraciones y valores sugeridos]** y, a continuación, seleccione **[!UICONTROL Valores sugeridos]** para que aparezcan controles adicionales. Desde aquí, seleccione **[!UICONTROL Añadir fila]** para empezar a añadir valores sugeridos.

![Imagen que muestra la opción Valores sugeridos seleccionada en la interfaz de usuario](../../images/ui/fields/enum/suggested-add-row.png)

En el **[!UICONTROL Nombre para mostrar]** , proporcione un nombre reconocible para el valor tal como desea que aparezca en la interfaz de usuario de segmentación. Para agregar más valores sugeridos, seleccione **[!UICONTROL Añadir fila]** y repita el proceso según sea necesario. Para quitar una fila agregada anteriormente, seleccione el icono Eliminar (![Imagen del icono de eliminación](../../images/ui/fields/enum/remove-icon.png)) junto a la fila en cuestión.

Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Se produce un retraso aproximado de cinco minutos para que los valores sugeridos actualizados de un campo se reflejen en la interfaz de usuario de segmentación.

### Administrar valores sugeridos para campos estándar

Algunos campos de componentes XDM estándar contienen sus propios valores sugeridos, como `eventType` de la variable [[!UICONTROL XDM ExperienceEvent] class](../../classes/experienceevent.md). Al utilizar estos campos en los esquemas, puede utilizar las conmutaciones disponibles para controlar qué valores sugeridos existentes se van a utilizar.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-standard.png)

Similar a los campos personalizados, seleccione **[!UICONTROL Añadir fila]** para añadir sus propios valores sugeridos para los campos estándar.

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/suggested-standard.png)

### Eliminación de valores sugeridos para campos estándar

Solo los valores sugeridos que defina se pueden eliminar de un campo estándar. Los valores sugeridos existentes se pueden deshabilitar para que ya no aparezcan en la lista desplegable de segmentación, pero no se pueden eliminar directamente.

Por ejemplo, considere un esquema de perfil en el que el valor sugerido para el estándar sea `person.gender` está desactivado:

![Imagen que muestra los valores de enumeración y los nombres para mostrar rellenados para el campo de cadena en la interfaz de usuario](../../images/ui/fields/enum/standard-enum-disabled.png)

En este ejemplo, el nombre para mostrar &quot;[!UICONTROL No específico]&quot; ahora está desactivado para que no se muestre en la lista desplegable de segmentación. Sin embargo, el valor `non_specific` sigue formando parte de la lista de campos enumerados y, por lo tanto, se permite su ingesta. En otras palabras, no se puede deshabilitar el valor de enumeración real para el campo estándar, ya que iría en contra del principio de permitir solo cambios que hagan un campo menos restrictivo.

Consulte la [sección inferior](#evolution) para obtener más información sobre las reglas para actualizar enumeraciones y valores sugeridos para campos de esquema existentes.

## Reglas de evolución para enumeraciones y valores sugeridos {#evolution}

Una vez que se ha utilizado un esquema con un campo de enumeración para introducir datos en Platform, cualquier cambio adicional realizado en la definición del esquema debe cumplir con los datos que ya están en el sistema. En general, los cambios realizados en un campo existente solo pueden hacer ese campo **less** restrictivo. Un campo no se puede hacer más restrictivo de lo que ya es.

Cuando se trata de enumeraciones y valores sugeridos, las siguientes reglas aplican posingesta:

* You **CAN** agregue valores sugeridos para campos estándar y personalizados con valores sugeridos existentes.
* You **CAN** elimine los valores sugeridos de los campos personalizados con valores sugeridos existentes.
* You **CAN** añada nuevos valores de enumeración para un campo de enumeración personalizado existente.
* You **CAN** cambie los valores de enumeración de un campo personalizado solo a valores sugeridos o conviértalos en una cadena sin enumeración ni valores sugeridos. **Este conmutador no se puede deshacer una vez aplicado.**
* You **NO SE PUEDE** elimine enumeraciones o valores sugeridos de los campos estándar.
* You **NO SE PUEDE** agregue valores de enumeración a un campo sin enumeración existente.
* You **NO SE PUEDE** elimine menos que todos los valores de enumeración existentes para un campo personalizado.
* You **NO SE PUEDE** cambiar de valores sugeridos a una enumeración.

## Combinación de reglas para enumeraciones y valores sugeridos {#merging}

Si varios esquemas utilizan el mismo campo de enumeración con configuraciones diferentes y esos esquemas se incluyen en una unión, determinadas reglas se aplican cuando se trata de cómo se concilian las diferencias de enumeración. Las reglas exactas dependen de si los esquemas que hacen referencia al mismo campo estándar (como `eventType`) o si hacen referencia a la misma ruta de campo personalizada en diferentes grupos de campos.

Si se hace referencia al mismo campo estándar:

* Cualquier valor sugerido adicional es **AÑADIDO** en la unión.
* Las actualizaciones realizadas en los valores sugeridos para la misma clave de enumeración son **ACTUALIZADO** en la unión.

Si hace referencia a la misma ruta de campo personalizada en diferentes grupos de campos:

* Cualquier valor sugerido adicional es **AÑADIDO** en la unión.
* Si se define el mismo valor sugerido adicional en más de un esquema, estos valores son **COMBINADO** en la unión. En otras palabras, el mismo valor sugerido no aparecerá dos veces después de la combinación.

## Pasos siguientes

Esta guía explica cómo definir enumeraciones y valores sugeridos para campos de cadena en la interfaz de usuario. Para obtener información sobre cómo administrar enumeraciones y valores sugeridos mediante la API del Registro de esquemas, consulte lo siguiente [tutorial](../../tutorials/suggested-values.md).

Para aprender a definir otros tipos de campos XDM en la variable [!DNL Schema Editor], consulte la descripción general de [definición de campos en la interfaz de usuario](./overview.md#special).
