---
title: Sugerencias de ubicación
description: Este artículo explica cómo funcionan las sugerencias de ubicación en la API de servidor de red perimetral, de modo que las solicitudes de usuario final siempre se puedan enrutar al mismo servidor.
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# Sugerencias de ubicación

## Información general {#overview}

La variable [!DNL Adobe Experience Platform Edge Network] utiliza varios servidores distribuidos globalmente para garantizar tiempos de respuesta rápidos, independientemente de la ubicación del usuario final. También utiliza enrutamiento basado en DNS para garantizar que las solicitudes siempre se enruten a la ubicación de red perimetral más cercana a los usuarios finales.

Si los usuarios finales se conectan a una VPN o cambian de tipo de red en sus dispositivos móviles durante una sesión, las solicitudes de red perimetral a menudo se pueden enrutar a una ubicación diferente. El enrutamiento entre sesiones puede resultar problemático, ya que las soluciones Adobe Experience Platform y Adobe Experience Cloud almacenan información de perfil de usuario final en la red perimetral.

Aquí es donde entran en juego las sugerencias de ubicación.

Para garantizar que los usuarios finales interactúen siempre con el servidor regional de red perimetral que contiene sus datos de perfil actuales, la funcionalidad de sugerencias de ubicación garantiza que todas las solicitudes a la red perimetral se envíen al mismo servidor en el que se realizó la primera solicitud de una sesión. Esto ayuda a los usuarios a tener una experiencia coherente, independientemente de los cambios de red que puedan experimentar durante una sesión.

## Uso de sugerencias de ubicación

Las sugerencias de ubicación se incluyen en la respuesta de la solicitud de red perimetral inicial y en todas las solicitudes posteriores, como se muestra en el ejemplo siguiente:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

La variable `EdgeNetwork` scope contiene toda la información relevante que la red perimetral necesita para enrutar las solicitudes posteriores en consecuencia. En la respuesta de la solicitud inicial y cada solicitud posterior a la red de Edge, habrá una sección en el controlador con un tipo de `locationHint:result`.

La sugerencia asociada con la variable `EdgeNetwork` el ámbito puede contener uno de los siguientes valores:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato de API**

Para garantizar que las solicitudes posteriores se enruten correctamente, inserte la sugerencia de ubicación en la ruta URL de las llamadas a la API posteriores entre la ruta base, normalmente `ee`y `v2` Versión de API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Almacenamiento de sugerencias de ubicación en cookies {#storing-hints-in-cookies}

Para garantizar que la sugerencia de ubicación devuelta por la red perimetral se mantenga durante la sesión, puede almacenar el valor de sugerencia de ubicación en una cookie, junto con la duración de la cookie, que se encuentra en la variable `ttlSeconds` (normalmente 1800 segundos).

Al igual que con la mayoría de las cookies, debe ampliar la duración de esta cookie cada vez que haya una respuesta de la red perimetral. Para garantizar la máxima compatibilidad con el SDK web, utilice el nombre de la cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. Los ID de organización de IMS suelen finalizar con `@AdobeOrg`. La variable `@` debe convertirse a un guión bajo para garantizar que la cookie tenga el formato correcto.
