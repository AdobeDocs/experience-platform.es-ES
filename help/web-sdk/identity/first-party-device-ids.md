---
title: ID de dispositivos de origen en el SDK web
description: Obtenga información sobre cómo configurar los ID de dispositivos de origen (FPID) para el SDK web de Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 9f10d48357b7fb28dc54375a4d077d0a1961a746
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---


# ID de dispositivos de origen en el SDK web

El SDK web de Adobe Experience Platform asigna [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=es) a los visitantes del sitio web mediante cookies para realizar un seguimiento del comportamiento del usuario. Para tener en cuenta las restricciones del explorador sobre la duración de las cookies, puede optar por establecer y administrar sus propios identificadores de dispositivo en su lugar. Estos se denominan ID de dispositivos de origen (FPID).

>[!NOTE]
>
>La compatibilidad con ID de dispositivos de origen solo está disponible al enviar datos al Edge Network de Platform a través del SDK web de Platform.

>[!IMPORTANT]
>
>Los ID de dispositivos de origen no son compatibles con la funcionalidad [cookies de terceros](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) del SDK web.
>Puede usar ID de dispositivos de origen o cookies de terceros, pero no puede usar ambas funciones simultáneamente.

Este documento explica cómo configurar los ID de dispositivos de origen para la implementación del SDK web de Platform.

## Requisitos previos

En esta guía se da por hecho que está familiarizado con el funcionamiento de los datos de identidad para el SDK web de Platform, incluida la función de los ECID y `identityMap`. Consulte la descripción general de [datos de identidad en el SDK web](./overview.md) para obtener más información.

## Uso de FPID

