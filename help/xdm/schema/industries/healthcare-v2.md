---
title: Modelo de datos de atención sanitaria V2
description: Obtenga información acerca de algunos casos de uso comunes de atención médica y las mejores clases, grupos de campos relacionados y tipos de datos que se deben usar.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 872dfce238bfed9bb3eccc0b4589d418db76d1d4
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 12%

---

# Modelo de datos V2 de [!UICONTROL Healthcare]

## Grupos de campos y clases {#field-groups}

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso sanitarios comunes.

<table>
  <thead>
    <tr>
      <th>Casos de uso</th>
      <th>Grupos de campo</th>
      <th>Clases compatibles</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Crear/actualizar paciente</strong>: cuando un paciente llega a la recepción del hospital, se establece un registro del paciente, que incluye detalles demográficos como un identificador (opcional), el nombre del paciente, su fecha de nacimiento, su sexo y su dirección. Esto sirve como un componente vital de la TI de la atención sanitaria.</td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vacunación</strong>: Facilitar el proceso de vacunación, administrar los registros de inmunización de los pacientes e integrar EMRs con los sistemas de administración de vacunas.</td>
      <td><a href="../../field-groups/event/healthcare-immunization.md">Inmunización</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">Evento de experiencia XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Ubicación</a></td>
      <td>
        <li><a href="../../classes/location.md">Ubicación</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-v2.md">Medicación</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-dispense.md">Dispensación de medicamentos</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-request.md">Solicitud de medicamento</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Cumplimiento posterior a la atención</strong>: Motivar a los pacientes y cuidadores a completar sus planes de tratamiento y reducir las tasas de envío de dinero.</td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Ubicación</a></td>
      <td>
        <li><a href="../../classes/location.md">Ubicación</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-care-plan.md">Plan de atención</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-goal.md">Meta</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Experiencia del consumidor con un seguro</strong>: Mejore la adquisición digital y las experiencias de los consumidores que buscan un seguro. Algunos ejemplos son: 
        <li> Comprender el comportamiento del consumidor para enviar correos electrónicos promocionales o anuncios de terceros segmentados a las personas que acceden a páginas que contienen información general (como planes, nombres o niveles de planes, Medicaid o programas de bienestar)
        </li> 
        <li> Enviar información relacionada con la vacuna sobre la salud del corazón para crear conciencia de marca o solicitudes para programar vacunas a personas que buscan información sobre la salud del corazón y la vacuna.
        </li>
      </td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/plan/healthcare-coverage.md">Cobertura</a></td>
      <td>
        <li><a href="../../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-account.md">Cuenta</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Ubicación</a></td>
      <td>
        <li><a href="../../classes/location.md">Ubicación</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-v2.md">Medicación</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-dispense.md">Dispensación de medicamentos</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-request.md">Solicitud de medicamento</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicación</a></li>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Experiencia mejorada del proveedor</strong>: Uso de los datos del proveedor del sistema EMR para sugerir proveedores alternativos en función de la disponibilidad, la ubicación y la especialidad de la cita. <br> <br>Mejora de las búsquedas de proveedores para mostrar los resultados con la disponibilidad deseada, comprobando que el proveedor seleccionado forma parte de la red de pagadores y proporcionando estimaciones de costos.
      </td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Ubicación</a></td>
      <td>
        <li><a href="../../classes/location.md">Ubicación</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-organization.md">Organización</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-practioner.md">Profesional</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-schedule.md">Programación</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Perfil individual de XDM</a></li>
        <li><a href="../../classes/provider.md">Proveedor</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Tipos de datos {#data-types}

En la tabla siguiente se describen los tipos de datos creados según las especificaciones de [!DNL HL7 FHIR Release 5].

| Nombre | Descripción |
| --- | --- |
| [[!UICONTROL Dirección]](../../data-types/healthcare/address.md) | Describe una dirección expresada mediante convenciones postales (a diferencia de GPS u otros formatos de definición de ubicación). |
| [[!UICONTROL Anotación]](../../data-types/healthcare/annotation.md) | Un nodo de texto con atribución al autor. |
| [[!UICONTROL Disponibilidad]](../../data-types/healthcare/availability.md) | Datos de disponibilidad de un artículo. |
| [[!UICONTROL Concepto codificable]](../../data-types/healthcare/codeable-concept.md) | Una referencia de un recurso a otro. |
| [[!UICONTROL Referencia codificable]](../../data-types/healthcare/codeable-reference.md) | Una referencia a un recurso o a un concepto. |
| [[!UICONTROL Codificación]](../../data-types/healthcare/coding.md) | Una referencia a un código definido por un sistema terminológico. |
| [[!UICONTROL Punto de contacto]](../../data-types/healthcare/contact-point.md) | Datos de contacto de una persona. |
| [[!UICONTROL Dosis]](../../data-types/healthcare/dosage.md) | Cómo se toma o se debe tomar el medicamento. |
| [[!UICONTROL Duración]](../../data-types/healthcare/duration.md) | Un largo periodo de tiempo. |
| [[!UICONTROL Detalles de contacto extendidos]](../../data-types/healthcare/extended-contact-detail.md) | Información de un contacto extendido. |
| [[!UICONTROL Nombre humano]](../../data-types/healthcare/human-name.md) | Información sobre el nombre de un ser humano u otra entidad viviente. |
| [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | Un identificador pensado para el cálculo. |
| [[!UICONTROL Dinero]](../../data-types/healthcare/money.md) | Una cantidad de utilidad económica en alguna moneda reconocida. |
| [[!UICONTROL Período]](../../data-types/healthcare/period.md) | Un período de tiempo definido por una fecha/hora de inicio y de finalización. |
| [[!UICONTROL Persona]](../../data-types/healthcare/person.md) | Información sobre un registro de persona genérico. |
| [[!UICONTROL Cantidad]](../../data-types/healthcare/quantity.md) | Una cantidad medida o medible. |
| [[!UICONTROL Intervalo]](../../data-types/healthcare/range.md) | Conjunto de valores enlazados por valores bajos y altos. |
| [[!UICONTROL Proporción]](../../data-types/healthcare/ratio.md) | Una proporción de dos valores [[!UICONTROL Quantity]](../../data-types/healthcare/quantity.md) mediante un numerador y un denominador. |
| [[!UICONTROL Referencia]](../../data-types/healthcare/reference.md) | Una referencia de un recurso a otro. |
| [[!UICONTROL Repetir]](../../data-types/healthcare/repeat.md) | Un conjunto de reglas que describen cuándo se programa un evento. |
| [[!UICONTROL Cantidad simple]](../../data-types/healthcare/simple-quantity.md) | Una cantidad medida o medible. |
| [[!UICONTROL Tiempo]](../../data-types/healthcare/timing.md) | Información sobre un evento que puede producirse varias veces. |
| [[!UICONTROL Detalle del servicio virtual]](../../data-types/healthcare/virtual-service-detail.md) | Detalles de contacto del servicio virtual. |
