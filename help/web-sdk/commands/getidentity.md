---
title: getIdentity
description: Obtenga la identidad de un visitante sin enviar datos de evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

El comando `getIdentity` le permite obtener un ID de visitante sin enviar datos de evento. Al ejecutar el comando `sendEvent`, el SDK web obtiene automáticamente la identidad del visitante si no hay ninguna presente.

Si necesita llamadas independientes para generar un ID de visitante y enviar datos, puede utilizar este comando.

## Obtener identidad mediante la extensión de etiqueta del SDK web

La extensión de etiqueta del SDK web no ofrece este comando a través de la interfaz de usuario de la extensión de etiqueta. Utilice el editor de código personalizado con sintaxis de biblioteca de JavaScript.

## Obtener identidad mediante la biblioteca de JavaScript del SDK web

Ejecute el comando `getIdentity` al llamar a la instancia configurada del SDK web. Las siguientes opciones están disponibles al configurar este comando:

* **`namespaces`**: una matriz de áreas de nombres. El valor predeterminado es `["ECID"]`. Los valores válidos incluyen `["ECID"]`, `null` o `undefined`.
* **`edgeConfigOverrides`**: un objeto [de anulación de configuración de secuencia de datos](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`identity.ECID`**: una cadena que contiene el ECID del visitante.
* **`edge.regionID`**: un entero que representa la región del Edge Network que el explorador visitó al adquirir una identidad. Es igual que la sugerencia de ubicación del Audience Manager heredado.
