---
title: Depuración
seo-title: Depuración del SDK web de Adobe Experience Platform
description: Aprenda a alternar la depuración del SDK web de la plataforma de experiencia
seo-description: Aprenda a alternar la depuración del SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Depuración

Cuando la depuración está habilitada, el SDK envía mensajes a la consola del navegador que pueden resultar útiles para depurar la implementación y para comprender el comportamiento del SDK. La depuración también resulta en una validación sincrónica del lado del servidor de los datos que se recopilan con el esquema que ha configurado.

La depuración está deshabilitada de forma predeterminada, pero se puede alternar de tres formas diferentes:

* `configure` command
* `setDebug` command
* Parámetro de cadena de consulta

## Alternar la depuración con el comando Configurar

Al configurar el SDK mediante el `configure` comando, habilite la depuración estableciendo la `debugEnabled` opción en `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Esto habilita la depuración para todos los usuarios de la página web en lugar de solo para su explorador personal.

## Alternar la depuración con el comando Depurar

Alternar la depuración con un comando independiente `debug` como se indica a continuación:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si prefiere no cambiar el código de la página web o no desea que los mensajes de registro se produzcan para todos los usuarios del sitio web, esto es especialmente útil porque puede ejecutar el `debug` comando en la consola JavaScript del explorador en cualquier momento.

## Alternar la depuración con un parámetro de cadena de consulta

Alternar la depuración estableciendo un parámetro de cadena de `alloy_debug` consulta en `true` o `false` como se indica a continuación:

```HTTP
http://example.com/?alloy_debug=true
```

De forma similar al `debug` comando, si prefiere no cambiar el código de la página web o no desea que los mensajes de registro se produzcan para todos los usuarios del sitio web, esto es especialmente útil porque puede configurar el parámetro de cadena de consulta al cargar la página web en el explorador.

## Prioridad y duración

Cuando la depuración se establece mediante el comando `debug` o el parámetro de cadena de consulta, anula cualquier `debug` opción establecida en el `configure` comando. En estos dos casos, la depuración también permanece alternada durante toda la sesión. En otras palabras, si se habilita la depuración mediante el comando debug o el parámetro de cadena de consulta, permanece habilitado hasta que se cumpla una de las siguientes condiciones:

* El final de la sesión
* Ejecute el `debug` comando
* El parámetro de cadena de consulta se establece de nuevo
