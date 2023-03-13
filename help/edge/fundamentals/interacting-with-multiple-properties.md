---
title: Interacción con varias propiedades en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo interactuar con varias propiedades del SDK web de Experience Platform.
keywords: varias propiedades;configurar;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Interactuar con varias propiedades

Hay ciertos casos en los que es posible que desee interactuar con dos propiedades diferentes en la misma página. Estos casos incluyen:

* Compañías que han sido adquiridas y están trabajando en la integración de sus sitios web juntos
* Relaciones de uso compartido de datos entre varias empresas
* Clientes que están probando nuevas soluciones de Adobe y no desean interrumpir la implementación existente

El SDK permite crear una instancia independiente para cada propiedad añadiendo otro nombre a la matriz en el código base. El ejemplo siguiente proporciona dos nombres, `mycustomname1` y `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, el script crea dos instancias del SDK. La función global para interactuar con la primera instancia se denomina `mycustomname1` y la función global para interactuar con la segunda instancia se denomina `mycustomname2`.

Al crear dos instancias independientes, cada una se puede configurar para una propiedad diferente. Cualquier comunicación o persistencia de datos que se produzca debido a la interacción con `mycustomname1` se mantiene aislado de `mycustomname2`.

Después del ejemplo anterior, puede ejecutar comandos utilizando cada una de las instancias de la siguiente manera:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Asegúrese de ejecutar el `configure` antes de ejecutar otros comandos en la misma instancia.

## Limitaciones

Para evitar conflictos con las cookies, solo se necesita una instancia de Adobe Experience Platform [!DNL Web SDK] dentro de una página puede tener un `edgeConfigId`. Del mismo modo, solo se permite una instancia de Adobe Experience Platform [!DNL Web SDK] puede tener un `orgId`.
