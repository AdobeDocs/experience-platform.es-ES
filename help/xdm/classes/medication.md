---
title: Clase de medicamentos
description: Este documento proporciona una descripción general de la clase Medication en Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Medicación] class

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Medicación] La clase comprende el conjunto mínimo de propiedades que definen una sustancia utilizada para el tratamiento médico, especialmente un medicamento o medicamento.

![Estructura de la clase](../images/classes/medication.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `medicationId` | [!UICONTROL Cadena] | Un identificador único para el medicamento. |
| `medicationName` | [!UICONTROL Cadena] | El nombre del medicamento. |

{style=&quot;table-layout:auto&quot;}

La clase se puede ampliar con el [[!UICONTROL Medicación médica] grupo de campos](../field-groups/medication/healthcare-medication.md) para describir más detalles sobre el medicamento o el medicamento.
