---
description: Descubra cómo gestiona Experience Platform los distintos tipos de errores devueltos por los destinos de flujo continuo y cómo intenta reenviar datos a la plataforma de destino.
title: Política de limitación y reintento de tasa para destinos de flujo continuo creados con Destination SDK
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Política de limitación y reintento de tasa para destinos de flujo continuo creados con Destination SDK

## Información general {#overview}

Los destinos creados por socios pueden devolver varios errores y tener diferentes políticas de limitación de velocidad. En esta página se explica cómo gestiona Experience Platform los distintos tipos de errores devueltos por los destinos de flujo continuo.

Al configurar un destino mediante Destination SDK, puede seleccionar entre dos tipos de agregación: [agregación del mejor esfuerzo](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) y [agregación configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Según el tipo de agregación que seleccione, lea a continuación cómo gestiona el Experience Platform los errores y las limitaciones de tasa.

## Mejor agregación de esfuerzos {#best-effort-aggregation}

Para las llamadas HTTP realizadas a su destino que no se realicen correctamente, el Experience Platform intenta realizar la llamada de nuevo una vez más inmediatamente después de la primera llamada. Si la llamada sigue fallando en el segundo intento, el Experience Platform descarta la llamada y no la vuelve a probar por tercera vez.

## Agregación configurable {#configurable-aggregation}

En el caso de las plataformas de destino configuradas con agregación configurable, el Experience Platform distingue entre el tipo de error devuelto por la plataforma:

* Errores en los casos en los que el Experience Platform intenta reenviar los datos a su plataforma:
   * Códigos de respuesta HTTP 420 y 429
   * Códigos de respuesta HTTP buenos a 500
* Errores en los que el Experience Platform *no* intente enviar los datos a su plataforma: todos los demás que devuelve su plataforma

### Método de reintento descrito {#retry-approach}

A continuación se describe el enfoque del Experience Platform para la agregación configurable. En este ejemplo se supone que el Experience Platform envía datos a una plataforma de destino que comienza a devolver códigos de error 429 si recibe más de 50 000 solicitudes por minuto:

* Minuto 1: El Experience Platform agrega 40.000 lotes con perfiles para enviarlos a la plataforma de destino. El Experience Platform realiza 40.000 solicitudes HTTP y todas tienen éxito.
* Minuto 2: El Experience Platform agrega lotes de 70.000 con perfiles para enviarlos a la plataforma de destino. El Experience Platform hace que las solicitudes HTTP de 70.000 y 50.000 sean correctas. Los otros 20k reciben un error de limitación de velocidad de su punto final y se volverá a intentar en 30 minutos.
* Minuto 3: El Experience Platform agrega 30.000 lotes con perfiles para enviarlos a la plataforma de destino. El Experience Platform realiza 30.000 solicitudes HTTP y todas tienen éxito.
* ...
* ...
* Minuto 32: El Experience Platform vuelve a intentar enviar los lotes de 20 000 que han fallado en el minuto 2. Todas las llamadas son correctas.

## Pasos siguientes {#next-steps}

Ahora sabe cómo gestiona el Experience Platform los errores y la limitación de velocidad desde las plataformas de destino, según la política de agregación que haya seleccionado al configurar el destino de flujo continuo. A continuación, puede revisar la siguiente documentación:

* [Probar la configuración de destino](/help/destinations/destination-sdk/test-destination.md)
* [Enviar para revisión un destino creado en Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
