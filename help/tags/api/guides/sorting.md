---
title: Clasificación de respuestas en la API de Reactor
description: Obtenga información sobre cómo filtrar los resultados al enumerar recursos en la API de Reactor.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---

# Clasificación de respuestas en la API de Reactor

La lista de puntos finales en la API de Reactor permite ordenar los recursos devueltos en función de atributos especificados. Puede configurar el orden de la respuesta suministrando un parámetro `sort` en la ruta de solicitud.

## Orden ascendente

Los recursos se pueden ordenar por un atributo en orden ascendente especificando el atributo
por el que ordenar y añadirlo como prefijo a `+`:

`GET /companies/:company_id/properties?sort=+name`

## Orden descendente

Los recursos se pueden ordenar por un atributo en orden descendente especificando el atributo por el que ordenar y añadirlo como prefijo a `-`:

`GET /companies/:company_id/properties?sort=-name`

## Múltiples ordenamientos

Para ordenar por varios valores, proporcione las directivas de ordenación como una lista de elementos separados por coma:

`GET /companies/:company_id/properties?sort=+name,-org_id`
