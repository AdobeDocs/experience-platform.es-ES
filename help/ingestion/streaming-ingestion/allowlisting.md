---
title: INCLUSIÓN EN LA LISTA DE PERMITIDOS de direcciones IP para la API de ingesta de transmisión
description: Obtenga información sobre cómo proteger el acceso a la API de ingesta de transmisión permitiendo solo direcciones IP especificadas mediante la inclusión en la lista de permitidos. En esta guía se explica cómo configurar, habilitar y administrar restricciones basadas en direcciones IP para la seguridad de API.
hide: true
hidefromtoc: true
badge: beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# INCLUSIÓN EN LA LISTA DE PERMITIDOS de direcciones IP para la API de ingesta de transmisión

>[!AVAILABILITY]
>
>La compatibilidad con la inclusión en la lista de permitidos de direcciones IP para la API de ingesta de transmisión está en versión beta y es posible que su organización aún no tenga acceso a ella. La funcionalidad y la documentación están sujetas a cambios.

Ahora puede lista de permitidos direcciones IP para la API de ingesta de transmisión. Utilice esta función para proteger los extremos de ingesta restringiendo el acceso solo a las direcciones IP especificadas.

## Funcionamiento de la inclusión en la lista de permitidos de direcciones IP

La función de inclusión en la lista de permitidos IP funciona de la siguiente manera:

1. **Enviar direcciones IP:** Proporcione una lista de direcciones IP de confianza, asignadas a sus zonas protegidas.
2. **Configuración:** Adobe configura la lista de permitidos a nivel de organización y de zona protegida para su organización.
3. **Aplicación:** Las solicitudes entrantes se evalúan en función de la lista de permitidos proporcionada:
   * Si la dirección IP coincide con su lista de permitidos, la solicitud se procesará normalmente.
   * Si la dirección IP no está en la lista de permitidos, la solicitud se bloquea y se recibe un error HTTP 403 sin ningún cuerpo de respuesta.

## Consideraciones clave

* La característica de inclusión en la lista de permitidos de direcciones IP se aplica solamente a la [API de ingesta de transmisión](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) y **no** se aplica a `server.adobedc.net` o `edge.adobedc.net`.
* Las nuevas zonas protegidas están abiertas de forma predeterminada hasta que la inclusión en la lista de permitidos esté habilitada.
* Si se elimina una zona protegida de la lista de permitidos, se volverá a abrir en Internet.
* Debe mantener la lista completa de asignaciones de zona protegida a direcciones IP de su lado y enviar siempre la lista completa en el formulario de inclusión en la lista de permitidos de direcciones IP. No se admiten actualizaciones incrementales.

## Habilitar la inclusión en la lista de permitidos de direcciones IP

Siga los pasos a continuación para habilitar la inclusión en la lista de permitidos de direcciones IP para su organización:

1. Descargue y complete el [formulario de inclusión en la lista de permitidos de direcciones IP](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Abra un ticket de asistencia y presente el asunto como **AEP DCS &amp; Streaming Ingestion - IP Inclusión en la lista de permitidos request**. Adjunte el formulario completado a este ticket.
3. Después de enviar el ticket, el Servicio de atención al cliente de Adobe reenviará la solicitud al departamento de ingeniería.
4. Los ingenieros habilitan la inclusión en la lista de permitidos y confirman la configuración.
5. A continuación, valide el acceso y confirme mediante el vale de asistencia.

| Organización | Nombre de zona protegida | Direcciones IP permitidas |
| --- | --- | --- |
| ACME | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| ACME | Dev | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Preguntas frecuentes

Lea lo siguiente para obtener respuestas a las preguntas frecuentes sobre la inclusión en la lista de permitidos de direcciones IP para la API de ingesta de transmisión.

### ¿Qué API están cubiertas?

Solo los extremos de la API de ingesta de transmisión `dcs.adobedc.net`.

## ¿Qué sucede si mi solicitud proviene de una dirección IP no incluida?

Se bloquea con un error HTTP 403.

### ¿Las nuevas zonas protegidas se protegen automáticamente?

No. Están abiertas hasta que se proporcionan asignaciones de direcciones IP a través del formulario de inclusión en la lista de permitidos.

### ¿Puedo enviar solo direcciones IP actualizadas cuando cambie mi lista de permitidos?

No. Siempre debe enviar la lista completa de entornos limitados y asignaciones de direcciones IP. No se aceptan actualizaciones parciales (incrementales).