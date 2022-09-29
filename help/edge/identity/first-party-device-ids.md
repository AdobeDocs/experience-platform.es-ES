---
title: ID de dispositivo de origen en el SDK web de Platform
description: Obtenga información sobre cómo configurar ID de dispositivos de origen (FPID) para el SDK web de Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 1%

---

# ID de dispositivo de origen en el SDK web de Platform

El SDK web de Adobe Experience Platform asigna [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) a los visitantes del sitio web mediante el uso de cookies para realizar un seguimiento del comportamiento del usuario. Para tener en cuenta las restricciones del explorador en los planes de vida de las cookies, puede optar por establecer y administrar sus propios identificadores de dispositivo. Estos se denominan ID de dispositivos de origen (FPID).

>[!NOTE]
>
>La compatibilidad con ID de dispositivo de origen solo está disponible al enviar datos a Platform Edge Network mediante el SDK web de Platform.

Este documento explica cómo configurar los ID de dispositivo de origen para la implementación del SDK web de Platform.

## Requisitos previos

En esta guía se asume que está familiarizado con el funcionamiento de los datos de identidad para el SDK web de la plataforma, incluida la función de los ECID y `identityMap`. Consulte la descripción general sobre [datos de identidad en el SDK web](./overview.md) para obtener más información.

## Uso de FPID

