---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles del comercio
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del comercio .
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos Commerce ] Detailsschema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL Comercio ] Detalla un grupo de campos de esquema estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), que se utiliza para describir datos de comercio como información de producto (SKU, nombre, cantidad) y operaciones de carro de compras estándar (pedido, cierre de compra, abandono).

![](../../images/field-groups/commerce-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `commerce` | [Comercio](../../data-types/commerce.md) | Un objeto que describe devoluciones de productos, registro de garantías y procesos de carro/pedido de compras. |
| `productListItems` | Matriz de [elementos de la lista de productos](../../data-types/product-list-item.md) | Lista de artículos que representan los productos seleccionados por un cliente, con opciones y precios específicos en un momento específico (que pueden diferir del registro del producto). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.schema.json)
