---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de Commerce
description: Obtenga información acerca del grupo de campos de esquema Detalles de Commerce.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# [!UICONTROL Detalles de Commerce] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de Commerce] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para describir datos de comercio, como información de producto (SKU, nombre, cantidad) y operaciones estándar del carro de compras (pedidos, pagos y abandonos).

![](../../images/field-groups/commerce-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Un objeto que describe las devoluciones de productos, el registro de garantías y los procesos del carro de compras/pedido. |
| `productListItems` | Matriz de [elementos de lista de productos](../../data-types/product-list-item.md) | Una lista de artículos que representa los productos seleccionados por un cliente, con opciones y precios específicos en un momento específico (que pueden diferir del registro del producto). |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
