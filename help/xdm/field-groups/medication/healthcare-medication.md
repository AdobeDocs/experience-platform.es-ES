---
title: Grupo de campos de esquema de medicina sanitaria
description: Este documento proporciona una visión general del grupo de campos de esquema de medicación para el sector sanitario.
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 6%

---

# [!UICONTROL Medicación médica] grupo de campos de esquema

[!UICONTROL Medicación médica] es un grupo de campos de esquema estándar para la variable [[!UICONTROL Medicación] class](../../classes/medication.md). Proporciona un único campo de tipo de objeto `medication` que captura detalles como nombre de marca, número de lote y cantidad.

![](../../images/field-groups/healthcare-medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ingredients` | Matriz de objetos | Enumera los ingredientes presentes en el medicamento. Cada objeto incluye las siguientes propiedades: <ul><li>`isActive`: (Booleano) Indica si este ingrediente se sigue utilizando activamente en este medicamento.</li><li>`name`: (Cadena) El nombre del ingrediente.</li><li>`quantity`: (Cadena) La cantidad del ingrediente presente en el medicamento.</li></ul> |
| `brandName` | Cadena | El nombre de marca del medicamento. |
| `codes` | Matriz de cadenas | Lista de códigos que identifican este medicamento. |
| `dosageUnitNumber` | Duplicada | El número de unidad de dosificación del medicamento. |
| `dosageUnitOfMeasurement` | Cadena | Unidad de medida para el número de dosis. |
| `expiryDate` | DateTime | Fecha de caducidad del medicamento. |
| `genericName` | Cadena | El nombre genérico del medicamento. |
| `lotNumber` | Cadena | Identificador único del lote del medicamento. |
| `manufacturerName` | Cadena | El nombre del fabricante del medicamento. |
| `quantity` | Duplicada | La cantidad de medicamento en el paquete. |
| `status` | Cadena | Estado general que indica si el medicamento/medicamento está activo o no. |
| `volume` | Duplicada | El volumen del medicamento. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
