---
title: User agent client hints
description: Descubra cómo funcionan las sugerencias del cliente del agente de usuario en el SDK web. Las sugerencias del cliente permiten a los propietarios de sitios web acceder a gran parte de la misma información disponible en la cadena del agente de usuario, pero de una manera que preserva la privacidad.
keywords: user-agent;sugerencias del cliente; cadena; cadena de user-agent; baja entropía; alta entropía
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 3%

---

# User agent client hints

## Información general {#overview}

Cada vez que un explorador web realiza una solicitud a un servidor web, el encabezado de la solicitud incluye información sobre el explorador y el entorno en el que se está ejecutando el explorador. Todos estos datos se agregan en una cadena, denominada cadena del agente de usuario.

Este es un ejemplo del aspecto que tendrá una cadena de agente de usuario en una solicitud procedente de un explorador Chrome que se ejecuta en un dispositivo [!DNL Mac OS].

>[!NOTE]
>
>A lo largo de los años, la cantidad de información del explorador y del dispositivo incluida en la cadena del agente de usuario ha aumentado y se ha modificado varias veces. El ejemplo siguiente muestra una selección de la información de agente de usuario más común.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Campo | Valor |
|---|---|
| Nombre del software | Chrome |
| Versión de software | 105 |
| Versión completa del software | 105.0.0.0 |
| Nombre del motor de diseño | AppleWebKit |
| Versión del motor de diseño | 537,36 |
| Sistema operativo | MAC OS X |
| Versión de sistema operativo | 10.15.7 |
| Device | Sistema operativo Mac X 10_15_7 |

## Casos de uso {#use-cases}

Las cadenas de agente de usuario se han utilizado durante mucho tiempo para proporcionar a los equipos de marketing y desarrollo información importante sobre cómo los navegadores, sistemas operativos y dispositivos muestran el contenido del sitio, así como la forma en que los usuarios interactúan con los sitios web.

Las cadenas de agente de usuario también se utilizan para bloquear el correo no deseado y filtrar bots que rastrean sitios por distintos motivos adicionales.

## Cadenas del agente de usuario en Adobe Experience Cloud {#user-agent-in-adobe}

Las soluciones de Adobe Experience Cloud utilizan las cadenas del agente de usuario de varias formas.

* Adobe Analytics utiliza la cadena del agente de usuario para aumentar y obtener información adicional relacionada con los sistemas operativos, los exploradores y los dispositivos utilizados para visitar un sitio web.
* Adobe Audience Manager y Adobe Target califican a los usuarios finales para campañas de segmentación y personalización, según la información proporcionada por la cadena del agente de usuario.

## Introducción a sugerencias del cliente del agente de usuario {#ua-ch}

En los últimos años, los propietarios de sitios y proveedores de marketing han utilizado cadenas de agentes de usuario junto con otra información incluida en los encabezados de solicitud para crear huellas digitales. Estas huellas digitales pueden utilizarse como medio para identificar a usuarios sin su conocimiento.

A pesar del importante propósito que tienen las cadenas de agente de usuario para los propietarios del sitio, los desarrolladores de navegadores han decidido cambiar el funcionamiento de las cadenas de agente de usuario para limitar los posibles problemas de privacidad de los usuarios finales.

