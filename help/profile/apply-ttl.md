---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;conjunto de datos;tiempo de vida;ttl;tiempo de vida;
solution: Experience Platform
title: Tiempo de vida en conjuntos de datos
description: Este documento proporciona una guía general sobre el tiempo de vida (TTL) para los conjuntos de datos en el Almacenamiento de perfiles para Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# Tiempo de vida del servicio de perfil (TTL)

El servicio de perfil permite a los usuarios aplicar el tiempo de vida (TTL) en los datos del Almacenamiento de perfiles. TTL es un mecanismo que limita la cantidad de tiempo que los datos viven dentro de un conjunto de datos. Esto le permite eliminar automáticamente los datos del Almacenamiento de perfiles que ya no son útiles para sus casos de uso.

Actualmente, Perfil solo admite el TTL de Evento de experiencia.

## Evento de experiencia TTL

El TTL de eventos de experiencia le permite aplicar TTL en conjuntos de datos habilitados para Perfil del cliente en tiempo real para eliminar datos del Almacenamiento de perfiles que ya no son válidos.

>[!NOTE]
>
>Deberá ponerse en contacto con el servicio de asistencia técnica para habilitar el TTL de Evento de experiencia en sus conjuntos de datos.

Después de habilitar el TTL de Evento de experiencia en un conjunto de datos habilitado para Perfil, Platform aplicará automáticamente el valor de caducidad del TTL a los datos de Evento de experiencia en un proceso de dos pasos:

1. Todos los datos nuevos que se incorporan al conjunto de datos tendrán el valor de caducidad TTL aplicado en el momento de la ingesta.
2. Todos los datos existentes en el conjunto de datos tendrán el valor de caducidad TTL aplicado retroactivamente como un trabajo de un solo sistema de relleno. Una vez que el valor de caducidad del TTL se haya colocado en el conjunto de datos, los eventos anteriores al valor de caducidad del TTL se perderán inmediatamente en cuanto se ejecute el trabajo del sistema. Todos los demás eventos se eliminarán en cuanto alcancen sus valores de caducidad de TTL desde la marca de tiempo del evento.

>[!NOTE]
>
>Una vez aplicado el TTL, cualquier dato anterior al número de días del TTL se **eliminará de forma permanente** y no se podrá restaurar.
> 
>Además, asegúrese de que la ventana retrospectiva del segmento se encuentre dentro del límite TTL. De lo contrario, los resultados del segmento pueden ser incorrectos después de aplicar TTL. Por lo tanto, si aplicara un TTL de 30 días y tuviera un segmento que intentara ver datos de hace hasta 45 días, el segmento generaría perfiles incorrectos.
> 
>Como resultado, debe mantener el mismo TTL para todos los conjuntos de datos, si es posible, para evitar el impacto de diferentes valores TTL en diferentes conjuntos de datos en la lógica de segmentación.

Por lo tanto, si aplicara un valor TTL de 30 días el 15 de mayo, se producirían los siguientes pasos:

1. Todos los eventos nuevos tendrán un valor TTL de 30 días aplicado a medida que se incorporan.
2. Todos los eventos existentes que tengan una marca de tiempo anterior al 15 de abril se eliminarán inmediatamente con el trabajo del sistema.
3. Todos los eventos existentes con una marca de tiempo más reciente que el 15 de abril tendrán un valor de caducidad TTL 30 días después de la marca de tiempo del evento. Por lo tanto, si un evento tiene una marca de tiempo del 18 de abril, se eliminará treinta días después de la fecha de esa marca de tiempo, que sería el 18 de mayo.

