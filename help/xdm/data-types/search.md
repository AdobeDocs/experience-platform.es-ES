---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;búsqueda;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Buscar tipo de datos
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de búsqueda (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de datos de búsqueda

 Búsquedas es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene información sobre la actividad de búsqueda web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `isPaid` | Booleano | Se utiliza para indicar si la búsqueda es paga o no. |
| `keywords` | Cadena | Las palabras clave para la búsqueda. |
| `pageDepth` | Número entero | Profundidad de página en los resultados de búsqueda. |
| `position` | Número entero | Posición o clasificación del listado en la página de resultados de la búsqueda. |
| `searchEngine` | Cadena | Motor de búsqueda utilizado por la búsqueda. |
| `searchEngineID` | Cadena | Identificador específico de la aplicación que se utiliza para identificar el motor de búsqueda. |
| `slot` | Cadena | Sección con nombre de la página donde apareció el resultado de la búsqueda. El valor de esta propiedad debe ser igual a uno de los valores de enumeración conocidos que defina, como `top`, `side` o `bottom`. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)