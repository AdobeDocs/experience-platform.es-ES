---
title: Grupo de campos de esquema de detalles de persona de negocio XDM
description: Obtenga información acerca del grupo de campos de esquema Detalles de persona de negocio de XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# [!UICONTROL Detalles de persona de negocios de XDM] grupo de campos de esquema

[!UICONTROL Detalles de persona de negocios de XDM] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que captura información sobre una persona individual en el contexto de una empresa de empresa a empresa (B2B).

![](../../images/field-groups/business-person-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `b2b` | Objeto | Un objeto que captura los detalles específicos de B2B sobre la persona. |
| `b2b.accountKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la cuenta empresarial relacionada con la persona. |
| `b2b.convertedContactKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para el contacto asociado si se convirtió el posible cliente. |
| `b2b.personKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la persona o el fragmento de perfil. |
| `b2b.accountID` | Cadena | Un ID único para la cuenta comercial a la que está asociada esta persona. |
| `b2b.blockedCause` | Cadena | Si la persona está bloqueada, esta propiedad proporciona el motivo por el que. |
| `b2b.convertedContactID` | Cadena | ID de contacto si el posible cliente se convirtió correctamente. |
| `b2b.convertedDate` | DateTime | La fecha de conversión si el posible cliente se convirtió correctamente. |
| `b2b.isBlocked` | Booleano | Indica si la persona está bloqueada. |
| `b2b.isConverted` | Booleano | Indica si el posible cliente se ha convertido. |
| `b2b.isMarketingSuspended` | Booleano | Indica si el marketing está suspendido para la persona. |
| `b2b.marketingSuspendedCause` | Cadena | Si el marketing está suspendido para la persona, esta propiedad proporciona el motivo por el que. |
| `b2b.personGroupID` | Cadena | Un identificador de grupo de la persona. |
| `b2b.personScore` | Doble | Una puntuación generada para la persona por un sistema CRM. |
| `b2b.personSource` | Cadena | Origen del que se recibió la información de la persona. |
| `b2b.personStatus` | Cadena | El estado actual de marketing o ventas de la persona. |
| `b2b.personType` | Cadena | El tipo de persona B2B. |
| `extSourceSystemAudit` | [Atributos de auditoría del sistema de origen externo](../../data-types/external-source-system-audit-attributes.md) | Si la relación de persona de negocios proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `extendedWorkDetails` | Objeto | Registra detalles adicionales relacionados con el trabajo de la persona. |
| `extendedWorkDetails.assistantDetails` | Objeto | Registra los siguientes atributos relacionados con el asistente de la persona: <ul><li>`name`: ([Nombre de persona](../../data-types/person-name.md)) El nombre completo del asistente.</li><li>`phone`: ([Número de teléfono](../../data-types/phone-number.md)) El número de teléfono del asistente.</li></ul> |
| `extendedWorkDetails.departments` | Matriz de cadenas | Lista de nombres de departamento donde trabaja la persona. |
| `extendedWorkDetails.jobTitle` | Cadena | El puesto que ocupa la persona. |
| `extendedWorkDetails.photoUrl` | Cadena | Dirección URL de una foto de la persona. |
| `extendedWorkDetails.reportsToID` | Cadena | Un identificador del administrador de informes de la persona. |
| `faxPhone` | [Número de teléfono](../../data-types/phone-number.md) | Número de teléfono del fax de la persona. |
| `homeAddress` | [Dirección postal](../../data-types/postal-address.md) | La dirección de la persona. |
| `homePhone` | [Número de teléfono](../../data-types/phone-number.md) | El número de teléfono de la casa de la persona. |
| `mobilePhone` | [Número de teléfono](../../data-types/phone-number.md) | Número de teléfono móvil de la persona. |
| `otherAddress` | [Dirección postal](../../data-types/postal-address.md) | Una dirección alternativa para la persona. |
| `otherPhone` | [Número de teléfono](../../data-types/phone-number.md) | Un número de teléfono alternativo para la persona. |
| `person` | [Persona](../../data-types/person.md) | Un actor, contacto o propietario individual. |
| `personalEmail` | [Correo electrónico](../../data-types/email-address.md) | La dirección de correo electrónico personal de la persona. |
| `workAddress` | [Dirección postal](../../data-types/postal-address.md) | La dirección de trabajo de la persona. |
| `workEmail` | [Correo electrónico](../../data-types/email-address.md) | La dirección de correo electrónico de trabajo de la persona. |
| `workPhone` | [Número de teléfono](../../data-types/phone-number.md) | Número de teléfono del trabajo de la persona. |
| `identityMap` | Mapa | Campo de asignación que contiene un conjunto de identidades con espacio de nombres para la persona. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../../profile/home.md), no intente actualizar manualmente el contenido del campo en las operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en la [conceptos básicos de composición de esquemas](../../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `isDeleted` | Booleano | Indica si esta persona se ha eliminado en el Marketo Engage.<br><br>Al usar el [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md)Sin embargo, cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Por configuración `isDeleted` hasta `true`Sin embargo, puede utilizar el campo para filtrar qué registros se han eliminado de las fuentes al consultar el lago de datos. |
| `organizations` | Matriz de cadenas | Una lista de nombres de organizaciones donde trabaja la persona. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
