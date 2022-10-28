---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;conjunto de datos;tiempo de vida;ttl;tiempo de vida;
solution: Experience Platform
title: Caducidad del evento de experiencia
description: Este documento proporciona una guía general sobre cómo configurar los tiempos de caducidad para eventos de experiencia individuales dentro de un conjunto de datos de Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: faf9e72f77f04b20d2399749eaacdb9ebdf412dc
workflow-type: tm+mt
source-wordcount: '466'
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
1. Todos los datos existentes en el conjunto de datos tienen el valor de caducidad aplicado retroactivamente como un trabajo único del sistema de relleno. Una vez que el valor de caducidad se haya colocado en el conjunto de datos, los eventos anteriores al valor de caducidad se perderán inmediatamente en cuanto se ejecute el trabajo del sistema. Todos los demás eventos se eliminarán en cuanto alcancen sus valores de caducidad desde la marca de tiempo del evento.

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
