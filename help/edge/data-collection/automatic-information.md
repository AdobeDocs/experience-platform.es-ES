---
title: Información recopilada automáticamente
seo-title: Información recopilada automáticamente por Adobe Experience Platform Web SDK
description: Descripción de cada fragmento de información que el SDK de Adobe Experience Cloud recopila automáticamente
seo-description: Descripción de cada fragmento de información que el SDK de Adobe Experience Cloud recopila automáticamente
keywords: collect information;context;configure;device;screenHeight;screen Height;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewport Height;viewportWidth;viewport Width;crowserDetails;browser details;implementationDetails;implementation Details;name;version;placeContext;localTime;local Time;localTimezoneOffset;local Timezone Offset;timestamp;web;url;webPageDetails;web Page Details;webReferrer;web Referrer;landscape;portrait;
translation-type: tm+mt
source-git-commit: e21374eb51ec1d572f6a4973d33cadf9ae17969b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 8%

---


# Información recopilada automáticamente

El SDK de Adobe Experience Cloud recopila una serie de datos automáticamente sin ninguna configuración especial. Sin embargo, esta información puede deshabilitarse si es necesario mediante la `context` opción del `configure` comando. [Consulte Configuración del SDK](../fundamentals/configuring-the-sdk.md). A continuación una lista de esos datos. El nombre entre paréntesis indica la cadena que se utilizará al configurar el contexto.

## Dispositivo (`device`)

Información sobre el dispositivo. Esto no incluye los datos que se pueden buscar en el servidor desde la cadena del agente de usuario.

### Altura de la pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Altura en píxeles de la pantalla.

### Orientación de la pantalla

| **Ruta en carga útil:** | **Valores posibles:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` O bien `portrait` |

La orientación de la pantalla.

### Ancho de la pantalla

| **Ruta en carga útil:** | **Ejemplo:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Ancho de la pantalla (en píxeles).

## Entorno (`environment`)

Detalles sobre el entorno del explorador.

### Tipo de entorno

Browser

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

El tipo de entorno por el que salió a la luz la experiencia. El SDK de Adobe Experience Platform para JavaScript siempre se establece `browser`.

### Altura de la ventanilla

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Altura del área de contenido del explorador (en píxeles).

### Ancho de la ventanilla

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

Identificador del kit de desarrollo de software (SDK).  Este campo utiliza un URI para mejorar la exclusividad entre los identificadores proporcionados por distintas bibliotecas de software.

### Versión

| **Ruta en carga útil:** | **Ejemplo:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Entorno

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Colocar contexto (`placeContext`)

Información sobre la ubicación del usuario final.

### Hora local

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Marca de hora local para el usuario final en formato ISO ampliado simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Desplazamiento de zona horaria local

| **Ruta en carga útil:** | **Ejemplo:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Número de minutos que el usuario se desplaza con respecto a GMT.

## Marca de tiempo

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Marca de hora del evento.  Esta parte del contexto no se puede eliminar.

Marca de hora UTC para el usuario final en formato ISO ampliado simplificado [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Detalles web (`web`)

Detalles sobre la página en la que se encuentra el usuario.

### Dirección URL de la página actual

| **Ruta en carga útil:** | **Ejemplo:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

La dirección URL de la página actual.

### URL de remitente del reenvío

| **Ruta en carga útil:** | **Ejemplo:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

Dirección URL de la página anterior visitada.
