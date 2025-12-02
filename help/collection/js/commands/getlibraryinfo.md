---
title: getLibraryInfo
description: Recupere información sobre la versión actual de la biblioteca de Web SDK.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

El comando `getLibraryInfo` proporciona información sobre la versión de la biblioteca Web SDK que se está utilizando actualmente. Puede utilizar este comando para realizar un seguimiento de las versiones de Web SDK que se implementan en distintas propiedades web.

Ejecute el comando `getLibraryInfo` al llamar a la instancia configurada de Web SDK. Este comando suele estar acompañado de una promesa de JavaScript que le permite recuperar los objetos que rellena.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`libraryInfo.commands`**: matriz de comandos que admite esta versión de Web SDK.
* **`libraryInfo.configs`**: matriz de opciones de configuración que admite esta versión de Web SDK.
* **`libraryInfo.version`**: versión de la biblioteca Web SDK.

## Información de biblioteca mediante la extensión de etiquetas Web SDK

La extensión de etiqueta no proporciona una interfaz para enviar este comando. Utilice el editor de código personalizado siguiendo la sintaxis de la biblioteca de JavaScript.

Si ejecuta este comando con la extensión de etiqueta, se incluyen tanto la versión de la extensión de etiqueta como la versión de la biblioteca, concatenadas con un símbolo `+`. La versión de la biblioteca Web SDK aparece primero, seguida de la versión de la extensión de etiquetas.
