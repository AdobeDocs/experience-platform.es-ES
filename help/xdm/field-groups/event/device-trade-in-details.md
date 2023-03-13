---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;dispositivo;intercambio;intercambio;intercambio;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de intercambio de dispositivos
description: Este documento proporciona información general del grupo de campos de esquema Detalles de intercambio de dispositivos.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# [!UICONTROL Detalles de intercambio de dispositivos] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de intercambio de dispositivos] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). Proporciona un solo campo (`deviceTradeInDetails`), que describe una transacción de intercambio de dispositivos, incluido el valor de intercambio, el ID del dispositivo original y el ID de nuevo dispositivo.

![Estructura de detalles de intercambio de dispositivos](../../images/field-groups/device-trade-in-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `tradeInValue` | [Moneda](../../data-types/currency.md) | El valor del dispositivo que se está negociando. |
| `newDeviceID` | Cadena | El ID del nuevo dispositivo con el que se está negociando. |
| `originalDeviceID` | Cadena | El ID del dispositivo que se está negociando. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
