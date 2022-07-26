---
title: Grupo de campos de esquema de detalles de aplicación
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de la aplicación .
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 4%

---

# [!UICONTROL Detalles de la aplicación] grupo de campos de esquema

[!UICONTROL Detalles de la aplicación] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). El grupo de campos proporciona un solo `application` a un esquema, que captura detalles relacionados con la aplicación, como bloqueos, uso de características, lanzamientos y actualizaciones.

![](../../images/field-groups/application-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `application` | [[!UICONTROL Aplicación]](../../data-types/financial-account.md) | Captura la información de la aplicación relacionada con un evento, incluido el nombre de la aplicación, la versión de la aplicación, las instalaciones, los lanzamientos, los bloqueos y los cierres. Podría ser la aplicación a la que se dirige el evento (como el destino de la notificación push que se envía) o la aplicación que origina el evento (como un clic o un inicio de sesión). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
