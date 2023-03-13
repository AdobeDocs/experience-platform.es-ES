---
title: Grupo de campos de esquema de detalles de actualización
description: Este documento proporciona información general sobre el grupo de campos de esquema Detalles de actualización.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL Detalles de actualización] grupo de campos de esquema

[!UICONTROL Detalles de actualización] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) se utiliza para recopilar información sobre un evento de marketing de actualización, incluidos detalles sobre la transacción y las diferentes formas en que se mostró la oferta a un cliente.

El grupo de campos proporciona un único campo de tipo de objeto, `upgrades`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de detalles de actualización](../../images/field-groups/upgrade-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `upgradeImpressions` | Matriz de [Impresiones](../../data-types/impressions.md) | Una matriz que enumera las impresiones registradas (vistas digitales o participaciones con la oferta de actualización) para el cliente. |
| `upgradeTransaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de moneda para la actualización. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
