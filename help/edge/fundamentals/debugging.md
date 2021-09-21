---
title: Depuración en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo alternar las funciones de depuración en el SDK web de Experience Platform.
keywords: depurar sdk web;depuración;configurar;configurar comando;depurar comando;edgeConfigId;setDebug;debugEnabled;depurar;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: d0d7fe42827579c502be9de29d36f24c94259b5f
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Depuración

Cuando la depuración está habilitada, el SDK envía mensajes a la consola del explorador que pueden resultar útiles para depurar la implementación y comprender cómo se comporta el SDK.

La depuración está deshabilitada de forma predeterminada, pero se puede activar de cuatro formas diferentes:

* `configure` command
* `setDebug` command
* parámetro de cadena de consulta
* Alternar en Habilitar depuración en Adobe Experience Platform Debugger. Adobe Experience Platform es una potente herramienta que examina sus páginas web y le ayuda a depurar problemas de implementación con sus productos de Experience Cloud. Adobe Experience Platform Debugger está disponible como extensión [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) y [Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/). La depuración se puede habilitar desde la pestaña de configuración de la sección SDK web de AEP.

![](../images/enable-debugging.png)

## Alternar depuración con el comando Configurar

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
>Esto permite la depuración para todos los usuarios de la página web en lugar de solo para su navegador personal.

## Alternar depuración con el comando Depuración

Alterne la depuración con un comando `debug` independiente de la siguiente manera:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si prefiere no cambiar el código de la página web o no desea que los mensajes de registro se produzcan para todos los usuarios del sitio web, esto es especialmente útil porque puede ejecutar el comando `debug` en la consola JavaScript del explorador en cualquier momento.

## Alternar depuración con un parámetro de cadena de consulta

Alterne la depuración estableciendo un parámetro de cadena de consulta `alloy_debug` en `true` o `false` como se indica a continuación:

```HTTP
http://example.com/?alloy_debug=true
```

De forma similar al comando `debug` , si prefiere no cambiar el código de la página web o no desea que se produzcan mensajes de registro para todos los usuarios del sitio web, esto es especialmente útil porque puede configurar el parámetro de cadena de consulta al cargar la página web dentro del explorador.

## Prioridad y duración

Cuando la depuración se configura mediante el comando `debug` o el parámetro de cadena de consulta, anula cualquier opción `debug` establecida en el comando `configure`. En estos dos casos, la depuración también permanece activada durante la sesión. En otras palabras, si habilita la depuración utilizando el comando debug o el parámetro de cadena de consulta, permanece habilitado hasta que se realice una de las siguientes acciones:

* El final de la sesión
* Ejecute el comando `debug`
* Vuelva a establecer el parámetro de cadena de consulta

## Recuperación de la información de la biblioteca

A menudo resulta útil acceder a algunos de los detalles de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el comando `getLibraryInfo` de la siguiente manera:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Actualmente, el objeto `libraryInfo` proporcionado contiene las siguientes propiedades:

* `version` Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se está cargando es 1.0.0, el valor sería `1.0.0`. Cuando la biblioteca se ejecuta dentro de la extensión de etiqueta (denominada &quot;AEP Web SDK&quot;), la versión de la biblioteca y la versión de la extensión de etiqueta unidas con un signo &quot;+&quot;. Por ejemplo, si la versión de la biblioteca fuera 1.0.0 y la versión de la extensión de etiqueta fuera 1.2.0, el valor sería `1.0.0+1.2.0`.
