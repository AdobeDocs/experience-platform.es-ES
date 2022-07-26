---
title: Grupo de campos de esquema Detalles del plan de atención médica
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del plan de salud.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# [!UICONTROL Detalles del plan de atención médica] grupo de campos de esquema

[!UICONTROL Detalles del plan de atención médica] es un grupo de campos de esquema estándar para la variable [[!UICONTROL Plan] class](../../classes/plan.md). Proporciona un único campo de tipo de objeto `healthcarePlanDetails` que captura propiedades relacionadas con un plan médico.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `networkDetails` | Matriz de objetos | Enumera los detalles de la red o redes definidas por el asegurador de proveedores a los que el beneficiario puede solicitar tratamiento y se cubrirá a la tasa &quot;en red&quot;. Cada objeto incluye las siguientes propiedades: <ul><li>`networkID`: (Cadena) El ID específico del asegurador para la red.</li><li>`networkName`: (Cadena) El nombre específico del asegurador para la red.</li></ul> |
| `affiliations` | Matriz de cadenas | Una lista de entidades comerciales afiliadas al plan. |
| `coverageType` | Cadena | El tipo de cobertura del plan. Los valores aceptados son:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booleano | Indica si el plan está activo. |
| `lastVerificationDate` | DateTime | Fecha en la que se verificó por última vez el plan. |
| `payerID` | Cadena | Identificador único del ordenante (es decir, el proveedor de seguros del plan). |
| `planLevel` | Cadena | Indica el nivel del plan. Los valores aceptados son:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Cadena | Indica el tipo de plan. Los valores aceptados son:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Cadena | El tipo de propietario para el que es un plan. Algunos ejemplos son individual, grupo, organización, etc. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
