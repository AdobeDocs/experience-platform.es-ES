---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dispositivo;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de marketing
description: Este documento proporciona información general sobre el tipo de datos de Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---

# [!UICONTROL Marketing] tipo de datos

[!UICONTROL Marketing] es un tipo de datos XDM estándar que describe actividades de marketing activas con un punto de contacto determinado.

![](../images/data-types/marketing.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignGroup` | Cadena | El nombre del grupo de campañas (en casos en los que varias campañas se agrupan como `50%_DISCOUNT`). |
| `campaignName` | Cadena | El nombre de la campaña de marketing, como `50%_DISCOUNT_USA` o `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Cadena | El código de seguimiento que se puede utilizar para identificar la campaña de marketing a la que está asociado el evento. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
