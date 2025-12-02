---
title: Uso de varias instancias de Web SDK
description: Aprenda a interactuar con varias propiedades de Experience Platform Web SDK.
keywords: varias propiedades
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 2c60ebdebd706ed7b5beb2438ae83665b6b6e47a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Uso de varias instancias de Web SDK

Hay ciertos casos en los que es posible que desee interactuar con dos propiedades diferentes en la misma página. Estos casos incluyen:

* Compañías que han sido adquiridas y están trabajando en la integración de sus sitios web juntos
* Relaciones de uso compartido de datos entre varias empresas
* Clientes que están probando nuevas soluciones de Adobe y no desean interrumpir la implementación existente

SDK permite crear una instancia independiente para cada propiedad agregando otro nombre a la matriz en el código base. El ejemplo siguiente proporciona dos nombres, `titanium` y `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, la secuencia de comandos crea dos instancias de SDK. La función global para interactuar con la primera instancia se denomina `titanium` y la función global para interactuar con la segunda instancia se denomina `copper`.

Al crear dos instancias independientes, cada una se puede configurar para una propiedad diferente. Cualquier comunicación o persistencia de datos que se produzca debido a la interacción con `titanium` se mantiene aislada de `copper`.

Después del ejemplo anterior, puede ejecutar comandos utilizando cada instancia:

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

Asegúrese de ejecutar el comando `configure` para cada instancia antes de ejecutar otros comandos en la misma instancia.

>[!IMPORTANT]
>
>Para evitar conflictos con las cookies, cada instancia de Web SDK debe tener su propio `datastreamId` único y su propio `orgId` único.
