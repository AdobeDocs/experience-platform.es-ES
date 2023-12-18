---
title: Tipo de datos de origen B2B
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia de origen B2B (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL Origen B2B] tipo de datos

[!UICONTROL Origen B2B] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que representa un identificador compuesto para una entidad B2B (como un [account](../classes/b2b/business-account.md), un [oportunidad](../classes/b2b/business-opportunity.md), o a [campaña](../classes/b2b/business-campaign.md)).

Al basarse únicamente en identificadores basados en cadenas, puede haber superposiciones entre ID de en varios sistemas (por ejemplo, se podría dar una oportunidad a un ID de cadena en un sistema CRM, pero ese mismo ID podría hacer referencia a una oportunidad completamente diferente). Esto puede provocar conflictos de datos al combinar datos en [Perfil del cliente en tiempo real](../../profile/home.md).

El [!UICONTROL Origen B2B] El tipo de datos permite utilizar el ID de cadena original de una entidad y combinarla con información contextual específica de la fuente para garantizar que siga siendo totalmente único en el sistema de Platform, independientemente de la fuente de la que se originó.

![Estructura de origen B2B](../images/data-types/b2b-source.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sourceID` | Cadena | ID único del registro de origen. |
| `sourceInstanceID` | Cadena | El ID de instancia u organización de los datos de origen. |
| `sourceKey` | Cadena | Un identificador único compuesto por `sourceId`, `sourceInstanceId`, y `sourceType` concatenados juntos en el siguiente formato: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Algunos conectores de origen, como Marketo, concatenan este valor automáticamente para determinados identificadores. Otros deben concatenarse manualmente utilizando [Preparación de datos `concat` función](../../data-prep/functions.md#string), por ejemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Cadena | Nombre de la plataforma que proporciona los datos de origen. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
