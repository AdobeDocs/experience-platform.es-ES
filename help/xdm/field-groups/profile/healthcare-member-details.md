---
title: Grupo de campos de esquema de detalles de miembros de atención sanitaria
description: Este documento proporciona información general sobre el grupo de campos Esquema de detalles del miembro de atención médica.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# [!UICONTROL Detalles del miembro de atención médica] grupo de campos de esquema

[!UICONTROL Detalles del miembro de atención médica] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que registra los detalles de una persona que tiene o recibirá servicio o atención médica, como información de contacto, médico de atención primaria e información del plan.

![Estructura del grupo de campos](../../images/field-groups/healthcare-member-details/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de facturación de la persona. |
| `faxPhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | Número de teléfono del fax de la persona. |
| `homeAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de la persona. |
| `homePhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de teléfono de la casa de la persona. |
| `mailingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de correo de la persona. |
| `memberDetails` | Objeto | Un objeto que contiene información detallada sobre los atributos y relaciones relacionados con la atención médica de la persona. Consulte la [subsección siguiente](#memberDetails) para obtener más información sobre la estructura del objeto. |
| `mobilePhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | Número de teléfono móvil de la persona. |
| `person` | [[!UICONTROL Persona]](../../data-types/person.md) | Un actor, contacto o propietario individual relacionado con la pertenencia a la atención médica de la persona. |
| `personalEmail` | [[!UICONTROL Correo electrónico]](../../data-types/email-address.md) | La dirección de correo electrónico personal de la persona. |
| `shippingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de envío de la persona. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` es un objeto que contiene información detallada sobre los atributos y relaciones de la persona relacionados con la atención médica. La estructura de `memberDetails` se describe a continuación.

![estructura memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `emergencyContact` | Objeto | Registra los siguientes datos de contacto de emergencia de la persona: <ul><li>`fullName`: (cadena) nombre completo del contacto de emergencia.</li><li>`phone`: (Cadena) Número de teléfono del contacto de emergencia.</li><li>`relationshipToMember`: (Cadena) La relación del contacto de emergencia con la persona.</li></ul> |
| `medications` | Matriz de objetos | Enumera los detalles de los medicamentos actuales y pasados asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`refillLocation`: ([[!UICONTROL Dirección postal]](../../data-types/postal-address.md)La ubicación de llenado de la medicación.</li><li>`ID`: ID de medicamento (cadena).</li><li>`isCurrent`: (booleano) indica si el medicamento es actual o anterior.</li><li>`numberOfRefills`: (Entero) El número de recargas recetadas por el proveedor de este medicamento.</li><li>`startDate`: (DateTime) La fecha en la que la persona comenzó a tomar el medicamento.</li></ul> |
| `multipleBirth` | Objeto | Registra detalles relacionados con nacimientos múltiples: <ul><li>`isMultipleBirth`: (Booleano) Indica si la persona dio a luz a varios hijos.</li><li>`multipleBirthNumber`: (entero) El número de bebés nacidos si `isMultipleBirth` es verdadero.</li></ul> |
| `plans` | Matriz de objetos | Enumera los detalles de los planes médicos actuales y pasados asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`coverageEndDate`: (DateTime) Fecha en la que finaliza la cobertura del plan.</li><li>`coverageStartDate`: (DateTime) Fecha en la que comienza la cobertura del plan.</li><li>`isActive`: (Booleano) Indica si el plan está activo.</li><li>`planId`: (Cadena) El ID del plan.</li></ul> |
| `primaryCarePhysicians` | Matriz de objetos | Enumera los detalles de los médicos de atención primaria asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`endDate`: (DateTime) La fecha en la que el médico de atención primaria finalizó la atención de la persona.</li><li>`fullname`: (cadena) nombre completo del médico.</li><li>`providerId`: (cadena) identificador único del médico.</li><li>`startDate`: (DateTime) La fecha en la que el médico de atención primaria comenzó a cuidar a la persona.</li></ul> |
| `specialists` | Matriz de objetos | Enumera los detalles de los especialistas en atención médica asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`fullname`: (Cadena) Nombre completo del especialista.</li><li>`providerId`: (cadena) identificador único del especialista.</li><li>`specialty`: (cadena) la especialidad del proveedor (como anestesiología, urología, radiología, dermatología, etc.).</li></ul> |
| `beneficiaryRelationship` | Cadena | La relación del beneficiario con el miembro de la atención médica si la persona es dependiente (por ejemplo, si es usted mismo, su cónyuge, su hijo, etc.). |
| `billingAccountID` | Cadena | Un identificador único de la cuenta de facturación de la persona. |
| `dateAgeCollected` | DateTime | La fecha en la que se recopiló la edad de la persona. |
| `deceasedDate` | DateTime | La fecha en la que la persona falleció si ha fallecido. |
| `isDeceased` | Booleano | Indica si la persona ha fallecido. |
| `isDependent` | Booleano | Indica si la persona es dependiente. |
| `nationality` | Cadena | La relación jurídica entre la persona y su estado, representada mediante el código ISO 3166-1 Alpha-2. |
| `preferredAvailability` | Cadena | La disponibilidad de día y hora preferida de la persona para una cita. |
| `primaryMemberID` | Cadena | Un identificador único del suscriptor principal si la persona es dependiente. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Consulte la documentación del esquema del sector para obtener más información sobre cómo se puede utilizar este grupo de campos para ofrecer servicios comunes [casos prácticos de la industria sanitaria](../../schema/industries/healthcare.md).
