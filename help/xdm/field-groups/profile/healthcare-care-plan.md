---
title: Grupo de campos del esquema del plan de atención
description: Obtenga información sobre el grupo de campos Esquema de plan de atención médica.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL Grupo de campos de esquema del plan de atención]

[!UICONTROL Plan de atención] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). Proporciona un único campo de tipo de objeto `healthcareCarePlan` que captura un plan de atención médica para un paciente o grupo.

![Estructura del grupo de campos](../../images/field-groups/healthcare-care-plan/care-plan.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Actividad] | `activity` | Matriz de objetos | Identifica una acción que se ha producido o que se planea que se produzca como parte del plan. Consulte la [sección siguiente](#activity) para obtener más información. |
| [!UICONTROL Direcciones] | `addresses` | Matriz de [[!UICONTROL referencia codificable]](../../data-types/healthcare/codeable-reference.md) | Identifica las condiciones o preocupaciones que gestiona el plan de atención. |
| [!UICONTROL Basado En] | `basedOn` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Un recurso de solicitud de nivel superior que este plan de atención satisface total o parcialmente. |
| [!UICONTROL Equipo de atención] | `careTeam` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Identifica a todas las personas y organizaciones que se espera que participen en la atención prevista por este plan. |
| [!UICONTROL Categoría] | `category` | Matriz de [[!UICONTROL concepto codificable]](../../data-types/healthcare/codeable-concept.md) | Identifica qué tipo de plan es para apoyar la diferenciación entre varios planes coexistentes. |
| [!UICONTROL Colaborador] | `contributor` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Identifica a la(s) persona(s), organización o dispositivo que proporcionó el contenido del plan de atención. |
| [!UICONTROL Custodio] | `custodian` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Una vez finalizado el plan, el tutor es responsable y se le atribuye el plan de atención. |
| [!UICONTROL Encuentro] | `encounter` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Encuentro durante el cual se creó el plan de atención. |
| [!UICONTROL Meta] | `goal` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Objetivo(s) previsto(s) de ejecución del plan. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../../data-types/healthcare/identifier.md) | Los identificadores de negocio asignados a este plan de atención por el ejecutante u otros sistemas que permanecen constantes mientras el recurso se actualiza y se propaga de servidor en servidor. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL anotación]](../../data-types/healthcare/annotation.md) | Notas generales sobre el plan de atención médica no cubiertas por otros atributos. |
| [!UICONTROL Parte De] | `partOf` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | El plan de atención médica más grande en el que este plan de atención en particular es un componente o paso. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | Indica cuándo entró en vigor el plan (o cuándo está previsto que lo haga) y cuándo finaliza. |
| [!UICONTROL Reemplaza] | `replaces` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | El plan de atención médica completado o terminado cuya función es asumida por este plan de atención médica. |
| [!UICONTROL Asunto] | `subject` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Identifica al paciente o grupo cuya atención prevista está descrita por el plan. |
| [!UICONTROL Información de apoyo] | `supportingInfo` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Identifica las partes del registro del paciente que influyeron en la formación del plan. Estos pueden incluir comorbilidades, procedimientos recientes, limitaciones o evaluaciones recientes. |
| [!UICONTROL Creado] | `created` | Fecha/Hora | Representa cuándo se creó este plan de atención médica en el sistema, que a menudo es una fecha generada por el sistema. |
| [!UICONTROL Descripción] | `description` | Cadena | Una descripción del alcance y la naturaleza del plan. |
| [!UICONTROL Crea Instancias Canónicas] | `instantiatesCanonical` | Matriz de cadenas | La dirección URL que señala a un protocolo, directriz, cuestionario u otra definición definidos por FHIR a los que se adhiere total o parcialmente este plan. |
| [!UICONTROL Crea Instancias De Uri] | `instantiatesUri` | Matriz de cadenas | La URL que señala a un protocolo, directriz, cuestionario u otra definición mantenida externamente y a la que se adhiere total o parcialmente este plan, representada como URI. |
| [!UICONTROL Intención] | `intent` | Cadena | La intención del plan de atención. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Estado] | `status` | Cadena | El estado del plan de atención. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Título] | `title` | Cadena | El nombre del plan de atención. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de actividad](../../images/field-groups/healthcare-care-plan/activity.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Actividad realizada] | `performedActivity` | Matriz de [[!UICONTROL referencia codificable]](../../data-types/healthcare/codeable-reference.md) | Los resultados de la actividad, como una cita o un procedimiento. |
| [!UICONTROL Referencia de actividad planificada] | `plannedActivityReference` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Los detalles de la actividad propuesta. |
| [!UICONTROL Progreso] | `progress` | Matriz de [[!UICONTROL anotación]](../../data-types/healthcare/annotation.md) | Notas sobre la adherencia, el estado o el progreso de la actividad. |
