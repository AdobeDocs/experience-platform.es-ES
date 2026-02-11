---
title: Actualizar variable
description: Modifica el contenido de un elemento de datos variable.
exl-id: 6c558d1e-85b4-45f9-ba4d-5fed1ec6e308
source-git-commit: 50881ef9498196f2de5519f050800334019a2586
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Actualizar variable

La acción **[!UICONTROL Update variable]** le permite realizar cambios parciales o incrementales en un [elemento de datos variable](../data-element-types.md#variable). Puede usar esta acción para generar un objeto al que posteriormente se pueda hacer referencia en una acción [[!UICONTROL Send event]](send-event.md). Rellenar elementos de datos y asignarlos a propiedades dentro de un objeto XDM se adapta a la mayoría de los casos de uso; esta acción proporciona más flexibilidad para permitirle establecer condicionalmente propiedades en diferentes elementos de datos en función de las condiciones de las reglas.

Antes de utilizar esta acción, ya debe tener un elemento de datos variable creado. Una vez que seleccione un elemento de datos de variable para modificarlo, aparecerá un editor, que le permitirá establecer los campos deseados para esta acción.

![Captura de pantalla de la acción de actualización de variable en la interfaz de configuración de acción](../assets/update-variable.png)

El esquema XDM utilizado en el editor coincide con el esquema seleccionado dentro del elemento de datos de la variable. Para definir una o varias propiedades del objeto, expanda los objetos y seleccione las propiedades que desee. Por ejemplo, en la captura de pantalla siguiente, la propiedad `producedBy` está establecida en el elemento de datos `%Produced by data element%`.

![Captura de pantalla de la interfaz de configuración de acción que muestra una propiedad actualizada](../assets/update-variable-set-property.png)

Si selecciona un elemento de datos variable que utiliza un objeto de datos en lugar de un objeto XDM, los campos disponibles dependen de los productos seleccionados al configurar el elemento de datos. Por ejemplo, si crea un objeto de datos que incluye Adobe Analytics, campos y selecciona el elemento de datos variable en esta interfaz de usuario proporcionarán campos que puede rellenar específicos de Adobe Analytics.

![Captura de pantalla de la interfaz de configuración de acción que muestra un elemento de datos variable basado en un objeto de datos](../assets/variable-data-element-data.png)
