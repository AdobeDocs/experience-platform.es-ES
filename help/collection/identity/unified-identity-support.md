---
title: Compatibilidad con identidad unificada en la recopilación de datos
description: Descubra cómo la compatibilidad con la identidad unificada reúne la persistencia de origen y la activación de terceros admitida en la recopilación de datos web.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Compatibilidad con identidad unificada en la recopilación de datos

>[!AVAILABILITY]
>
>Esta función se encuentra actualmente en fase beta. La disponibilidad, el comportamiento y la documentación pueden cambiar.

La compatibilidad con la identidad unificada permite que Edge Network funcione en contextos de identidad de origen y de terceros. Agrupa la identificación duradera de origen en sus propiedades con flujos de trabajo de activación de terceros en exploradores compatibles con cookies de terceros. Para obtener información general sobre cómo administra Web SDK los ECID, FPID y otras señales de identidad, consulte [Identidad en la recopilación de datos](./overview.md).

Con la compatibilidad con la identidad unificada, puede:

* **Maximizar el alcance de la audiencia**: active las audiencias de Experience Platform en destinos de terceros (DSP, SSP y redes) para obtener una mayor proporción de su tráfico.
* **Mantener la precisión de la medición**: Mantenga la identificación consistente de los visitantes en todas sus propiedades y plataformas publicitarias.
* **Refuerce la implementación**: Use identificadores de dispositivos de origen como base y, al mismo tiempo, mantenga la compatibilidad con flujos de trabajo de activación de terceros.

Cuando un visitante llega a su sitio, Edge Network evalúa las señales de identidad disponibles, vinculando automáticamente los contextos de origen y de terceros cuando las condiciones lo permiten. Los exploradores que bloquean cookies de terceros siguen funcionando en modo de origen sin interrupciones en la implementación.

## Funcionamiento

Edge Network genera ECID mediante la evaluación de las señales de identidad disponibles en el siguiente orden de prioridad:

| Prioridad | Fuente | Contexto | Comportamiento |
| --- | --- | --- | --- |
| 1 | **ID de Demdex** | Terceros | Si hay un ID de Demdex, el ECID se predefine a partir de él. Esta semilla produce un ECID coherente entre los dominios que comparten la misma cookie de terceros. |
| 2 | **FPID** | Datos de origen | Si no hay ningún ID de Demdex, pero existe un FPID, el ECID se siembra a partir del FPID y se deriva un ID de Demdex de él. |
| 3 | **Random** | Datos de origen | Si no hay disponibles ni un ID de Demdex ni un FPID, se genera un nuevo ECID aleatorio y se deriva un ID de Demdex de él. |

Los ECID y los ID de Demdex se vinculan criptográficamente a través de un algoritmo determinista, lo que significa que uno se puede derivar del otro. Esta relación es lo que permite a Edge Network traducir entre contextos de identidad de origen y de terceros sin requerir una lógica de gestión de visitantes independiente en la implementación.

Como la relación es determinista, las audiencias creadas en ECID de origen pueden activarse a través de infraestructura de terceros cuando el ID de Demdex correspondiente está disponible.

Para los visitantes que ya tienen un ECID derivado de FPID, Edge Network puede vincular automáticamente su identidad de origen al contexto de identidad de terceros. Esto sucede de forma transparente cuando el explorador admite cookies de terceros y no requiere cambios en la implementación. Cuando se produce la vinculación automática:

1. Edge Network detecta que el ECID del visitante no se derivó de un ID de Demdex.
1. Si el explorador del visitante admite cookies de terceros, se activa una sincronización de identidad ligera.
1. El sistema crea un vínculo entre el ECID de origen del visitante y su identidad de terceros.
1. El vínculo se almacena en el almacén de identidades, lo que permite la activación de audiencias en destinos de terceros.

La vinculación automática preserva los ECID existentes y evita el acantilado de visitantes. Con el tiempo, una mayor parte de la audiencia se convierte gradualmente en apta para la activación de terceros a medida que los visitantes regresan y se produce la vinculación.

La activación de audiencias de terceros se basa en la sincronización de ID (sincronización de ID). Cuando Edge Network establece o actualiza una identidad de terceros, devuelve instrucciones de sincronización de ID en la respuesta. Estas instrucciones indican al explorador que sincronice la identidad del visitante con los dominios de los socios (DSP, redes de anuncios y otras plataformas de activación), de modo que las audiencias de Experience Platform puedan coincidir y entregarse en esas plataformas.

