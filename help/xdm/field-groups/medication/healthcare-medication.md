---
title: Healthcare Medication Schema Field Group
description: Obtenga información sobre el grupo de campo Esquema de medicación para atención médica.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 6%

---

# [!UICONTROL Medicación sanitaria] grupo de campos de esquema

[!UICONTROL Medicación sanitaria] es un grupo de campos de esquema estándar para [[!UICONTROL Medicación] clase](../../classes/medication.md). Proporciona un único campo de tipo de objeto `medication` que captura detalles como el nombre de la marca, el número de lote y la cantidad.

![](../../images/field-groups/healthcare-medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `ingredients` | Matriz de objetos | Enumera los ingredientes presentes en el medicamento. Cada objeto incluye las siguientes propiedades: <ul><li>`isActive`: (booleano) indica si este ingrediente aún se utiliza activamente en este medicamento.</li><li>`name`: (cadena) nombre del ingrediente.</li><li>`quantity`: (Cadena) La cantidad de ingrediente presente en el medicamento.</li></ul> |
| `brandName` | Cadena | El nombre comercial de la droga. |
| `codes` | Matriz de cadenas | Una lista de los códigos que identifican este medicamento. |
| `dosageUnitNumber` | Doble | Número de la unidad de dosis del medicamento. |
| `dosageUnitOfMeasurement` | Cadena | La unidad de medida del número de dosis. |
| `expiryDate` | DateTime | Fecha de caducidad del medicamento. |
| `genericName` | Cadena | El nombre genérico del fármaco. |
| `lotNumber` | Cadena | El identificador único del lote del fármaco. |
| `manufacturerName` | Cadena | El nombre del fabricante de la droga. |
| `quantity` | Doble | La cantidad de medicamento en el paquete. |
| `status` | Cadena | Un estado general que indica si el fármaco/medicamento está activo o no. |
| `volume` | Doble | El volumen de la droga. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
