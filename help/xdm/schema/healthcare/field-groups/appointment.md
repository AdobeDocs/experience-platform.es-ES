---
title: Grupo de campos de esquema de cita
description: Obtenga información acerca del grupo de campos Esquema de cita.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8224a2ee-51ac-4512-b0e4-5f1ab6bfddc4
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 5%

---

# [!UICONTROL Cita] grupo de campos de esquema

[!UICONTROL Cita] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../../classes/individual-profile.md) y la [[!DNL Provider class]](../../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareAppointment` que contiene información sobre la reserva de un evento de atención médica entre pacientes, profesionales, personas relacionadas y/o dispositivos para una fecha y hora específicas.

![Un diagrama de esquema de la estructura del grupo de campos de cita.](../../../images/healthcare/field-groups/appointment/appointment.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Cuenta] | `account` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | El conjunto de cuentas que se espera usar para la facturación. |
| [!UICONTROL Tipo de cita] | `appointmentType` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El estilo de cita o paciente que se ha reservado en la ranura (no el tipo de servicio). |
| [!UICONTROL Basado En] | `basedOn` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | La solicitud que se asigna a la cita para evaluar, como una solicitud de procedimiento. |
| [!UICONTROL Motivo de cancelación] | `cancellationReason` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El motivo codificado de la cancelación de la cita. Esto se utiliza a menudo en los informes, la facturación o el procesamiento para determinar si se requieren más acciones o si se aplican tarifas específicas. |
| [!UICONTROL Clase] | `class` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Conceptos que representan la clasificación de un encuentro con un paciente, como ambulatorio, ambulatorio, hospitalizado o de emergencia. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Una lista de identificadores únicos vinculados a la cita. Estos identificadores se asignan en función de reglas empresariales o cuando un vínculo URL directo a la cita no es adecuado. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL anotación]](../data-types/annotation.md) | Notas o comentarios adicionales sobre la cita. |
| [!UICONTROL Cita de origen] | `originatingAppointment` | [[!UICONTROL Referencia]](../data-types/reference.md) | La cita de origen en un conjunto recurrente de citas relacionadas. |
| [!UICONTROL Participante] | `participant` | Matriz de objetos | Una lista de los participantes involucrados en la cita. Consulte la [sección siguiente](#participant) para obtener más información. |
| [!UICONTROL Instrucción para el paciente] | `patientInstruction` | Matriz de [[!UICONTROL referencia codificable]](../data-types/reference.md) | El diagnóstico relevante para la cita. |
| [!UICONTROL Cita anterior] | `previousAppointment` | [[!UICONTROL Referencia]](../data-types/reference.md) | La cita anterior en una serie de citas relacionadas. |
| [!UICONTROL Prioridad] | `priority` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La prioridad del nombramiento que puede utilizarse para tomar decisiones informadas si es necesario volver a priorizar los nombramientos. iCal Standard especifica `0` como sin definir, `1` como prioridad más alta y `9` como prioridad más baja. |
| [!UICONTROL Motivo] | `reason` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El motivo por el que se está programando la cita, que suele ser una condición o un procedimiento. |
| [!UICONTROL Plantilla de repetición] | `recurrenceTemplate` | Matriz de objetos | Contiene los detalles del patrón de periodicidad o la plantilla utilizada para crear citas periódicas.  Consulte la [sección siguiente](#recurrence) para obtener más información. |
| [!UICONTROL Reemplaza] | `replaces` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | La cita que se está reemplazando por esta cita. En los casos en que hay una cancelación, los detalles de la cancelación se pueden encontrar en la propiedad `cancellationReason` del recurso al que se hace referencia. |
| [!UICONTROL Período solicitado] | `requestedPeriod` | Matriz de [[!UICONTROL Periodo]](../data-types/period.md) | Un conjunto de intervalos de fechas (que puede incluir horas) durante los cuales se prefiere programar la cita. |
| [!UICONTROL Categoría de servicio] | `serviceCategory` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Una amplia categorización del servicio que se va a realizar durante la cita. |
| [!UICONTROL Tipo de servicio] | `serviceType` | Matriz de [[!UICONTROL referencia codificable]](../data-types/codeable-reference.md) | El servicio específico que se va a realizar durante la cita. |
| [!UICONTROL Ranura] | `slot` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Los espacios de tiempo de los horarios de los participantes que se llenarán con la cita. |
| [!UICONTROL Especialidad] | `speciality` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | La especialidad de un profesional requerido para realizar el servicio solicitado en esta cita. |
| [!UICONTROL Asunto] | `subject` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | El paciente o grupo asociado con la cita. |
| [!UICONTROL Información de apoyo] | `supportingInformation` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Información adicional proporcionada al hacer la cita para apoyarla. |
| [!UICONTROL Servicio virtual] | `virtualService` | Matriz de [[!UICONTROL detalles de servicio virtual]](../data-types/virtual-service-detail.md) | Detalles de conexión de un servicio virtual, como una llamada de conferencia. |
| [!UICONTROL Fecha de cancelación] | `cancellationDate` | Fecha/Hora | La fecha y hora en que se canceló la cita. |
| [!UICONTROL Creado] | `created` | Fecha/Hora | La fecha y la hora de creación de la cita. |
| [!UICONTROL Descripción] | `description` | Cadena | Una breve descripción de la cita. La información detallada o expandida debe colocarse en el campo `note`. |
| [!UICONTROL Fin] | `end` | Fecha/Hora | La fecha y hora en que finaliza la cita. |
| [!UICONTROL Duración de minutos] | `minutesDuration` | Entero | El número de minutos que durará la cita. Puede ser inferior a la duración entre las horas de inicio y finalización. El valor mínimo aceptado es `0`. |
| [!UICONTROL Ocurrencia cambiada] | `occurenceChanged` | Booleano | Un indicador que indica si esta cita difiere del patrón recurrente. |
| [!UICONTROL ID de periodicidad] | `RecurrenceId` | Entero | Número de secuencia que identifica una cita específica en un patrón recurrente. El valor mínimo es `0`. |
| [!UICONTROL Start] | `start` | Fecha/Hora | La fecha y hora en que tendrá lugar la cita. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de la cita. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos: <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Un diagrama de esquema de la estructura de objetos de participante.](../../../images/healthcare/field-groups/appointment/participant.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Referencia]](../data-types/reference.md) | La persona, dispositivo, ubicación o servicio que participa en la cita. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Período de tiempo durante el cual el participante (actor) participa en la cita. |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | La función del participante (actor) en la cita. |
| [!UICONTROL Requerido] | `required` | Booleano | Si se requiere la presencia de este participante. |
| [!UICONTROL estado] | `status` | Cadena | El estado de aceptación del participante. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos: <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Un diagrama de esquema de la estructura del objeto de la plantilla de periodicidad.](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Plantilla mensual] | `monthlyTemplate` | Matriz de objetos | Información sobre citas periódicas mensuales. Consulte la [sección siguiente](#monthly-template) para obtener más información. |
| [!UICONTROL Tipo de periodicidad] | `recurrenceType` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La frecuencia con la que la serie de citas debe repetirse, como semanal, mensual o anual. |
| [!UICONTROL Zona horaria] | `timezone` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Zona horaria de la cita periódica. |
| [!UICONTROL Plantilla semanal] | `weeklyTemplate` | Matriz de objetos | Información sobre citas periódicas semanales. Consulte la [sección siguiente](#weekly-template) para obtener más información. |
| [!UICONTROL Plantilla anual] | `yearlyTemplate` | Objeto | Información sobre citas periódicas anuales. Contiene una propiedad, `yearInterval`, que contiene un valor entero que indica cada enésimo año que se repite la cita. |
| [!UICONTROL Fecha de exclusión] | `excludingDate` | Matriz de fechas | Cualquier fecha, como festivos, que deba excluirse de la periodicidad. |
| [!UICONTROL Excluyendo El Id. De Periodicidad] | `excludingRecurrenceId` | Matriz de enteros | Cualquier ID de periodicidad que deba excluirse de la periodicidad. Esta es una alternativa a `excludingDate` donde se indica el `reccurenceID` de la cita que se va a excluir. |
| [!UICONTROL Fecha de la última ocurrencia] | `lastOccurenceDate` | Fecha | La fecha después de la cual no se programarán más citas periódicas. |
| [!UICONTROL Recuento de ocurrencias] | `occurenceCount` | Entero | ¿Cuántas citas están planificadas en la periodicidad? El valor mínimo es `0`. |
| [!UICONTROL Fecha de ocurrencia] | `occurenceDate` | Matriz de fechas | Una lista de fechas específicas en las que se programan las citas. |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Un diagrama de esquema de la estructura semanal de objetos de plantilla.](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Viernes] | `friday` | Booleano | Indica que las citas periódicas deben tener lugar los viernes. |
| [!UICONTROL Lunes] | `monday` | Booleano | Indica que las citas periódicas deben tener lugar los lunes. |
| [!UICONTROL Sábado] | `saturday` | Booleano | Indica que las citas periódicas deben tener lugar los sábados. |
| [!UICONTROL Domingo] | `sunday` | Booleano | Indica que las citas periódicas deben tener lugar los domingos. |
| [!UICONTROL Jueves] | `thursday` | Booleano | Indica que las citas periódicas deben tener lugar los jueves. |
| [!UICONTROL Martes] | `tuesday` | Booleano | Indica que las citas periódicas deben tener lugar los martes. |
| [!UICONTROL Miércoles] | `wednesday` | Booleano | Indica que las citas periódicas deben tener lugar los miércoles. |
| [!UICONTROL Intervalo de semanas] | `weekInterval` | Entero | Especifica la frecuencia con la que se repiten las citas, expresada en términos de cada enésima semana. El valor predeterminado es cada semana, por lo que el valor típico es 2 o superior. |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Un diagrama de esquema de la estructura de objetos de plantilla mensual.](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Día De La Semana] | `dayOfWeek` | [[!UICONTROL Codificación]] | Indica que las citas deben tener lugar en este día específico de la semana. |
| [!UICONTROL N Semana Del Mes] | `nthWeekOfMonth` | [[!UICONTROL Codificación]](../data-types/coding.md) | Indica la enésima semana del mes en que debe repetirse la cita. |
| [!UICONTROL Día Del Mes] | `dayOfMonth` | Entero | Indica que las citas deben tener lugar en este día específico del mes. |
| [!UICONTROL Intervalo De Mes] | `monthInterval` | Entero | Indica que las citas periódicas deben tener lugar cada enésimo mes. |

