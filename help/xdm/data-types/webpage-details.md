---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;Detalles de la página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de detalles de página Web
topic: overview
description: Este documento proporciona información general sobre los detalles de la página web del tipo de datos del Modelo de datos de experiencia (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# [!UICONTROL Tipo de datos de ] detalles de página Web

[!UICONTROL Los ] detalles de una página web son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles sobre una página web que se acaba de cargar y ver, tal como lo registra un evento ExperienceEvent.

El tipo de datos está diseñado para los detalles de página completa y las cargas iniciales de página de aplicaciones Web de una sola página (SPA). Para las interacciones que se producen en una página cargada que no déclencheur una carga de página nueva, consulte el tipo de datos [interacción Web](./web-interactions.md).

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medida]](./measure.md) | El número de vistas en una página web. |
| `URL` | Cadena | Dirección URL normal o habitual de la página web. Puede que sea o no la dirección URL real que se utiliza para llegar a la página. Para registrar la dirección URL utilizada para llegar a la página, utilice `webLink`. El formato URI debe seguir el estándar [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de error o no. Este indicador se utiliza para categorizar ampliamente las interacciones web. El error lo define la aplicación y puede corresponderse con una página servida con un código de error HTTP. |
| `isHomePage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de inicio o no. Este indicador se utiliza para categorizar ampliamente las interacciones web. La definición de página de inicio viene determinada por la solicitud. |
| `name` | Cadena | Nombre normativo de la página web. Este nombre no es necesariamente el título de la página o se asocia directamente con el contenido de la misma, sino que se utiliza para organizar las páginas de un sitio con fines de clasificación. |
| `server` | Cadena | Servidor normativo o habitual que aloja la página web. Puede ser o no el host o servidor que realmente sirvió para la interacción de la página. |
| `siteSection` | Cadena | Nombre normativo de la sección del sitio donde reside esta página Web. Se puede utilizar para clasificar o categorizar la interacción. |
| `viewName` | Cadena | El nombre de la vista, dentro de una página. Esta propiedad se utiliza comúnmente con aplicaciones de una sola página o páginas que tienen fichas o controles que cambian la mayoría del diseño de la página. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)