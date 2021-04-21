---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;esquemas;búsqueda;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de búsqueda
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de búsqueda (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---

# [!UICONTROL Search] tipo de datos

[!UICONTROL Search] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene información sobre la actividad de búsqueda web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `isPaid` | Booleano | Se utiliza para indicar si la búsqueda es de pago o no. |
| `keywords` | Cadena | Las palabras clave de la búsqueda. |
| `pageDepth` | Número entero | La profundidad de página en los resultados de búsqueda. |
| `position` | Número entero | Posición o clasificación de la lista en la página de resultados de la búsqueda. |
| `searchEngine` | Cadena | Motor de búsqueda utilizado por la búsqueda. |
| `searchEngineID` | Cadena | Identificador específico de la aplicación que se usa para identificar el motor de búsqueda. |
| `slot` | Cadena | Sección con nombre de la página donde apareció el resultado de la búsqueda. El valor de esta propiedad debe ser igual a uno de los valores de enumeración conocidos que defina, como `top`, `side` o `bottom`. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
