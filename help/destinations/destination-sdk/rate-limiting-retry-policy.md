---
description: Descubra cómo Experience Platform gestiona los distintos tipos de errores devueltos por los destinos de flujo continuo y cómo reintenta enviar datos a la plataforma de destino.
title: Política de limitación de velocidad y reintentos para destinos de streaming creados con Destination SDK
exl-id: 7a4edf8d-f905-4d55-a25d-4b9c6063ff88
source-git-commit: 61b8d40d6ecade10b0793bf7ad7c3e83974a0f02
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Política de limitación de velocidad y reintentos para destinos de streaming creados con Destination SDK

## Información general {#overview}

Los destinos creados por el socio pueden devolver varios errores y tener diferentes políticas de limitación de velocidad. En esta página se explica cómo Experience Platform gestiona los distintos tipos de errores devueltos por los destinos de flujo continuo.

Al configurar un destino con Destination SDK, puede seleccionar entre dos tipos de agregación: [agregación de mejor esfuerzo](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) y [agregación configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Según el tipo de agregación que seleccione, lea a continuación cómo gestiona Experience Platform los errores y las limitaciones de velocidad.

## Agregación del mejor esfuerzo {#best-effort-aggregation}

Para cualquier llamada HTTP realizada al destino que falle, el Experience Platform intenta realizar la llamada de nuevo una vez más inmediatamente después de la primera llamada. Si la llamada sigue fallando en el segundo intento, el Experience Platform descarta la llamada y no la vuelve a intentar una tercera vez.

## Agregación configurable {#configurable-aggregation}

En el caso de las plataformas de destino configuradas con agregación configurable, el Experience Platform distingue entre el tipo de error devuelto por la plataforma:

* Errores en los que el Experience Platform reintenta enviar los datos a su plataforma:
   * Códigos de respuesta HTTP 420 y 429
   * Códigos de respuesta HTTP buenos a 500
* Errores donde el Experience Platform *no tiene* vuelva a intentar enviar los datos a su plataforma: todas las demás que devuelve su plataforma

### Método de reintento descrito {#retry-approach}

A continuación se describe el método Experience Platform para la agregación configurable. En este ejemplo se supone que Experience Platform envía datos a una plataforma de destino que empieza a devolver 429 códigos de error si recibe más de 50 000 solicitudes por minuto:

* Minuto 1: El Experience Platform añade 40.000 lotes con perfiles para enviarlos a su plataforma de destino. El Experience Platform realiza 40 000 solicitudes HTTP y todas se realizan correctamente.
* Minuto 2: El Experience Platform agrega 70 000 lotes con perfiles para enviarlos a la plataforma de destino. El Experience Platform realiza 70 000 solicitudes HTTP y 50 000 se realizan correctamente. Los otros 20 000 reciben un error de limitación de velocidad de su punto de conexión y se volverán a probar en 30 minutos.
* Minuto 3: El Experience Platform agrega 30.000 lotes con perfiles para enviarlos a la plataforma de destino. El Experience Platform realiza 30 000 solicitudes HTTP y todas se realizan correctamente.
* ...
* ...
* Minuto 32: el Experience Platform vuelve a intentar enviar los lotes de 20 000 que han fallado en el minuto 2. Todas las llamadas se realizan correctamente.

## Pasos siguientes {#next-steps}

Ahora sabe cómo gestiona el Experience Platform los errores y la limitación de velocidad desde las plataformas de destino, según la política de agregación seleccionada al configurar el destino de flujo continuo. A continuación, puede revisar la siguiente documentación:

* [Pruebe la configuración de destino](/help/destinations/destination-sdk/test-destination.md)
* [Enviar para revisión un destino creado en Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
