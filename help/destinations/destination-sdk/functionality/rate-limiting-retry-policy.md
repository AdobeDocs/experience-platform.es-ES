---
description: Descubra cómo Experience Platform gestiona los distintos tipos de errores devueltos por los destinos de flujo continuo y cómo reintenta enviar datos a la plataforma de destino.
title: Limitación de velocidad y directiva de reintentos para destinos de streaming creados con Destination SDK
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Limitación de velocidad y directiva de reintentos para destinos de streaming creados con Destination SDK

Los destinos creados por el socio pueden devolver varios errores y tener diferentes políticas de limitación de velocidad. En esta página se explica cómo Experience Platform gestiona los distintos tipos de errores devueltos por los destinos de flujo continuo.

Al configurar un destino mediante Destination SDK, puede seleccionar entre dos tipos de agregación: [agregación óptima](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) y [agregación configurable](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Según el tipo de agregación que seleccione, lea a continuación cómo Experience Platform gestiona los errores y las limitaciones de velocidad.

## Agregación del mejor esfuerzo {#best-effort-aggregation}

Experience Platform reintenta llamadas que devuelven los siguientes códigos de respuesta HTTP: **403, 408, 409, 429, 500, 502, 503, 504**. Se realizan dos reintentos en los siguientes intervalos:

* Primer intento de reintento: después de 15 segundos
* Segundo intento de reintento: después de 30 segundos

Experience Platform *no* reintenta las llamadas que devuelven otros códigos de respuesta HTTP, como 400 (solicitud incorrecta). Si la llamada sigue fallando después de ambos intentos de reintento, Experience Platform anula la activación y no la vuelve a intentar.

Puede solicitar una política de reintentos diferente para flujos de datos específicos poniéndose en contacto con Atención al cliente.

## Agregación configurable {#configurable-aggregation}

En el caso de las plataformas de destino configuradas con agregación configurable, Experience Platform distingue entre el tipo de error devuelto por la plataforma:

* Errores en los que Experience Platform reintenta enviar los datos a su plataforma:
   * Códigos de respuesta HTTP 420 y 429
   * Códigos de respuesta HTTP superiores a 500
* Errores en los que Experience Platform *no* intenta enviar los datos a su plataforma: todos los demás devueltos por su plataforma

### Método de reintento descrito {#retry-approach}

A continuación se describe el método de Experience Platform para la agregación configurable. En este ejemplo se supone que Experience Platform envía datos a una plataforma de destino que empieza a devolver 429 códigos de error si recibe más de 50 000 solicitudes por minuto:

* Minuto 1: Experience Platform agrega 40.000 lotes con perfiles para enviarlos a la plataforma de destino. Experience Platform realiza 40.000 solicitudes HTTP y todas se realizan correctamente.
* Minuto 2: Experience Platform agrega 70.000 lotes con perfiles para enviarlos a la plataforma de destino. Experience Platform realiza 70 000 solicitudes HTTP y 50 000 se realizan correctamente. Los otros 20 000 reciben un error de limitación de velocidad de su punto de conexión y se volverán a probar en 30 minutos.
* Minuto 3: Experience Platform agrega 30.000 lotes con perfiles para enviarlos a la plataforma de destino. Experience Platform realiza 30.000 solicitudes HTTP y todas se realizan correctamente.
* ...
* ...
* Minuto 32: Experience Platform vuelve a intentar enviar los lotes de 20 000 que han fallado en el minuto 2. Todas las llamadas se realizan correctamente.

## Próximos pasos {#next-steps}

Ahora sabe cómo gestiona Experience Platform los errores y la limitación de velocidad desde las plataformas de destino, según la política de agregación seleccionada al configurar el destino de flujo continuo. A continuación, puede revisar la siguiente documentación:

* [Pruebe la configuración de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Enviar para revisión un destino creado en Destination SDK](../guides/submit-destination.md)
