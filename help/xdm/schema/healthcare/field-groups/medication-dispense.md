---
title: Grupo de campos del esquema de dispensación de medicación
description: Obtenga información sobre el grupo de campos Esquema de dispensación de medicamentos.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# [!UICONTROL Dispensación de medicamentos] grupo de campos de esquema

[!UICONTROL Medication Dispense] es un grupo de campos de esquema estándar para [[!DNL Medication] class](../../../classes/medication.md), [[!DNL XDM Individual Profile] Class](../../../classes/individual-profile.md) y [[!DNL Provider class]](../../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareMedicationDispense` que captura información sobre un medicamento que se va a administrar o que se ha administrado a una persona o paciente determinados.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Autorizar la prescripción] | `authorizingPrescription` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | El pedido que permite dispensar la prescripción. |
| [!UICONTROL Basado En] | `basedOn` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | El plan de dispensación del medicamento se basa en. |
| [!UICONTROL Categoría] | `category` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | La categoría en la que se dispensa el medicamento, como la categoría legal del medicamento o la clasificación del medicamento. |
| [!UICONTROL Días de suministro] | `daysSupply` | [[!UICONTROL Cantidad simple]](../data-types/simple-quantity.md) | El número de días que el medicamento suministrará al paciente. |
| [!UICONTROL Destino] | `destination` | [[!UICONTROL Referencia]](../data-types/reference.md) | La instalación o ubicación donde se envió o se enviará el medicamento, como parte del evento de dispensación. |
| [!UICONTROL Instrucción de dosificación] | `dosageInstruction` | Matriz de [[!UICONTROL dosis]](../data-types/dosage.md) | Describe cómo el paciente debe usar el medicamento. |
| [!UICONTROL Encuentro] | `encounter` | [[!UICONTROL Referencia]](../data-types/reference.md) | El encuentro que establece el contexto para este evento. |
| [!UICONTROL Historial de eventos] | `eventHistory` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Resumen de los eventos que ocurrieron en torno a la dispensación. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Identificadores asociados con la dispensación. Los procesos empresariales deben definir los identificadores o utilizarlos para hacer referencia a ellos cuando una referencia URL directa no sea adecuada. |
| [!UICONTROL Ubicación] | `location` | [[!UICONTROL Referencia]](../data-types/reference.md) | El lugar físico principal donde se dispensó el medicamento. |
| [!UICONTROL Medicamento] | `medication` | [[!UICONTROL Referencia codificable]](../data-types/codeable-reference.md) | Identifica el medicamento que se solicita. Debe ser un enlace a un recurso que represente los detalles del medicamento o un código que identifique el medicamento. |
| [!UICONTROL Motivo de no ejecución] | `notPerformedReason` | [[!UICONTROL Referencia codificable]](../data-types/codeable-reference.md) | La razón por la que no se dispensó el medicamento. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL anotación]](../data-types/annotation.md) | Información adicional sobre la dispensación. |
| [!UICONTROL Parte De] | `partOf` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | El procedimiento o la solicitud de medicación que activó la dispensación. |
| [!UICONTROL Ejecutante] | `performer` | Matriz de objetos | Indica quién o qué realizó el evento de dispensación. Consulte la [sección siguiente](#performer) para obtener más información. |
| [!UICONTROL Cantidad] | `quantity` | [[!UICONTROL Cantidad simple]](../data-types/simple-quantity.md) | La cantidad de medicamento que se ha dispensado, incluida la unidad de medida. |
| [!UICONTROL Receptor] | `receiver` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Identifica a la persona que tomó el medicamento o la ubicación de donde se lo entregaron. |
| [!UICONTROL Asunto] | `subject` | [[!UICONTROL Referencia]](../data-types/reference.md) | Un vínculo a un recurso que representa a la persona o grupo al que se administrará el medicamento. |
| [!UICONTROL Sustitución] | `substitution` | Objeto | Indica si se realizó o no la sustitución como parte de la dispensación. Contiene cuatro propiedades: <li>`wasSubstituted`: un valor booleano que es verdadero si el dispensador solicitó una sustitución.</li> <li>`type`: un valor de [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) que proporciona un código que indica si se realizó una sustitución.</li> <li>`reason`: matriz de [[!UICONTROL valores de concepto codificable]](../data-types/codeable-concept.md) que contiene los motivos de la sustitución.</li> <li>`responsibleParty`: un valor [[!UICONTROL Reference]](../data-types/reference.md) que proporciona la persona o la parte responsable de la sustitución. </li> |
| [!UICONTROL Información de apoyo] | `supportingInformation` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Información adicional que avala la administración del medicamento. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Describe el tipo de evento de dispensación que se realiza, como un llenado de emergencia o parcial. |
| [!UICONTROL Grabado] | `recorded` | Fecha/Hora | La fecha y la hora en que se inició la actividad de dispensación si `whenPrepared` o `whenHandedOver` no se ha rellenado. |
| [!UICONTROL Instrucción de dosificación procesada] | `renderedDosageInstruction` | Cadena | La presentación completa de la dosis incluida en todas las instrucciones de dosificación. Para utilizar cuando se incluyen instrucciones de dosificación múltiple para representar la dosificación compleja, como el aumento o disminución de las dosis. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de dispensación. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Estado cambiado] | `statusChanged` | Fecha/Hora | La fecha y hora en que cambió el estado del registro de dispensación. |
| [!UICONTROL Al Entregar] | `whenHandedOver` | Fecha/Hora | La fecha y hora en que se le proporcionó el medicamento dispensado al paciente. |
| [!UICONTROL Al Prepararse] | `whenPrepared` | Fecha/Hora | La fecha y hora en que se empaquetó y revisó el medicamento dispensado. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura del ejecutante](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Referencia]](../data-types/reference.md) | El profesional (o similar) que realizó la acción. Debe asumirse que el actor es el dispensador del medicamento. |
| [!UICONTROL Función] | `function` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El tipo de ejecutante en la dispensación, como el ingresador de fecha, el empaquetador o el comprobador final. |
