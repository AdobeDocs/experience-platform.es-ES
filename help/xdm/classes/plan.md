---
title: Clase de plan
description: Obtenga información acerca de la clase Plan en el Modelo de datos de experiencia (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Plan] clase

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Plan] La clase registra el conjunto mínimo de propiedades que definen un plan, como un plan de salud o un plan de seguro.

![Estructura de clase](../images/classes/plan.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `planId` | [!UICONTROL Cadena] | Un identificador único del plan. |
| `planName` | [!UICONTROL Cadena] | El nombre del plan. |

{style="table-layout:auto"}

La clase se puede ampliar con la variable [[!UICONTROL Detalles del plan de atención médica] grupo de campos](../field-groups/plan/healthcare-plan-details.md) para describir más detalles acerca de un plan de seguro de salud.
