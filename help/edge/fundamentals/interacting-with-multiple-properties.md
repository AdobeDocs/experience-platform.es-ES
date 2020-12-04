---
title: Interactuar con varias propiedades
seo-title: SDK web de Adobe Experience Platform que interactúa con varias propiedades
description: Descubra cómo interactuar con varias propiedades del SDK web de Experience Platform
seo-description: Descubra cómo interactuar con varias propiedades del SDK web de Experience Platform
keywords: multiple properties;configure;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 1%

---


# Interactuar con varias propiedades

Hay algunos casos en los que podría interesarle interactuar con dos propiedades diferentes en la misma página. Se incluyen:

* Compañías que se han adquirido y que están trabajando en la integración de sus sitios web
* Relaciones de uso compartido de datos entre varias compañías
* Clientes que están probando nuevas soluciones de Adobe y no desean interrumpir su implementación existente

El SDK permite crear una instancia independiente para cada propiedad agregando otro nombre a la matriz en el código base. En el siguiente ejemplo, hemos proporcionado dos nombres `mycustomname1` y `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, la secuencia de comandos crea dos instancias del SDK. Se nombra la función global para interactuar con la primera instancia `mycustomname1` y se asigna un nombre a la función global para interactuar con la segunda instancia `mycustomname2`.

Al crear dos instancias independientes, cada una se puede configurar para una propiedad diferente. Cualquier persistencia de comunicación o datos que se produzca debido a la interacción con `mycustomname1` se mantiene aislada de `mycustomname2` y viceversa.

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

Asegúrese de ejecutar el `configure` comando para cada instancia antes de ejecutar otros comandos en la misma instancia.

## Limitaciones

Para evitar conflictos con las cookies, solo una instancia de Adobe Experience Platform [!DNL Web SDK] dentro de una página puede tener un `edgeConfigId`.  Del mismo modo, solo una instancia de Adobe Experience Platform [!DNL Web SDK] puede tener un `orgId`.