La solución que desarrollaron se llama [user agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Las sugerencias del cliente siguen permitiendo que los sitios web recopilen la información necesaria sobre el explorador, el sistema operativo y el dispositivo, a la vez que brindan una mayor protección contra los métodos de seguimiento encubiertos, como la huella digital.

Las sugerencias del cliente permiten a los propietarios de sitios web acceder a gran parte de la misma información disponible en la cadena del agente de usuario, pero de una manera que preserva la privacidad.

Cuando los exploradores modernos envían un usuario a un servidor web, toda la cadena del agente de usuario se envía en cada solicitud, independientemente de si es necesaria o no. Las sugerencias del cliente, por otro lado, aplican un modelo en el que el servidor debe solicitar al explorador la información adicional que desea conocer sobre el cliente. Al recibir esta solicitud, el explorador puede aplicar sus propias directivas o configuración de usuario para determinar qué datos se devuelven. En lugar de exponer toda la cadena del agente de usuario de forma predeterminada en todas las solicitudes, el acceso ahora se administra de forma explícita y auditable.

## Compatibilidad con exploradores {#browser-support}

[Las sugerencias del cliente del agente de usuario](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) se introdujeron con [!DNL Google Chrome]versión 89.

Otros exploradores basados en Chromium admiten la API de Client Hints, como:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorías {#categories}

Existen dos categorías de sugerencias del cliente del agente de usuario:

* [Sugerencias de cliente de baja entropía](#low-entropy)
* [Sugerencias de cliente de alta entropía](#high-entropy)

### Sugerencias de cliente de baja entropía {#low-entropy}

Las sugerencias de cliente de baja entropía incluyen información básica que no se puede usar para tomar huellas digitales de los usuarios. Información como la marca del explorador, la plataforma y si la solicitud proviene de un dispositivo móvil.

Las sugerencias de cliente de baja entropía están habilitadas de forma predeterminada en el SDK web y se pasan en cada solicitud.

| Encabezado HTTP | JavaScript | Incluido en el agente de usuario de forma predeterminada | Incluido en las sugerencias del cliente de forma predeterminada |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sí | Sí |
| `Sec-CH-UA-Platform` | `platform` | Sí | Sí |
| `Sec-CH-UA-Mobile` | `mobile` | Sí | Sí |

### Sugerencias de cliente de alta entropía {#high-entropy}

Las sugerencias de cliente de alta entropía son información más detallada sobre el dispositivo cliente, como la versión de plataforma, la arquitectura, el modelo, los bits (plataformas de 64 o 32 bits) o la versión completa del sistema operativo. Esta información podría utilizarse potencialmente en la toma de huellas digitales.

| Propiedad | Descripción | Encabezado HTTP | Ruta de XDM | Ejemplo | Incluido en el agente de usuario de forma predeterminada | Incluido en las sugerencias del cliente de forma predeterminada |
| --- | --- | --- | --- | --- |---|---|
| Versión de sistema operativo | La versión del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Sí | No |
| Arquitectura | Arquitectura de CPU subyacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Sí | No |
| Modelo de dispositivo | Nombre del dispositivo utilizado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Sí | No |
| Mordacidad | Número de bits que admite la arquitectura de CPU subyacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Sí | No |
| Proveedor del explorador | Compañía que creó el explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Sí | No |
| Nombre del explorador | El explorador utilizado. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Sí | No |
| Versión del explorador | La versión significativa del explorador. La sugerencia de baja entropía `Sec-CH-UA` también recopila este elemento. La versión exacta del explorador no se recopila automáticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Sí | No |


Las sugerencias de cliente de alta entropía están deshabilitadas de forma predeterminada en el SDK web. Para habilitarlas, debe configurar manualmente el SDK web para solicitar sugerencias de cliente de alta entropía.

## Impacto de las sugerencias de cliente de alta entropía en las soluciones de Experience Cloud {#impact-in-experience-cloud-solutions}

Algunas soluciones de Adobe Experience Cloud dependen de la información incluida en las sugerencias del cliente de alta entropía al generar informes.

Si no habilita sugerencias de cliente de alta entropía en su entorno, los informes y características de Adobe Analytics y Audience Manager que se describen a continuación no funcionarán.

### Informes de Adobe Analytics que dependen de sugerencias del cliente de alta entropía {#analytics}

La dimensión [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=es) incluye la versión del sistema operativo que se almacena como una sugerencia de cliente de alta entropía. Si no está habilitada la opción sugerencias de clientes de alta entropía, la versión del sistema operativo puede ser inexacta para las visitas recopiladas de los exploradores Chromium.

### Características de Audience Manager que dependen de sugerencias de cliente de alta entropía {#aam}

[!DNL Google] ha actualizado la funcionalidad del explorador [!DNL Chrome] para minimizar la información recopilada a través del encabezado `User-Agent`. Como resultado, los clientes de Audience Manager que usen [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es) ya no recibirán información confiable para rasgos basados en [claves a nivel de plataforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=es).

Los clientes de Audience Manager que usen claves de nivel de plataforma para el direccionamiento deben cambiar a [SDK web de Experience Platform](/help/web-sdk/home.md) en lugar de [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es) y habilitar las [sugerencias de cliente de alta entropía](#enabling-high-entropy-client-hints) para seguir recibiendo datos de rasgos confiables.

## Habilitar sugerencias de cliente de alta entropía {#enabling-high-entropy-client-hints}

Para habilitar sugerencias de cliente de alta entropía en la implementación del SDK web, debe incluir la opción de contexto `highEntropyUserAgentHints` adicional en el campo [`context`](/help/web-sdk/commands/configure/context.md).

Por ejemplo, para recuperar sugerencias de cliente de alta entropía de las propiedades web, la configuración tendría este aspecto:

`context: ["highEntropyUserAgentHints", "web"]`

## Ejemplo {#example}

Las sugerencias del cliente contenidas en los encabezados de la primera solicitud realizada por el explorador a un servidor web contendrán la marca del explorador, la versión principal del explorador y un indicador de si el cliente es un dispositivo móvil. Cada fragmento de datos tendrá su propio valor de encabezado en lugar de agruparse en una sola cadena de agente de usuario, como se muestra a continuación:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

El encabezado [!DNL User-Agent] equivalente para el mismo explorador tendría este aspecto:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Aunque la información es similar, la primera solicitud al servidor contiene sugerencias del cliente. Solo incluyen un subconjunto de lo que está disponible en la cadena del agente de usuario. Falta en la solicitud la arquitectura del sistema operativo, la versión completa del sistema operativo, el nombre del motor de diseño, la versión del motor de diseño y la versión completa del explorador.

Sin embargo, en solicitudes posteriores, [!DNL Client Hints API] permite que los servidores web soliciten detalles adicionales sobre el dispositivo. Cuando se solicitan estos valores, según la directiva del explorador o la configuración del usuario, la respuesta del explorador puede incluir esa información.

A continuación se muestra un ejemplo del objeto JSON devuelto por [!DNL Client Hints API] cuando se solicitan valores de entropía altos:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
