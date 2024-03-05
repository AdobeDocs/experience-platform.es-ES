---
title: Configuración de un CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo configurar un CSP para el SDK web de Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurar;configuración;SDK;edge;SDK web;configurar;contexto;web;dispositivo;entorno;configuración de sdk web;directiva de seguridad de contenido;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configuración de un CSP

A [Política de seguridad de contenido](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) se utiliza para restringir los recursos que un explorador puede utilizar. El CSP también puede limitar la funcionalidad de los recursos de script y estilo. El SDK web de Adobe Experience Platform no requiere un CSP, pero añadir uno puede reducir la superficie de ataque para evitar ataques malintencionados.

El CSP debe reflejar cómo [!DNL Platform Web SDK] se implementa y configura. El siguiente CSP muestra qué cambios pueden ser necesarios para que el SDK funcione correctamente. Es probable que se requiera una configuración CSP adicional, según el entorno específico.

## Ejemplo de política de seguridad de contenido

Los siguientes ejemplos muestran cómo configurar un CSP.

### Permitir el acceso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

En el ejemplo anterior, `EDGE-DOMAIN` debe reemplazarse por el dominio de origen. El dominio de origen está configurado para [edgeDomain](../commands/configure/edgedomain.md) configuración. Si no se ha configurado ningún dominio de origen, `EDGE-DOMAIN` debe reemplazarse por `*.adobedc.net`. Si la migración de visitantes está activada mediante [idMigrationEnabled](../commands/configure/idmigrationenabled.md), el `connect-src` la directiva también debe incluir `*.demdex.net`.

### Utilice NONCE para permitir elementos de estilo y scripts en línea

[!DNL Platform Web SDK] Puede modificar el contenido de la página y debe aprobarse para crear etiquetas de estilo y script en línea. Para ello, Adobe recomienda utilizar un nonce para [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) Directiva CSP. Un nonce es un token aleatorio criptográficamente fuerte generado por el servidor que se genera una vez por cada vista de página única.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Además, el nonce de CSP debe agregarse como atributo al [!DNL Platform Web SDK] [código base](../install/library.md) etiqueta de script. [!DNL Platform Web SDK] utilizará ese nonce cuando añada scripts en línea o etiquetas de estilo a la página:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si no se utiliza un nonce, la otra opción es añadir `unsafe-inline` a la `script-src` y `style-src` Directivas CSP:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>El Adobe sí **no** se recomienda especificar `unsafe-inline` porque permite que cualquier script se ejecute en la página, lo que limita las ventajas del CSP.

## Configuración de un CSP para mensajería en la aplicación {#in-app-messaging}

Al configurar [Mensajería en la aplicación web](../personalization/web-in-app-messaging.md), debe incluir la siguiente directiva en su CSP:

```
default-src  blob:;
```
