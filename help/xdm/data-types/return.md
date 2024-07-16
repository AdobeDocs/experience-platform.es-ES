---
title: Tipo de datos de devolución
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de retorno (XDM).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL Devolver] tipo de datos

[!UICONTROL Devolver] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura la información esencial relacionada con una Autorización de devolución de mercancía (RMA).

![Diagrama del tipo de datos devuelto.](../images/data-types/return.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Identificador de devolución] | `returnID` | cadena | El identificador único de esta RMA. |
| [!UICONTROL Estado de retorno] | `returnStatus` | cadena | El estado actual de la autorización de devolución de material (por ejemplo, Pendiente o Cerrada). |
| [!UICONTROL ID de compra de pedido] | `purchaseID` | cadena | El identificador único del pedido/compra al que pertenece la RMA. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
