---
title: Notas de la versión de la extensión de capa de datos del cliente de Adobe
description: Últimas notas de la versión de la extensión de capa de datos del cliente de Adobe en Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 100%

---

# Notas de la versión de la extensión de capa de datos del cliente de Adobe

## Versión 2.0.2

* Carga de la biblioteca principal ACDL (versión 2.0.2)
* La versión 2.0.0 de la biblioteca principal ACDL ha eliminado la capacidad de aprovechar event.beforeState y event.afterState. Por lo tanto, hemos modificado estos objetos para que siempre devuelvan objetos vacíos. Las implementaciones que dependen de esta funcionalidad deberán actualizarse al pasar a esta versión.

## Versión 1.1.3

* Carga de la biblioteca principal ACDL (versión 1.1.3)

## Versión 1.1.2

La extensión proporciona la siguiente funcionalidad en el lanzamiento inicial:

* Carga de la biblioteca principal ACDL (versión 1.1.1)
* Cambio del nombre de la capa de datos de Adobe
* Eventos:
   * Escucha de todos los eventos
   * Escuchar todos los datos insertados
   * Escucha de un evento específico insertado
   * Todos los eventos se pueden escuchar en diferentes ámbitos
* Elementos de datos:
   * Estado calculado: Estado global o específico
   * Tamaño de la capa de datos
* Acciones:
   * Restablezca el tamaño de la capa de datos (conservando el último estado calculado)
   * Insertar objeto en la capa de datos
