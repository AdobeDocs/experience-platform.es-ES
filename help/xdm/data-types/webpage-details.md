---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;Detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de detalles de página web
description: Obtenga información sobre los detalles de la página web del tipo de datos del Modelo de datos de experiencia (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 11%

---

# [!UICONTROL Detalles de página web] tipo de datos

[!UICONTROL Detalles de página web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de una página web que acaba de cargarse y verse, según lo registrado por un ExperienceEvent.

SPA El tipo de datos está diseñado para obtener detalles de página completa y cargas de página iniciales de aplicaciones web de una sola página (). Para las interacciones que se producen en una página cargada que no almacena en déclencheur una nueva carga de página, consulte el tipo de datos [web interaction](./web-interaction.md).

![detalles de página web](../images/data-types/web-page-details.PNG){width="500"}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medida]](./measure.md) | Número de vistas de una página web. |
| `URL` | Cadena | La URL normativa o habitual de la página web. Puede ser o no la dirección URL real utilizada para llegar a la página. Para registrar la dirección URL usada para llegar a la página, use `webLink`. El formato URI debe seguir el estándar [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de error o no. Este indicador se utiliza para categorizar las interacciones web en un sentido amplio. El error lo define la aplicación y puede corresponder a una página servida con un código de error HTTP. |
| `isHomePage` | Booleano | Esta propiedad utiliza un indicador para indicar si la página es una página de inicio o no. Este indicador se utiliza para categorizar las interacciones web en un sentido amplio. La definición de página principal viene determinada por la aplicación. |
| `name` | Cadena | El nombre normativo de la página web. Este nombre no es necesariamente el título de la página ni está asociado directamente con el contenido de la página, pero se utiliza para organizar las páginas de un sitio con fines de clasificación. |
| `server` | Cadena | El servidor normativo o habitual que aloja la página web. Puede ser o no el host o servidor que realmente sirvió a la interacción de la página. |
| `siteSection` | Cadena | El nombre normativo de la sección del sitio donde reside esta página web. Esto puede utilizarse para clasificar o categorizar la interacción. |
| `viewName` | Cadena | Nombre de la vista, dentro de una página. Esta propiedad se utiliza normalmente en aplicaciones de una sola página o páginas que tienen fichas o controles que cambian la mayor parte del diseño de página. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
