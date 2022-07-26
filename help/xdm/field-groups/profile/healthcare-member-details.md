---
title: Grupo de campos de esquema Detalles del Miembro de Atención de Salud
description: Este documento proporciona una visión general del grupo de campos de esquema Detalles del Miembro de Salud.
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# [!UICONTROL Detalles de los miembros del sector sanitario] grupo de campos de esquema

[!UICONTROL Detalles de los miembros del sector sanitario] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que recoge los detalles de una persona que tiene o va a recibir atención o servicios médicos, como información de contacto, médico de atención primaria e información del plan.

![Estructura del grupo de campo](../../images/field-groups/healthcare-member-details/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de facturación de la persona. |
| `faxPhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de teléfono de la persona. |
| `homeAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de casa de la persona. |
| `homePhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de teléfono de casa de la persona. |
| `mailingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección postal de la persona. |
| `memberDetails` | Objeto | Un objeto que contiene información detallada sobre los atributos y relaciones relacionados con el cuidado de la salud de la persona. Consulte la [subsección abajo](#memberDetails) para obtener más información sobre la estructura del objeto. |
| `mobilePhone` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de teléfono móvil de la persona. |
| `person` | [[!UICONTROL Persona]](../../data-types/person.md) | Un actor individual, contacto o propietario relacionado con la membresía de salud de la persona. |
| `personalEmail` | [[!UICONTROL Dirección de correo electrónico]](../../data-types/email-address.md) | La dirección de correo electrónico personal de la persona. |
| `shippingAddress` | [[!UICONTROL Dirección postal]](../../data-types/postal-address.md) | La dirección de envío de la persona. |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` es un objeto que contiene información detallada sobre los atributos y relaciones relacionados con el cuidado de la salud de la persona. La estructura de `memberDetails` se describe a continuación.

![estructura memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `emergencyContact` | Objeto | Captura los siguientes detalles de contacto de emergencia para la persona: <ul><li>`fullName`: (Cadena) El nombre completo del contacto de emergencia.</li><li>`phone`: (Cadena) El número de teléfono del contacto de emergencia.</li><li>`relationshipToMember`: (Cadena) La relación del contacto de emergencia con la persona.</li></ul> |
| `medications` | Matriz de objetos | Enumera los detalles de los medicamentos actuales y pasados asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`refillLocation`: ([[!UICONTROL Dirección postal]](../../data-types/postal-address.md)) El lugar de reposición del medicamento.</li><li>`ID`: (Cadena) ID de medicamentos.</li><li>`isCurrent`: (Booleano) Indica si la medicación es actual o pasada.</li><li>`numberOfRefills`: (Número entero) El número de recargas prescritas por el proveedor de esta medicación.</li><li>`startDate`: (DateTime) La fecha en la que la persona comenzó a tomar el medicamento.</li></ul> |
| `multipleBirth` | Objeto | Captura detalles relacionados con nacimientos múltiples: <ul><li>`isMultipleBirth`: (Booleano) Indica si la persona dio varios nacimientos.</li><li>`multipleBirthNumber`: (Número entero) El número de bebés nacidos si `isMultipleBirth` es verdadero.</li></ul> |
| `plans` | Matriz de objetos | Enumera los detalles de planes médicos actuales y pasados asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`coverageEndDate`: (DateTime) La fecha en la que finaliza la cobertura del plan.</li><li>`coverageStartDate`: (DateTime) La fecha en la que comienza la cobertura del plan.</li><li>`isActive`: (Booleano) Indica si el plan está activo.</li><li>`planId`: (Cadena) El ID del plan.</li></ul> |
| `primaryCarePhysicians` | Matriz de objetos | Enumera los detalles de los médicos de atención primaria asociados con la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`endDate`: (DateTime) La fecha en la que el médico primario terminó la atención para la persona.</li><li>`fullname`: (Cadena) El nombre completo del médico.</li><li>`providerId`: (Cadena) Identificador único del médico.</li><li>`startDate`: (DateTime) La fecha en la que el médico primario inició la atención para la persona.</li></ul> |
| `specialists` | Matriz de objetos | Enumera los detalles de los especialistas sanitarios asociados a la persona. Cada elemento de matriz es un objeto que captura los siguientes detalles: <ul><li>`fullname`: (Cadena) El nombre completo del especialista.</li><li>`providerId`: (Cadena) Identificador único del especialista.</li><li>`specialty`: (Cadena) La especialidad del proveedor (como anestesiología, urología, radiología, dermatología, etc.).</li></ul> |
| `beneficiaryRelationship` | Cadena | La relación beneficiaria con el miembro de la atención de salud si la persona es dependiente (por ejemplo, usted mismo, cónyuge, hijo, etc.). |
| `billingAccountID` | Cadena | Identificador único de la cuenta de facturación de la persona. |
| `dateAgeCollected` | DateTime | La fecha en que se recopiló la edad de la persona. |
| `deceasedDate` | DateTime | La fecha en que la persona murió si falleció. |
| `isDeceased` | Booleano | Indica si la persona ha fallecido. |
| `isDependent` | Booleano | Indica si la persona es dependiente. |
| `nationality` | Cadena | La relación jurídica entre la persona y su estado, representada utilizando el código ISO 3166-1 Alpha-2. |
| `preferredAvailability` | Cadena | El día y la hora preferidos de la persona para una cita. |
| `primaryMemberID` | Cadena | Identificador único del suscriptor principal si la persona es dependiente. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Consulte la documentación del esquema del sector para obtener más información sobre cómo se puede utilizar este grupo de campos para servir [casos de uso del sector sanitario](../../schema/industries/healthcare.md).
