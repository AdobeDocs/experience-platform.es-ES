---
title: Depuración en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo alternar las funcionalidades de depuración en el SDK web de Experience Platform.
keywords: depurar sdk web;depuración;configurar;comando configure;depurar comando;edgeConfigId;setDebug;debugEnabled;depurar;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# Depuración

Cuando la depuración está habilitada, el SDK envía mensajes a la consola del explorador que pueden resultar útiles para depurar la implementación y comprender cómo se comporta el SDK.

La depuración está deshabilitada de forma predeterminada, pero se puede activar de cuatro formas diferentes:

* `configure` mando
* `setDebug` mando
* parámetro de cadena de consulta
* Activar o desactivar la depuración en Adobe Experience Platform Debugger. Adobe Experience Platform es una potente herramienta que examina sus páginas web y le ayuda a depurar los problemas de implementación con los productos de Experience Cloud. Adobe Experience Platform Debugger está disponible como [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) y [Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/) extensión. La depuración se puede habilitar desde la pestaña de configuración de la sección SDK web de AEP.

![](../assets/enable-debugging.png)

## Alternar la depuración con el comando Configurar

Al configurar el SDK mediante `configure` , habilite la depuración configurando el comando `debugEnabled` opción para `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Esto habilita la depuración para todos los usuarios de la página web en lugar de solo para su navegador personal.

## Alternar la depuración con el comando Debug

Alternar depuración con una independiente `debug` como se indica a continuación:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si prefiere no cambiar el código de la página web o no desea que se produzcan mensajes de registro para todos los usuarios del sitio web, esto resulta especialmente útil porque puede ejecutar el `debug` dentro de la consola JavaScript del explorador en cualquier momento.

## Alternar la depuración con un parámetro de cadena de consulta

Alternar depuración estableciendo un `alloy_debug` parámetro de cadena de consulta a `true` o `false` como sigue:

```HTTP
http://example.com/?alloy_debug=true
```

Similar a la `debug` , si prefiere no cambiar el código de la página web o no desea que se produzcan mensajes de registro para todos los usuarios del sitio web, esto resulta especialmente útil porque puede establecer el parámetro de cadena de consulta al cargar la página web en el explorador.

## Prioridad y duración

Cuando la depuración se establece mediante `debug` parámetro de cadena de consulta o comando, anula cualquier `debug` opción establecida en la `configure` comando. En estos dos casos, la depuración también permanece activada durante la sesión. En otras palabras, si habilita la depuración mediante el comando debug o el parámetro de cadena de consulta, permanecerá habilitada hasta que se realice una de las siguientes acciones:

* El final de la sesión
* Usted ejecuta el `debug` mando
* Ha vuelto a establecer el parámetro de cadena de consulta

## Recuperando información de biblioteca

A menudo, es útil acceder a algunos de los detalles detrás de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el `getLibraryInfo` como se indica a continuación:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Actualmente, el proporciona `libraryInfo` contiene las propiedades siguientes:

* `version`: Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se carga es 1.0.0, el valor sería `1.0.0`. Cuando la biblioteca se ejecuta dentro de la extensión de etiqueta (denominada &quot;SDK web de AEP&quot;), la versión es la versión de la biblioteca y la versión de la extensión de etiqueta unida con un signo &quot;+&quot;. Por ejemplo, si la versión de la biblioteca fuera 1.0.0 y la versión de la extensión de etiqueta fuera 1.2.0, el valor sería `1.0.0+1.2.0`.
* `commands`: estos son todos los comandos disponibles compatibles con la biblioteca cargada.
* `configs`: estas son todas las configuraciones actuales en la biblioteca cargada.
