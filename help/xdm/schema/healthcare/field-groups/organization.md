---
title: Grupo de campos de esquema de organización
description: Obtenga información sobre el grupo de campos Esquema de organización.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 6%

---

# [!UICONTROL Organización] grupo de campos de esquema

[!UICONTROL Organization] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] class](../../../classes/individual-profile.md) y [[!DNL Provider class]](../../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareOrganization` que contiene información sobre agrupaciones de personas u organizaciones con un propósito común.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/organization/organization.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| ---| --- | --- | --- |
| [!UICONTROL Detalles de contacto] | `contact` | Matriz de [[!UICONTROL detalles de contacto extendidos]](../data-types/extended-contact-detail.md) | Los datos de contacto de los dispositivos de comunicación disponibles para la organización específica. Esto puede incluir direcciones, números de teléfono, números de fax, números móviles, direcciones de correo electrónico y sitios web. |
| [!UICONTROL Punto final] | `endpoint` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Puntos finales técnicos que proporcionan acceso a los servicios operados por la organización. |
| [!UICONTROL Identificador] | `indentifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | El identificador utilizado para identificar la organización en varios sistemas diferentes. |
| [!UICONTROL Parte De La Organización] | `partOf` | [[!UICONTROL Referencia]](../data-types/reference.md) | La organización de la que forma parte esta organización. |
| [!UICONTROL Calificación] | `qualification` | Matriz de objetos | Las certificaciones oficiales, acreditaciones, capacitación, designaciones y licencias que autorizan y/o respaldan de otra manera la prestación de atención por parte de la organización. Consulte la [sección siguiente](#qualification) para obtener más información. |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El tipo de organización que es. |
| [!UICONTROL Activo] | `active` | Booleano | Si el registro de la organización sigue en uso. |
| [!UICONTROL Alias] | `alias` | Matriz de cadenas | Una lista de nombres alternativos que la organización conoce como, o que se conocían como en el pasado. |
| [!UICONTROL Descripción] | `description` | Cadena | La descripción de la organización que ayuda a proporcionar un contexto general para garantizar que se selecciona la organización correcta. |
| [!UICONTROL Nombre] | `name` | Cadena | El nombre asociado con la organización. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de calificación](../../../images/healthcare/field-groups/organization/qualification.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Representación codificada de la calificación. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Identificador asignado a esta calificación para esta organización. |
| [!UICONTROL Emisor] | `issuer` | [[!UICONTROL Referencia]](../data-types/reference.md) | Organización que regula y emite la calificación. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Período durante el cual la calificación es válida. |
