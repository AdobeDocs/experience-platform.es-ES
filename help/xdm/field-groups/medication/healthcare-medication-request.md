---
title: Grupo de campos de esquema de solicitud de medicación
description: Obtenga información sobre el grupo de campos del esquema de solicitud de medicamento.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL Solicitud de medicación] grupo de campos de esquema

[!UICONTROL Solicitud de medicación] es un grupo de campos de esquema estándar para [[!DNL Medication] class](../../classes/location.md), [[!DNL XDM Individual Profile] Class](../../classes/individual-profile.md) y [[!DNL Provider class]](../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareMedicationDispense` que captura un pedido o solicitud tanto para el suministro del medicamento como para las instrucciones para la administración del medicamento a un paciente.

![Estructura del grupo de campos](../../images/field-groups/healthcare-medication-request/medication-request.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Basado En] | `basedOn` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | El plan o solicitud que se cumple con esta solicitud de medicamento. |
| [!UICONTROL Categoría] | `category` | Matriz de [[!UICONTROL concepto codificable]](../../data-types/healthcare/codeable-concept.md) | La categorización o agrupación de la solicitud de medicación. |
| [!UICONTROL Tipo De Tratamiento] | `courseOfTherapyType` | [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) | La descripción del patrón general para la administración de la medicación al paciente. |
| [!UICONTROL Dispositivo] | `device` | Matriz de [[!UICONTROL referencia codificable]](../../data-types/healthcare/codeable-reference.md) | El tipo de dispositivo que se va a utilizar para la administración del medicamento. |
| [!UICONTROL Solicitud de dispensación] | `dispenseRequest` | Objeto | Indica los detalles específicos de la solicitud de dispensación, generalmente conocida como una solicitud de medicación. Consulte la [sección siguiente](#dispense-request) para obtener más información. |
| [!UICONTROL Instrucción de dosificación] | `dosageInstructions` | Matriz de [[!UICONTROL dosis]](../../data-types/healthcare/dosage.md) | Instrucciones específicas sobre cómo el paciente debe usar el medicamento. |
| [!UICONTROL Período de dosis efectiva] | `effectiveDosePeriod` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | Período durante el cual se debe tomar el medicamento. Cuando hay varias líneas de `dosageInstruction` (por ejemplo, al reducir dosis), esta es la fecha más temprana y la última de las instrucciones de dosificación. |
| [!UICONTROL Encuentro] | `encounter` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Encuentro durante el cual se creó la solicitud. |
| [!UICONTROL Historial de eventos] | `eventHistory` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Vínculo a registros de eventos relacionados con la solicitud de medicación, como el cumplimiento de la solicitud, momentos de transiciones de estado clave o actualizaciones relevantes. |
| [!UICONTROL Identificador de grupo] | `groupIdentifier` | [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | Un identificador compartido en varias instancias de solicitud independientes activadas por un solo autor. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../../data-types/healthcare/identifier.md) | Identificadores asociados con la solicitud de medicación que se definen mediante procesos empresariales o que se utilizan para referirse a ella cuando una referencia URL directa al propio recurso no es apropiada. |
| [!UICONTROL Información de Source] | `informationSource` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | La persona u organización que proporcionó la información para la solicitud si el origen es alguien distinto de `requester`. |
| [!UICONTROL Seguro] | `insurance` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Planes de seguro, extensiones de cobertura, preautorizaciones y/o predeterminaciones que puedan ser necesarias para prestar el servicio solicitado. |
| [!UICONTROL Medicamento] | `medication` | [[!UICONTROL Referencia codificable]](../../data-types/healthcare/codeable-reference.md) | Identifica el medicamento que se solicita. Debe ser un enlace a un recurso que represente los detalles del medicamento o un código que identifique el medicamento. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL anotación]](../../data-types/healthcare/annotation.md) | Información adicional sobre la prescripción que los demás atributos no pudieron transmitir. |
| [!UICONTROL Ejecutante] | `performer` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | El ejecutante especificado del tratamiento/administración del medicamento. Para los dispositivos, este es el dispositivo que está destinado a realizar la administración del medicamento. |
| [!UICONTROL Tipo de ejecutante] | `performerType` | [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) | Indica el tipo de ejecutante para la administración del medicamento. |
| [!UICONTROL Receta Previa] | `priorPrescription` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | La referencia a un pedido o una prescripción que se va a reemplazar con esta solicitud. |
| [!UICONTROL Motivo] | `reason` | Matriz de [[!UICONTROL referencia codificable]](../../data-types/healthcare/reference.md) | La razón o indicación para ordenar o no ordenar el medicamento. |
| [!UICONTROL Grabadora] | `recorder` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | La persona que ingresó el pedido en nombre de otra persona. |
| [!UICONTROL Solicitante] | `requester` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | La persona, organización o dispositivo que inició la solicitud y es responsable de su activación. |
| [!UICONTROL Motivo del estado] | `statusReason` | [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) | El motivo del estado actual de la solicitud. |
| [!UICONTROL Asunto] | `subject` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | La persona o grupo para el que se ha solicitado la medicación. |
| [!UICONTROL Sustitución] | `substitution` | Objeto | Indica si una sustitución puede o no formar parte de la dispensación. Contiene tres propiedades: <li>`allowedBoolean`: un valor booleano que es verdadero si el prescriptor permite una sustitución.</li> <li>`allowedCodeableConcept`: un valor de [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) que proporciona un código si el prescriptor permite una sustitución.</li> <li>`reason`: un valor de [[!UICONTROL concepto codificable]](../../data-types/healthcare/codeable-concept.md) que indica un motivo para la sustitución.</li> |
| [!UICONTROL Información de apoyo] | `supportingInformation` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Información para apoyar el cumplimiento del medicamento, como la altura y el peso del paciente. |
| [!UICONTROL Creado El] | `authoredOn` | Fecha/Hora | La fecha (y opcionalmente la hora) en que se escribió la prescripción. |
| [!UICONTROL No Realizar] | `doNotPerform` | Booleano | Un indicador booleano que es verdadero es que el paciente debe dejar (o no comenzar) a tomar el medicamento. |
| [!UICONTROL Intención] | `intent` | Cadena | La intención de la solicitud. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Prioridad] | `priority` | Cadena | La prioridad de la solicitud. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Instrucción de dosificación procesada] | `renderedDosageInstruction` | Cadena | La presentación completa de la dosis incluida en todas las instrucciones de dosificación. Para utilizar cuando se incluyen instrucciones de dosificación múltiple para representar la dosificación compleja, como el aumento o disminución de las dosis. |
| [!UICONTROL Notificado] | `reported` | Booleano | Indica si este registro se capturó como un registro de informes secundario en lugar de como un registro de origen de verdad principal original. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de dispensación. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Estado cambiado] | `statusChanged` | Fecha/Hora | La fecha (y, opcionalmente, la hora) en la que se cambió el estado de. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Estructura de solicitud de dispensación](../../images/field-groups/healthcare-medication-request/dispense-request.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Intervalo de dispensación] | `dispenseInterval` | [[!UICONTROL Duración]](../../data-types/healthcare/duration.md) | Período mínimo de tiempo que debe transcurrir entre la dispensación del medicamento. |
| [!UICONTROL Dispensador] | `dispenser` | [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | La organización a la que va a dispensar el medicamento según lo especificado por el prescriptor. |
| [!UICONTROL Instrucción del dispensador] | `dispenserInstruction` | Matriz de [[!UICONTROL anotación]](../../data-types/healthcare/annotation.md) | Información adicional para el dispensador, como el asesoramiento que debe proporcionarse al paciente |
| [!UICONTROL Ayuda de administración de dosis] | `doseAdministrationAid` | [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) | Información sobre el tipo de embalaje de adherencia que debe suministrarse para la dispensación de medicamentos. |
| [!UICONTROL Duración de suministro esperada] | `expectedSupplyDuration` | [[!UICONTROL Duración]](../../data-types/healthcare/duration.md) | El período de tiempo durante el cual se espera utilizar el producto suministrado, o el tiempo que se espera que dure la dispensación. |
| [!UICONTROL Relleno inicial] | `initialFill` | Objeto | Información para el relleno inicial. Contiene dos propiedades: <li>`quantity`: un valor de [[!UICONTROL Cantidad simple]](../../data-types/healthcare/simple-quantity.md) que proporciona la cantidad que se debe proporcionar durante la primera dispensación.</li> <li>`duration`: valor de [[!UICONTROL Duration]](../../data-types/healthcare/duration.md) que proporciona el tiempo que se espera que dure la primera dispensación.</li> |
| [!UICONTROL Cantidad] | `quantity` | [[!UICONTROL Cantidad simple]](../../data-types/healthcare/simple-quantity.md) | La cantidad que se dispensará para un relleno. |
| [!UICONTROL Período de validez] | `validityPeriod` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | Período de validez de la prescripción. |
| [!UICONTROL Número De Repeticiones Permitidas] | `numberOfRepeatsAllowed` | Entero | El número de recargas autorizadas, con un valor mínimo de 0. |
