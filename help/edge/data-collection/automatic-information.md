---
title: Información recopilada automáticamente
description: Información general sobre los datos que el SDK web de Adobe Experience Platform recopila automáticamente.
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# Información recopilada automáticamente

El SDK web de Adobe Experience Platform recopila automáticamente parte de la información de forma predeterminada. Si su organización no desea recopilar automáticamente estos datos, puede utilizar la variable `context` en la opción [`configure` mando](../fundamentals/configuring-the-sdk.md).

Palabras clave excluidas de `context` no se incluyen en la recopilación de datos. Si la variable `context` La matriz no existe en `configure` , todos los datos de la tabla siguiente se recopilan automáticamente.

| Nombre | Descripción | `context` palabra clave matricial | Ruta de XDM | Valor de ejemplo |
| --- | --- | --- | --- | --- |
| Altura de pantalla | Altura de la pantalla en píxeles. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Anchura de pantalla | Ancho de la pantalla en píxeles. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Orientación de pantalla | La orientación de la pantalla. | `device` | `events[].xdm.device.screenOrientation` | `landscape` o `portrait` |
| Tipo de entorno | El tipo de entorno a través del cual surgió la experiencia. El SDK web de Adobe Experience Platform siempre establece este campo como `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Altura de ventanilla | Altura del área de contenido del explorador en píxeles. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Anchura de ventanilla | Anchura del área de contenido del explorador en píxeles. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| Nombre del SDK | El identificador del SDK. Este campo utiliza un URI para mejorar la exclusividad entre los identificadores proporcionados por diferentes bibliotecas de software. Cuando se utiliza la biblioteca independiente, el valor es `https://ns.adobe.com/experience/alloy`. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, el valor es `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| Versión de SDK | Cuando se utiliza la biblioteca independiente, el valor es la versión de la biblioteca. Cuando la biblioteca se utiliza como parte de la extensión de etiqueta, el valor es una concatenación de la versión de la biblioteca y la versión de la extensión de etiqueta. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Entorno | Entorno donde se recopilaron los datos. El SDK web de Adobe Experience Platform siempre establece este campo como `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Hora local | Marca de tiempo local para el usuario final en formato ISO extendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Desplazamiento de zona horaria local | Número de minutos que el usuario está desfasado de GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Marca de tiempo | La marca de tiempo UTC para el usuario final en formato ISO extendido simplificado [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Siempre incluido | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| URL de la página actual | Dirección URL de la página actual. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL de referente | La URL de la página anterior visitada. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
