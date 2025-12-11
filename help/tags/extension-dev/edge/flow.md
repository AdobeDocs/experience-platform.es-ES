---
title: Flujo de extensión de Edge
description: Descubra cómo los componentes de una extensión de Edge en Adobe Experience Platform interactúan entre sí durante la ejecución.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 78%

---

# Flujo de extensión de Edge

En las extensiones de Edge, cada evento, condición, acción y tipo de elemento de datos tiene una vista que permite a los usuarios modificar la configuración y un módulo de biblioteca que se puede modificar en función de la configuración definida por el usuario.

Como se muestra en el siguiente diagrama de alto nivel, la vista de tipo de evento de la extensión se mostrará dentro de un iframe en la aplicación integrada con Adobe Experience Platform. A continuación, la vista se utiliza para modificar la configuración que luego se guarda en Experience Platform. Cuando se crea la biblioteca de tiempo de ejecución de etiquetas, tanto el módulo de biblioteca de tipo de evento de la extensión como la configuración definida por el usuario se incluirán en la biblioteca que se implementa en el nodo Edge. La configuración definida por el usuario desde Experience Platform se inserta en el módulo de biblioteca durante la ejecución.

![Diagrama de flujo de extensión](../images/flow/edge/event-processing-flow.png)

En el diagrama siguiente se puede ver el vínculo existente entre eventos, condiciones y acciones dentro del flujo de procesamiento de reglas.

![Diagrama de flujo de procesamiento de reglas](../images/flow/edge/rule-processing-flow.png)

El flujo de procesamiento de reglas contiene las fases siguientes:

1. Los métodos `settings` y `trigger` se proporcionan al módulo de biblioteca de evento durante el inicio.
1. Cuando el módulo de biblioteca de evento determina que se ha producido el evento, el módulo de biblioteca de evento llama a `trigger`.
1. Experience Platform pasa `settings` a los módulos de la biblioteca de tipo de condición de la regla en los que se evalúan las condiciones.
1. Cada tipo de condición muestra si una condición se evalúa como verdadera.
1. Si se cumplen todas las condiciones, se ejecutan las acciones de la regla.
