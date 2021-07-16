---
title: Delegar ID de descriptor
description: Obtenga información sobre los ID de descriptor delegados en la API de Reactor y cómo vinculan recursos con extensiones.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# Delegar ID de descriptor

Cuando se utilizan etiquetas en Adobe Experience Platform, todas las funcionalidades que se pueden implementar en el sitio las proporcionan las extensiones. El desarrollador de extensiones define las capacidades proporcionadas por cada extensión. Cuando se implementa una extensión, se agrupa con sus distintas capacidades en forma de [extension package](../endpoints/extension-packages.md). Las funcionalidades que los desarrolladores añaden a un paquete de extensión se consideran &quot;delegados&quot; de ese paquete.

A cada delegado dentro de un paquete de extensión se le asigna un ID de descriptor delegado único. El ID del descriptor delegado de un recurso determinado indica al sistema qué tipo de recurso es y a qué paquete de extensión pertenece.

## Sintaxis

Un ID de descriptor delegado consta de tres cadenas unidas por dos puntos (`::`), que representan el nombre del paquete de extensión, el tipo delegado y el nombre delegado, respectivamente. Estas cadenas están compuestas para ser legibles por el usuario y el sistema las genera y asigna automáticamente cuando se incorpora un paquete de extensión.

Por ejemplo, si un paquete de extensión denominado `example-package` tiene una acción denominada `custom-code`, dicha acción tendría el siguiente ID de descriptor delegado: `example-package::actions::custom-code`.

## Uso de ID de descriptor delegado en recursos aplicables

Los ID de descriptor delegados son importantes para comprender a la hora de definir componentes de regla (eventos, condiciones y acciones) y elementos de datos en la API. Las secciones siguientes describen cómo entran en juego estos ID para cada recurso.

### Regla componentes

Un [componente de regla](../endpoints/rule-components.md) debe estar asociado a un evento, condición o acción que pertenezca a un paquete de extensión. Representa el &quot;tipo&quot; del componente de regla en lo que respecta a la lógica de la regla general (un evento, una condición o una acción). Por lo tanto, al crear un componente de regla, se debe proporcionar un ID de descriptor delegado para indicar a qué evento, condición o acción se debe asociar el componente de regla.

Por ejemplo, para crear un componente de regla de evento basado en un evento `click` en un paquete de extensión `example-package`, el componente de regla utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::events::click`.

Consulte la sección sobre [creación de un componente de regla](../endpoints/rule-components.md#create) para obtener más información.

### Elementos de datos

Un [elemento de datos](../endpoints/data-elements.md) debe asociarse con un paquete de extensión cuando se cree por primera vez, ya que cada paquete de extensión define los tipos compatibles para sus elementos de datos delegados, así como su comportamiento deseado.

Por ejemplo, para crear un elemento de datos que utilice el tipo `cookie` como se define en el paquete de extensión `example-package`, el elemento de datos utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::dataElements::cookie`.

Consulte la sección sobre [creación de un elemento de datos](../endpoints/data-elements.md#create) para obtener más información.

### Extensiones

Una [extensión](../endpoints/extensions.md) se asocia automáticamente a un paquete de extensión cuando se crea por primera vez y se representa dentro del objeto `relationships` de la extensión. Si la extensión requiere una configuración personalizada, también requiere un ID de descriptor delegado.

>[!NOTE]
>
>Las extensiones que no requieren configuración personalizada no necesitan un ID de descriptor delegado.

Por ejemplo, para añadir un ID de descriptor delegado a una extensión que pertenece al paquete de extensión `example-package`, la extensión utilizaría el siguiente valor `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Consulte la guía sobre [creación de una extensión](../endpoints/extensions.md#create) para obtener más información.