---
title: Flujo de extensión web
description: Descubra cómo los componentes de extensión web interactúan entre sí durante la ejecución en Adobe Experience Platform.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 93%

---

# Flujo de extensión web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En las extensiones web, cada evento, condición, acción y tipo de elemento de datos tiene una vista que permite a los usuarios modificar la configuración y un módulo de biblioteca para modificar en función de la configuración definida por el usuario.

Como se muestra en el siguiente diagrama de alto nivel, la vista de tipo de evento de la extensión se mostrará dentro de un iframe en la aplicación integrada con Adobe Experience Platform. El usuario utiliza la vista para modificar la configuración que luego se guarda en Platform. Cuando se crea la biblioteca de tiempo de ejecución de etiquetas, tanto el módulo de biblioteca de tipo de evento de la extensión como la configuración definida por el usuario se incluirán en la biblioteca de tiempo de ejecución. En tiempo de ejecución, Platform insertará la configuración definida por el usuario en el módulo de biblioteca.

![Diagrama de flujo de extensión](../images/flow/web/extension-flow.png)

En el diagrama siguiente se puede ver el vínculo existente entre eventos, condiciones y acciones dentro del flujo de procesamiento de reglas.

![Diagrama de flujo de procesamiento de reglas](../images/flow/web/rule-processing-flow.png)

El flujo de procesamiento de reglas contiene las fases siguientes:

1. Los métodos `settings` y `trigger` se proporcionan al módulo de biblioteca de evento durante el inicio.
1. Cuando el módulo de biblioteca de evento determina que se ha producido el evento, el módulo de biblioteca de evento llama a `trigger`.
1. Las etiquetas pasan `settings` a los módulos de la biblioteca de condiciones de la regla en los que se evalúan las condiciones.
1. Cada módulo de biblioteca de condiciones devuelve si una condición se evalúa como verdadera.
1. Si se cumplen todas las condiciones, se ejecutan las acciones de la regla.
