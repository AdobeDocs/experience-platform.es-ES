---
title: Consentimiento e identidad en la recopilación de datos
description: Comprenda cómo las opciones de consentimiento afectan al comportamiento de identidad en las implementaciones de Web SDK, incluida la generación de ECID, la persistencia de cookies y la continuidad del visitante.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Consentimiento e identidad en la recopilación de datos

El consentimiento y la identidad están estrechamente relacionados en las implementaciones de Web SDK. La forma y el momento en que se recopila el consentimiento afectan directamente al momento y al momento en que Web SDK genera un ECID, establece cookies de identidad y envía datos a Edge Network. Cuando el consentimiento no se gestiona con cuidado, el resultado es a menudo una inflación de visitantes inesperada, brechas en la continuidad de la identidad o ambas cosas.

Esta página explica cómo las opciones de consentimiento interactúan con el comportamiento de identidad y proporciona instrucciones para configurar la implementación a fin de evitar escollos comunes. Para obtener información general sobre cómo administra Web SDK los ECID, FPID y otras señales de identidad, consulte [Identidad en la recopilación de datos](./overview.md).

## Cómo afecta el consentimiento a la identidad {#how-consent-affects-identity}

Web SDK utiliza la variable de configuración [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) y el comando [`setConsent`](/help/collection/js/commands/setconsent.md) para controlar si envía datos a Edge Network. El estado de consentimiento determina directamente cuándo se genera un ECID y cuándo se configuran las cookies de identidad.

En la tabla siguiente se muestra el efecto combinado de `defaultConsent` y `setConsent` en la recopilación de datos, la configuración de cookies y el comportamiento de identidad.

| `defaultConsent` | `setConsent` | Se produce la recopilación de datos | Conjunto de cookies del explorador | Comportamiento de identidad |
| --- | --- | --- | --- | --- |
| `in` | Sin configurar | Sí | Sí | Se genera un ECID inmediatamente en la primera solicitud. Las cookies de identidad se configuran al cargar la página. |
| `in` | `in` | Sí | Sí | Se conserva el ECID existente del visitante. El comportamiento de identidad no cambia. |
| `in` | `out` | No | Sí | La recopilación de datos se detiene. Las cookies de identidad de ECID y `kndctr_` existentes permanecen en el explorador hasta que caducan. |
| `pending` | Sin configurar | No | No | No se genera ningún ECID. No se han establecido cookies. Los eventos se ponen en cola localmente hasta que se llama a `setConsent`. |
| `pending` | `in` | Sí | Sí | Se envían los eventos en cola. Se genera un ECID en la primera solicitud y se establecen las cookies de identidad. |
| `pending` | `out` | No | Sí | Los eventos en cola se descartan. No se genera ningún ECID. La cookie de consentimiento se configura para registrar las preferencias del visitante. |
| `out` | Sin configurar | No | No | No se genera ningún ECID. No se han establecido cookies. No se envían eventos. |
| `out` | `in` | Sí | Sí | Se genera un ECID en la primera solicitud y se establecen las cookies de identidad. |
| `out` | `out` | No | Sí | No se genera ningún ECID. La cookie de consentimiento se configura para registrar las preferencias del visitante. |

