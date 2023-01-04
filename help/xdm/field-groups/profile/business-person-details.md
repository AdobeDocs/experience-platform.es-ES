---
title: Detalles de persona comercial XDM Grupo de campos de esquema
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de persona empresarial XDM.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 5%

---

# [!UICONTROL Detalles de persona comercial XDM] grupo de campos de esquema

[!UICONTROL Detalles de persona comercial XDM] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que captura información sobre una persona en el contexto de una empresa de empresa a empresa (B2B).

![](../../images/field-groups/business-person-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `b2b` | Objeto | Un objeto que captura los detalles específicos de B2B sobre la persona. |
| `b2b.accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la cuenta comercial relacionada con la persona. |
| `b2b.convertedContactKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto del contacto asociado si se convirtió el posible cliente. |
| `b2b.personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona o del fragmento de perfil. |
| `b2b.accountID` | Cadena | Un ID único para la cuenta comercial a la que está asociada esta persona. |
| `b2b.blockedCause` | Cadena | Si la persona está bloqueada, esta propiedad proporciona el motivo. |
| `b2b.convertedContactID` | Cadena | El ID de contacto si el posible cliente se ha convertido correctamente. |
| `b2b.convertedDate` | DateTime | La fecha de conversión si el posible cliente se ha convertido correctamente. |
| `b2b.isBlocked` | Booleano | Indica si la persona está bloqueada. |
| `b2b.isConverted` | Booleano | Indica si el posible cliente se convierte. |
| `b2b.isMarketingSuspended` | Booleano | Indica si el marketing está suspendido para la persona. |
| `b2b.marketingSuspendedCause` | Cadena | Si se suspende el marketing para la persona, esta propiedad proporciona el motivo. |
| `b2b.personGroupID` | Cadena | Identificador de grupo de la persona. |
| `b2b.personScore` | Duplicada | Puntuación generada para la persona por un sistema CRM. |
| `b2b.personSource` | Cadena | Fuente de la que se recibió la información de la persona. |
| `b2b.personStatus` | Cadena | El estado actual de marketing o ventas de la persona. |
| `b2b.personType` | Cadena | El tipo de persona B2B. |
| `extSourceSystemAudit` | [Atributos de auditoría del sistema de fuentes externas](../../data-types/external-source-system-audit-attributes.md) | Si la relación de persona comercial proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `extendedWorkDetails` | Objeto | Captura detalles adicionales relacionados con el trabajo de la persona. |
| `extendedWorkDetails.assistantDetails` | Objeto | Captura los siguientes atributos relacionados con el asistente de la persona: <ul><li>`name`: ([Nombre de la persona](../../data-types/person-name.md)) El nombre completo del asistente.</li><li>`phone`: ([Número de teléfono](../../data-types/phone-number.md)) El número de teléfono del asistente.</li></ul> |
| `extendedWorkDetails.departments` | Matriz de cadenas | Lista de nombres de departamento donde trabaja la persona. |
| `extendedWorkDetails.jobTitle` | Cadena | El puesto que ocupa la persona. |
| `extendedWorkDetails.photoUrl` | Cadena | Dirección URL de una foto de la persona. |
| `extendedWorkDetails.reportsToID` | Cadena | Identificador del administrador de informes de la persona. |
| `faxPhone` | [Número de teléfono](../../data-types/phone-number.md) | El número de teléfono de la persona. |
| `homeAddress` | [Dirección postal](../../data-types/postal-address.md) | La dirección de casa de la persona. |
| `homePhone` | [Número de teléfono](../../data-types/phone-number.md) | El número de teléfono de casa de la persona. |
| `mobilePhone` | [Número de teléfono](../../data-types/phone-number.md) | El número de teléfono móvil de la persona. |
| `otherAddress` | [Dirección postal](../../data-types/postal-address.md) | Una dirección alternativa para la persona. |
| `otherPhone` | [Número de teléfono](../../data-types/phone-number.md) | Un número de teléfono alternativo para la persona. |
| `person` | [Persona](../../data-types/person.md) | Un actor individual, contacto o propietario. |
| `personalEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | La dirección de correo electrónico personal de la persona. |
| `workAddress` | [Dirección postal](../../data-types/postal-address.md) | La dirección de trabajo de la persona. |
| `workEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | La dirección de correo electrónico del trabajo de la persona. |
| `workPhone` | [Número de teléfono](../../data-types/phone-number.md) | El número de teléfono de trabajo de la persona. |
| `identityMap` | Mapa | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para la persona. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en la [conceptos básicos de la composición del esquema](../../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `isDeleted` | Booleano | Indica si esta persona se ha eliminado en el Marketo Engage.<br><br>Al usar la variable [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Si configura `isDeleted` a `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `organizations` | Matriz de cadenas | Lista de nombres de organización donde trabaja la persona. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
