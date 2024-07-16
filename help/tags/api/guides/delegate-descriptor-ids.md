---
title: Delegación de ID de descriptor
description: Obtenga información sobre los ID de descriptor delegados en la API de Reactor y cómo vinculan recursos con extensiones.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 99%

---

# Delegación de ID de descriptor

Cuando se utilizan etiquetas en Adobe Experience Platform, todas las funcionalidades que se pueden implementar en el sitio las proporcionan las extensiones. El desarrollador de extensiones define las funcionalidades proporcionadas por cada extensión. Cuando se implementa una extensión, se agrupa con sus distintas funcionalidades en forma de [paquete de extensiones](../endpoints/extension-packages.md). Las funcionalidades que los desarrolladores añaden a un paquete de extensiones se consideran “delegados” de ese paquete.

A cada delegado de un paquete de extensiones se le asigna un ID de descriptor delegado único. El ID del descriptor delegado de un recurso determinado indica al sistema qué tipo de recurso es y a qué paquete de extensiones pertenece.

## Sintaxis

Un ID de descriptor delegado consta de tres cadenas unidas por dos puntos (`::`), que representan el nombre del paquete de extensiones, el tipo delegado y el nombre delegado, respectivamente. Estas cadenas están compuestas para ser legibles en lenguaje natural, y el sistema las genera y asigna automáticamente cuando se incorpora un paquete de extensiones.

Por ejemplo, si un paquete de extensiones denominado `example-package`tiene una acción denominada`custom-code`, dicha acción tendría el siguiente ID de descriptor delegado: `example-package::actions::custom-code`.

## Uso de ID de descriptor delegado en recursos aplicables

Los ID de descriptor delegados son importantes para comprender la definición de componentes de regla (eventos, condiciones y acciones) y elementos de datos en la API. Las secciones siguientes describen cómo entran en juego estos ID para cada recurso.

### Componentes de regla

Un [componente de regla](../endpoints/rule-components.md) debe estar asociado a un evento, condición o acción que pertenezca a un paquete de extensión. Representa el “tipo” del componente de regla en lo que respecta a la lógica de la regla general (un evento, una condición o una acción). Por lo tanto, al crear un componente de regla, se debe proporcionar un ID de descriptor delegado para indicar a qué evento, condición o acción se debe asociar el componente de regla.

Por ejemplo, para crear un componente de regla de evento basado en un evento `click` en un paquete de extensión `example-package`, el componente de regla utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::events::click`.

Consulte la sección sobre [creación de un componente de regla](../endpoints/rule-components.md#create) para obtener más información.

### Elementos de datos

Un [elemento de datos](../endpoints/data-elements.md) debe asociarse con un paquete de extensión cuando se crea por primera vez, ya que cada paquete de extensión define los tipos compatibles para sus elementos de datos delegados, así como su comportamiento deseado.

Por ejemplo, para crear un elemento de datos que utilice el tipo `cookie` como se define en el paquete de extensión `example-package`, el elemento de datos utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::dataElements::cookie`.

Consulte la sección sobre [creación de un elemento de datos](../endpoints/data-elements.md#create) para obtener más información.

### Extensiones

Una [extensión](../endpoints/extensions.md) se asocia automáticamente a un paquete de extensión cuando se crea por primera vez y se representa dentro del objeto `relationships` de la extensión. Si la extensión requiere una configuración personalizada, también requiere un ID de descriptor delegado.

>[!NOTE]
>
>Las extensiones que no requieren configuración personalizada no necesitan un ID de descriptor delegado.

Por ejemplo, para añadir un ID de descriptor delegado a una extensión que pertenece al paquete de extensión `example-package`, la extensión utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Consulte la guía sobre [creación de una extensión](../endpoints/extensions.md#create) para obtener más información.
