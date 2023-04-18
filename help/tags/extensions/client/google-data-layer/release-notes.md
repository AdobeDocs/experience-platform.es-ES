---
title: Notas de la versión de la extensión de la capa de datos de Google
description: Últimas notas de la versión de la extensión de etiqueta de capa de datos de Google en Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Notas de la versión de la extensión de la capa de datos de Google

## Versión 1.0.4

* Versión beta pública de la extensión.

## Versión 1.0.6

* Adición de una acción para restablecer la capa de datos al estado calculado.
* Se corrigieron errores en el elemento de datos que impiden la captura de valores desde el estado calculado.

## Versión 1.1.1

Una mejora importante y una versión corregida de errores resultantes de los comentarios de las pruebas beta.

* Se corrige un problema en el que un elemento de datos de extensión de capa de datos de Google vacío que se utilizaba en una regla de capa que no era de datos (por ejemplo, Library Loaded) devolvía el objeto de capa de datos, no el estado calculado.
* Corrige un problema en el cual el estado calculado de la capa de datos no se pasaba del ayudante en eventos en el momento de la activación del evento, sino en el momento de la ejecución de la regla.
* Agrega un botón de alternancia al cuadro de diálogo del elemento de datos que permite al usuario elegir si solo se deben devolver valores de eventos.
* Corrige un problema en el cual los oyentes de eventos de regla no capturaban correctamente el historial de eventos.
* Mejoras menores en la claridad del código.

## Versión 1.2.0

* Añade una acción para insertar en la capa de datos mediante un cuadro de diálogo multicampo de valor clave.
* Corrige un error que impedía la carga de la extensión cuando las etiquetas se implementaban sincrónicamente.
* Corrige un error que causaba un error al guardar un elemento de datos en determinadas circunstancias.
* Agrega documentación al cuadro de diálogo de evento explicando el uso del objeto de evento Etiquetas .
* Agrega una advertencia sobre los bucles infinitos al cuadro de diálogo de eventos.
