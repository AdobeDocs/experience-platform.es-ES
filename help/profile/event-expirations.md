---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;tiempo de vida;ttl;tiempo de vida;
solution: Experience Platform
title: Caducidad de evento de experiencia
description: Este documento proporciona instrucciones generales para configurar los tiempos de caducidad de los eventos de experiencia individuales dentro de un conjunto de datos de Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: bb2d0075b234ec750046e1f28cac07a58a9d7e72
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Caducidad de Experience Event

En Adobe Experience Platform, puede configurar los tiempos de caducidad para todos los eventos de experiencia que se incorporan a un conjunto de datos habilitado para [Perfil del cliente en tiempo real](./home.md). Esto permite eliminar automáticamente del almacén de perfiles los datos que ya no son válidos o útiles para sus casos de uso.

Las caducidades de Experience Event no se pueden configurar a través de la IU o las API de Platform. En su lugar, debe ponerse en contacto con el servicio de asistencia para habilitar la caducidad de los eventos de experiencia en los conjuntos de datos necesarios.

>[!IMPORTANT]
>
>Las caducidades de eventos de experiencia no se deben confundir con las caducidades de conjuntos de datos, que eliminan todo el conjunto de datos después de alcanzar la fecha de caducidad. Se configuran manualmente mediante [Higiene de datos de Adobe Experience Platform](../hygiene/home.md).

## Proceso de caducidad automatizado

Una vez habilitadas las caducidades de los eventos de experiencia en un conjunto de datos con perfil habilitado, Platform aplica automáticamente los valores de caducidad de cada evento capturado en un proceso de dos pasos:

1. Todos los datos nuevos que se incorporan al conjunto de datos tienen el valor de caducidad aplicado en el momento de la ingesta en función de la marca de tiempo del evento.
1. Todos los datos existentes en el conjunto de datos tienen el valor de caducidad aplicado de forma retroactiva como un trabajo de sistema de relleno único. Una vez que el valor de caducidad se haya colocado en el conjunto de datos, los eventos anteriores al valor de caducidad se perderán inmediatamente en cuanto se ejecute el trabajo del sistema. Todos los demás eventos se eliminarán en cuanto alcancen sus valores de caducidad desde la marca de tiempo del evento. Cuando se hayan eliminado todos los eventos de experiencia, si el perfil ya no tiene atributos de perfil, este ya no existirá.

>[!WARNING]
>
>Una vez aplicados, cualquier dato que sea anterior a la cantidad de días asignados por el valor de caducidad es **eliminado permanentemente** y no se pueden restaurar.

Por ejemplo, si aplica un valor de caducidad de 30 días el 15 de mayo, se producirían los siguientes pasos:

1. Todos los eventos nuevos obtienen un valor de caducidad de 30 días aplicados a medida que se incorporan.
1. Todos los eventos existentes que tengan una marca de tiempo anterior al 15 de abril se eliminarán inmediatamente con el trabajo del sistema.
1. Todos los eventos existentes que tienen una marca de tiempo posterior al 15 de abril tienen un valor de caducidad 30 días después de su marca de tiempo de evento. Por lo tanto, si un evento tiene la marca de tiempo del 18 de abril, se elimina 30 días después de la fecha de dicha marca de tiempo, que sería el 18 de mayo.

## Efectos en la segmentación

Debe asegurarse de que las ventanas retrospectivas de sus segmentos se encuentren dentro de los límites de caducidad de sus conjuntos de datos dependientes para mantener la precisión de los resultados. Por ejemplo, si aplica un valor de caducidad de 30 días y tiene un segmento que intenta ver datos de hace hasta 45 días, la audiencia resultante probablemente sea inexacta.

Por lo tanto, si es posible, debe mantener el mismo valor de caducidad del Evento de experiencia para todos los conjuntos de datos para evitar el impacto de valores de caducidad diferentes en conjuntos de datos diferentes en la lógica de segmentación.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de los datos de Experience Event:

### ¿En qué se diferencia la caducidad de los datos de Experience Event de la del perfil seudónimo?

La caducidad de los datos de Experience Event y la caducidad de los datos de Perfil seudónimos son funciones complementarias.

#### Granularidad

La caducidad de los datos del Experience Event funciona en una **conjunto de datos** nivel. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

La caducidad de datos del perfil seudónimo funciona en un **espacio aislado** nivel. Como resultado, la caducidad de los datos afectará a todos los perfiles de la zona protegida.

#### Tipos de identidad

La caducidad de datos de Experience Event elimina los eventos **solamente** se basa en la marca de tiempo del registro de evento. Las áreas de nombres de identidad incluidas son **ignorado** para fines de caducidad.

Caducidad de datos de perfil seudónimo **solamente** considera los perfiles que tienen gráficos de identidad que contienen áreas de nombres de identidad seleccionadas por el cliente, como `ECID`, `AAID`u otros tipos de cookies. Si el perfil contiene **cualquiera** área de nombres de identidad adicional que se **no** en la lista seleccionada por el cliente, el perfil **no** se eliminarán.

#### Elementos eliminados

Caducidad de datos de Experience Event **solamente** elimina eventos y hace **no** quitar datos de clase de perfil. Los datos de clase de perfil solo se eliminan cuando se eliminan todos los datos en **todo** conjuntos de datos y hay **no** registros de clase de perfil restantes para el perfil.

Eliminación de la caducidad de datos de perfil seudónimo **ambos** registros de eventos y perfiles. Como resultado, los datos de clase de perfil también se eliminarán.

### ¿Cómo se puede usar la caducidad de datos de perfil seudónimo junto con la caducidad de datos de Experience Event?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia se pueden utilizar para complementarse.

Usted debe **siempre** configure la caducidad de datos de Experience Event en sus conjuntos de datos, en función de sus necesidades de retención de datos sobre sus clientes conocidos. Una vez configurada la caducidad de datos del Evento de experiencia, puede utilizar la caducidad de datos del Perfil seudónimo para eliminar automáticamente los Perfiles seudónimos. Normalmente, el periodo de caducidad de los datos de los perfiles seudónimos es menor que el periodo de caducidad de los datos de los eventos de experiencia.

En un caso de uso típico, puede establecer la caducidad de los datos de Experience Event en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos del perfil seudónimo en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de la licencia de Platform.
