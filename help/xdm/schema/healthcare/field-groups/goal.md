---
title: Grupo de campos de esquema de objetivo
description: Obtenga información acerca del grupo de campos Esquema de objetivo.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# [!UICONTROL Objetivo] grupo de campos de esquema

[!UICONTROL Goal] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] class](../../../classes/individual-profile.md) y [[!DNL Provider class]](../../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareGoal` que describe los objetivos deseados para la atención de un paciente, un grupo o una organización.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/goal/goal.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Estado de logro] | `achievementStatus` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Describe la progresión, o la falta de la misma, hacia el objetivo frente al objetivo. |
| [!UICONTROL Direcciones] | `addresses` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Las condiciones y otros elementos de registro de salud que se pretende abordar con el objetivo. |
| [!UICONTROL Categoría] | `category` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Indica una categoría dentro de la que se encuentra el objetivo, como la dieta o la conducta. |
| [!UICONTROL Descripción] | `description` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código o texto que describe el objetivo. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Los identificadores de negocio asignados a este objetivo por el ejecutante u otros sistemas que permanecen constantes mientras el recurso se actualiza y se propaga de servidor en servidor. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL anotación]](../data-types/annotation.md) | Comentarios sobre el objetivo. |
| [!UICONTROL Resultado] | `outcome` | Matriz de [[!UICONTROL referencia codificable]](../data-types/codeable-reference.md) | Identifica el cambio (o la falta de cambio) cuando se evalúa el estado del objetivo. |
| [!UICONTROL Prioridad] | `priority` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Identifica el nivel de importancia mutuamente acordado asociado con el logro o el mantenimiento del objetivo. |
| [!UICONTROL Source] | `source` | [[!UICONTROL Referencia]](../data-types/reference.md) | Indica el origen de la meta, como el paciente o el profesional. |
| [!UICONTROL Iniciar concepto codificable] | `startCodeableConcept` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Evento tras el cual se debe persuadir al objetivo. |
| [!UICONTROL Asunto |]`subject` | [[!UICONTROL Referencia]](../data-types/reference.md) | Identifica al paciente, grupo u organización para el que se establece el objetivo. |
| [!UICONTROL Target] | `target` | Matriz de objetos | Indica la cronología de pasos específicos del objetivo. Consulte la [sección siguiente](#target) para obtener más información. |
| [!UICONTROL Continuo] | `continous` | Booleano | Indica si después de cumplir el objetivo se necesita la actividad en curso para mantenerlo. |
| [!UICONTROL Estado del ciclo vital] | `lifecycleStatus` | Cadena | El estado del ciclo de vida de la meta. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Fecha de inicio] | `startDate` | Fecha | La fecha después de la cual debe comenzar a perseguirse el objetivo. |
| [!UICONTROL Fecha de estado] | `statusDate` | Fecha | Identifica cuándo se creó el estado. |
| [!UICONTROL Motivo del estado] | `statusReason` | Cadena | Registra el motivo del estado actual. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de destino](../../../images/healthcare/field-groups/goal/target.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Concepto codificable con detalles] | `detailCodeableConcept` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código de objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Cantidad detallada] | `detailQuantity` | [[!UICONTROL Cantidad]](../data-types/quantity.md) | Cantidad objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Intervalo de detalle] | `detailRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | Rango objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Proporción de detalles] | `detailRatio` | [[!UICONTROL Proporción]](../data-types/ratio.md) | La proporción objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Medida] | `measure` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El parámetro cuyo valor se está rastreando. |
| [!UICONTROL Booleano de detalle] | `detailBoolean` | Booleano | Indica el cumplimiento del objetivo. |
| [!UICONTROL Número entero detallado] | `detailInteger` | Entero | Número de objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Cadena de detalle] | `detailString` | Cadena | Valor objetivo que debe alcanzarse para indicar el cumplimiento del objetivo. |
| [!UICONTROL Fecha de vencimiento] | `dueDate` | Fecha | La fecha en la que debe cumplirse el objetivo. |
