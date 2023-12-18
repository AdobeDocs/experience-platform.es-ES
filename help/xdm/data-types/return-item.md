---
title: Tipo de datos del elemento de devolución
description: Obtenga información acerca del tipo de datos Modelo de datos de experiencia de elementos devueltos (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL Devolver elemento] tipo de datos

[!UICONTROL Devolver elemento] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles esenciales relacionados con el proceso de devolución de un artículo comprado.

![Diagrama del tipo de datos del elemento devuelto.](../images/data-types/return-item.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Estado de devolución] | `returnStatus` | string | El estado del elemento devuelto (por ejemplo, Pendiente o Aprobado). |
| [!UICONTROL Motivo de devolución] | `returnReason` | string | El motivo por el que se solicitó la devolución del artículo. |
| [!UICONTROL Condición de artículo devuelto] | `returnItemCondition` | string | La condición del artículo para el que se solicita la devolución. |
| [!UICONTROL Resolución de retorno] | `returnResolution` | string | La resolución o el resultado deseado que se espera de la devolución (por ejemplo, Reembolso o Cambio). |
| [!UICONTROL Cantidad de devolución solicitada] | `returnQuantityRequested` | entero | La cantidad del artículo que el comprador solicitó devolver. |
| [!UICONTROL Cantidad de devolución autorizada] | `returnQuantityAuthorized` | entero | La cantidad del artículo que se puede devolver. |
| [!UICONTROL Cantidad de devolución recibida] | `returnQuantityReceived` | entero | La cantidad de artículos devueltos recibidos. |
| [!UICONTROL Cantidad de devolución aprobada] | `returnQuantityApproved` | entero | La cantidad del artículo con una devolución totalmente completa y aprobada. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
