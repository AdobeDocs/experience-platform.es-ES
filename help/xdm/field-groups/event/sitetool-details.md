---
title: Detalles del sitio Grupo de campos de esquema
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del sitio .
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# [!UICONTROL Detalles del sitio] grupo de campos de esquema

[!UICONTROL Detalles del sitio] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). El grupo de campos proporciona un solo `sitetool` a un esquema, que captura información recopilada por una herramienta de sitio.

![Estructura del grupo de campo](../../images/field-groups/sitetool-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `dataGatheringEvent` | Objeto | Indica si este evento es un evento de recopilación de datos junto con otros detalles relacionados. Contiene las siguientes propiedades:<ul><li>`data`: (Mapa) Contiene los datos JSON que se recopilan y envían como parte del evento de envío de cuestionario, encuesta o encuesta.</li><li>`isTrue`: (Booleano) Indica si este evento es de recopilación de datos, como un cuestionario, una encuesta o una encuesta.</li><li>`score`: (Número entero) La puntuación asegurada por el actor en función de las respuestas al evento.</li></ul> |
| `actor` | Cadena | Una persona o miembro que realizó la acción. |
| `actorID` | Cadena | Identificador único de la persona o miembro que realizó la acción. |
| `isKeyEvent` | Booleano | Indica si este evento es un evento clave. |
| `name` | Cadena | Nombre del sitio, como bots de chat, encuestas, etc. |
| `section` | Cadena | La sección relevante del sitio, como main o sub. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