Los FPID realizan un seguimiento de los visitantes mediante el uso de cookies de origen. Las cookies de origen son más eficaces cuando se establecen con un servidor que aprovecha un DNS [Un registro](https://datatracker.ietf.org/doc/html/rfc1035) (para IPv4) o [Registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), a diferencia de un CNAME DNS o un código JavaScript.

>[!IMPORTANT]
>
>Los registros o registros AAAA solo se admiten para configurar y rastrear cookies. El método principal de recopilación de datos es mediante un CNAME DNS. En otras palabras, los FPID se establecen utilizando un registro A o AAAA, y luego se envían a Adobe mediante un CNAME.
>
>La variable [Programa de certificados administrados por Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) también es compatible con la recopilación de datos de origen.

Una vez establecida una cookie FPID, su valor se puede recuperar y enviar a Adobe a medida que se recopilan los datos del evento. Los FPID recopilados se utilizan como semillas para generar ECID, que siguen siendo los identificadores principales en las aplicaciones de Adobe Experience Cloud.

Para enviar un FPID para un visitante de un sitio web a la red perimetral de plataforma, debe incluir el FPID en la variable `identityMap` para ese visitante. Consulte la sección más adelante en este documento en [uso de FPID en `identityMap`](#identityMap) para obtener más información.

### Requisitos de formato de ID

La red perimetral de plataforma solo acepta ID que cumplan con la [Formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Los ID de dispositivo que no estén en formato UUIDv4 se rechazarán.

La generación de un UUID casi siempre resultará en un ID aleatorio único, con la probabilidad de que se produzca un conflicto insignificante. UUIDv4 no se puede enviar utilizando direcciones IP o cualquier otra información personal identificable (PII). Los UUID son ubicuos y se pueden encontrar bibliotecas para prácticamente todos los lenguajes de programación para generarlos.

## Configuración de una cookie con su propio servidor

Al configurar una cookie con un servidor que usted posee, se pueden utilizar diversos métodos para evitar que la cookie se restrinja debido a las políticas del explorador:

* Generar cookies mediante lenguajes de secuencias de comandos del lado del servidor
* Establecer cookies como respuesta a una solicitud de API realizada a un subdominio u otro extremo del sitio
* Generar cookies mediante un CMS
* Generar cookies mediante una CDN

>[!IMPORTANT]
>
>Cookies configuradas con el `document.cookie` casi nunca estará protegido de las políticas del explorador que restringen la duración de las cookies.

### Cuándo configurar la cookie

La cookie FPID debe configurarse de forma ideal antes de realizar cualquier solicitud a la red perimetral. Sin embargo, en los casos en que esto no sea posible, se sigue generando un ECID utilizando métodos existentes y actúa como identificador principal siempre que exista la cookie.

Suponiendo que el ECID se vea eventualmente afectado por una directiva de eliminación de explorador, pero el FPID no, el FPID se convertirá en el identificador principal de la próxima visita y se utilizará para sembrarlo en cada visita posterior.

### Configuración de la caducidad de la cookie

Configurar la caducidad de una cookie es algo que debe considerarse cuidadosamente a medida que implementa la funcionalidad FPID. Al tomar esta decisión, debe tener en cuenta los países o regiones en los que opera su organización, junto con las leyes y políticas de cada una de esas regiones.

Como parte de esta decisión, es posible que desee adoptar una directiva de configuración de cookies para toda la empresa o una que varíe para los usuarios en cada configuración regional donde opere.

Independientemente del ajuste que elija para la caducidad inicial de una cookie, debe asegurarse de incluir una lógica que amplíe la caducidad de la cookie cada vez que se produzca una nueva visita al sitio.

## Impacto de los indicadores de cookies

Existen diversos indicadores de cookies que afectan al modo en que se tratan las cookies en los distintos navegadores:

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Las cookies configuradas mediante la variable `HTTPOnly` no se puede acceder al indicador mediante secuencias de comandos del lado del cliente. Esto significa que si establece un `HTTPOnly` al configurar FPID, debe aprovechar un lenguaje de secuencias de comandos del lado del servidor para leer el valor de la cookie para incluirlo en la variable `identityMap`.

Si decide que Platform Edge Network lea el valor de la cookie FPID, configurando la variable `HTTPOnly` este indicador garantizará que no se pueda acceder al valor desde ninguna secuencia de comandos del lado del cliente, pero no tendrá ningún impacto negativo en la capacidad de lectura de la cookie de Platform Edge Network.

>[!NOTE]
>
>Uso del `HTTPOnly` El indicador no afecta a las políticas de cookies que pueden restringir la duración de las cookies. Sin embargo, sigue siendo algo que debe tener en cuenta a medida que establece y lee el valor de FPID.

### `Secure` {#secure}

Las cookies configuradas con la variable `Secure` solo se envían al servidor con una solicitud cifrada a través del protocolo HTTPS. El uso de este indicador puede ayudar a garantizar que los atacantes intermediarios no puedan acceder fácilmente al valor de la cookie. Siempre que sea posible, es aconsejable configurar la variable `Secure` indicador.

### `SameSite` {#same-site}

La variable `SameSite` permite a los servidores determinar si las cookies se envían con solicitudes entre sitios. El atributo proporciona cierta protección contra los ataques de falsificación entre sitios. Existen tres valores posibles: `Strict`, `Lax` y `None`. Consulte con su equipo interno para determinar qué configuración es la adecuada para su organización.

Si no `SameSite` se especifica, la configuración predeterminada para algunos exploradores ahora es `SameSite=Lax`.

## Uso de FPID en `identityMap` {#identityMap}

A continuación, se muestra un ejemplo de cómo establecería un FPID por su cuenta en el `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Al igual que con otros tipos de identidad, puede incluir el FPID con otras identidades dentro de `identityMap`. El siguiente es un ejemplo de FPID incluido con un ID de CRM autenticado:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Si el FPID está contenido en una cookie que está leyendo la red perimetral cuando la recopilación de datos de origen está habilitada, solo debe capturar el ID de CRM autenticado:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Lo siguiente `identityMap` resultaría en una respuesta de error de la red perimetral, ya que falta la variable `primary` indicador de FPID. Por lo menos uno de los ID presentes en `identityMap` debe marcarse como `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

La respuesta de error devuelta por Experience Edge en este caso sería similar a la siguiente:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## Jerarquía de ID

Cuando haya un ECID y un FPID presentes, se dará prioridad al ECID para identificar al usuario. Esto garantizará que, cuando haya un ECID existente en el almacén de cookies del explorador, siga siendo el identificador principal y los recuentos de visitantes existentes no corran el riesgo de verse afectados. Para los usuarios existentes, el FPID no se convertirá en la identidad principal hasta que el ECID caduque o se elimine como resultado de una directiva del navegador o de un proceso manual.

Las identidades tienen prioridad en el siguiente orden:

1. ECID incluido en el `identityMap`
1. ECID almacenado en una cookie
1. FPID incluido en el `identityMap`
1. FPID almacenado en una cookie

## Migración a ID de dispositivos de origen

Si va a usar FPID desde una implementación anterior, puede que sea difícil visualizar el aspecto de la transición en un nivel bajo.

Para ayudar a ilustrar este proceso, considere un escenario que involucre a un cliente que previamente ha visitado su sitio y que impacto tendría una migración de FPID en la forma en que se identifica a ese cliente en las soluciones de Adobe.

![Diagrama que muestra cómo se actualizan los valores de ID de un cliente entre visitas después de migrar a FPID](../assets/identity/tracking/visits.png)

| Visita | Descripción |
| --- | --- |
| Primera visita | Supongamos que aún no ha empezado a configurar la cookie FPID. El ECID contenido en la variable [Cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) será el identificador utilizado para identificar al visitante. |
| Segunda visita | Se ha iniciado el despliegue de la solución de ID de dispositivo de origen. El ECID existente sigue estando presente y sigue siendo el identificador principal para la identificación del visitante. |
| Tercera visita | Entre la segunda y la tercera visita, ha transcurrido una cantidad de tiempo suficiente para que el ECID se haya eliminado debido a la política del explorador. Sin embargo, como el FPID se estableció utilizando un registro A de DNS, el FPID persiste. Ahora el FPID se considera el ID principal y se utiliza para iniciar el ECID, que se escribe en el dispositivo de usuario final. Ahora el usuario sería considerado un visitante nuevo en las soluciones de Adobe Experience Platform y Experience Cloud . |
| Cuarta visita | Entre la tercera y la cuarta visita, ha transcurrido un tiempo suficiente para que el ECID se haya eliminado debido a la política del navegador. Al igual que en la visita anterior, el FPID se mantiene debido a la forma en que se configuró. Esta vez, se genera el mismo ECID que la visita anterior. El usuario se ve en todas las soluciones del Experience Platform y del Experience Cloud como el mismo usuario que en la visita anterior. |
| Quinta visita | Entre la cuarta y la quinta visita, el usuario final borró todas las cookies de su explorador. Se genera un nuevo FPID que se utiliza para iniciar la creación de un nuevo ECID. Ahora el usuario sería considerado un visitante nuevo en las soluciones de Adobe Experience Platform y Experience Cloud . |

{style=&quot;table-layout:auto&quot;}

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre los ID de dispositivos de origen.

### ¿En qué se diferencia la inicialización de un ID de la simple generación de un ID?

El concepto de sembrado es único, ya que el FPID pasado a Adobe Experience Cloud se convierte en un ECID mediante un algoritmo determinista. Cada vez que se envía el mismo FPID a la red perimetral de Adobe Experience Platform, el mismo ECID se envía desde el FPID.

### ¿Cuándo se debe generar el ID del dispositivo de origen?

Para reducir la posible inflación de visitantes, el FPID debe generarse antes de realizar la primera solicitud utilizando el SDK web de Platform. Sin embargo, si no puede hacerlo, se generará un ECID para ese usuario y se utilizará como identificador principal. El FPID que se generó no pasará a ser el identificador principal hasta que el ECID ya no esté presente.

### ¿Qué métodos de recopilación de datos admiten los ID de dispositivos de origen?

Actualmente, solo el SDK web de Platform admite FPID.

### ¿Los FPID se almacenan en cualquier plataforma o solución de Experience Cloud?

Una vez que se ha utilizado el FPID para iniciar un ECID, se abandona del `identityMap` y sustituido por el ECID que se ha generado. El FPID no se almacena en ninguna solución de Adobe Experience Platform o Experience Cloud.
