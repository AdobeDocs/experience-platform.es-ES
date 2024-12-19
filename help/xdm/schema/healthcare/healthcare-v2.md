---
title: Modelo de datos de atención sanitaria V2
description: Obtenga información acerca de algunos casos de uso comunes de atención médica y las mejores clases, grupos de campos relacionados y tipos de datos que se deben usar.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 6d1745b93d2ad7cf6ef96510bd5128a43de9ef03
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# Modelo de datos V2 de [!UICONTROL Healthcare]

## Grupos de campos y clases {#field-groups}

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso sanitarios comunes.

| Ejemplo de uso | Grupos de campos y clases compatibles |
| --- | --- |
| **Crear/actualizar paciente**: cuando un paciente llega a la recepción del hospital, se establece un registro del paciente, que incluye detalles demográficos como un identificador (opcional), el nombre del paciente, su fecha de nacimiento, su sexo y su dirección. Esto sirve como un componente vital de la TI de la atención sanitaria. | <ul><li>**[Perfiles individuales XDM](../../classes/individual-profile.md)**:<ul><li>[Paciente](./field-groups/patient.md)</li></ul></li></ul> |
| **Vacunación**: Facilitar el proceso de vacunación, administrar los registros de inmunización de los pacientes e integrar EMRs con los sistemas de administración de vacunas. | <ul><li>**[ExperienceEvent de XDM](../../classes/experienceevent.md)**:<ul><li>[Vacunación](./field-groups/immunization.md)</li></ul></li><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Ubicación](./classes/location.md)**:<ul><li>[Ubicación](./field-groups/location.md)</li></ul><li>**[Medicamento](../../classes/medication.md)**:<ul><li>[Medicamento](./field-groups/medication.md)</li><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li></ul></li><li>**[Proveedor](../../classes/provider.md)**:<ul><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li></ul></li></ul> |
| **Cumplimiento posterior a la atención**: Motivar a los pacientes y cuidadores a completar sus planes de tratamiento y reducir las tasas de envío de dinero. | <ul><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Plan de atención](./field-groups/care-plan.md)</li><li>[Meta](./field-groups/goal.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Ubicación](./classes/location.md)**:<ul><li>[Ubicación](./field-groups/location.md)</li></ul><li>**[Proveedor](../../classes/provider.md)**:<ul><li>[Meta](./field-groups/goal.md)</li></ul></li></ul> |
| **Experiencia del consumidor con un seguro**: Mejore la adquisición digital y las experiencias de los consumidores que buscan un seguro. Algunos ejemplos son: <li> Comprender el comportamiento del consumidor para enviar correos electrónicos promocionales o anuncios de terceros segmentados a las personas que acceden a páginas que contienen información general (como planes, nombres o niveles de planes, Medicaid o programas de bienestar)</li><li> Enviar información relacionada con la vacuna sobre la salud del corazón para crear conciencia de marca o solicitudes para programar vacunas a personas que buscan información sobre la salud del corazón y la vacuna. </li> | <ul><li>**[Perfil individual de XDM](../../classes/individual-profile.md)**:<ul><li>[Cuenta](./field-groups/account.md)</li><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Ubicación](./classes/location.md)**:<ul><li>[Ubicación](./field-groups/location.md)</li></ul><li>**[Medicamento](../../classes/medication.md)**:<ul><li>[Medicamento](./field-groups/medication.md)</li><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li></ul></li><li>**[Proveedor](../../classes/provider.md)**:<ul><li>[Cuenta](./field-groups/account.md)</li><li>[Dispensación de medicamentos](./field-groups/medication-dispense.md)</li><li>[Solicitud de medicamento](./field-groups/medication-request.md)</li></ul><li>**[Plan](../../classes/plan.md)**:<ul><li>[Meta](./field-groups/coverage.md)</li></ul></li></ul> |
| **Experiencia mejorada del proveedor**: Uso de los datos del proveedor del sistema EMR para sugerir proveedores alternativos en función de la disponibilidad, la ubicación y la especialidad de la cita. <br> <br>Mejora de las búsquedas de proveedores para mostrar los resultados con la disponibilidad deseada, comprobando que el proveedor seleccionado forma parte de la red de pago y proporcionando estimaciones de costos. | <ul><li>**[Perfiles individuales XDM](../../classes/individual-profile.md)**:<ul><li>[Cita](./field-groups/appointment.md)</li><li>[Organización](./field-groups/organization.md)</li><li>[Paciente](./field-groups/patient.md)</li><li>[Profesional](./field-groups/practioner.md)</li><li>[Programación](./field-groups/schedule.md)</li></ul></li><li>**[Ubicación](./classes/location.md)**:<ul><li>[Ubicación](./field-groups/location.md)</li></ul><li>**[Proveedor](../../classes/provider.md)**:<ul><li>[Cita](./field-groups/appointment.md)</li><li>[Organización](./field-groups/organization.md)</li><li>[Profesional](./field-groups/practioner.md)</li><li>[Programación](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:fixed"}

## Tipos de datos {#data-types}

En la tabla siguiente se describen los tipos de datos creados según las especificaciones de [!DNL HL7 FHIR Release 5].

| Nombre | Descripción |
| --- | --- |
| [[!UICONTROL Dirección]](./data-types/address.md) | Describe una dirección expresada mediante convenciones postales (a diferencia de GPS u otros formatos de definición de ubicación). |
| [[!UICONTROL Anotación]](./data-types/annotation.md) | Un nodo de texto con atribución al autor. |
| [[!UICONTROL Disponibilidad]](./data-types/availability.md) | Datos de disponibilidad de un artículo. |
| [[!UICONTROL Concepto codificable]](./data-types/codeable-concept.md) | Una referencia de un recurso a otro. |
| [[!UICONTROL Referencia codificable]](./data-types/codeable-reference.md) | Una referencia a un recurso o a un concepto. |
| [[!UICONTROL Codificación]](./data-types/coding.md) | Una referencia a un código definido por un sistema terminológico. |
| [[!UICONTROL Punto de contacto]](./data-types/contact-point.md) | Datos de contacto de una persona. |
| [[!UICONTROL Dosis]](./data-types/dosage.md) | Cómo se toma o se debe tomar el medicamento. |
| [[!UICONTROL Duración]](./data-types/duration.md) | Un largo periodo de tiempo. |
| [[!UICONTROL Detalles de contacto extendidos]](./data-types/extended-contact-detail.md) | Información de un contacto extendido. |
| [[!UICONTROL Nombre humano]](./data-types/human-name.md) | Información sobre el nombre de un ser humano u otra entidad viviente. |
| [[!UICONTROL Identificador]](./data-types/identifier.md) | Un identificador pensado para el cálculo. |
| [[!UICONTROL Dinero]](./data-types/money.md) | Una cantidad de utilidad económica en alguna moneda reconocida. |
| [[!UICONTROL Período]](./data-types/period.md) | Un período de tiempo definido por una fecha/hora de inicio y de finalización. |
| [[!UICONTROL Persona]](./data-types/person.md) | Información sobre un registro de persona genérico. |
| [[!UICONTROL Cantidad]](./data-types/quantity.md) | Una cantidad medida o medible. |
| [[!UICONTROL Intervalo]](./data-types/range.md) | Conjunto de valores enlazados por valores bajos y altos. |
| [[!UICONTROL Proporción]](./data-types/ratio.md) | Una proporción de dos valores [[!UICONTROL Quantity]](./data-types/quantity.md) mediante un numerador y un denominador. |
| [[!UICONTROL Referencia]](./data-types/reference.md) | Una referencia de un recurso a otro. |
| [[!UICONTROL Repetir]](./data-types/repeat.md) | Un conjunto de reglas que describen cuándo se programa un evento. |
| [[!UICONTROL Cantidad simple]](./data-types/simple-quantity.md) | Una cantidad medida o medible. |
| [[!UICONTROL Tiempo]](./data-types/timing.md) | Información sobre un evento que puede producirse varias veces. |
| [[!UICONTROL Detalle del servicio virtual]](./data-types/virtual-service-detail.md) | Detalles de contacto del servicio virtual. |

