---
title: getIdentity
description: Obtenga la identidad de un visitante sin enviar datos de evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# `getIdentity`

El comando `getIdentity` le permite obtener un ID de visitante sin enviar datos de evento. Al ejecutar el comando `sendEvent`, el SDK web obtiene automáticamente la identidad del visitante si no hay ninguna presente.

Si necesita llamadas independientes para generar un ID de visitante y enviar datos, puede utilizar este comando.

## Obtener identidad mediante la extensión de etiqueta del SDK web

La extensión de etiqueta del SDK web no ofrece este comando a través de la interfaz de usuario de la extensión de etiqueta. Utilice el editor de código personalizado con sintaxis de biblioteca de JavaScript.

## Obtener identidad mediante la biblioteca de JavaScript del SDK web

Ejecute el comando `getIdentity` al llamar a la instancia configurada del SDK web. Las siguientes opciones están disponibles al configurar este comando:

* **`namespaces`**: una matriz de áreas de nombres. El valor predeterminado es `["ECID"]`. Otros valores admitidos son: `["CORE"]`, `null`, `undefined`. Puede solicitar [!DNL ECID] y [!DNL CORE ID] al mismo tiempo. Ejemplo: `"namespaces": ["ECID","CORE"]`.
* **`edgeConfigOverrides`**: un objeto [de anulación de configuración de secuencia de datos](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`identity.ECID`**: una cadena que contiene el ECID del visitante.
* **`identity.CORE`**: una cadena que contiene el CORE ID del visitante.
* **`edge.regionID`**: un entero que representa la región del Edge Network que el explorador visitó al adquirir una identidad. Es igual que la sugerencia de ubicación del Audience Manager heredado.