>[!NOTE]
>
>Las cookies de identidad y consentimiento se establecen incluso cuando un visitante se excluye. Estas cookies son necesarias para cumplir con las preferencias de recopilación de datos del visitante. Consulte [Cookies de Web SDK](https://experienceleague.adobe.com/es/docs/core-services/interface/data-collection/cookies/web-sdk) para obtener una lista completa de las cookies que establece Web SDK.

Cuando un visitante vuelve a conceder el consentimiento después de revocarlo anteriormente (llamando a `setConsent` con `"general": "in"` después de `"general": "out"`), Web SDK reanuda el envío de eventos y utiliza el ECID existente de la cookie si no ha caducado. Se conserva la identidad del visitante.

Una vez que un visitante concede o deniega el consentimiento, Web SDK mantiene su preferencia en una cookie de consentimiento de `kndctr_`. En cargas de página subsiguientes, SDK lee esta cookie y aplica la preferencia almacenada automáticamente; no es necesario que vuelva a llamar a `setConsent` a menos que cambie la preferencia del visitante. Tenga en cuenta que el valor de configuración `defaultConsent` no persiste entre cargas de página, pero el consentimiento resuelto del visitante (establecido mediante `setConsent`) sí.

>[!NOTE]
>
>Los eventos en cola mientras el consentimiento es `pending` se guardan en la memoria y no sobreviven a las recargas de la página. Si un visitante navega a una página nueva antes de que se resuelva el consentimiento, se pierden los eventos en cola de la página anterior.

## Patrones de implementación {#implementation-patterns}

### Modelo de inclusión (se requiere consentimiento antes de la recopilación) {#opt-in}

Utilice este patrón cuando las regulaciones (como el RGPD) requieran un consentimiento explícito antes de recopilar datos.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Con este patrón:
* No se genera ningún ECID hasta que se concede el consentimiento.
* Los eventos activados antes del consentimiento (como la vista de página inicial) se ponen en cola y se envían después de otorgarlo.
* Las cookies de identidad solo se establecen después de la primera solicitud de Edge Network correcta.

### Modelo de exclusión (colección de forma predeterminada, detener en caso de denegación) {#opt-out}

Utilice este patrón cuando las regulaciones permitan la recopilación de datos de forma predeterminada con una opción de exclusión.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Con este patrón:
* Se genera un ECID inmediatamente en la primera carga de página.
* Todos los eventos se envían hasta que el visitante se excluye.
* Después de la exclusión, Web SDK deja de enviar eventos, pero las cookies existentes permanecen.

## Consentimiento con ID de dispositivo de origen {#consent-with-fpids}

Si su implementación utiliza [ID de dispositivos de origen (FPID)](./fpid.md), el servidor establece la cookie FPID independientemente del estado de consentimiento de Web SDK. La cookie FPID es un identificador que administra en su propia infraestructura. Sin embargo, el FPID solo se envía a Edge Network cuando Web SDK realiza una solicitud (que se cierra mediante consentimiento):

* Con `defaultConsent: "pending"`, el FPID existe en el explorador, pero no se utiliza para inicializar un ECID hasta que se conceda el consentimiento.
* Con `defaultConsent: "in"`, el FPID se utiliza en la primera solicitud y siembra el ECID inmediatamente.

Si la implementación del consentimiento requiere que no se establezca ningún identificador antes del consentimiento, retrase la configuración de la cookie FPID hasta que se comunique el consentimiento. La única función de acceso de consentimiento de Web SDK no impide que se establezca la cookie FPID, ya que la administra el servidor.

## Peligros comunes {#common-pitfalls}

+++**El banner de consentimiento borra las cookies de identidad**

**Problema**: Algunas plataformas de administración de consentimiento (CMP) borran todas las cookies (incluidas las cookies de identidad de `kndctr_`) al presentar el banner de consentimiento, antes de que el visitante realice una elección. Cuando el visitante da su consentimiento, Web SDK genera un nuevo ECID porque se ha eliminado el anterior. El visitante aparece como una persona nueva en el sistema de informes.

**Síntomas**:
* Un pico en el recuento de visitantes únicos después de implementar un banner de consentimiento.
* Los visitantes que regresan se cuentan como nuevos visitantes cada vez que caduca su consentimiento e interactúan de nuevo con el titular.

**Solución**: configure su CMP para conservar las cookies `kndctr_`. Estas cookies son cookies de identidad, no de seguimiento: identifican el dispositivo y no contienen datos de comportamiento. Si su CMP requiere la eliminación de cookies, agregue `kndctr_` cookies con el prefijo a una lista de exclusión. De forma alternativa, retrasar la eliminación de cookies hasta que el visitante deniegue explícitamente el consentimiento en lugar de borrarlas de forma preventiva.

+++

+++**El consentimiento demorado causa identidad duplicada**

**Problema**: Cuando `defaultConsent` está establecido en `pending`, Web SDK espera el consentimiento antes de enviar datos. Si el consentimiento se concede más adelante en el ciclo de vida de la página (por ejemplo, después de una interacción de banner que interrumpe la carga de una página), la siguiente secuencia puede causar problemas:

1. Se carga la página. `defaultConsent: "pending"`. Web SDK no envía solicitudes.
2. El visitante da su consentimiento. CMP déclencheur una recarga de página.
3. La página se vuelve a cargar. Web SDK se inicializa con el consentimiento ahora concedido y genera un ECID.

Este flujo es normal y funciona correctamente. El problema surge cuando la CMP o la implementación borran las cookies de forma involuntaria entre los pasos 2 y 3, o cuando la SDK web se configura de forma diferente en la recarga.

**Solución**: Asegúrese de que la configuración de Web SDK (especialmente `orgId` y `defaultConsent`) sea idéntica en cada carga de página. Si la CMP déclencheur una recarga después del consentimiento, compruebe que las cookies de identidad sobreviven a la recarga.

+++

+++**Usando `defaultConsent: "in"` con un banner de consentimiento**

**Problema**: Algunas implementaciones establecen `defaultConsent: "in"` y luego llaman a `setConsent` con `"general": "out"` si el visitante se niega. Este método genera un ECID y envía al menos una solicitud antes de que se deniegue el consentimiento. En función de los requisitos regulatorios, es posible que esta recopilación de datos inicial no se ajuste a la política de privacidad de su organización.

**Solución**: Si su entorno normativo requiere consentimiento antes de cualquier recopilación de datos o generación de ECID, use `defaultConsent: "pending"` en su lugar. Esta configuración garantiza que Web SDK no se comunique con Edge Network hasta que se conceda explícitamente el consentimiento.

+++
