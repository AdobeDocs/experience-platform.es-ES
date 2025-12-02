---
title: entorno
description: El entorno de compilación que utiliza actualmente la propiedad de etiqueta.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

El objeto `_satellite.environment` indica qué entorno de compilación está usando actualmente la propiedad de etiqueta.

```js
readonly _satellite.environment: Environment
```

## Campos disponibles

Los campos siguientes están disponibles al llamar a este objeto.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Nombre | Tipo | Descripción |
|---|---|---|
| **`id`** | `string` | El identificador único del entorno. Puede localizar el ID de entorno seleccionando el icono **[!UICONTROL Install]** en [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) en la interfaz de usuario de etiquetas. |
| **`stage`** | `development \| staging \| production` | El tipo de entorno. |