Los FPID rastrean visitantes mediante cookies de origen. Las cookies de origen son más efectivas cuando se establecen con un servidor que usa un registro DNS [A](https://datatracker.ietf.org/doc/html/rfc1035) (para IPv4) o [registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), a diferencia de un código CNAME o JavaScript DNS.

>[!IMPORTANT]
>
>`A` o `AAAA` registros solo se admiten para configurar y rastrear cookies. El método principal para la recopilación de datos es a través de un CNAME DNS. En otras palabras, los FPID se establecen mediante un registro A o AAAA y, a continuación, se envían al Adobe mediante un CNAME.
>
>El [programa de certificados administrados por Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) también se admite para la recopilación de datos de origen.

Una vez establecida una cookie FPID, su valor se puede recuperar y enviar al Adobe a medida que se recopilan los datos del evento. Los FPID recopilados se utilizan como semillas para generar ECID, que siguen siendo los identificadores principales en las aplicaciones de Adobe Experience Cloud.

Para enviar un FPID para un visitante de un sitio web al Edge Network de Platform, debe incluir el FPID en el `identityMap` para ese visitante. Consulte la sección más adelante en este documento sobre [el uso de FPID en `identityMap`](#identityMap) para obtener más información.

### Requisitos de formato de ID

El Edge Network de Platform solo acepta ID que cumplan con el [formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Los ID de dispositivo que no estén en formato UUIDv4 se rechazarán.

La generación de un UUID casi siempre resultará en un ID único y aleatorio, con una probabilidad insignificante de que se produzca una colisión. UUIDv4 no se puede inicializar mediante direcciones IP u otra información de identificación personal (PII). Los UUID son ubicuos y se pueden encontrar bibliotecas para prácticamente todos los lenguajes de programación para generarlos.

## Configuración de una cookie de ID de origen en la interfaz de usuario de flujos de datos {#setting-cookie-datastreams}

Puede especificar un nombre de cookie en la interfaz de usuario de flujos de datos, donde puede residir [!DNL FPID], en lugar de tener que leer el valor de la cookie e incluir el FPID en el mapa de identidad.

>[!IMPORTANT]
>
>Esta característica requiere que tenga habilitada la [recopilación de datos de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en).

Consulte la [documentación de flujos de datos](../../datastreams/configure.md) para obtener información detallada sobre cómo configurar un flujo de datos.

Al configurar su secuencia de datos, habilite la opción **[!UICONTROL Cookie de ID de origen]**. Esta configuración indica al Edge Network que haga referencia a una cookie especificada cuando busque un ID de dispositivo de origen, en lugar de buscar este valor en el [mapa de identidad](#identityMap).

Consulte la documentación de [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es) para obtener más información sobre cómo funcionan con Adobe Experience Cloud.

![Imagen de la interfaz de usuario de la plataforma que muestra la configuración de secuencia de datos destacando la configuración de cookie de ID de origen](../assets/first-party-id-datastreams.png)

Al habilitar esta configuración, debe proporcionar el nombre de la cookie en la que se espera almacenar el ID.

Cuando utiliza ID de origen, no puede realizar sincronizaciones de ID de terceros. Las sincronizaciones de ID de terceros dependen del servicio [!DNL Visitor ID] y del `UUID` generado por ese servicio. Al utilizar la funcionalidad de ID de origen, el ECID se genera sin el uso del servicio [!DNL Visitor ID], lo que hace imposible la sincronización de ID de terceros.

Cuando se usan ID de origen, no se admiten las funciones de Audience Manager dirigidas a la activación en plataformas de socios, dado que las sincronizaciones de ID de socios de Audience Manager se basan principalmente en `UUIDs` o `DIDs`. El ECID derivado de un ID de origen no está vinculado a un `UUID`, por lo que no se puede direccionar.

## Configuración de una cookie mediante su propio servidor

Al configurar una cookie mediante un servidor de su propiedad, se pueden utilizar varios métodos para evitar que la cookie se restrinja debido a las políticas del explorador:

* Generación de cookies mediante lenguajes de scripts del lado del servidor
* Establecer cookies en respuesta a una solicitud de API realizada a un subdominio u otro extremo del sitio
* Generación de cookies mediante un CMS
* Generación de cookies mediante una CDN

>[!IMPORTANT]
>
>Las cookies configuradas mediante el método `document.cookie` de JavaScript casi nunca se protegerán de las directivas del explorador que restringen las duraciones de las cookies.

### Cuándo se establece la cookie

Idealmente, la cookie FPID debe configurarse antes de realizar cualquier solicitud al Edge Network. Sin embargo, en los casos en los que esto no es posible, se sigue generando un ECID con los métodos existentes y actúa como identificador principal siempre que exista la cookie.

Suponiendo que el ECID se vea afectado finalmente por una política de eliminación del explorador, pero el FPID no, el FPID se convertirá en el identificador principal en la siguiente visita y se utilizará para inicializar el ECID en cada visita posterior.

### Configuración de la caducidad de la cookie

Configurar la caducidad de una cookie es algo que debe considerarse cuidadosamente al implementar la funcionalidad FPID. Al decidir esto, debe tener en cuenta los países o regiones en los que opera su organización junto con las leyes y políticas de cada una de esas regiones.

Como parte de esta decisión, es posible que desee adoptar una política de establecimiento de cookies para toda la compañía o una que varíe para los usuarios en cada configuración regional en la que opera.

Independientemente de la configuración que elija para la caducidad inicial de una cookie, debe asegurarse de incluir una lógica que amplíe la caducidad de la cookie cada vez que se produce una nueva visita al sitio.

## Impacto de los indicadores de cookies

Existen varios indicadores de cookies que afectan a cómo se tratan las cookies en los distintos exploradores:

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [SameSite](#same-site)

### `HTTPOnly` {#http-only}

No se puede tener acceso a las cookies configuradas con el indicador `HTTPOnly` mediante scripts del lado del cliente. Esto significa que si establece un indicador `HTTPOnly` al configurar el FPID, debe utilizar un lenguaje de scripts del lado del servidor para leer el valor de la cookie para incluirlo en `identityMap`.

Si elige que el Edge Network de Platform lea el valor de la cookie FPID, configurar el indicador `HTTPOnly` garantiza que ningún script del lado del cliente pueda acceder al valor, pero no tendrá ningún impacto negativo en la capacidad del Edge Network de Platform para leer la cookie.

>[!NOTE]
>
>El uso del indicador `HTTPOnly` no afecta a las directivas de cookies que pueden restringir la duración de las cookies. Sin embargo, sigue siendo algo que debe tener en cuenta al establecer y leer el valor del FPID.

### `Secure` {#secure}

Las cookies configuradas con el atributo `Secure` solo se envían al servidor con una solicitud cifrada a través del protocolo HTTPS. El uso de este indicador puede ayudar a garantizar que los atacantes intermediarios no puedan acceder fácilmente al valor de la cookie. Siempre que sea posible, es aconsejable establecer el indicador `Secure`.

### `SameSite` {#same-site}

El atributo `SameSite` permite a los servidores determinar si las cookies se envían con solicitudes entre sitios. El atributo proporciona cierta protección contra ataques de falsificación entre sitios. Existen tres valores posibles: `Strict`, `Lax` y `None`. Consulte con su equipo interno para determinar qué configuración es correcta para su organización.

Si no se especifica ningún atributo `SameSite`, la configuración predeterminada para algunos exploradores es ahora `SameSite=Lax`.

## Usando FPID en `identityMap` {#identityMap}

A continuación se muestra un ejemplo de cómo establecería un FPID en `identityMap`:

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

Al igual que con otros tipos de identidad, puede incluir el FPID con otras identidades dentro de `identityMap`. A continuación se muestra un ejemplo del FPID incluido con un ID de CRM autenticado:

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

Si el FPID está contenido en una cookie que lee el Edge Network cuando la recopilación de datos de origen está habilitada, solo debe capturar el ID de CRM autenticado:

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

Los(as) siguientes `identityMap` resultarían en una respuesta de error del Edge Network, ya que le falta el indicador `primary` para el FPID. Al menos uno de los identificadores presentes en `identityMap` debe marcarse como `primary`.

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

La respuesta de error devuelta por el Edge Network en este caso sería similar a la siguiente:

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

Cuando hay presentes tanto un ECID como un FPID, el ECID tiene prioridad a la hora de identificar al usuario. Esto garantiza que, cuando un ECID existente esté presente en el almacén de cookies del explorador, siga siendo el identificador principal y que los recuentos de visitantes existentes no se vean afectados. Para los usuarios existentes, el FPID no se convertirá en la identidad principal hasta que el ECID caduque o se elimine como resultado de una política del explorador o un proceso manual.

Las identidades se priorizan en el siguiente orden:

1. ECID incluido en `identityMap`
1. ECID almacenado en una cookie
1. FPID incluido en `identityMap`
1. FPID almacenado en una cookie

## Migración a ID de dispositivos de origen

Si está migrando a mediante FPID desde una implementación anterior, puede resultar difícil visualizar el aspecto que podría tener la transición en un nivel bajo.

Para ilustrar este proceso, considere un escenario que implique a un cliente que haya visitado anteriormente su sitio y el impacto que una migración FPID tendría en la forma en que se identifica a ese cliente en las soluciones de Adobe.

![Diagrama que muestra cómo se actualizan los valores de ID de un cliente entre visitas después de migrar a FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>La cookie `ECID` siempre tiene prioridad sobre `FPID`.

| Visita | Descripción |
| --- | --- |
| Primera visita | Supongamos que aún no ha empezado a configurar la cookie FPID. El ECID contenido en la [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) será el identificador usado para identificar al visitante. |
| Segunda visita | Se ha iniciado el despliegue de la solución ID de dispositivo de origen. El ECID existente sigue presente y sigue siendo el identificador principal para la identificación del visitante. |
| Tercera visita | Entre la segunda y la tercera visita, ha transcurrido tiempo suficiente para que el ECID se haya eliminado debido a la política del explorador. Sin embargo, como el FPID se estableció mediante un registro A DNS, el FPID persiste. El FPID ahora se considera el ID principal y se utiliza para inicializar el ECID, que se escribe en el dispositivo del usuario final. Ahora se considerará al usuario como un nuevo visitante en las soluciones de Adobe Experience Platform y de Experience Cloud. |
| Cuarta visita | Entre la tercera y la cuarta visita, ha transcurrido tiempo suficiente para que el ECID se haya eliminado debido a la política del explorador. Al igual que la visita anterior, el FPID se mantiene debido a la forma en que se estableció. Esta vez, se genera el mismo ECID que la visita anterior. El usuario se ve en todas las soluciones de Experience Platform y Experience Cloud como el mismo usuario de la visita anterior. |
| Quinta visita | Entre la cuarta y la quinta visita, el usuario final borró todas las cookies del explorador. Se genera un nuevo FPID y se utiliza para iniciar la creación de un nuevo ECID. Ahora se considerará al usuario como un nuevo visitante en las soluciones de Adobe Experience Platform y de Experience Cloud. |

{style="table-layout:auto"}

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca de los ID de dispositivos de origen.

### ¿En qué se diferencia sembrar un ID de simplemente generarlo?

El concepto de inicialización es único, ya que el FPID pasado a Adobe Experience Cloud se convierte en un ECID utilizando un algoritmo determinista. Cada vez que se envía el mismo FPID al Edge Network de Adobe Experience Platform, se siembra el mismo ECID desde el FPID.

### ¿Cuándo se debe generar el ID del dispositivo de origen?

Para reducir la inflación potencial de visitantes, el FPID debe generarse antes de realizar la primera solicitud mediante el SDK web. Sin embargo, si no puede hacerlo, se generará un ECID para ese usuario y se utilizará como identificador principal. El FPID generado no se convertirá en el identificador principal hasta que el ECID ya no esté presente.

### ¿Qué métodos de recopilación de datos admiten los ID de dispositivos de origen?

Actualmente, solo el SDK web admite FPID.

### ¿Los FPID se almacenan en alguna plataforma o solución de Experience Cloud?

Una vez que el FPID se ha utilizado para iniciar un ECID, se elimina del `identityMap` y se reemplaza por el ECID que se ha generado. FPID no se almacena en ninguna solución de Adobe Experience Platform o de Experience Cloud.
