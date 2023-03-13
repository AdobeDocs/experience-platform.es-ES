---
title: Clase de medicamento
description: Este documento proporciona información general sobre la clase de medicamentos en el Modelo de datos de experiencia (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL Medicación] clase

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Medicación] Esta clase registra el conjunto mínimo de propiedades que definen una sustancia utilizada para el tratamiento médico, especialmente un medicamento o un fármaco.

![Estructura de clase](../images/classes/medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `medicationId` | [!UICONTROL Cadena] | Un identificador único del medicamento. |
| `medicationName` | [!UICONTROL Cadena] | El nombre del medicamento. |

{style="table-layout:auto"}

La clase se puede ampliar con la variable [[!UICONTROL Medicación sanitaria] grupo de campos](../field-groups/medication/healthcare-medication.md) para obtener más información sobre el medicamento o fármaco.
