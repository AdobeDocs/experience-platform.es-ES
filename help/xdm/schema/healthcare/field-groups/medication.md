---
title: Grupo de campo del esquema de medicación
description: Obtenga información sobre el grupo de campos Esquema de medicación.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 6%

---

# [!UICONTROL Medicación] grupo de campos de esquema

[!UICONTROL Medication] es un grupo de campos de esquema estándar para la [[!DNL Medication] clase](../../../classes/medication.md). Proporciona un único campo de tipo de objeto `healthcareMedication` que captura la información de un medicamento.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/medication/medication.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| ---|  --- | --- | --- |
| [!UICONTROL Lote] | `batch` | Objeto | Detalles sobre un medicamento envasado. Contiene dos propiedades: <li>`lotNumber`: un valor de cadena para el identificador asignado al lote.</li> <li>`expirationDate`: un valor DateTime para cuándo caducará el lote.</li> |
| [!UICONTROL Código] | `code` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código que identifica este medicamento. |
| [!UICONTROL Definición] | `definition` | [[!UICONTROL Referencia]](../data-types/reference.md) | La definición del medicamento. |
| [!UICONTROL Formulario de dosis] | `doseForm` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Describe la forma de dosis de la medicación, como tabletas o cápsulas. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Un identificador del medicamento. |
| [!UICONTROL Ingrediente] | `ingredient` | Matriz de objetos | Describe la información de los ingredientes del medicamento. Consulte la [sección siguiente](#ingredient) para obtener más información. |
| [!UICONTROL Titular de la autorización de comercialización] | `marketingAuthorizationHolder` | [[!UICONTROL Referencia]](../data-types/reference.md) | La organización que tiene la autorización para comercializar el medicamento. |
| [!UICONTROL Volumen total] | `totalVolume` | [[!UICONTROL Cantidad]](../data-types/quantity.md) | La cantidad de producto proporcionada en el medicamento cuando el código del producto no deduce un tamaño del paquete. |
| [!UICONTROL Estado] | `status` | Cadena | El estado del medicamento. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de ingredientes](../../../images/healthcare/field-groups/medication/ingredient.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Elemento] | `item` | [[!UICONTROL Referencia codificable]](../data-types/codeable-reference.md) | El ingrediente que se describe. |
| [!UICONTROL Concepto codificable de intensidad] | `strengthCodeableConcept` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La cantidad de ingrediente presente, expresada en una terminología definida por el sistema. |
| [!UICONTROL Cantidad de fuerza] | `strengthQuantity` | [[!UICONTROL Cantidad]](../data-types/quantity.md) | La cantidad de ingrediente presente. |
| [!UICONTROL Proporción de fuerza] | `strengthRatio` | [[!UICONTROL Proporción]](../data-types/ratio.md) | La proporción del ingrediente presente. |
| [!UICONTROL Activo] | `isActive` | Booleano | Indica si el ingrediente está activo. |
