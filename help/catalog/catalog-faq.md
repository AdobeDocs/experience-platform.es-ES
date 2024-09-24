---
keywords: servicio de catálogo; preguntas; preguntas más frecuentes; faq; conjuntos de datos faq
title: Preguntas frecuentes
description: Respuestas a las preguntas más frecuentes sobre el servicio de catálogo de Adobe Experience Platform y los conjuntos de datos.
source-git-commit: 0bb10754e2f5bc289567368c803d4397cec77bf6
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Preguntas frecuentes {#faq}

Este documento proporciona respuestas a las preguntas frecuentes sobre el servicio de catálogo de Adobe Experience Platform y los conjuntos de datos. Si tiene alguna pregunta o solución de problemas relacionados con otros servicios de Platform, incluidos problemas encontrados en todas las API de Platform, consulte la [guía de solución de problemas para Experience Platform](../landing/troubleshooting.md).

## Políticas y reglas de retención {#retention-policies-and-rules}

### ¿A qué tipos de conjuntos de datos puedo aplicar reglas de política de retención?

+++Respuesta

Puede configurar políticas de retención en conjuntos de datos creados con la clase ExperienceEvent XDM. Para el servicio de perfil, las políticas de retención solo se pueden aplicar a conjuntos de datos de ExperienceEvent después de haberlos habilitado para el perfil.

+++

### ¿Puedo establecer diferentes políticas de retención para el lago de datos y el servicio de perfil?

+++Respuesta

Sí, puede aplicar diferentes políticas de retención para el lago de datos y el servicio de perfil.

+++

## Ejecución y tiempo del trabajo de retención {#retention-job-execution-and-timing}

### ¿Cuándo eliminará el trabajo de retención de conjuntos de datos los datos de los servicios de lago de datos?

+++Respuesta

Las caducidades de los conjuntos de datos se evalúan y procesan semanalmente, eliminando todos los registros que han caducado. Un evento se considera caducado si se ha ingerido en Platform durante más de 30 días (fecha de ingesta > 30 días) y su fecha de evento supera el periodo de retención definido.

+++

### ¿Cuándo eliminará el trabajo de retención de conjuntos de datos los datos de los servicios de perfil?

+++Respuesta

Una vez establecida una directiva de retención, los eventos existentes se eliminan inmediatamente de Platform si su marca de tiempo de evento supera el período de retención. Los nuevos eventos se eliminan una vez que su marca de tiempo supera el período de retención.

Por ejemplo, si aplica una directiva de caducidad de 30 días el 15 de mayo, ocurre lo siguiente:

- Los nuevos eventos reciben una caducidad de 30 días a medida que se incorporan.
- Los eventos existentes con una marca de tiempo anterior al 15 de abril se eliminan inmediatamente.
- Los eventos existentes con una marca de tiempo después del 15 de abril caducarán 30 días después de su marca de tiempo. Por ejemplo, un evento del 18 de abril se eliminaría el 18 de mayo.

+++

## Monitorización y uso del conjunto de datos

### ¿Cómo puedo comprobar el uso actual de mi conjunto de datos?

+++Respuesta

Puede ver el tamaño de almacenamiento a nivel de conjunto de datos más reciente en el lago de datos y el perfil como métricas independientes en la página de inventario [!UICONTROL Conjuntos de datos]. También puede ordenar las columnas para identificar los conjuntos de datos más grandes y asegurarse de que se aplican las políticas de retención. El uso a nivel de zona protegida está disponible en el tablero Uso de licencias. Consulte la [documentación de uso de licencias](../dashboards/guides/license-usage.md) para obtener más información.

+++

### ¿Cómo puedo verificar si el trabajo de retención de datos se realizó correctamente?

+++Respuesta

Puede comprobar la marca de tiempo del último trabajo de retención de datos en la [IU de configuración de retención de conjuntos de datos](./datasets/user-guide.md#data-retention-policy) y en la página de inventario de [!UICONTROL Conjuntos de datos]. Los informes sobre el uso del conjunto de datos histórico no están disponibles actualmente, pero están planificados para futuras versiones.

+++

## Recuperación de datos {#data-recovery}

### ¿Puedo recuperar los datos eliminados?

+++Respuesta

No, una vez aplicada la política de retención, los datos anteriores al período de retención se eliminan de forma permanente y no se pueden recuperar.

+++

