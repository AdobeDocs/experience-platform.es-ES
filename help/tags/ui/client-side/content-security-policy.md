---
title: Ayuda sobre Política de seguridad de contenido (CSP)
description: Obtenga información sobre cómo lidiar con las restricciones de la Política de seguridad de contenido (CSP) al integrar su sitio web con etiquetas en Adobe Experience Platform.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 97%

---

# Ayuda sobre Política de seguridad de contenido (CSP)

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una directiva de seguridad de contenido (CSP) es una función de seguridad que ayuda a evitar ataques de secuencias de comandos entre sitios (XSS). Esto sucede cuando se engaña al explorador para que ejecute contenido malicioso que parece provenir de una fuente de confianza, pero que realmente proviene de otro lugar. Los CSP permiten al navegador (en nombre del usuario) verificar que el script viene de una fuente de confianza.

Los CSP se implementan agregando un encabezado HTTP `Content-Security-Policy` a las respuestas del servidor o agregando un elemento `<meta>` configurado en la sección `<head>` de los archivos HTML.

>[!NOTE]
>
> Para obtener información más detallada sobre los CSP, consulte los [documentos web de MDN](https://developer.mozilla.org/es/docs/Web/HTTP/CSP).

Las etiquetas de Adobe Experience Platform son un sistema de administración de etiquetas diseñado para cargar dinámicamente scripts en su sitio web. Un CSP predeterminado bloquea estas secuencias de comandos cargadas dinámicamente debido a posibles problemas de seguridad. Este documento proporciona instrucciones sobre cómo configurar el CSP para permitir scripts cargados dinámicamente desde etiquetas.

Si quiere que las etiquetas funcionen con su CSP, existen dos desafíos principales que se deben superar:

* **El origen de la biblioteca de etiquetas debe ser de confianza.** Si no se cumple esta condición, el explorador bloqueará la biblioteca de etiquetas y otros archivos JavaScript necesarios y no se cargarán en la página.
* **Se deben permitir los scripts en línea.** Si no se cumple esta condición, las acciones de regla de código personalizado se bloquean en la página y no se ejecutan correctamente.

El aumento de la seguridad requiere una mayor cantidad de trabajo en nombre del creador de contenido. Si desea utilizar etiquetas y dispone de un CSP, debe corregir ambos problemas sin marcar incorrectamente otros scripts como seguros. El resto de este documento ofrece instrucciones sobre cómo lograrlo.

## Adición de etiquetas como fuente de confianza

Al utilizar un CSP, debe incluir todos los dominios de confianza dentro del valor del encabezado `Content-Security-Policy`. El valor que debe proporcionar para las etiquetas variará según el tipo de alojamiento que utilice.

### Alojamiento propio

Si está [alojando su biblioteca usted mismo](../publishing/hosts/self-hosting-libraries.md), la fuente de su biblioteca es probablemente su propio dominio. Puede especificar que el dominio host es un origen seguro mediante la siguiente configuración:

**Encabezado HTTP**

```http
Content-Security-Policy: script-src 'self'
```

**Etiqueta `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Alojamiento administrado por Adobe

Si utiliza un host [administrado por Adobe](../publishing/hosts/managed-by-adobe-host.md), la compilación se mantiene en `assets.adobedtm.com`. Debe especificar `self` como dominio seguro para que no se rompan los scripts que ya se están cargando, pero también necesita que `assets.adobedtm.com` aparezca como seguro o la biblioteca de etiquetas no se cargará en la página. En este caso, debe utilizar la siguiente configuración:

**Encabezado HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**Etiqueta `<meta>` HTML**


Hay un requisito previo muy importante: debe cargar la biblioteca de etiquetas [asíncronas](./asynchronous-deployment.md). Esto no funciona con una carga sincrónica de la biblioteca de etiquetas (lo que provoca errores de consola y reglas que no se ejecutan correctamente).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Debe especificar `self` como dominio seguro para que no se rompan los scripts que ya se están cargando, pero también necesita que `assets.adobedtm.com` aparezca como origen seguro o la compilación de la biblioteca no se cargará en la página.

## Scripts en línea

CSP deshabilita los scripts en línea de forma predeterminada y, por lo tanto, debe configurarse manualmente para permitirlos. Tiene dos opciones para permitir scripts en línea:

* [Permitir a través de nonce](#nonce) (buena seguridad)
* [Permitir todos los scripts en línea](#unsafe-inline) (menos seguro)

>[!NOTE]
>
>La especificación CSP tiene detalles para una tercera opción mediante hashes, pero este método no es viable con sistemas de administración de etiquetas como las etiquetas. Para obtener más información sobre las limitaciones del uso de hashes con etiquetas en Experience Platform, consulte la [guía de integridad de subrecursos (SRI)](./sri.md).

### Permitir a través de nonce {#nonce}

Este método implica generar una cadena nonce criptográfica y agregarla a su CSP y a cada script en línea de su sitio. Cuando el explorador recibe una instrucción para cargar un script en línea con una cadena nonce, el explorador compara el valor nonce con el contenido en el encabezado CSP. Si coincide, se carga la secuencia de comandos. Esta cadena nonce debe cambiarse con cada nueva carga de página.

>[!IMPORTANT]
>
>Para utilizar este método, debe cargar la compilación asincrónicamente. Esto no funciona al cargar la compilación sincrónicamente, lo que provoca que los errores de la consola y las reglas no se ejecuten correctamente. Consulte la guía de [implementación asincrónica](./asynchronous-deployment.md) para obtener más información.

Los ejemplos siguientes muestran cómo se puede agregar nonce a la configuración CSP para un host administrado por Adobe. Si utiliza alojamiento propio, puede excluir `assets.adobedtm.com`.

**Encabezado HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**Etiqueta `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Una vez configurado el encabezado o la etiqueta HTML, debe indicar a la etiqueta dónde buscar la cadena nonce al cargar un script en línea. Para que una etiqueta use el nonce cuando carga el script, debe:

1. Crear un elemento de datos que haga referencia a dónde se encuentra la cadena nonce en la capa de datos.
1. Configurar la extensión principal y especificar qué elemento de datos ha utilizado.
1. Publicar los cambios de su elemento de datos y extensión principal.

>[!NOTE]
>
>El proceso anterior solo controla la carga del código personalizado, no lo que hace ese código personalizado. Si un script en línea contiene código personalizado que no es compatible con el CSP, este tiene prioridad. Por ejemplo, si utiliza un código personalizado para cargar scripts en línea anexándolos al DOM, la etiqueta no podrá añadir el nonce correctamente, así que la acción de ese código personalizado en particular no funcionará como se esperaba.

### Permitir todos los scripts en línea {#unsafe-inline}

Si usar nonces no funciona, puede configurar su CSP para que permita los scripts en línea. Esta es la opción menos segura, pero también más fácil de implementar y mantener.

Los ejemplos siguientes muestran cómo se pueden permitir todos los scripts en línea en el encabezado CSP.

#### Alojamiento propio

Utilice las siguientes configuraciones si utiliza el alojamiento propio:

**Encabezado HTTP**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**Etiqueta `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Alojamiento administrado por Adobe

Utilice las siguientes configuraciones si utiliza alojamiento administrado por Adobe:

**Encabezado HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**Etiqueta `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Pasos siguientes

Al leer este documento, debería haber comprendido cómo configurar el encabezado CSP para aceptar el archivo de biblioteca de etiquetas y los scripts en línea.

Como medida de seguridad adicional, también puede optar por utilizar la integridad de los subrecursos (SRI) para validar las compilaciones de biblioteca recuperadas. Sin embargo, esta funcionalidad tiene algunas limitaciones importantes cuando se utiliza con sistemas de administración de etiquetas como las etiquetas. Consulte la guía sobre la compatibilidad con la SRI [en Experience Platform](./sri.md) para obtener más información.
