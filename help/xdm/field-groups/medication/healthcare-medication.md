---
title: Healthcare Medication Schema Field Group
description: Obtenga información sobre el grupo de campo Esquema de medicación para atención médica.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL Medicación para el cuidado de la salud] grupo de campo de esquema

[!UICONTROL Medicación para atención médica] es un grupo de campo de esquema estándar para la clase [[!UICONTROL Medicación]](../../classes/medication.md). Proporciona un único campo de tipo de objeto `medication` que captura detalles como el nombre de la marca, el número de lote y la cantidad.

![](../../images/field-groups/healthcare-medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ingredients` | Matriz de objetos | Enumera los ingredientes presentes en el medicamento. Cada objeto incluye las siguientes propiedades: <ul><li>`isActive`: (booleano) indica si este ingrediente se sigue usando activamente en este medicamento.</li><li>`name`: (Cadena) Nombre del ingrediente.</li><li>`quantity`: (Cadena) La cantidad de ingrediente presente en el medicamento.</li></ul> |
| `brandName` | Cadena | El nombre comercial de la droga. |
| `codes` | Matriz de cadenas | Una lista de los códigos que identifican este medicamento. |
| `dosageUnitNumber` | Duplicada | Número de la unidad de dosis del medicamento. |
| `dosageUnitOfMeasurement` | Cadena | La unidad de medida del número de dosis. |
| `expiryDate` | Fecha/Hora | Fecha de caducidad del medicamento. |
| `genericName` | Cadena | El nombre genérico del fármaco. |
| `lotNumber` | Cadena | El identificador único del lote del fármaco. |
| `manufacturerName` | Cadena | El nombre del fabricante de la droga. |
| `quantity` | Duplicada | La cantidad de medicamento en el paquete. |
| `status` | Cadena | Un estado general que indica si el fármaco/medicamento está activo o no. |
| `volume` | Duplicada | El volumen de la droga. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
