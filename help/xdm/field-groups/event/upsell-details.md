---
title: Grupo de campos de esquema de detalles de ampliación
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de ampliación .
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Grupo de campos ] Upsell Detailsschema

[!UICONTROL Upsell ] Detail es un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) cliente que captura información relacionada con un evento de marketing de mejora, que incluye detalles sobre la transacción y las diferentes maneras en que se mostró la oferta a un cliente.

El grupo de campos proporciona un único campo de tipo de objeto, `upsells`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de Detalles de ventas adicionales](../../images/field-groups/upsell-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `upsellImpressions` | Matriz de [Impresiones](../../data-types/impressions.md) | Matriz que enumera las impresiones registradas (vistas digitales o participaciones con la oferta de ventas adicionales) para el cliente. |
| `upsellTransaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de moneda para la mejora de ventas. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
