---
title: Interaccione con varias propiedades en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo interactuar con varias propiedades del SDK web de Experience Platform.
keywords: varias propiedades;configurar;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Interaccione con varias propiedades

En algunos casos, es posible que desee interactuar con dos propiedades diferentes en la misma página. Estos casos incluyen:

* Empresas que han adquirido y están trabajando en la integración de sus sitios web
* Relaciones de intercambio de datos entre varias empresas
* Clientes que están probando nuevas soluciones de Adobe y que no desean interrumpir su implementación existente

El SDK permite crear una instancia independiente para cada propiedad añadiendo otro nombre a la matriz en el código base. El siguiente ejemplo proporciona dos nombres, `mycustomname1` y `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, la secuencia de comandos crea dos instancias del SDK. La función global para interactuar con la primera instancia se llama `mycustomname1` y la función global para interactuar con la segunda instancia se llama `mycustomname2`.

Al crear dos instancias independientes, cada una se puede configurar para una propiedad diferente. Cualquier comunicación o persistencia de datos que se produzca debido a la interacción con `mycustomname1` se mantiene aislada de `mycustomname2`.

Siguiendo el ejemplo anterior, puede ejecutar comandos utilizando cada una de las instancias, de la siguiente manera:

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

Asegúrese de ejecutar el comando `configure` para cada instancia antes de ejecutar otros comandos en la misma instancia.

## Limitaciones

Para evitar conflictos con las cookies, solo una instancia de Adobe Experience Platform [!DNL Web SDK] dentro de una página puede tener un `edgeConfigId` en particular. Del mismo modo, solo una instancia de Adobe Experience Platform [!DNL Web SDK] puede tener un `orgId` concreto.
