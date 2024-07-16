---
title: Grupo de campos de detección de bots
description: Obtenga información acerca del grupo de campos de esquema del grupo de campos Detección de bots (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL Detección de bots] grupo de campos

[!UICONTROL Detección de bots] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona información sobre el tráfico generado por el bot.

![Un diagrama del grupo de campos [!UICONTROL Detección de bots].](../../images/field-groups/bot-detection-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Detección de bots] | `botDetection` | objeto | Proporciona información sobre el tráfico generado por el bot. |
| [!UICONTROL Puntuación] | `score` | número | La puntuación de probabilidad de bots de cero a uno. Una puntuación de cero significa que el tráfico no es un bot. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
