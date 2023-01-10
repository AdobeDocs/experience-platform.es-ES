---
title: Sugerencias del cliente de User-Agent
description: Descubra cómo funcionan las sugerencias de cliente de agente de usuario en el SDK web
keywords: user-agent;sugerencias del cliente; string; cadena user-agent; baja entropía; alta entropía
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 4a2ae40fc64c4340ddb05db881c2176bb2aedc46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 5%

---

# Sugerencias del cliente de User-Agent

## Información general {#overview}

Cada vez que un explorador web realiza una solicitud a un servidor web, el encabezado de la solicitud incluye información sobre el explorador y el entorno en el que se ejecuta el explorador. Todos estos datos se acumulan en una cadena denominada [!DNL User-Agent] cadena.

A continuación, se muestra un ejemplo de lo que puede ser [!DNL User-Agent] tiene el aspecto de una solicitud procedente de un explorador Chrome que se ejecuta en una [!DNL Mac OS] dispositivo.

>[!NOTE]
>
>A lo largo de los años, la cantidad de información del explorador y del dispositivo incluida en la variable [!DNL User-Agent] La cadena ha crecido y se ha modificado varias veces. El ejemplo siguiente muestra una selección de los más comunes [!DNL User-Agent] información.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Campo | Valor |
|---|---|
| Nombre del software | Chrome |
| Versión de software | 105 |
| Versión completa del software | 105.0.0.0 |
| Nombre del motor de diseño | AppleWebKit |
| Versión del motor de diseño | 537.36 |
| Sistema operativo | Mac OS X |
| Versión del sistema operativo | 10.15.7 |
| Device | Intel Mac OS X 10_15_7 |

## Casos de uso {#use-cases}

[!DNL User-Agent] Las cadenas se han utilizado durante mucho tiempo para proporcionar a los equipos de marketing y desarrollo información importante sobre cómo los navegadores, sistemas operativos y dispositivos muestran el contenido del sitio, así como sobre cómo interactúan los usuarios con los sitios web.

[!DNL User-Agent] las cadenas también se utilizan para bloquear el correo no deseado y filtrar bots que rastrean sitios para diversos fines adicionales.

## [!DNL User-Agent] cadenas en Adobe Experience Cloud {#user-agent-in-adobe}

Las soluciones de Adobe Experience Cloud utilizan la variable [!DNL User-Agent] cadenas de varias formas.

* Adobe Analytics utiliza el [!DNL User-Agent] para aumentar y obtener información adicional relacionada con los sistemas operativos, navegadores y dispositivos utilizados para visitar un sitio web.
* Adobe Audience Manager y Adobe Target califican a los usuarios finales para campañas de segmentación y personalización, según la información proporcionada por la [!DNL User-Agent] cadena.

## Introducción a las sugerencias del cliente User-Agent {#ua-ch}

En los últimos años, los propietarios de sitios y los proveedores de marketing han utilizado [!DNL User-Agent] cadenas junto con otra información incluida en los encabezados de solicitud para crear huellas digitales. Estas huellas dactilares pueden utilizarse como medio para identificar a los usuarios sin su conocimiento.

A pesar del importante propósito que [!DNL User-Agent] Las cadenas sirven para los propietarios del sitio, los desarrolladores de exploradores han decidido cambiar la forma en que [!DNL User-Agent] las cadenas funcionan, para limitar los posibles problemas de privacidad para los usuarios finales.

