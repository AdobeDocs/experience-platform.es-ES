---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles comerciales
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles comerciales.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# [!UICONTROL Detalles de comercio] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de comercio] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), se utiliza para describir datos de comercio, como información de productos (SKU, nombre y cantidad) y operaciones estándar del carro de compras (pedidos, pagos y abandonos).

![](../../images/field-groups/commerce-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Un objeto que describe las devoluciones de productos, el registro de garantías y los procesos del carro de compras/pedido. |
| `productListItems` | Matriz de [Elementos de lista de productos](../../data-types/product-list-item.md) | Una lista de artículos que representa los productos seleccionados por un cliente, con opciones y precios específicos en un momento específico (que pueden diferir del registro del producto). |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
