---
title: Clase de lista de marketing empresarial XDM
description: Este documento proporciona información general sobre la clase XDM Business Marketing List en Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 4%

---

# [!UICONTROL Lista de marketing empresarial XDM] class

>[!IMPORTANT]
>
>Esta clase está diseñada para ser utilizada por organizaciones con acceso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a CDP B2B Edition en tiempo real para que esta clase participe en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Lista de marketing empresarial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una lista de marketing. Las listas de marketing permiten priorizar a los clientes potenciales que tienen más probabilidades de comprar un producto.

![](../../images/classes/b2b/business-marketing-list.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la lista de marketing proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `marketingListKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de la lista de marketing. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `marketingListID`. |
| `marketingListDescription` | Cadena | Una descripción para la lista de marketing. |
| `marketingListID` | Cadena | Un ID único para la entidad de la lista de marketing. |
| `marketingListName` | Cadena | Nombre de la lista de marketing. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
