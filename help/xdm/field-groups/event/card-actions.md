---
title: Grupo de campos de esquema de acciones de tarjeta
description: Obtenga información acerca del grupo de campos Esquema de acciones de tarjeta.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---

# [!UICONTROL Acciones de tarjeta] grupo de campos de esquema

[!UICONTROL Acciones de tarjeta] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `personalFinances.cardActions` a un esquema, que captura detalles sobre una acción de tarjeta, como el tipo de tarjeta, el estado de activación y el estado de bloqueo.

![](../../images/field-groups/card-actions.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `cardActivated` | Número entero | Registra cuándo se ha activado correctamente la tarjeta. |
| `cardActivationStart` | Número entero | Registra cuándo se ha iniciado el proceso de activación de la tarjeta. |
| `cardCancelled` | Número entero | Registra cuándo se ha cancelado una tarjeta. |
| `cardControlsLocked` | Número entero | Registra cuándo se han bloqueado los controles de una tarjeta. |
| `cardControlsUnlocked` | Número entero | Registra cuándo se han desbloqueado los controles de una tarjeta. |
| `cardID` | Cadena | El identificador de la tarjeta que se está activando. Este valor puede ser diferente del número de tarjeta. |
| `cardLocked` | Número entero | Registra cuándo se ha bloqueado una tarjeta. |
| `cardOrderNew` | Número entero | Registra cuándo se ha solicitado una tarjeta. |
| `cardOrderType` | Cadena | El tipo de pedido de tarjeta asociado con un evento de pedido de tarjeta. |
| `cardType` | Cadena | El tipo de tarjeta. |
| `cardUnlocked` | Número entero | Registra cuándo se ha desbloqueado una tarjeta. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
