---
title: Paginación de respuestas en la API de Reactor
description: Obtenga información sobre cómo paginar los resultados al enumerar recursos en la API de Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Paginación de respuestas en la API de Reactor

Las respuestas devueltas por la API de Reactor se paginan. El tamaño de página predeterminado es de 25 elementos. Los detalles sobre la paginación se incluyen en la sección `meta.pagination `del objeto de respuesta de API:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

Es posible obtener una página específica y modificar el tamaño de una página incluyendo un parámetro de consulta `page` en la ruta de solicitud.

## Recuperar una página específica

Para obtener una página específica:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Cambiar el tamaño de la página

Para cambiar el tamaño de la página:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

Se pueden combinar distintas opciones:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
