---
title: Card Actions Schema Field Group
description: This document provides an overview of the Card Actions schema field group.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 8%

---

# 

[[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) `personalFinances.cardActions`

![](../../images/field-groups/card-actions.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `cardActivated` | Número entero | Tracks when the card has been successfully activated. |
| `cardActivationStart` | Número entero | Tracks when the card activation process has been started. |
| `cardCancelled` | Número entero | Tracks when a card has been cancelled. |
| `cardControlsLocked` | Número entero | Tracks when a card&#39;s controls have been locked. |
| `cardControlsUnlocked` | Número entero | Tracks when a card&#39;s controls have been unlocked. |
| `cardID` | Cadena | The identifier for the card being activated. This value might be different from the card number. |
| `cardLocked` | Número entero | Tracks when a card has been locked. |
| `cardOrderNew` | Número entero | Tracks when a card has been requested. |
| `cardOrderType` | Cadena | The type of card order associated with a card order event. |
| `cardType` | Cadena | The type of card. |
| `cardUnlocked` | Número entero | Tracks when a card has been unlocked. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json)
