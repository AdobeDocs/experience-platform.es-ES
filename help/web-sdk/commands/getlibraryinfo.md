---
title: getLibraryInfo
description: Recupere información sobre la versión de la biblioteca del SDK web actual.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

El `getLibraryInfo` proporciona información sobre la versión de la biblioteca del SDK web que se utiliza actualmente. Puede utilizar este comando para realizar un seguimiento de las versiones del SDK web que implementa en distintas propiedades web.

## Información de biblioteca mediante la extensión de etiqueta del SDK web

La extensión de etiqueta no proporciona una interfaz para enviar este comando. Utilice el editor de código personalizado siguiendo la sintaxis de la biblioteca JavaScript.

Si ejecuta este comando con la extensión de etiqueta, se incluyen la versión de la extensión de etiqueta y la versión de la biblioteca, concatenadas con un `+` símbolo. La versión de la biblioteca del SDK web aparece primero, seguida de la versión de la extensión de la etiqueta.

## Información de biblioteca mediante la biblioteca JavaScript del SDK web

Ejecute el `getLibraryInfo` al llamar a la instancia configurada del SDK web. Este comando suele estar acompañado de una promesa de JavaScript que le permite recuperar los objetos que rellena.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objeto Response

Si decide hacerlo [gestionar respuestas](command-responses.md) con este comando, están disponibles las siguientes propiedades en el objeto response:

* **`libraryInfo.commands`**: matriz de comandos que admite esta versión del SDK web.
* **`libraryInfo.configs`**: matriz de opciones de configuración que admite esta versión del SDK web.
* **`libraryInfo.version`**: versión de la biblioteca del SDK web.
