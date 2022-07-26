---
title: Clase Plan
description: Este documento proporciona una descripción general de la clase Plan en Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL Plan] class

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Plan] captura el conjunto mínimo de propiedades que definen un plan, como un plan de salud o de seguro.

![Estructura de la clase](../images/classes/plan.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `planId` | [!UICONTROL Cadena] | Identificador único del plan. |
| `planName` | [!UICONTROL Cadena] | El nombre del plan. |

{style=&quot;table-layout:auto&quot;}

La clase se puede ampliar con el [[!UICONTROL Detalles del plan de atención médica] grupo de campos](../field-groups/plan/healthcare-plan-details.md) para describir más detalles sobre un plan de seguro médico.
