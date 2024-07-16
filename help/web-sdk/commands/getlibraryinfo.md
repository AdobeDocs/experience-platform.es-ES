---
title: getLibraryInfo
description: Recupere información sobre la versión de la biblioteca del SDK web actual.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

El comando `getLibraryInfo` proporciona información sobre la versión de la biblioteca de SDK web que se está utilizando actualmente. Puede utilizar este comando para realizar un seguimiento de las versiones del SDK web que implementa en distintas propiedades web.

## Información de biblioteca mediante la extensión de etiqueta del SDK web

La extensión de etiqueta no proporciona una interfaz para enviar este comando. Utilice el editor de código personalizado siguiendo la sintaxis de la biblioteca de JavaScript.

Si ejecuta este comando con la extensión de etiqueta, se incluyen tanto la versión de la extensión de etiqueta como la versión de la biblioteca, concatenadas con un símbolo `+`. La versión de la biblioteca del SDK web aparece primero, seguida de la versión de la extensión de la etiqueta.

## Información de biblioteca mediante la biblioteca JavaScript del SDK web

Ejecute el comando `getLibraryInfo` al llamar a la instancia configurada del SDK web. Este comando suele estar acompañado de una promesa de JavaScript que le permite recuperar los objetos que rellena.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`libraryInfo.commands`**: matriz de comandos que admite esta versión del SDK web.
* **`libraryInfo.configs`**: matriz de opciones de configuración que admite esta versión del SDK web.
* **`libraryInfo.version`**: versión de la biblioteca del SDK web.
