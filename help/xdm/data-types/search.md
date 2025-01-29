---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;búsqueda;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Buscar tipo de datos
description: Obtenga información acerca del tipo de datos Modelo de datos de experiencia de búsqueda (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---

# [!UICONTROL Buscar] tipo de datos

[!UICONTROL Buscar] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene información sobre la actividad de búsqueda web.

![buscar imagen](../images/data-types/search.PNG){width=500}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `isPaid` | Booleano | Se utiliza para indicar si la búsqueda es de pago o no. |
| `keywords` | Cadena | Las palabras clave para la búsqueda. |
| `pageDepth` | Entero | Profundidad de página en los resultados de búsqueda. |
| `position` | Entero | La posición o rango de la lista en la página de resultados de búsqueda. |
| `searchEngine` | Cadena | El motor de búsqueda usado por la búsqueda. |
| `searchEngineID` | Cadena | El identificador específico de la aplicación utilizado para identificar el motor de búsqueda. |
| `slot` | Cadena | La sección con nombre de la página donde apareció el resultado de la búsqueda. El valor de esta propiedad debe ser igual a uno de los valores de enumeración conocidos que defina, como `top`, `side` o `bottom`. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
