---
title: Clase de medicamento
description: Obtenga información sobre la clase de medicamentos en el modelo de datos de experiencia (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# clase [!UICONTROL Medicamento]

En el Experience Data Model (XDM), la clase [!UICONTROL Medication] captura el conjunto mínimo de propiedades que definen una sustancia utilizada para el tratamiento médico, especialmente un medicamento o un fármaco.

![Estructura de clase](../images/classes/medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `medicationId` | [!UICONTROL Cadena] | Un identificador único del medicamento. |
| `medicationName` | [!UICONTROL Cadena] | El nombre del medicamento. |

{style="table-layout:auto"}

La clase se puede ampliar con el grupo de campo [[!UICONTROL Medicamentos para la atención médica]](../field-groups/medication/healthcare-medication.md) para describir más detalles sobre el medicamento o el medicamento.
