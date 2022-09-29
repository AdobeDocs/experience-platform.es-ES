---
title: Depuración en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo alternar las funciones de depuración en el SDK web de Experience Platform.
keywords: depurar sdk web;depuración;configurar;configurar comando;depurar comando;edgeConfigId;setDebug;debugEnabled;depurar;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# Depuración

Cuando la depuración está habilitada, el SDK envía mensajes a la consola del explorador que pueden resultar útiles para depurar la implementación y comprender cómo se comporta el SDK.

La depuración está deshabilitada de forma predeterminada, pero se puede activar de cuatro formas diferentes:

* `configure` command
* `setDebug` command
* parámetro de cadena de consulta
* Alternar en Habilitar depuración en Adobe Experience Platform Debugger. Adobe Experience Platform es una potente herramienta que examina sus páginas web y le ayuda a depurar problemas de implementación con sus productos de Experience Cloud. Adobe Experience Platform Debugger está disponible como un [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) y [Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/) extensión. La depuración se puede habilitar desde la pestaña de configuración de la sección SDK web de AEP.

![](../assets/enable-debugging.png)

## Alternar depuración con el comando Configurar

Al configurar el SDK mediante el `configure` habilitar depuración configurando `debugEnabled` a `true`.

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

Alternar depuración con una `debug` como se indica a continuación:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si prefiere no cambiar el código de la página web o no desea que los mensajes de registro se produzcan para todos los usuarios del sitio web, esto es especialmente útil porque puede ejecutar la variable `debug` en la consola JavaScript de su explorador en cualquier momento.

## Alternar depuración con un parámetro de cadena de consulta

Alternar depuración estableciendo un `alloy_debug` parámetro de cadena de consulta a `true` o `false` de la siguiente manera:

```HTTP
http://example.com/?alloy_debug=true
```

Similar a la variable `debug` , si prefiere no cambiar el código de la página web o no desea que los mensajes de registro se produzcan para todos los usuarios del sitio web, esto es especialmente útil porque puede configurar el parámetro de cadena de consulta al cargar la página web dentro del explorador.

## Prioridad y duración

Cuando la depuración se configura mediante la variable `debug` comando o parámetro de cadena de consulta, anula cualquier `debug` configurado en la variable `configure` comando. En estos dos casos, la depuración también permanece activada durante la sesión. En otras palabras, si habilita la depuración utilizando el comando debug o el parámetro de cadena de consulta, permanece habilitado hasta que se realice una de las siguientes acciones:

* El final de la sesión
* Ejecute el `debug` command
* Vuelva a establecer el parámetro de cadena de consulta

## Recuperación de la información de la biblioteca

A menudo resulta útil acceder a algunos de los detalles de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el `getLibraryInfo` como se indica a continuación:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Actualmente, la `libraryInfo` contiene las siguientes propiedades:

* `version`: Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se está cargando es 1.0.0, el valor sería `1.0.0`. Cuando la biblioteca se ejecuta dentro de la extensión de etiqueta (denominada &quot;AEP Web SDK&quot;), la versión de la biblioteca y la versión de la extensión de etiqueta unidas con un signo &quot;+&quot;. Por ejemplo, si la versión de la biblioteca fuera 1.0.0 y la versión de la extensión de etiqueta fuera 1.2.0, el valor sería `1.0.0+1.2.0`.
* `commands`: Estos son todos los comandos disponibles admitidos por la biblioteca cargada.
* `configs`: Estas son todas las configuraciones actuales de la biblioteca cargada.
