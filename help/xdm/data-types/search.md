---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;búsqueda;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Buscar tipo de datos
description: Este documento proporciona información general sobre el tipo de datos del modelo de datos de experiencia de búsqueda (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---

# [!UICONTROL Buscar] tipo de datos

[!UICONTROL Buscar] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene información sobre la actividad de búsqueda web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `isPaid` | Booleano | Se utiliza para indicar si la búsqueda es de pago o no. |
| `keywords` | Cadena | Las palabras clave para la búsqueda. |
| `pageDepth` | Número entero | Profundidad de página en los resultados de búsqueda. |
| `position` | Número entero | La posición o rango de la lista en la página de resultados de búsqueda. |
| `searchEngine` | Cadena | Motor de búsqueda utilizado por la búsqueda. |
| `searchEngineID` | Cadena | El identificador específico de la aplicación utilizado para identificar el motor de búsqueda. |
| `slot` | Cadena | La sección con nombre de la página donde apareció el resultado de la búsqueda. El valor de esta propiedad debe ser igual a uno de los valores de enumeración conocidos que defina, como `top`, `side`, o `bottom`. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
