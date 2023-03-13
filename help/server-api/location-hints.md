---
title: Sugerencias de ubicación
description: Este artículo explica cómo funcionan las sugerencias de ubicación en la API del servidor de red perimetral, de modo que las solicitudes de los usuarios finales siempre se puedan enrutar al mismo servidor.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Sugerencias de ubicación

## Información general {#overview}

El [!DNL Adobe Experience Platform Edge Network] utiliza varios servidores distribuidos globalmente para garantizar tiempos de respuesta rápidos independientemente de la ubicación del usuario final. También utiliza el enrutamiento basado en DNS para garantizar que las solicitudes siempre se enruten a la ubicación de la red perimetral más cercana a los usuarios finales.

Si los usuarios finales se conectan a una VPN o cambian tipos de red en sus dispositivos móviles durante una sesión, las solicitudes de red perimetral suelen enrutarse a una ubicación diferente. El enrutamiento entre servidores a mitad de la sesión puede resultar problemático, ya que las soluciones de Adobe Experience Platform y Adobe Experience Cloud almacenan información del perfil del usuario final en la red perimetral.

Aquí es donde entran en juego las sugerencias de ubicación.

Para garantizar que los usuarios finales siempre interactúen con el servidor regional de la red perimetral que contiene sus datos de perfil actuales, la funcionalidad de sugerencias de ubicación garantiza que todas las solicitudes a la red perimetral se envíen al mismo servidor donde se realizó la primera solicitud de una sesión. Esto ayuda a los usuarios a tener una experiencia coherente, independientemente de los cambios de red que puedan experimentar durante una sesión.

## Uso de sugerencias de ubicación

Las sugerencias de ubicación se incluyen en la respuesta de la solicitud inicial de red perimetral y en todas las solicitudes posteriores, como se muestra en el ejemplo siguiente:

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

El `EdgeNetwork` El ámbito contiene toda la información relevante que la red perimetral necesita para enrutar las solicitudes posteriores en consecuencia. En la respuesta de la solicitud inicial y de cada solicitud posterior a la red de Edge, habrá una sección en el identificador con un tipo de `locationHint:result`.

La sugerencia asociada con `EdgeNetwork` el ámbito puede contener uno de los siguientes valores:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato de API**

Para asegurarse de que las solicitudes posteriores se enruten correctamente, inserte la sugerencia de ubicación en la ruta URL de las llamadas de API posteriores entre la ruta base, generalmente `ee`, y `v2` Versión de API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Almacenar sugerencias de ubicación en cookies {#storing-hints-in-cookies}

Para asegurarse de que la sugerencia de ubicación devuelta por la red perimetral persiste durante la sesión, puede almacenar el valor de la sugerencia de ubicación en una cookie, junto con la duración de la cookie, que se encuentra en `ttlSeconds` (normalmente 1800 segundos).

Al igual que con la mayoría de las cookies, debe ampliar la duración de esta cookie cada vez que haya una respuesta de la red perimetral. Para garantizar la máxima compatibilidad con el SDK web, utilice el nombre de la cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. Los ID de organización de IMS suelen terminar con `@AdobeOrg`. El `@` El valor de se debe convertir en un guion bajo para garantizar que la cookie tenga el formato correcto.
