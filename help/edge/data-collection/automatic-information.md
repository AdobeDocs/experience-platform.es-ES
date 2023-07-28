---
title: Información recopilada automáticamente en el SDK web de Adobe Experience Platform
description: Información general sobre cada fragmento de información que el SDK de Adobe Experience Platform recopila automáticamente.
keywords: recopilar información;contexto;configurar;dispositivo;screenHeight;screen Height;screenHeight;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewportHeight;viewportWidth;viewportWidth;viewportWidth;crowserDetails;browser details;implementationDetails;nombre;versión;placeContext;localTime;local Time;localTimezoneOffset;local TimezoneOffset;local Timestamp;web;url;webPageDetails;web Page Details;web Page Details;webReferrer;web
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: e3f507e010ea2a32042b53d46795d87e82e3fb72
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Información recopilada automáticamente

El SDK web de Adobe Experience Platform recopila automáticamente una serie de fragmentos de información sin ninguna configuración especial. Sin embargo, esta información se puede deshabilitar si es necesario utilizando `context` en la opción `configure` comando. [Consulte Configuración del SDK](../fundamentals/configuring-the-sdk.md). A continuación se muestra una lista de esos datos. El nombre entre paréntesis indica la cadena que se debe utilizar al configurar el contexto.

## Dispositivo (`device`)

Información sobre el dispositivo. Esto no incluye datos que se puedan buscar en el lado del servidor desde la cadena del agente de usuario.

### Altura de pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altura de la pantalla (en píxeles).

### Orientación de pantalla

| **Ruta en carga útil:** | **Valores posibles:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` o `portrait` |

La orientación de la pantalla.

### Anchura de pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Ancho de la pantalla (en píxeles).

## Entorno (`environment`)

Detalles sobre el entorno del explorador.

### Tipo de entorno

Explorador

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

El tipo de entorno a través del cual surgió la experiencia. El SDK web de Adobe Experience Platform siempre establece esto como `browser`.

### Altura de ventanilla

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altura del área de contenido del explorador (en píxeles).

### Anchura de ventanilla

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Ancho del área de contenido del explorador (en píxeles).

## Detalles de implementación

Información sobre el SDK utilizado para recopilar el evento.

### Nombre

| **Ruta en carga útil:** | **Ejemplo:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identificador del kit de desarrollo de software (SDK).  Este campo utiliza un URI para mejorar la exclusividad entre los identificadores proporcionados por diferentes bibliotecas de software. Cuando se utiliza la biblioteca independiente, el valor es `https://ns.adobe.com/experience/alloy`. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, el valor es `https://ns.adobe.com/experience/alloy+reactor`.

### Versión

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Cuando se utiliza la biblioteca independiente, el valor es simplemente la versión de la biblioteca. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, esta es la versión de la biblioteca y la versión de la extensión de etiqueta unidas con un signo +. Por ejemplo, si la versión de la biblioteca fuera 2.1.0 y la versión de la extensión de la etiqueta fuera 2.1.3, el valor sería `2.1.0+2.1.3`.

### Entorno {#environment}

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Entorno donde se recopilaron los datos. Siempre se establece en `browser`.

## Contexto del lugar (`placeContext`) {#place-context}

Información sobre la ubicación del usuario final.

### Hora local

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Marca de tiempo local para el usuario final en formato ISO extendido simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Desplazamiento de zona horaria local

| **Ruta en carga útil:** | **Ejemplo:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Número de minutos que el usuario está desfasado de GMT.

## Marca de tiempo

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

La marca de tiempo del evento.  Esta parte del contexto no se puede eliminar.

Marca de tiempo UTC para el usuario final en formato ISO extendido simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Detalles web (`web`)

Detalles sobre la página en la que se encuentra el usuario.

### URL de la página actual

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

Dirección URL de la página actual.

### URL de referente

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

La URL de la página anterior visitada.
