---
title: Tipo de datos de devolución
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de retorno (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 6%

---

# [!UICONTROL Volver] tipo de datos

[!UICONTROL Volver] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura la información esencial relacionada con una Autorización de devolución de mercancía (RMA).

![Diagrama del tipo de datos Devolver.](../images/data-types/return.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Identificador de devolución] | `returnID` | string | El identificador único de esta RMA. |
| [!UICONTROL Estado de devolución] | `returnStatus` | string | El estado actual de la autorización de devolución de material (por ejemplo, Pendiente o Cerrada). |
| [!UICONTROL ID de compra del pedido] | `purchaseID` | string | El identificador único del pedido/compra al que pertenece la RMA. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

