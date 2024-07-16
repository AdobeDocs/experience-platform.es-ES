---
title: Grupo de campos de esquema de detalles de ventas adicionales
description: Obtenga información acerca del grupo de campos de esquema Detalles de ampliación de venta.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Detalles de ampliación de venta] grupo de campos de esquema

[!UICONTROL Detalles de ampliación de venta] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para capturar información con respecto a un evento de marketing de ampliación de venta, incluidos detalles sobre la transacción y las diferentes formas en que se mostró la oferta a un cliente.

El grupo de campos proporciona un único campo de tipo de objeto, `upsells`. Las propiedades contenidas en este objeto se explican a continuación.

![Estructura de detalles de ampliación de venta](../../images/field-groups/upsell-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `upsellImpressions` | Matriz de [Impresiones](../../data-types/impressions.md) | Una matriz que enumera las impresiones registradas (vistas digitales o participaciones con la oferta de ampliación de venta) para el cliente. |
| `upsellTransaction` | [Transacción](../../data-types/transaction.md) | Describe la transacción de divisa para la ampliación de venta. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
