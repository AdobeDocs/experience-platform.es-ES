---
title: Grupo de campos de esquema de detalles de solicitud de oferta
description: Este documento proporciona información general sobre el grupo de campos de esquema Detalles de la solicitud de oferta.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL Detalles de solicitud de presupuesto] grupo de campos de esquema

[!UICONTROL Detalles de solicitud de presupuesto] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `quotes` objeto a un esquema, que captura los detalles del proceso de solicitud para varios tipos de presupuestos, incluidas pólizas de seguro, seguros médicos, pedidos de fabricación y pedidos de alta tecnología.

![](../../images/field-groups/quote-request-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `discount` | [[!UICONTROL Moneda]](../../data-types/currency.md) | El importe de descuento de una cotización que se muestra a un visitante. |
| `premium` | [[!UICONTROL Moneda]](../../data-types/currency.md) | La cantidad de la prima de una cotización que se muestra a un visitante. |
| `location` | [!UICONTROL Cadena] | El código postal utilizado para encontrar minoristas cerca de la ubicación del visitante. |
| `requestID` | [!UICONTROL Cadena] | Un identificador único para la solicitud de presupuesto. |
| `selectedRetailer` | [!UICONTROL Cadena] | El minorista seleccionado para la solicitud de presupuesto, si corresponde. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
