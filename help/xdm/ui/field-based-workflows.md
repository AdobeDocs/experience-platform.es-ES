---
title: Flujos de trabajo basados en el campo en el Editor de esquemas (Beta)
description: Aprenda a añadir individualmente campos de grupos de campos existentes a los esquemas del Modelo de datos de experiencia (XDM).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 07faf4dd749219a955df720a8c740427113a5de2
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# Flujos de trabajo basados en el campo en el Editor de esquemas (Beta)

>[!IMPORTANT]
>
>Los flujos de trabajo descritos en este documento beta ahora están disponibles de forma general en Adobe Experience Platform. Para obtener las últimas directrices sobre los flujos de trabajo basados en el campo en el Editor de esquemas, consulte la [guía de la interfaz de usuario de schemas](./resources/schemas.md) en su lugar. Esta guía se eliminará próximamente.

Adobe Experience Platform ofrece un conjunto sólido de [grupos de campos](../schema/composition.md#field-group) para su uso en esquemas del Modelo de datos de experiencia (XDM). La estructura y la semántica detrás de estos grupos de campo están cuidadosamente diseñadas para satisfacer una amplia variedad de casos de uso de segmentación y otras aplicaciones posteriores en Platform. También puede definir sus propios grupos de campos personalizados para satisfacer necesidades comerciales únicas.

Cuando se agrega un grupo de campos a un esquema, ese esquema hereda todos los campos contenidos en ese grupo. Sin embargo, ahora puede agregar campos individuales al esquema sin necesidad de incluir otros campos del grupo de campos asociado que no necesariamente utilice.

Esta guía trata los diferentes métodos para añadir campos individuales a un esquema en la interfaz de usuario de Platform.

## Requisitos previos

Este tutorial supone que está familiarizado con el [composición de esquemas XDM](../schema/composition.md) y cómo usar el Editor de esquemas en la interfaz de usuario de Platform. Para continuar, debe iniciar el proceso de [creación de un nuevo esquema](./resources/schemas.md) y asignarlo a una clase estándar antes de continuar con esta guía.

## Eliminación de campos agregados de grupos de campos estándar {#remove-field-group}

Después de agregar un grupo de campos estándar a un esquema, puede quitar los campos estándar que no necesite.

>[!NOTE]
>
>La eliminación de campos de un grupo de campos estándar solo afecta al esquema en el que se está trabajando y no afecta al propio grupo de campos. Si elimina los campos estándar de un esquema, dichos campos seguirán estando disponibles en todos los demás esquemas que empleen el mismo grupo de campos.

En el ejemplo siguiente, el grupo de campos estándar **[!UICONTROL Detalles demográficos]** se ha agregado a un esquema. Quitar un único campo como `taxId`, seleccione el campo en el lienzo y, a continuación, seleccione **[!UICONTROL Eliminar]** en el carril derecho.

![Quitar un solo campo](../images/ui/field-based-workflows/remove-single-field.png)

Si desea quitar varios campos, puede administrar el grupo de campos como un todo. Seleccione un campo que pertenezca al grupo en el lienzo y, a continuación, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

![Administrar campos relacionados](../images/ui/field-based-workflows/manage-related-fields.png)

Aparece un cuadro de diálogo que muestra la estructura del grupo de campos en cuestión. Desde aquí puede utilizar las casillas de verificación proporcionadas para seleccionar o anular la selección de los campos que necesite. Cuando esté satisfecho, seleccione **[!UICONTROL Confirmar]**.

![Seleccionar campos del grupo de campos](../images/ui/field-based-workflows/select-fields.png)

El lienzo vuelve a aparecer con solo los campos seleccionados presentes en la estructura del esquema.

![Campos añadidos](../images/ui/field-based-workflows/fields-added.png)

## Añadir campos estándar directamente a un esquema

Puede agregar campos de grupos de campos estándar directamente a un esquema sin necesidad de conocer previamente su grupo de campos correspondiente. Para añadir un campo estándar a un esquema, seleccione el signo más (**+**) junto al nombre del esquema en el lienzo. Un **[!UICONTROL Campo sin título]** el marcador de posición aparece en la estructura del esquema y el carril correcto se actualiza para mostrar los controles que deben configurarse.

![Marcador de posición de campo](../images/ui/field-based-workflows/root-custom-field.png)

En **[!UICONTROL Nombre del campo]**, empiece a escribir el nombre del campo que desee añadir. El sistema busca automáticamente campos estándar que coincidan con la consulta y los enumera en **[!UICONTROL Campos estándar recomendados]**, incluidos los grupos de campos a los que pertenecen.

![Campos estándar recomendados](../images/ui/field-based-workflows/standard-field-search.png)

Aunque algunos campos estándar comparten el mismo nombre, su estructura puede variar según el grupo de campos del que provengan. Si un campo estándar está anidado dentro de un objeto principal en la estructura del grupo de campos, el campo principal también se incluye en el esquema si se agrega el campo secundario.

Seleccione el icono de vista previa (![Icono de vista previa](../images/ui/field-based-workflows/preview-icon.png)) junto a un campo estándar para ver la estructura de su grupo de campos y comprender mejor cómo se puede anidar. Para añadir el campo estándar al esquema, seleccione el icono de signo más (![Icono Más](../images/ui/field-based-workflows/add-icon.png)).

![Añadir campo estándar](../images/ui/field-based-workflows/add-standard-field.png)

El lienzo se actualiza para mostrar el campo estándar añadido al esquema, incluidos los campos principales anidados dentro de la estructura del grupo de campos. El nombre del grupo de campos también se enumera en **[!UICONTROL Grupos de campo]** en el carril izquierdo. Si desea agregar más campos del mismo grupo de campos, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

![Campo estándar añadido](../images/ui/field-based-workflows/standard-field-added.png)

## Añadir campos personalizados directamente a un esquema

Al igual que el flujo de trabajo para los campos estándar, también puede añadir sus propios campos personalizados directamente a un esquema.

Para añadir campos al nivel raíz de un esquema, seleccione el signo más (**+**) junto al nombre del esquema en el lienzo. Un **[!UICONTROL Campo sin título]** el marcador de posición aparece en la estructura del esquema y el carril correcto se actualiza para mostrar los controles que deben configurarse.

![Campo personalizado raíz](../images/ui/field-based-workflows/root-custom-field.png)

Comience a escribir el nombre del campo que desee añadir y el sistema empezará automáticamente a buscar campos estándar coincidentes. Para crear un nuevo campo personalizado, seleccione la opción superior anexada con **([!UICONTROL Campo nuevo])**.

![Campo nuevo](../images/ui/field-based-workflows/custom-field-search.png)

A partir de aquí, proporcione un nombre para mostrar y un tipo de datos para el campo. En **[!UICONTROL Asignar grupo de campos]**, debe seleccionar un grupo de campos para el nuevo campo al que desea asociar. Comience a escribir el nombre del grupo de campos y si ya lo ha hecho [grupos de campos personalizados creados](./resources/field-groups.md#create) aparecerán en la lista desplegable. También puede escribir un nombre único en el campo para crear un nuevo grupo de campos.

![Seleccionar grupo de campos](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Si selecciona un grupo de campos personalizado existente, cualquier otro esquema que emplee ese grupo de campos también heredará el campo recién agregado después de guardar los cambios. Por este motivo, seleccione únicamente un grupo de campos existente si desea este tipo de propagación. De lo contrario, debe optar por crear un nuevo grupo de campos personalizados.

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![Aplicar campo](../images/ui/field-based-workflows/apply-field.png)

El nuevo campo se agrega al lienzo y tiene un área de nombres debajo de su [ID de inquilino](../api/getting-started.md#know-your-tenant_id) para evitar conflictos con campos XDM estándar. El grupo de campos al que ha asociado el nuevo campo también aparece en **[!UICONTROL Grupos de campo]** en el carril izquierdo.

![ID del inquilino](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>El resto de los campos proporcionados por el grupo de campos personalizados seleccionado se eliminan del esquema de forma predeterminada. Si desea añadir algunos de estos campos al esquema, seleccione un campo perteneciente al grupo y, a continuación, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

### Añadir campos personalizados a la estructura de los grupos de campos estándar

Si el esquema en el que está trabajando tiene un campo de tipo objeto proporcionado por un grupo de campos estándar, puede agregar sus propios campos personalizados a ese objeto estándar. Seleccione el signo más (**+**) junto a la raíz del objeto y proporcione los detalles del campo personalizado en el carril derecho.

![Añadir campo al objeto estándar](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Después de aplicar los cambios, el nuevo campo aparece debajo del espacio de nombres del ID del inquilino dentro del objeto estándar. Esta área de nombres anidada evita conflictos de nombre de campo dentro del propio grupo de campos para evitar que se rompan los cambios en otros esquemas que utilizan el mismo grupo de campos.

![Campo añadido al objeto estándar](../images/ui/field-based-workflows/added-to-standard-object.png)

## Pasos siguientes

Esta guía abarcaba los nuevos flujos de trabajo basados en campos para el Editor de esquemas en la interfaz de usuario de Platform. Para obtener más información sobre la administración de esquemas en la interfaz de usuario, consulte la [Información general sobre la IU](./overview.md).
