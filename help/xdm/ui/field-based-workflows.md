---
title: Flujos de trabajo basados en campos en el Editor de esquemas
description: Aprenda a añadir individualmente campos de grupos de campos existentes a los esquemas XDM (Experience Data Model).
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Flujos de trabajo basados en campos en el Editor de esquemas

Adobe Experience Platform proporciona un conjunto sólido de [grupos de campos](../schema/composition.md#field-group) estandarizados para su uso en esquemas XDM (Experience Data Model). La estructura y la semántica detrás de estos grupos de campo se personalizan cuidadosamente para satisfacer una amplia variedad de casos de uso de segmentación y otras aplicaciones de flujo descendente en Platform. También puede definir sus propios grupos de campos personalizados para satisfacer necesidades comerciales únicas.

Cuando se agrega un grupo de campos a un esquema, ese esquema hereda todos los campos contenidos en ese grupo. Sin embargo, ahora puede agregar campos individuales al esquema sin necesidad de incluir otros campos del grupo de campos asociado que no utilice necesariamente.

Esta guía describe los diferentes métodos para agregar campos individuales a un esquema en la interfaz de usuario de Platform.

## Requisitos previos

Este tutorial supone que está familiarizado con la [composición de esquemas XDM](../schema/composition.md) y con cómo utilizar el Editor de esquemas en la IU de Platform. Para continuar, debe iniciar el proceso de [creación de un nuevo esquema](./resources/schemas.md) y asignarlo a una clase estándar antes de continuar con esta guía.

## Quitar campos agregados de grupos de campos estándar {#remove-field-group}

Después de agregar un grupo de campos estándar a un esquema, puede quitar los campos estándar que no necesite.

>[!NOTE]
>
>La eliminación de campos de un grupo de campos estándar solo afecta al esquema en el que se está trabajando y no afecta al propio grupo de campos. Si elimina los campos estándar en un esquema, esos campos seguirán estando disponibles en todos los demás esquemas que empleen el mismo grupo de campos.

En el ejemplo siguiente, se ha agregado el grupo de campos estándar **[!UICONTROL Detalles demográficos]** a un esquema. Para quitar un solo campo como `maritalStatus`, selecciónelo en el lienzo y, a continuación, seleccione **[!UICONTROL Quitar]** en el carril derecho.

![Se ha resaltado el Editor de esquemas con el grupo de campos, el campo Marital Status y Remove.](../images/ui/field-based-workflows/remove-single-field.png)

Si desea eliminar varios campos, puede administrar el grupo de campos en su conjunto. Seleccione un campo que pertenezca al grupo en el lienzo y, a continuación, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

![Se resaltaron el Editor de esquemas con un campo y Administrar campos relacionados.](../images/ui/field-based-workflows/manage-related-fields.png)

Aparecerá un cuadro de diálogo que muestra la estructura del grupo de campos en cuestión. Desde aquí puede utilizar las casillas de verificación proporcionadas para seleccionar o anular la selección de los campos necesarios. Cuando esté satisfecho, seleccione **[!UICONTROL Confirmar]**.

![El cuadro de diálogo Administrar campos relacionados con el diagrama de grupo de campos y Confirmar resaltados.](../images/ui/field-based-workflows/select-fields.png)

El lienzo vuelve a aparecer con solo los campos seleccionados presentes en la estructura del esquema.

![Editor de esquemas con el grupo de campos recién editado resaltado.](../images/ui/field-based-workflows/fields-added.png)

## Añadir campos estándar directamente a un esquema

Puede añadir campos de grupos de campos estándar directamente a un esquema sin necesidad de conocer previamente su grupo de campos correspondiente. Para agregar un campo estándar a un esquema, seleccione el icono más (**+**) junto al nombre del esquema en el lienzo. Aparece un marcador de posición **[!UICONTROL Campo sin título]** en la estructura de esquema y el carril derecho se actualiza para mostrar los controles y configurar el campo.

![Editor de esquemas con un marcador de posición de campo raíz resaltado.](../images/ui/field-based-workflows/root-custom-field.png)

En **[!UICONTROL Nombre de campo]**, empiece a escribir el nombre del campo que desea agregar. El sistema busca automáticamente los campos estándar que coinciden con la consulta y los enumera en **[!UICONTROL Campos estándar recomendados]**, incluidos los grupos de campos a los que pertenecen.

![Se resaltó el nombre del campo y se mostró una lista de campos estándar recomendados dentro de las propiedades de campo del Editor de esquemas.](../images/ui/field-based-workflows/standard-field-search.png)

Aunque algunos campos estándar comparten el mismo nombre, su estructura puede variar según el grupo de campos del que procedan. Si un campo estándar está anidado en un objeto principal en la estructura de grupo de campos, el campo principal también se incluye en el esquema si se agrega el campo secundario.

Seleccione el icono de vista previa (![Icono de vista previa](/help/images/icons/preview.png)) junto a un campo estándar para ver la estructura de su grupo de campos y comprender mejor cómo se puede anidar. Para agregar el campo estándar al esquema, seleccione el icono más (![Icono más](/help/images/icons/add-circle.png)).

![El icono de agregar resaltado en un elemento de los campos estándar sugeridos.](../images/ui/field-based-workflows/add-standard-field.png)

El lienzo se actualiza para mostrar el campo estándar agregado al esquema, incluidos los campos principales en los que está anidado dentro de la estructura de grupo de campos. El nombre del grupo de campos también se enumera en **[!UICONTROL Grupos de campos]** en el carril izquierdo. Si desea agregar más campos del mismo grupo de campos, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

![Se ha resaltado el Editor de esquemas con el grupo de campos, el campo estándar y los campos relacionados de Administrar.](../images/ui/field-based-workflows/standard-field-added.png)

## Añadir campos personalizados directamente a un esquema

Al igual que el flujo de trabajo para los campos estándar, también puede agregar sus propios campos personalizados directamente a un esquema.

Para agregar campos al nivel raíz de un esquema, seleccione el icono de signo más (**+**) junto al nombre del esquema en el lienzo. Aparece un marcador de posición **[!UICONTROL Campo sin título]** en la estructura de esquema y el carril derecho se actualiza para mostrar los controles y configurar el campo.

![El editor de esquemas con el icono de agregar y un campo de nivel raíz sin título resaltado.](../images/ui/field-based-workflows/root-custom-field.png)

Empiece a escribir el nombre del campo que desea añadir y el sistema comenzará automáticamente a buscar los campos estándar coincidentes. Para crear un nuevo campo personalizado, seleccione la opción superior anexada con **([!UICONTROL Nuevo campo])**.

![Nombre de campo y sugerencia de nuevo campo resaltados en las propiedades de campo del Editor de esquemas.](../images/ui/field-based-workflows/custom-field-search.png)

Desde aquí, proporcione un nombre para mostrar y un tipo de datos para el campo. En **[!UICONTROL Asignar grupo de campos]**, debe seleccionar un grupo de campos al que se asociará el nuevo campo. Empiece a escribir el nombre del grupo de campos y, si anteriormente ha [creado grupos de campos personalizados](./resources/field-groups.md#create), aparecerán en la lista desplegable. También puede escribir un nombre único en el campo para crear un nuevo grupo de campos.

![Los valores de las propiedades Nombre para mostrar, Tipo y Asignar a resaltados en el Editor de esquemas.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Si selecciona un grupo de campos personalizados existente, cualquier otro esquema que emplee ese grupo de campos también heredará el campo recién agregado después de guardar los cambios. Por este motivo, seleccione únicamente un grupo de campos existente si desea este tipo de propagación. De lo contrario, debe optar por crear un nuevo grupo de campos personalizados.

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![Aplicar está resaltado en las propiedades de campo del Editor de esquemas.](../images/ui/field-based-workflows/apply-field.png)

El nuevo campo se agrega al lienzo y tiene un espacio de nombres bajo su [ID de inquilino](../api/getting-started.md#know-your-tenant_id) para evitar conflictos con los campos XDM estándar. El grupo de campos con el que asoció el nuevo campo también aparece en **[!UICONTROL Grupos de campos]** en el carril izquierdo.

![Editor de esquemas con el nuevo campo agregado al lienzo y el espacio de nombres debajo de su id. de inquilino. El grupo de campos y el campo están resaltados.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>El resto de los campos proporcionados por el grupo de campos personalizados seleccionado se eliminan del esquema de forma predeterminada. Si desea agregar algunos de estos campos al esquema, seleccione un campo que pertenezca al grupo y, a continuación, seleccione **[!UICONTROL Administrar campos relacionados]** en el carril derecho.

### Agregar campos personalizados a la estructura de grupos de campos estándar

Si el esquema en el que está trabajando tiene un campo de tipo de objeto proporcionado por un grupo de campos estándar, puede agregar sus propios campos personalizados a ese objeto estándar. Seleccione el icono más (**+**) junto a la raíz del objeto.

>[!IMPORTANT]
>
>Todos los campos agregados a un grupo de campos en un esquema también aparecerán en todos los demás esquemas que empleen el mismo grupo de campos.

![Editor de esquemas con el icono más junto a un objeto estándar resaltado.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Consulte [Crear y editar esquemas en la guía de la interfaz de usuario](./resources/schemas.md#custom-fields-for-standard-groups) para obtener más información sobre cómo agregar campos personalizados.

## Pasos siguientes

En esta guía se describen los nuevos flujos de trabajo basados en campos para el Editor de esquemas en la IU de Platform. Para obtener más información sobre la administración de esquemas en la interfaz de usuario, consulte [Descripción general de la interfaz de usuario](./overview.md).
