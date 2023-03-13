---
title: Grupo de campos de esquema de detalles de herramienta del sitio
description: Este documento proporciona información general del grupo de campos de esquema Detalles de la herramienta del sitio.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---

# [!UICONTROL Detalles de Sitetool] grupo de campos de esquema

[!UICONTROL Detalles de Sitetool] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `sitetool` objeto a un esquema, que captura la información recopilada por una herramienta de sitio.

![Estructura del grupo de campos](../../images/field-groups/sitetool-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `dataGatheringEvent` | Objeto | Indica si este evento es un evento de recopilación de datos junto con otros detalles relacionados. Contiene las siguientes propiedades:<ul><li>`data`: (Mapa) Contiene los datos JSON que se recopilan y envían como parte del evento de envío de prueba, encuesta o encuesta.</li><li>`isTrue`: (booleano) indica si este evento es de recopilación de datos, como una prueba, una encuesta o una encuesta.</li><li>`score`: (entero) puntuación que asegura el actor en función de las respuestas de eventos.</li></ul> |
| `actor` | Cadena | Una persona o miembro que realizó la acción. |
| `actorID` | Cadena | Un identificador único de la persona/miembro que realizó la acción. |
| `isKeyEvent` | Booleano | Indica si este evento es un evento clave. |
| `name` | Cadena | Nombre de la herramienta del sitio, como bot de chat, encuesta, etc. |
| `section` | Cadena | La sección correspondiente de la herramienta del sitio, como principal o secundaria. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
