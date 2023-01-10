---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;dispositivo;comercio;comercio;comercio;comercio en;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de comercio de dispositivos
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del comercio de dispositivos .
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL Detalles del comercio de dispositivos] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles del comercio de dispositivos] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Proporciona un solo campo (`deviceTradeInDetails`), que describe una transacción de intercambio de dispositivos, incluido el valor de intercambio, el ID del dispositivo original y el nuevo ID del dispositivo.

![Estructura de Detalles del comercio de dispositivos](../../images/field-groups/device-trade-in-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `tradeInValue` | [Moneda](../../data-types/currency.md) | El valor del dispositivo que se está intercambiando. |
| `newDeviceID` | Cadena | El ID del nuevo dispositivo para el que se va a intercambiar. |
| `originalDeviceID` | Cadena | El ID del dispositivo que se está intercambiando. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
