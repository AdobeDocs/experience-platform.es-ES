---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquema;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de marketing
description: Obtenga información sobre el tipo de datos XDM de marketing.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# Tipo de datos [!UICONTROL Marketing]

[!UICONTROL Marketing] es un tipo de datos XDM estándar que describe actividades de marketing que están activas con un punto de contacto en particular.

![](../images/data-types/marketing.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignGroup` | Cadena | Nombre del grupo de campañas (en casos en los que se agrupan varias campañas como `50%_DISCOUNT`). |
| `campaignName` | Cadena | Nombre de la campaña de marketing, como `50%_DISCOUNT_USA` o `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Cadena | El código de seguimiento que se puede utilizar para identificar la campaña de marketing a la que está asociado el evento. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
