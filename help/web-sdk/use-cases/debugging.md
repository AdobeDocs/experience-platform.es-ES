---
title: Métodos de depuración
description: Obtenga información sobre cómo alternar las funcionalidades de depuración en el SDK web.
keywords: depurar sdk web;depuración;depurar comando;setDebug;debugEnabled;depurar
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Métodos de depuración

Cuando la depuración está habilitada, el SDK web envía mensajes a la consola del explorador que pueden resultar útiles para depurar la implementación. La depuración es útil cuando desea comprender cómo se comporta el SDK según las reglas y los elementos de datos que haya establecido.

La depuración está deshabilitada de forma predeterminada, pero se puede activar de cuatro formas diferentes. Puede utilizar cualquier combinación de estos métodos para habilitar o deshabilitar la depuración de la forma más adecuada para el flujo de trabajo de desarrollo.

## Usar `debugEnabled` en el comando `configure`

Establezca el booleano `debugEnabled` en true al configurar la extensión. Esta opción se utiliza generalmente para entornos de desarrollo, ya que permite depurar a todos los que visiten cualquier página del sitio:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

Consulte [`debugEnabled`](../commands/configure/debugenabled.md) para obtener más información.

## Usar el comando `setDebug`

De forma similar al booleano anterior, este comando habilita la depuración en todos los visitantes de la página.

```js
alloy("setDebug", {"enabled": true});
```

Consulte el comando [`setDebug`](../commands/setdebug.md) para obtener más información.

## Establecer un parámetro de cadena de consulta

Puede habilitar la depuración agregando la cadena de consulta `?alloy_debug=true` al final de cualquier dirección URL. Por ejemplo:

`http://example.com/?alloy_debug=true`

Este método solo se aplica al equipo local, lo que le permite depurar sitios web de producción sin habilitar la depuración para todos. La activación de la depuración de esta manera permanece activada durante el resto de la sesión de navegación o hasta que la desactive.

## Usar el Adobe Experience Platform Debugger

El Adobe Experience Platform Debugger es una potente herramienta que examina sus páginas web y le ayuda a depurar la implementación de productos de Experience Cloud. Puede habilitar la depuración desde la pestaña Configuración de la sección SDK web de AEP.

![Habilitar depurador](../assets/enable-debugging.png)

Consulte [descripción general del Adobe Experience Platform Debugger](/help/debugger/home.md) para obtener más información.
