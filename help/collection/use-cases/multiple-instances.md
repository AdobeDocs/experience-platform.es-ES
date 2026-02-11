---
title: Uso de varias instancias de Web SDK
description: Aprenda a interactuar con varias propiedades de Experience Platform Web SDK.
keywords: varias propiedades
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Uso de varias instancias de Web SDK

Hay ciertos casos en los que es posible que desee interactuar con dos propiedades diferentes en la misma página. Los escenarios posibles incluyen:

* Compañías que han sido adquiridas y están trabajando en la integración de sus sitios web juntos
* Relaciones de uso compartido de datos entre varias empresas
* Clientes que están probando nuevas soluciones de Adobe y no desean interrumpir la implementación existente

SDK le permite crear una instancia independiente para cada propiedad agregando otro nombre a la matriz en [código base](../js/install/base-code.md). El ejemplo siguiente proporciona dos nombres, `titanium` y `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Como resultado, el script crea dos funciones globales (`titanium` y `copper` en el ejemplo anterior) que se convierten en dos instancias de SDK cuando se inicializa la biblioteca. Cada instancia mantiene su propia configuración y estado; cualquier comando que utilice `titanium` se mantiene aislado de `copper`.

>[!TIP]
>
>Si usa el código base con etiquetas, asegúrese de que todos los nombres de instancia que establezca coincidan con todos los [nombres de instancia de SDK](/help/tags/extensions/client/web-sdk/configure/general.md) al configurar la extensión de etiqueta.

Siguiendo el ejemplo del patrón de nomenclatura de `titanium` y `copper` como instancias de Web SDK, puede ejecutar comandos de forma independiente:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Asegúrese de ejecutar el comando [`configure`](../js/commands/configure/overview.md) para cada instancia antes de ejecutar otros comandos en la misma instancia.

>[!IMPORTANT]
>
>Para evitar conflictos con las cookies, cada instancia de Web SDK debe tener su propio `datastreamId` único y su propio `orgId` único.
