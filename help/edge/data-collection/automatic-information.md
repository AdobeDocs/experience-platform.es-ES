---
title: Información recopilada automáticamente en el SDK web de Adobe Experience Platform
description: Información general sobre cada parte de información que el SDK de Adobe Experience Platform recopila automáticamente.
keywords: recopilar información;contexto;configurar;dispositivo;screenHeight;altura de pantalla;orientación de pantalla;orientación de pantalla;ancho de pantalla;entorno;altura de ventanilla;altura de ventanilla;anchura de ventanilla;anchura de ventanilla;detalles del navegador;detalles de implementación;detalles de implementación;nombre;versión;contexto;hora local;hora local;zona horaria local;desplazamiento de zona horaria local;desplazamiento de zona horaria local marca de tiempo;web;url;webPageDetails;detalles de página web;webReferrer;web Referrer;horizontal;vertical;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Información recopilada automáticamente

El SDK web de Adobe Experience Platform recopila una serie de elementos de información automáticamente sin ninguna configuración especial. Sin embargo, esta información se puede deshabilitar si es necesario mediante la opción `context` del comando `configure`. [Consulte Configuración del SDK](../fundamentals/configuring-the-sdk.md). A continuación se muestra una lista de esas informaciones. El nombre entre paréntesis indica la cadena que se utiliza al configurar el contexto.

## Dispositivo (`device`)

Información sobre el dispositivo. Esto no incluye datos que se puedan buscar en el lado del servidor desde la cadena del agente de usuario.

### Altura de la pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altura de la pantalla (en píxeles).

### Orientación de la pantalla

| **Ruta en carga útil:** | **Valores posibles:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` o `portrait` |

La orientación de la pantalla.

### Anchura de la pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Anchura de la pantalla (en píxeles).

## Entorno (`environment`)

Detalles sobre el entorno del explorador.

### Tipo de entorno

Explorador

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

El tipo de entorno a través del cual apareció la experiencia. El SDK web de Adobe Experience Platform siempre lo establece en `browser`.

### Altura de la ventanilla móvil

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altura del área de contenido del explorador (en píxeles).

### Anchura de la ventanilla móvil

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

El identificador del kit de desarrollo de software (SDK).  Este campo utiliza una URI para mejorar la exclusividad entre los identificadores proporcionados por diferentes bibliotecas de software. Cuando se utiliza la biblioteca independiente, el valor es `https://ns.adobe.com/experience/alloy`. Cuando la biblioteca se utiliza como parte de la extensión de etiquetas, el valor es `https://ns.adobe.com/experience/alloy+reactor`.

### Versión

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Cuando se utiliza la biblioteca independiente, el valor es simplemente la versión de la biblioteca. Cuando la biblioteca se utiliza como parte de la extensión de etiquetas, esta es la versión de la biblioteca y la versión de la extensión de etiqueta unida con &quot;+&quot;. Por ejemplo, si la versión de la biblioteca fuera 2.1.0 y la versión de la extensión de etiqueta fuera 2.1.3, el valor sería `2.1.0+2.1.3`.

### Entorno

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Entorno en el que se recopilaron los datos. Esto siempre se establece en `browser`.

## Colocar contexto (`placeContext`)

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

Número de minutos que el usuario está desplazado de GMT.

## Marca de tiempo

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Marca de tiempo del evento.  Esta parte del contexto no se puede eliminar.

Marca de tiempo UTC para el usuario final en formato ISO extendido simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Detalles web (`web`)

Detalles sobre la página en la que se encuentra el usuario.

### Dirección URL de la página actual

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

La dirección URL de la página actual.

### Dirección URL del referente

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

Dirección URL de la página anterior visitada.