La solución que desarrollaron se llama [Sugerencias del cliente de User-Agent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Las sugerencias del cliente siguen permitiendo que los sitios web recopilen la información necesaria sobre el explorador, el sistema operativo y el dispositivo, a la vez que brindan una mayor protección contra los métodos de seguimiento encubiertos, como la huella digital.

Las sugerencias del cliente permiten a los propietarios de sitios web acceder a gran parte de la misma información disponible en la [!DNL User-Agent] cadena, pero de una forma más preservada de la privacidad.

Cuando los navegadores modernos envían un usuario a un servidor web, todo el [!DNL User-Agent] se envía en cada solicitud, independientemente de si es necesaria. Por otro lado, las sugerencias del cliente refuerzan un modelo en el que el servidor debe solicitar al explorador la información adicional que desea conocer sobre el cliente. Al recibir esta solicitud, el explorador puede aplicar sus propias políticas o configuración de usuario para determinar qué datos se devuelven. En lugar de exponer todo [!DNL User-Agent] de forma predeterminada en todas las solicitudes, el acceso ahora se administra de forma explícita y auditable.

## Compatibilidad con exploradores {#browser-support}

[Sugerencias del cliente de User-Agent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) se han introducido con [!DNL Google Chrome ]versión 89.

Los exploradores adicionales basados en Chromium admiten la API de sugerencias del cliente, como:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorías {#categories}

Existen dos categorías de sugerencias del cliente User-Agent:

* [Sugerencias de cliente de baja entropía](#low-entropy)
* [Sugerencias de cliente de entropía alta](#high-entropy)

### Sugerencias de cliente de baja entropía {#low-entropy}

Las sugerencias de cliente de baja entropía incluyen información básica que no se puede usar para los usuarios de huellas digitales. Información como la marca del explorador, la plataforma y si la solicitud procede de un dispositivo móvil.

Las sugerencias de cliente de baja entropía están habilitadas de forma predeterminada en el SDK web y se pasan en cada solicitud.

| Encabezado HTTP | JavaScript | Incluido en User-Agent de forma predeterminada | Incluido en las sugerencias del cliente de forma predeterminada |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sí | Sí |
| `Sec-CH-UA-Platform` | `platform` | Sí | Sí |
| `Sec-CH-UA-Mobile` | `mobile` | Sí | Sí |

### Sugerencias de cliente de entropía alta {#high-entropy}

Las sugerencias de cliente de alta entropía son información más detallada sobre el dispositivo cliente, como la versión de la plataforma, la arquitectura, el modelo, la integridad (plataformas de 64 o 32 bits) o la versión completa del sistema operativo. Esta información podría utilizarse en la toma de huellas digitales.

| Encabezado HTTP | JavaScript | Incluido en User-Agent de forma predeterminada | Incluido en las sugerencias del cliente de forma predeterminada |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sí | No |
| `Sec-CH-UA-Arc` | `architecture` | Sí | No |
| `Sec-CH-UA-Model` | `model` | Sí | No |
| `Sec-CH-UA-Bitness` | `Bitness` | Sí | No |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sí | No |

Las sugerencias de cliente de alta entropía están deshabilitadas de forma predeterminada en el SDK web. Para habilitarlos, debe configurar manualmente el SDK web para solicitar sugerencias de cliente de alta entropía.

## Las sugerencias de cliente de alta entropía afectan a las soluciones de Experience Cloud {#impact-in-experience-cloud-solutions}

Algunas soluciones de Adobe Experience Cloud dependen de la información incluida en las sugerencias de cliente de alta entropía al generar informes.

Si no habilita las sugerencias de cliente de alta entropía en su entorno, los informes y características de Adobe Analytics y Audience Manager que se describen a continuación no funcionarán.

### Informes de Adobe Analytics basados en sugerencias de cliente de alta entropía {#analytics}

La variable [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) incluye la versión del sistema operativo que se almacena como una sugerencia de cliente de alta entropía. Si las sugerencias de clientes de alta entropía no están habilitadas, la versión del sistema operativo puede ser inexacta para las visitas recopiladas en los exploradores Chromium.

### Características del Audience Manager que dependen de sugerencias de cliente de alta entropía {#aam}

Si los rasgos del Audience Manager utilizan cualquiera de las siguientes propiedades, debe habilitar las sugerencias de cliente de alta entropía. De lo contrario, las características dejarán de funcionar.

* Versión del sistema operativo
* Modelo de dispositivo
* Fabricante del dispositivo
* Proveedor de dispositivo

## Habilitar sugerencias de cliente de alta entropía {#enabling-high-entropy-client-hints}

Para habilitar las sugerencias de cliente de alta entropía en la implementación del SDK web, debe incluir el complemento `highEntropyUserAgentHints` contexto, tal como se describe en la sección [documentación de configuración](configuring-the-sdk.md#context), junto con la configuración existente.

Por ejemplo, para recuperar sugerencias de cliente de alta entropía de propiedades web, la configuración tendría este aspecto:

`context: ["highEntropyUserAgentHints", "web"]`

## Ejemplo {#example}

Las sugerencias del cliente contenidas en los encabezados de la primera solicitud realizada por el explorador a un servidor web contendrán la marca del explorador, la versión principal del explorador y un indicador de si el cliente es un dispositivo móvil. Cada fragmento de datos tendrá su propio valor de encabezado en lugar de agruparse en un solo [!DNL User-Agent] como se muestra a continuación:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

El equivalente [!DNL User-Agent] para el mismo explorador tendría este aspecto:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Aunque la información es similar, la primera solicitud al servidor contiene sugerencias del cliente. Solo incluyen un subconjunto de lo que está disponible en la variable [!DNL User-Agent] cadena. Falta en la solicitud la arquitectura del sistema operativo, la versión completa del sistema operativo, el nombre del motor de diseño, la versión del motor de diseño y la versión completa del explorador.

Sin embargo, en solicitudes posteriores, la variable [!DNL Client Hints API] permite a los servidores web solicitar detalles adicionales sobre el dispositivo. Cuando se solicitan estos valores, según la política del explorador o la configuración del usuario, la respuesta del explorador puede incluir esa información.

A continuación se muestra un ejemplo del objeto JSON devuelto por el [!DNL Client Hints API] cuando se solicitan valores de entropía altos:


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
