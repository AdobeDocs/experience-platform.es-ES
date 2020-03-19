---
title: Interactuar con varias propiedades
seo-title: SDK web de Adobe Experience Platform Interactuar con varias propiedades
description: Descubra cómo interactuar con varias propiedades del SDK web de la plataforma de experiencia
seo-description: Descubra cómo interactuar con varias propiedades del SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Interactuar con varias propiedades

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Hay algunos casos en los que podría interesarle interactuar con dos propiedades diferentes en la misma página. Son:

* Empresas que han sido adquiridas y que están trabajando en la integración de sus sitios web
* Relaciones de intercambio de datos entre varias empresas
* Clientes que están probando nuevas soluciones de Adobe y que no desean interrumpir su implementación existente

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
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("event", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("event", {
  "data": {
    "key": "value"
  }
});
```

Asegúrese de ejecutar el comando `configure` para cada instancia antes de ejecutar otros comandos en la misma instancia.

## Limitaciones

Para evitar conflictos con las cookies, solo una instancia del SDK web de Adobe Experience Platform dentro de una página puede tener un `configId`.  Del mismo modo, solo una instancia del SDK web de Adobe Experience Platform puede tener un `orgId`.
