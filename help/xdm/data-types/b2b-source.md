---
title: Tipo de datos de Source B2B
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de Source B2B.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL Tipo de datos B2B Source]

[!UICONTROL B2B Source] es un tipo de datos XDM (Experience Data Model) estándar que representa un identificador compuesto para una entidad B2B (como una [cuenta](../classes/b2b/business-account.md), una [oportunidad](../classes/b2b/business-opportunity.md) o una [campaña](../classes/b2b/business-campaign.md)).

Al basarse únicamente en identificadores basados en cadenas, puede haber superposiciones entre ID de en varios sistemas (por ejemplo, se podría dar una oportunidad a un ID de cadena en un sistema CRM, pero ese mismo ID podría hacer referencia a una oportunidad completamente diferente). Esto puede provocar conflictos de datos al combinar datos en [Perfil del cliente en tiempo real](../../profile/home.md).

El tipo de datos [!UICONTROL B2B Source] le permite usar el identificador de cadena original de una entidad y combinarlo con información contextual específica del origen para garantizar que siga siendo totalmente único en el sistema de Platform, independientemente del origen desde el que se originó.

![Estructura de Source B2B](../images/data-types/b2b-source.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sourceID` | Cadena | ID único del registro de origen. |
| `sourceInstanceID` | Cadena | El ID de instancia u organización de los datos de origen. |
| `sourceKey` | Cadena | Identificador único compuesto por `sourceId`, `sourceInstanceId` y `sourceType` concatenados juntos en el siguiente formato: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Algunos conectores de origen, como Marketo, concatenan este valor automáticamente para determinados identificadores. Otros se deben concatenar manualmente mediante la función [Data Prep `concat`](../../data-prep/functions.md#string), por ejemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Cadena | Nombre de la plataforma que proporciona los datos de origen. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
