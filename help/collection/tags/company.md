---
title: compañía
description: Obtenga información sobre la organización de IMS propietaria de la propiedad de etiquetas implementada.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

El objeto `_satellite.company` muestra información sobre la organización de IMS propietaria de la propiedad de etiqueta.

```ts
readonly _satellite.company: Company
```

## Campos disponibles

Los campos siguientes están disponibles al llamar a este objeto:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **`orgId`** | `string` | El ID de organización de IMS de la propiedad de etiqueta. |
| **`dynamicCdnEnabled`** | `boolean` | Determina si la propiedad de etiquetas utiliza la función de cambio dinámico de CDN de Adobe. Si se establece en `true`, cambia automáticamente la CDN desde la que un visitante solicita la etiqueta en función de su ubicación. |
| **`cdnAllowList`** | `string[]` | Las CDN permitidas desde las que cargar la propiedad de etiqueta. |

`_satellite._container.company` también contiene información similar. Consulte [`_container`](container.md) para obtener más información.
