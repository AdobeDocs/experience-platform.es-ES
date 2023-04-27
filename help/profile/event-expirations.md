---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;conjunto de datos;tiempo de vida;ttl;tiempo de vida;
solution: Experience Platform
title: Caducidad del evento de experiencia
description: Este documento proporciona una guía general sobre cómo configurar los tiempos de caducidad para eventos de experiencia individuales dentro de un conjunto de datos de Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: bb2d0075b234ec750046e1f28cac07a58a9d7e72
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Caducidad de eventos de experiencia

En Adobe Experience Platform, puede configurar los tiempos de caducidad de todos los eventos de experiencia que se incorporan en un conjunto de datos habilitado para [Perfil del cliente en tiempo real](./home.md). Esto le permite eliminar automáticamente los datos del Almacenamiento de perfiles que ya no son válidos ni útiles para sus casos de uso.

Las caducidades de los eventos de experiencia no se pueden configurar mediante la interfaz de usuario de Platform ni las API. En su lugar, debe ponerse en contacto con el servicio de asistencia para habilitar las caducidades de los eventos de experiencia en los conjuntos de datos necesarios.

>[!IMPORTANT]
>
>Las caducidades de los eventos de experiencia no se deben confundir con las caducidades de los conjuntos de datos, que eliminan todo el conjunto de datos una vez que se alcanza la fecha de caducidad. Estos se configuran manualmente mediante [Higiene de los datos de Adobe Experience Platform](../hygiene/home.md).

## Proceso de caducidad automatizada

Una vez que las caducidades de los eventos de experiencia se han habilitado en un conjunto de datos habilitado para el perfil, Platform aplica automáticamente los valores de caducidad de cada evento capturado en un proceso de dos pasos:

1. Todos los datos nuevos que se incorporan al conjunto de datos tienen el valor de caducidad aplicado en el momento de la ingesta en función de la marca de tiempo del evento.
1. Todos los datos existentes en el conjunto de datos tienen el valor de caducidad aplicado retroactivamente como un trabajo único del sistema de relleno. Una vez que el valor de caducidad se haya colocado en el conjunto de datos, los eventos anteriores al valor de caducidad se perderán inmediatamente en cuanto se ejecute el trabajo del sistema. Todos los demás eventos se eliminarán en cuanto alcancen sus valores de caducidad desde la marca de tiempo del evento. Cuando se hayan eliminado todos los eventos de experiencia, si el perfil ya no tiene atributos de perfil, el perfil dejará de existir.

>[!WARNING]
>
>Una vez aplicados, cualquier dato anterior al número de días asignado por el valor de caducidad es **eliminado permanentemente** y no se pueden restaurar.

Por ejemplo, si aplicara un valor de caducidad de 30 días el 15 de mayo, se producirían los siguientes pasos:

1. Todos los eventos nuevos obtienen un valor de caducidad de 30 días que se aplica a medida que se incorporan.
1. Todos los eventos existentes con una marca de tiempo anterior al 15 de abril se eliminan inmediatamente con el trabajo del sistema.
1. Todos los eventos existentes con una marca de tiempo más reciente que el 15 de abril tienen un valor de caducidad de 30 días después de la marca de tiempo del evento. Por lo tanto, si un evento tiene una marca de tiempo del 18 de abril, se elimina 30 días después de la fecha de la marca de tiempo, que sería el 18 de mayo.

## Efectos en la segmentación

Debe asegurarse de que las ventanas retrospectivas de sus segmentos se encuentran dentro de los límites de caducidad de sus conjuntos de datos dependientes para mantener los resultados precisos. Por ejemplo, si aplica un valor de caducidad de 30 días y tiene un segmento que intenta ver datos de hace hasta 45 días, es probable que la audiencia resultante no sea precisa.

Por lo tanto, debe mantener el mismo valor de caducidad del evento de experiencia para todos los conjuntos de datos, si es posible, para evitar el impacto de diferentes valores de caducidad en diferentes conjuntos de datos en la lógica de segmentación.

## Preguntas frecuentes {#faq}

En la siguiente sección se enumeran las preguntas más frecuentes sobre la caducidad de datos de Evento de experiencia:

### ¿En qué se diferencia la caducidad de los datos de Evento de experiencia de la caducidad de los datos de Perfil seudónimos?

La caducidad de los datos del evento de experiencia y la caducidad de los datos del perfil seudónimos son características complementarias.

#### Granularidad

La caducidad de datos de Evento de experiencia funciona en un evento **conjunto de datos** nivel. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

La caducidad de datos de perfil pseudoanónima funciona en un **entorno limitado** nivel. Como resultado, la caducidad de los datos afectará a todos los perfiles del simulador para pruebas.

#### Tipos de identidad

La caducidad de los datos del evento de experiencia elimina eventos **only** en función de la marca de tiempo del registro de evento. Las áreas de nombres de identidad incluidas son **ignorado** para fines de caducidad.

Pseudónimo Caducidad de datos de perfil **only** considera perfiles que tienen gráficos de identidad que contienen áreas de nombres de identidad seleccionadas por el cliente, como `ECID`, `AAID`, u otros tipos de cookies. Si el perfil contiene **any** área de nombres de identidad adicional que era **not** en la lista seleccionada del cliente, el perfil **not** se eliminará.

#### Elementos eliminados

Caducidad de datos de Evento de experiencia **only** elimina eventos y hace **not** quitar datos de clase de perfil. Los datos de la clase de perfil solo se eliminan cuando se eliminan todos los datos de **all** conjuntos de datos y hay **no** registros de clase de perfil restantes para el perfil.

La caducidad de datos de perfil pseudonímica elimina **both** registros de evento y perfil. Como resultado, también se eliminarán los datos de la clase de perfil.

### ¿Cómo se puede utilizar la caducidad de datos de perfil seudónimos junto con la caducidad de datos de eventos de experiencia?

La caducidad de los datos del perfil y la caducidad de los datos del evento de experiencia pueden utilizarse para complementarse.

Debería **always** configure la caducidad de los datos de Experience Event en sus conjuntos de datos, según sus necesidades de retención de datos sobre sus clientes conocidos. Una vez configurada la caducidad de los datos de los eventos de experiencia, puede utilizar la caducidad de los datos de perfil seudónimos para eliminar automáticamente los perfiles seudónimos. Normalmente, el periodo de caducidad de los datos para los perfiles seudónimos es inferior al periodo de caducidad de los eventos de experiencia.

En un caso de uso típico, puede configurar la caducidad de los datos de los eventos de experiencia en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos de perfil seudónimos en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de las licencias de Platform.
