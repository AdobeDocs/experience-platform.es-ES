---
title: Clasificación de respuestas en la API de Reactor
description: Obtenga información sobre cómo filtrar los resultados al enumerar recursos en la API de Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Clasificación de respuestas en la API de Reactor

La lista de extremos en la API de Reactor permite ordenar los recursos devueltos en función de atributos especificados. Puede configurar el orden de la respuesta suministrando un parámetro `sort` en la ruta de solicitud.

## Orden ascendente

Los recursos se pueden ordenar por un atributo en orden ascendente especificando la variable
atributo por el que ordenar y añadirlo como prefijo a `+`:

`GET /companies/:company_id/properties?sort=+name`

## Orden descendente

Los recursos se pueden ordenar por un atributo en orden descendente especificando la variable
atributo por el que ordenar y añadirlo como prefijo a `-`:

`GET /companies/:company_id/properties?sort=-name`

## Múltiples ordenamientos

Para ordenar por varios valores, proporcione las directivas de ordenación separadas por coma
lista:

`GET /companies/:company_id/properties?sort=+name,-org_id`