## Requisitos previos

La compatibilidad con la identidad unificada requiere lo siguiente:

* El sitio utiliza la recopilación de datos de origen en un dominio que usted controla.
* Su implementación utiliza FPID u otra estrategia de persistencia de origen como base.
* Las cookies de terceros están habilitadas en la configuración de Web SDK.
* La sincronización de ID de terceros está habilitada para el conjunto de datos.
* El visitante usa un explorador que permite cookies de terceros (consulte [Compatibilidad del explorador](#browser-compatibility) a continuación).

## Configuración

1. **Habilitar cookies de terceros en Web SDK**: habilite la configuración **Usar cookies de terceros** en la implementación de Web SDK. Si usa la extensión de etiqueta, habilite **[!UICONTROL Use third-party cookies]** en [Configuración de identidad](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies). Si usa la biblioteca de JavaScript, establezca [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) en `true`.

1. **Habilitar sincronización de ID de terceros en el conjunto de datos**: habilite la opción **[!UICONTROL Third-Party ID Sync]** en la configuración avanzada del conjunto de datos. Consulte [Crear y configurar flujos de datos](/help/datastreams/configure.md#advanced-options).

1. **Asegúrese de que la persistencia de origen esté implementada**: Confirme que su estrategia de persistencia de origen (como los FPID) ya está implementada en su dominio propio. Consulte [ID de dispositivos de origen en la recopilación de datos](fpid.md).

## Validación

Para comprobar que la compatibilidad con la identidad unificada funciona:

1. Abra las herramientas para desarrolladores del explorador y vaya a la ficha **Red**.
1. Borre las solicitudes existentes y almacene en déclencheur un evento de Web SDK (carga de página o evento personalizado) en una sesión nueva o de incógnito.
1. Encuentre la respuesta de Edge Network (busque llamadas a `adobedc.demdex.net` y su punto final de recopilación de origen).
1. Inspeccione la carga de respuesta para ver las instrucciones de sincronización de ID.

Cuando hay instrucciones de sincronización de ID, la respuesta incluye un identificador de `identity:exchange` similar al siguiente:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Elemento | Descripción |
| --- | --- |
| `type: "identity:exchange"` | Indica que hay instrucciones de sincronización de ID. |
| Matriz `payload` | Lista de direcciones URL de sincronización de ID de socio. |
| `url` valores | Redirija las direcciones URL a dominios asociados para la sincronización de ID. |
| `id` valores | Identificadores de socio. |

>[!TIP]
>
>Si no ve el identificador `identity:exchange` en la respuesta:
>
>* Asegúrese de realizar la prueba con una sesión de explorador nueva o de incógnito. Las identidades existentes no almacenan en déclencheur las nuevas sincronizaciones.
>* Compruebe que la configuración de la secuencia de datos y de Web SDK es correcta.
>* Confirme que está utilizando un explorador que admite cookies de terceros (consulte la tabla siguiente).

Después de confirmar la actividad de sincronización de ID, compruebe que:

* La identidad de origen persiste como se espera en las cargas de página en el dominio que posee.
* Los flujos de activación e informes se comportan según lo esperado en los entornos admitidos.

## Compatibilidad del explorador {#browser-compatibility}

Las funciones de identidad de terceros dependen de la compatibilidad del explorador con cookies de terceros. La siguiente tabla resume el comportamiento esperado:

| Explorador | Compatibilidad con cookies de terceros | Demdex disponible | Comportamiento de identidad |
| --- | --- | --- | --- |
| Google Chrome | Admitido | Sí | Demdex → ECID (coherente entre dominios) |
| Microsoft Edge | Admitido de forma predeterminada | Sí | Demdex → ECID (coherente entre dominios) |
| Mozilla Firefox | Bloqueado de forma predeterminada (ETP) | No (de forma predeterminada) | FPID → ECID (por dominio) |
| Apple Safari | Bloqueado (ITP) | No | FPID → ECID (por dominio) |

En los exploradores que bloquean cookies de terceros, la identificación de origen sigue funcionando normalmente. Las funciones de activación de terceros solo están disponibles cuando el explorador permite cookies de terceros.

## Limitaciones

* El comportamiento de la identidad de terceros depende completamente del explorador del visitante que permite las cookies de terceros. No hay reserva para la activación de terceros en exploradores que los bloqueen.
* La vinculación automática requiere que el visitante vuelva al sitio. La proporción de la audiencia elegible para la activación de terceros aumenta gradualmente con el tiempo.
