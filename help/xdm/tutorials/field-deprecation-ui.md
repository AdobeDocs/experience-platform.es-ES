---
title: Poner en desuso un campo XDM en la interfaz de usuario
description: Obtenga información sobre cómo reemplazar los campos del Modelo de datos de experiencia (XDM) con el Editor de esquemas en el Experience Platform.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Poner en desuso un campo XDM en la interfaz de usuario

El modelo de datos de Experience (XDM) le ofrece la flexibilidad para administrar su modelo de datos, ya que sus necesidades comerciales cambian al eliminar los campos de esquema tras la ingesta de datos. Los campos no deseados pueden quedar en desuso para eliminarlos de la vista de la interfaz de usuario y también para ocultarlos de las IU posteriores. Normalmente, una casilla del Editor de esquemas permite mostrar los campos obsoletos y, si es necesario, también puede desactivarlos.

Como los campos obsoletos están ocultos en la interfaz de usuario de forma predeterminada, esto optimiza el esquema en el Editor de esquemas e impide que se agreguen campos no deseados a dependencias descendentes como el generador de segmentos, el diseñador de recorridos, etc. La desaprobación de campos también es compatible con versiones anteriores. Otros sistemas que utilizan campos obsoletos, como segmentos y consultas, seguirán evaluándolos según lo previsto. Si se utiliza un campo obsoleto en un segmento existente, se trata normalmente, lo que significa que el campo se muestra como se espera en el lienzo del generador de segmentos o se evalúa en función de cualquier dato disponible en los campos obsoletos. Se trata de un cambio que no rompe y que no afecta negativamente a ningún flujo de datos existente.

>[!NOTE]
>
>Antes de ingerir los datos en un esquema, puede eliminar los grupos de campos innecesarios. Consulte la documentación sobre [cómo quitar un grupo de campos de un esquema](../ui/resources/schemas.md#remove-fields) para obtener más información.

Una vez introducidos los datos en el esquema, ya no se pueden quitar campos del esquema sin realizar cambios graduales. En este caso, puede eliminar un campo no deseado de un esquema o de un recurso personalizado utilizando la variable [Editor de esquemas](./create-schema-ui.md) o [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Este documento explica cómo desactivar campos para distintos recursos XDM mediante el Editor de esquemas en la interfaz de usuario del Experience Platform. Para ver los pasos sobre la desaprobación de un campo XDM mediante la API, consulte el tutorial sobre [desaprobación de un campo XDM mediante la API del Registro de esquemas](./field-deprecation-api.md).

## Poner en desuso un campo {#deprecate}

Para eliminar un campo personalizado, vaya al Editor de esquemas para el esquema que desee editar. Seleccione el campo que desea eliminar de la lista [!UICONTROL Estructura] del lienzo, seguido de **[!UICONTROL Poner en desuso]** de la variable [!UICONTROL Propiedades de campo].

![El editor de esquemas con un campo seleccionado y Deprecate resaltado.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Aparece un cuadro de diálogo para confirmar las opciones y notificarle que el campo se eliminará de la vista de IU del esquema de unión y se ocultará de las IU posteriores. Para completar la acción, seleccione **[!UICONTROL Confirmar]**.

![El cuadro de diálogo Poner en desuso el campo con Confirmar resaltado.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

El campo se ha eliminado de la vista de IU.

>[!NOTE]
>
>Una vez en desuso, las IU posteriores, como los paneles de Segmentación, el Customer Journey Analytics y Adobe Journey Optimizer, ya no muestran los campos en desuso como parte de su flujo de trabajo. Sin embargo, las IU descendentes tienen la opción de mostrar los campos obsoletos si es necesario y seguir tratando el campo obsoleto como si fuera normal. Consulte su documentación correspondiente para obtener más información. Las consultas y segmentos que utilicen el campo obsoleto seguirán ejecutándose según lo esperado.

## Mostrar campos obsoletos {#show-deprecated}

Para ver los campos obsoletos anteriormente, vaya al esquema correspondiente en el Editor de esquemas. Seleccione el **[!UICONTROL Mostrar campos obsoletos]** en la [!UICONTROL Composición] del lienzo.

El campo obsoleto ahora aparece en la vista de IU. Select **[!UICONTROL Guardar]** para confirmar la configuración.

![El Editor de esquemas con un campo seleccionado, Mostrar campos obsoletos y Guardar resaltados.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Anular la desuso de campos {#undeprecate-fields}

Para deshacer un campo obsoleto, primero [mostrar el campo obsoleto](#show-deprecated) como se ha descrito anteriormente, seleccione el campo obsoleto en el [!UICONTROL Estructura] para obtener más información. A continuación, seleccione **[!UICONTROL No eliminar]** de la variable [!UICONTROL Propiedades del campo] barra lateral seguida de **[!UICONTROL Guardar]**.

![El Editor de esquemas con el campo obsoleto, Desaprobar y Guardar resaltado.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

La variable [!UICONTROL Campo no obsoleto] se abre. Para confirmar los cambios, seleccione **[!UICONTROL Confirmar]**.

![La variable [!UICONTROL Campo no obsoleto] con Confirmar resaltado.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

El campo ahora se muestra como estándar en la vista de interfaz de usuario y también en las IU posteriores. De nuevo, ahora tiene la opción de eliminar el campo.

## Pasos siguientes

Este documento trataba sobre cómo eliminar los campos XDM mediante la interfaz de usuario del Editor de esquemas. Para obtener más información sobre la configuración de campos para los recursos personalizados, consulte la guía de [definición de campos XDM en la API](./custom-fields-api.md). Para obtener más información sobre la administración de descriptores, consulte la [guía de extremo de descriptores](../api/descriptors.md).
