---
title: Tipo de datos de búsqueda interna del sitio
description: Obtenga información acerca del tipo de datos XDM de búsqueda interna del sitio.
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# [!UICONTROL Búsqueda interna del sitio] tipo de datos

[!UICONTROL Búsqueda interna del sitio] es un tipo de datos XDM estándar que describe una búsqueda del sitio interna, incluidos todos los comportamientos y detalles de búsqueda relacionados.

![](../images/data-types/internal-site-search.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booleana] | Indica si un visitante utilizó un valor de búsqueda sugerido o autocompletado para ejecutar la búsqueda. |
| `autoCompleteTypedValue` | [!UICONTROL Cadena] | En los casos de autocompletar, los usuarios suelen abandonar la búsqueda y seleccionar un término específico en la lista desplegable. Este valor registra lo que el usuario comenzó a escribir para generar el conjunto específico de términos de búsqueda sugeridos. |
| `autoCompleteValue` | [!UICONTROL Cadena] | En los casos de autocompletar, los usuarios suelen abandonar la búsqueda y seleccionar un término específico en el menú desplegable. Este valor se utiliza para realizar un seguimiento de los términos específicos seleccionados. |
| `instances` | [!UICONTROL Entero] | El número de veces que se produjo la búsqueda interna del sitio. |
| `locationInPage` | [!UICONTROL Cadena] | Cuando hay varios cuadros de búsqueda en la página, este valor debe usarse para identificar la ubicación específica que el usuario usó para realizar la búsqueda. |
| `nullInstances` | [!UICONTROL Entero] | El número de veces que se produjo la búsqueda del sitio interno que no arrojó resultados. |
| `numberOfResults` | [!UICONTROL Entero] | Número total de resultados de búsqueda devueltos. |
| `postalCode` | [!UICONTROL Cadena] | El código postal utilizado para la búsqueda, si corresponde. |
| `productFindingMethods` | [!UICONTROL Cadena] | El valor del término de búsqueda del sitio interno con enlace de comercialización. Este valor indica qué término se buscó inmediatamente antes de ver un producto. |
| `radiusDistance` | [!UICONTROL Entero] | Combinado con `radiusType`, indica la distancia seleccionada del radio de búsqueda. |
| `radiusType` | [!UICONTROL Entero] | El tipo de distancia seleccionado de `radiusDistance`, ya sea millas o kilómetros. |
| `refinementInstances` | [!UICONTROL Entero] | El número de veces que se refinó la búsqueda del sitio interno. |
| `refinementType` | Matriz de cadenas | Enumera los tipos de refinamiento aplicados a los resultados de búsqueda. Algunos ejemplos son departamento, marca, precio, en tienda, calificación, color, material, etc. |
| `refinementValue` | [!UICONTROL Cadena] | El valor al que se refinó la búsqueda. |
| `resultsPageNumber` | [!UICONTROL Entero] | Para los resultados de búsqueda paginados, este valor rastrea la página de resultados que está viendo el visitante. |
| `resultsPerPage` | [!UICONTROL Entero] | En el caso de los resultados de búsqueda paginados, este valor rastrea el número de resultados de búsqueda mostrados por página. |
| `searchType` | [!UICONTROL Cadena] | Registra el método de búsqueda que se está ejecutando, si corresponde. Algunos ejemplos son una búsqueda de escritura anticipada, una búsqueda de escritura directa o cualquier otro tipo de funcionalidad de búsqueda personalizada que pueda tener un sitio. |
| `sortOrder` | [!UICONTROL Cadena] | Combinado con `sortType`, indica el orden de los resultados de búsqueda, ya sea ascendente o descendente. |
| `term` | [!UICONTROL Cadena] | El término de búsqueda interno del sitio especificado por el visitante. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
