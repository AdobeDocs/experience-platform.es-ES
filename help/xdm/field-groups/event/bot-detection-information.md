---
title: Grupo de campos de detección de bots
description: Obtenga información acerca del grupo de campos de esquema del grupo de campos Detección de bots (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 5%

---

# [!UICONTROL Detección de bots] grupo de campos

[!UICONTROL Detección de bots] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona información sobre el tráfico generado por el bot.

![Un diagrama de la [!UICONTROL Detección de bots] grupo de campos.](../../images/field-groups/bot-detection-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Detección de bots] | `botDetection` | objeto | Proporciona información sobre el tráfico generado por el bot. |
| [!UICONTROL Puntuación] | `score` | number | La puntuación de probabilidad de bots de cero a uno. Una puntuación de cero significa que el tráfico no es un bot. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

