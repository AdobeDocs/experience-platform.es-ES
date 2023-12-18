---
title: Grupo de campos de esquema de detalles de aplicación
description: Obtenga información acerca del grupo de campos de esquema Detalles de la aplicación.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 4%

---

# [!UICONTROL Detalles de aplicación] grupo de campos de esquema

[!UICONTROL Detalles de aplicación] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `application` objeto a un esquema, que captura detalles relacionados con la aplicación, como bloqueos, uso de funciones, inicios y actualizaciones.

![](../../images/field-groups/application-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `application` | [[!UICONTROL Aplicación]](../../data-types/financial-account.md) | Registra información de la aplicación relacionada con un evento, incluido el nombre de la aplicación, su versión, instalaciones, inicios, bloqueos y cierres. Podría ser la aplicación a la que apunta el evento (como el destino de una notificación push que se envía) o la aplicación que origina el evento (como un clic o un inicio de sesión). |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
