---
title: Actualizar grupo de campos de esquema
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de la actualización .
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Actualizar ] grupo de campos Detailsschema

[!UICONTROL Actualizar ] Detalla un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) cliente para capturar información relacionada con un evento de marketing de actualización, incluidos detalles sobre la transacción y las diferentes formas en que se mostró la oferta a un cliente.

El grupo de campos proporciona un único campo de tipo de objeto, `upgrades`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de detalles de la actualización](../../images/field-groups/upgrade-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `upgradeImpressions` | Matriz de [Impresiones](../../data-types/impressions.md) | Matriz que enumera las impresiones registradas (vistas digitales o participaciones con la oferta de actualización) para el cliente. |
| `upgradeTransaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de moneda para la actualización. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
