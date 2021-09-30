---
title: Tipo de datos de origen B2B
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de origen B2B (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# [!UICONTROL Tipo de ] datos de origen B2B (Beta)

>[!IMPORTANT]
>
>Este tipo de datos está disponible como parte de la plataforma de datos del cliente en tiempo real B2B Edition, que actualmente está en versión beta. La documentación y la funcionalidad están sujetas a cambios.

[!UICONTROL B2B ] Source es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que representa un identificador compuesto para una entidad B2B (como una  [cuenta](../classes/b2b/business-account.md), una  [oportunidad](../classes/b2b/business-opportunity.md) o una  [campaña](../classes/b2b/business-campaign.md)).

Al depender únicamente de identificadores basados en cadenas, puede haber superposiciones entre ID en varios sistemas (por ejemplo, se podría dar un ID de cadena en un sistema CRM, pero ese mismo ID podría referirse a una oportunidad completamente diferente). Esto puede provocar conflictos de datos al combinar datos en [Perfil del cliente en tiempo real](../../profile/home.md).

El tipo de datos [!UICONTROL B2B Source] le permite utilizar el ID de cadena original de una entidad y combinarlo con información contextual específica del origen para garantizar que sea completamente único en el sistema de Platform independientemente del origen del que se originó.

![Estructura de origen B2B](../images/data-types/b2b-source.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sourceID` | Cadena | Un ID exclusivo para el registro de origen. |
| `sourceInstanceID` | Cadena | ID de instancia u organización de los datos de origen. |
| `sourceKey` | Cadena | Un identificador único compuesto por `sourceId`, `sourceInstanceId` y `sourceType` concatenado juntos en el siguiente formato: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Algunos conectores de origen como Marketo concatenan este valor automáticamente para determinados identificadores. Otros deben concatenarse manualmente utilizando la función [Data Prep `concat`](../../data-prep/functions.md#string), por ejemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Cadena | Nombre de la plataforma que proporciona los datos de origen. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
