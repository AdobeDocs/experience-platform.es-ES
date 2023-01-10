---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de detalles de página web
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia (XDM) de la página web.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 4%

---

# [!UICONTROL Detalles de la página web] tipo de datos

[!UICONTROL Detalles de la página web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles sobre una página web que acaba de cargarse y visualizarse, tal como lo registró un ExperienceEvent.

El tipo de datos está pensado para detalles de página completos y cargas de página iniciales de aplicaciones web de una sola página (SPA). Para las interacciones que están ocurriendo en una página cargada que no déclencheur una nueva carga de página, consulte la [interacción web](./web-interaction.md) tipo de datos.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medida]](./measure.md) | Número de vistas en una página web. |
| `URL` | Cadena | Dirección URL normal o habitual de la página web. Puede ser o no la dirección URL real que se usa para llegar a la página. Para registrar la dirección URL utilizada para llegar a la página, use `webLink`. El formato URI debe seguir el [RFC 3986](https://tools.ietf.org/html/rfc3986) estándar. |
| `isErrorPage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de error o no. Este indicador se utiliza para categorizar de forma amplia las interacciones web. El error lo define la aplicación y se puede corresponder a una página servida con un código de error HTTP. |
| `isHomePage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de inicio o no. Este indicador se utiliza para categorizar de forma amplia las interacciones web. La definición de la página principal viene determinada por la aplicación. |
| `name` | Cadena | Nombre normativo de la página web. Este nombre no es necesariamente el título de la página o se asocia directamente con el contenido de la página, pero se utiliza para organizar las páginas de un sitio con fines de clasificación. |
| `server` | Cadena | Servidor normativo o habitual que aloja la página web. Puede ser o no el host o servidor que realmente sirvió para la interacción de la página. |
| `siteSection` | Cadena | Nombre normativo de la sección del sitio donde reside esta página web. Se puede utilizar para clasificar o categorizar la interacción. |
| `viewName` | Cadena | Nombre de la vista, dentro de una página. Esta propiedad se utiliza comúnmente con aplicaciones de una sola página o páginas que tienen pestañas o controles que cambian la mayoría del diseño de la página. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
