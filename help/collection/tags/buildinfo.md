---
title: buildInfo
description: Obtenga información sobre la compilación de etiquetas implementada en el sitio.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

El objeto `_satellite.buildInfo` contiene información sobre la compilación de la propiedad de etiqueta implementada. Este objeto es muy útil cuando se depuran compilaciones frecuentes para garantizar que se está utilizando la versión más reciente.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Campos disponibles

Los campos siguientes están disponibles al llamar a este objeto.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| **`minified`** | `boolean` | Indica si la biblioteca está minificada. Las compilaciones de producción generalmente se minifican (`true`), mientras que las compilaciones de desarrollo y ensayo no suelen ser (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | La fecha y la hora de creación y publicación del archivo JavaScript. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine) es el motor de Adobe que procesa las reglas de etiquetas y delega la lógica a las extensiones de etiquetas. Este campo contiene la fecha y la hora de la compilación de Turbine utilizada para publicar la propiedad de etiqueta. |
| **`turbineVersion`** | `string` | La versión de Turbine utilizada para generar y publicar la propiedad de etiqueta. |

`_satellite._container.buildInfo` también contiene información similar. Consulte [`_container`](container.md) para obtener más información.
