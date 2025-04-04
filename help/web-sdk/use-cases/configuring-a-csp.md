---
title: Configuración de un CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo configurar un CSP para Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurar;configuración;SDK;edge;Web SDK;configurar;contexto;web;dispositivo;entorno;configuración de sdk web;directiva de seguridad de contenido;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configuración de un CSP

Se usa una [Política de seguridad de contenido](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) para restringir los recursos que un explorador puede usar. El CSP también puede limitar la funcionalidad de los recursos de script y estilo. Adobe Experience Platform Web SDK no requiere un CSP, pero añadir uno puede reducir la superficie de ataque para evitar ataques malintencionados.

El CSP necesita reflejar cómo se implementa y configura [!DNL Experience Platform Web SDK]. El siguiente CSP muestra qué cambios pueden ser necesarios para que SDK funcione correctamente. Es probable que se requiera una configuración CSP adicional, según el entorno específico.

## Ejemplo de política de seguridad de contenido

Los siguientes ejemplos muestran cómo configurar un CSP.

### Permitir el acceso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

En el ejemplo anterior, `EDGE-DOMAIN` debe reemplazarse con el dominio de origen. El dominio de origen está configurado para la configuración [edgeDomain](../commands/configure/edgedomain.md). Si no se ha configurado ningún dominio de origen, `EDGE-DOMAIN` debe reemplazarse por `*.adobedc.net`. Si la migración de visitantes está activada mediante [idMigrationEnabled](../commands/configure/idmigrationenabled.md), la directiva `connect-src` también debe incluir `*.demdex.net`.

### Utilice NONCE para permitir elementos de estilo y scripts en línea

[!DNL Experience Platform Web SDK] puede modificar el contenido de la página y debe aprobarse para crear etiquetas de estilo y script en línea. Para ello, Adobe recomienda utilizar un nonce para la directiva CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Un nonce es un token aleatorio criptográficamente fuerte generado por el servidor que se genera una vez por cada vista de página única.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Además, el nonce de CSP debe agregarse como atributo a la etiqueta de script [!DNL Experience Platform Web SDK] [código base](../install/library.md). [!DNL Experience Platform Web SDK] usará ese nonce cuando agregue etiquetas de estilo o script en línea a la página:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si no se usa un nonce, la otra opción es agregar `unsafe-inline` a las directivas CSP `script-src` y `style-src`:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe recomienda **not** especificar `unsafe-inline` porque permite que se ejecute cualquier script en la página, lo que limita los beneficios del CSP.

## Configuración de un CSP para mensajería en la aplicación {#in-app-messaging}

Al configurar [Mensajería en la aplicación web](../personalization/web-in-app-messaging.md), debe incluir la siguiente directiva en su CSP:

```
default-src  blob:;
```
