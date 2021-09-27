---
title: Clase de lista de marketing empresarial XDM
description: Este documento proporciona información general sobre la clase XDM Business Marketing List en Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing ] Listclass

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL XDM Business Marketing ] List es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una lista de marketing. Las listas de marketing permiten priorizar a los clientes potenciales que tienen más probabilidades de comprar un producto.

![](../../images/classes/b2b/business-marketing-list.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la lista de marketing proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `marketingListKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de la lista de marketing. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `marketingListID`. |
| `marketingListDescription` | Cadena | Una descripción para la lista de marketing. |
| `marketingListID` | Cadena | Un ID único para la entidad de la lista de marketing. |
| `marketingListName` | Cadena | Nombre de la lista de marketing. |
