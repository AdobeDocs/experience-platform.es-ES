---
title: Tipo de datos del elemento de devolución
description: Obtenga información acerca del tipo de datos Modelo de datos de experiencia de elementos devueltos (XDM).
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# [!UICONTROL Devolver elemento] tipo de datos

[!UICONTROL Devolver artículo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles esenciales relacionados con el proceso de devolución de un artículo comprado.

![Diagrama del tipo de datos del elemento devuelto.](../images/data-types/return-item.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Estado de retorno] | `returnStatus` | cadena | El estado del elemento devuelto (por ejemplo, Pendiente o Aprobado). |
| [!UICONTROL Motivo de retorno] | `returnReason` | cadena | El motivo por el que se solicitó la devolución del artículo. |
| [!UICONTROL Condición de artículo de devolución] | `returnItemCondition` | cadena | La condición del artículo para el que se solicita la devolución. |
| [!UICONTROL Resolución de retorno] | `returnResolution` | cadena | La resolución o el resultado deseado que se espera de la devolución (por ejemplo, Reembolso o Cambio). |
| [!UICONTROL Cantidad de devolución solicitada] | `returnQuantityRequested` | entero | La cantidad del artículo que el comprador solicitó devolver. |
| [!UICONTROL Cantidad de devolución autorizada] | `returnQuantityAuthorized` | entero | La cantidad del artículo que se puede devolver. |
| [!UICONTROL Cantidad de devolución recibida] | `returnQuantityReceived` | entero | La cantidad de artículos devueltos recibidos. |
| [!UICONTROL Devolver cantidad aprobada] | `returnQuantityApproved` | entero | La cantidad del artículo con una devolución totalmente completa y aprobada. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
