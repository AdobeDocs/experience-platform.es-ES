---
title: Depuración en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo alternar las funciones de depuración en el SDK web de Experience Platform.
keywords: depurar sdk web;depurar;configurar;configurar comando;depurar comando;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Depuración

Cuando la depuración está habilitada, el SDK envía mensajes a la consola del navegador que pueden resultar útiles para depurar la implementación y para comprender el comportamiento del SDK. La depuración también resulta en una validación sincrónica del lado del servidor de los datos que se recopilan con el esquema que ha configurado.

La depuración está deshabilitada de forma predeterminada, pero se puede activar de tres formas diferentes:

* `configure` command
* `setDebug` command
* Parámetro de cadena de consulta

## Alternar la depuración con el comando Configurar

Al configurar el SDK mediante el comando `configure`, habilite la depuración estableciendo la opción `debugEnabled` en `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Esto habilita la depuración para todos los usuarios de la página web en lugar de solo para su explorador personal.

## Alternar la depuración con el comando Depurar

Alternar la depuración con un comando `debug` independiente de la siguiente manera:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si prefiere no cambiar el código de la página web o no desea que se produzcan mensajes de registro para todos los usuarios del sitio web, esto es particularmente útil porque puede ejecutar el comando `debug` en la consola JavaScript del explorador en cualquier momento.

## Alternar la depuración con un parámetro de cadena de consulta

Alternar la depuración estableciendo un parámetro de cadena de consulta `alloy_debug` en `true` o `false` de la siguiente manera:

```HTTP
http://example.com/?alloy_debug=true
```

Al igual que el comando `debug`, si prefiere no cambiar el código de la página web o no desea que se produzcan mensajes de registro para todos los usuarios del sitio web, esto es especialmente útil porque puede establecer el parámetro de cadena de consulta al cargar la página web en el explorador.

## Prioridad y duración

Cuando la depuración se establece mediante el comando `debug` o el parámetro de cadena de consulta, anula cualquier opción `debug` establecida en el comando `configure`. En estos dos casos, la depuración también permanece activada durante toda la sesión. En otras palabras, si se habilita la depuración mediante el comando debug o el parámetro de cadena de consulta, permanece habilitado hasta que se cumpla una de las siguientes condiciones:

* El final de la sesión
* Ejecute el comando `debug`
* El parámetro de cadena de consulta se establece de nuevo

## Recuperando información de biblioteca

A menudo resulta útil acceder a algunos de los detalles de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el comando `getLibraryInfo` de la siguiente manera:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Actualmente, el objeto `libraryInfo` proporcionado contiene las siguientes propiedades:

* `version` Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se carga fuera 1.0.0, el valor sería `1.0.0`.
