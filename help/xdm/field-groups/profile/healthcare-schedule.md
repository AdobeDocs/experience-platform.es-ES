---
title: Programar grupo de campos de esquema
description: Obtenga información sobre el grupo de campos Esquema de programación.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL Programar] grupo de campos de esquema

[!UICONTROL Horario] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) y la [[!DNL Provider class]](../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareSchedule` que es un contenedor para los espacios de tiempo que pueden estar disponibles para las citas de reserva.

![Estructura del grupo de campos](../../images/field-groups/schedule.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | Matriz de [[!UICONTROL referencia]](../../data-types/healthcare/reference.md) | Las ranuras que hacen referencia a esta programación y proporcionan los detalles de disponibilidad de estos recursos a los que se hace referencia. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../../data-types/healthcare/identifier.md) | Los identificadores externos para la programación. |
| [!UICONTROL Horizonte de Planificación] | `planningHorizon` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | El período de tiempo que cubren las ranuras que hacen referencia a este programa, incluso si no existen. |
| [!UICONTROL Categoría de servicio] | `serviceCategory` | Matriz de [[!UICONTROL concepto codificable]](../../data-types/healthcare/codeable-concept.md) | Una amplia categorización del servicio que se va a realizar durante la cita. |
| [!UICONTROL Tipo de servicio] | `serviceType` | Matriz de [[!UICONTROL referencia codificable]](../../data-types/healthcare/codeable-reference.md) | El servicio específico que se va a realizar durante la cita. |
| [!UICONTROL Especialidad] | `specialty` | Matriz de [[!UICONTROL concepto codificable]](../../data-types/healthcare/codeable-concept.md) | La especialidad del profesional que se requeriría para realizar el servicio solicitado en la cita. |
| [!UICONTROL Activo] | `active` | Booleano | Indica si el registro de programación está en uso activo. |
| [!UICONTROL Comentario] | `comment` | Cadena | Comentarios sobre la disponibilidad con el fin de describir cualquier información ampliada, como restricciones personalizadas en las ranuras. |
| [!UICONTROL Nombre] | `name` | Cadena | La descripción de la programación tal como se presentará a un consumidor durante la búsqueda. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
