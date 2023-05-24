---
title: Notas de la versión de Google Data Layer Extension
description: Últimas notas de la versión de la extensión de capa de datos de Google en Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Notas de la versión de Google Data Layer Extension

## Versión 1.0.4

* Lanzamiento público en versión beta de la extensión.

## Versión 1.0.6

* Adición de una acción para restablecer la capa de datos al estado calculado.
* Se han corregido errores en los elementos de datos que evitaban la recuperación de valores desde el estado calculado.

## Versión 1.1.1

Una mejora significativa y la corrección de errores resultantes de los comentarios sobre las pruebas beta.

* Se corrige un problema en el cual un elemento de datos de extensión de capa de datos de Google vacío utilizado en una regla que no es de capa de datos (por ejemplo, Library Loaded) devolvía el objeto de capa de datos, no el estado calculado.
* Corrige un problema en el cual el estado calculado de la capa de datos no se pasaba desde el asistente en eventos en el momento de la activación del evento, sino en el momento de la ejecución de la regla.
* Agrega un conmutador al cuadro de diálogo de elementos de datos que permite al usuario elegir si solo se deben devolver valores de eventos.
* Corrige un problema en el cual los oyentes de eventos de regla no capturaban correctamente el historial de eventos.
* Pequeñas mejoras en la claridad del código.

## Versión 1.2.0

* Agrega una acción para insertar en la capa de datos mediante un cuadro de diálogo multicampo clave-valor.
* Se ha corregido un error que impedía que la extensión se cargara cuando las etiquetas se implementaban sincrónicamente.
* Se ha corregido un error que provocaba un error al guardar un elemento de datos en algunas circunstancias.
* Agrega documentación al cuadro de diálogo de evento que explica el uso del objeto de evento Etiquetas.
* Agrega una advertencia sobre bucles infinitos al cuadro de diálogo del evento.
