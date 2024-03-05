---
title: getIdentity
description: Obtenga la identidad de un visitante sin enviar datos de evento.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

El `getIdentity` permite obtener un ID de visitante sin enviar datos de evento. Cuando ejecute el `sendEvent` , el SDK web obtiene automáticamente la identidad del visitante si no hay ninguna presente.

Si necesita llamadas independientes para generar un ID de visitante y enviar datos, puede utilizar este comando.

## Obtener identidad mediante la extensión de etiqueta del SDK web

La extensión de etiqueta del SDK web no ofrece este comando a través de la interfaz de usuario de la extensión de etiqueta. Utilice el editor de código personalizado con sintaxis de biblioteca JavaScript.

## Obtener identidad mediante la biblioteca JavaScript del SDK web

Ejecute el `getIdentity` al llamar a la instancia configurada del SDK web. Las siguientes opciones están disponibles al configurar este comando:

* **`namespaces`**: una matriz de áreas de nombres. El valor predeterminado es `["ECID"]`. Los valores válidos incluyen `["ECID"]`, `null`, o `undefined`.
* **`edgeConfigOverrides`**: Un [objeto de anulación de configuración de secuencia de datos](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objeto Response

Si decide hacerlo [gestionar respuestas](command-responses.md) con este comando, están disponibles las siguientes propiedades en el objeto response:

* **`identity.ECID`**: una cadena que contiene el ECID del visitante.
* **`edge.regionID`**: Un entero que representa la región de red perimetral que el explorador visitó al adquirir una identidad. Es igual que la sugerencia de ubicación del Audience Manager heredado.
