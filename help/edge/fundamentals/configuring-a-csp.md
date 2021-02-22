---
title: Configuración de un CSP
seo-title: Configuración de un CSP para Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo configurar un CSP para el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo configurar un CSP para el SDK web de Experience Platform
keywords: configurar;configuración;SDK;edge;Web SDK;configurar;contexto;web;dispositivo;entorno;configuración de Web sdk;directiva de seguridad de contenido;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# Configuración de un CSP

Se utiliza una [Política de seguridad de contenido](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) para restringir los recursos que un explorador puede utilizar. El CSP también puede limitar la funcionalidad de los recursos de script y estilo. El SDK web de Adobe Experience Platform no requiere un CSP, pero si se agrega uno puede reducir la superficie de ataque para evitar ataques malintencionados.

El CSP debe reflejar cómo [!DNL Platform Web SDK] se implementa y se configura. El siguiente CSP muestra los cambios que pueden ser necesarios para que el SDK funcione correctamente. Es probable que se requiera una configuración CSP adicional, según el entorno específico.

## Ejemplo de directiva de seguridad de contenido

Los siguientes ejemplos muestran cómo configurar un CSP.

### Permitir el acceso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

En el ejemplo anterior, `EDGE-DOMAIN` debe reemplazarse por el dominio de origen. El dominio de origen está configurado para la configuración [edgeDomain](configuring-the-sdk.md#edge-domain). Si no se ha configurado ningún dominio de origen, `EDGE-DOMAIN` debe reemplazarse por `*.adobedc.net`. Si se activa la migración de visitantes mediante [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), la directiva `connect-src` también debe incluir `*.demdex.net`.

### Utilice NONCE para permitir elementos de estilo y secuencia de comandos en línea

[!DNL Platform Web SDK] puede modificar el contenido de la página y debe aprobarse para crear etiquetas de estilo y script en línea. Para lograrlo, Adobe recomienda utilizar un valor nonce para la directiva [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP. Una cadena nonce es un token aleatorio cifrado y seguro generado por el servidor que se genera una vez por cada vista de página única.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Además, la cadena nonce CSP debe agregarse como un atributo a la etiqueta de script [!DNL Platform Web SDK] [base code](installing-the-sdk.md#adding-the-code). [!DNL Platform Web SDK] a continuación, utilizará esa cadena nonce al agregar etiquetas de estilo o script en línea a la página:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si no se utiliza una cadena nonce, la otra opción es agregar `unsafe-inline` a las directivas `script-src` y `style-src` CSP:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe **no** recomienda especificar `unsafe-inline` porque permite que se ejecute cualquier script en la página, lo que limita los beneficios del CSP.
