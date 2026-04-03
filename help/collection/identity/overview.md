---
title: Identidad en la recopilación de datos
description: Descubra cómo la recopilación de datos utiliza ECID, CORE ID, persistencia de origen e identityMap en implementaciones web.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identidad en la recopilación de datos

La recopilación de datos de Adobe utiliza señales de identidad para reconocer a los visitantes que regresan y llevar el contexto a través de las experiencias. Cuando un visitante llega a su sitio, Edge Network genera un Experience Cloud ID (ECID) y lo mantiene en una cookie de origen. Este ECID es el identificador de dispositivo principal que se utiliza en las aplicaciones de Adobe Experience Cloud y es la base en la que se basan el análisis, la personalización y la activación de audiencia. En su implementación, puede acceder al ECID del visitante en el lado del cliente a través del comando [`getIdentity`](/help/collection/js/commands/getidentity.md). En el nivel de flujo de datos, puede usar la [preparación de datos para la recopilación de datos](/help/datastreams/data-prep.md) para asignar el ECID a un campo XDM personalizado antes de que llegue a los servicios descendentes.

El ECID identifica un dispositivo, no una persona. Para enlazar la actividad a una persona conocida, puede enviar identificadores adicionales, como un ID de CRM o un correo electrónico con hash, junto con el ECID mediante el XDM [`identityMap`](./identity-map.md). Adobe recomienda establecer un área de nombres de nivel de persona como [identidad principal](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) siempre que haya una disponible.

Más allá del ECID predeterminado, la recopilación de datos admite señales de identidad adicionales en función de la implementación:

* **ID de dispositivos de origen (FPID)**: Identificadores de dispositivos que genera y administra en la infraestructura que controla. Edge Network usa un FPID para [inicializar el ECID](./fpid.md), lo que le proporciona una persistencia de cookies más sólida en las propiedades propias cuando las restricciones del explorador acortan la vida de las cookies administradas por Adobe.
* **CORE ID**: Identificador independiente basado en demdex que participa en flujos de trabajo de identidad de terceros cuando hay cookies de terceros disponibles. El identificador principal es distinto del ECID y se puede recuperar mediante [`getIdentity`](/help/collection/js/commands/getidentity.md). Para obtener más información sobre cómo funcionan juntos los contextos de identidad de origen y de terceros, consulte [Compatibilidad con identidad unificada](./unified-identity-support.md).

Si actualiza desde la API de visitante o concilia un comportamiento de identidad anterior, consulte [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) para migrar las cookies AMCV existentes.

## Colección de origen y de terceros {#first-party-and-third-party-collection}

Web SDK siempre establece la identidad [cookies](https://experienceleague.adobe.com/es/docs/core-services/interface/data-collection/cookies/web-sdk) (como `kndctr_` cookies) como cookies de origen en su dominio, independientemente de qué extremo reciba la solicitud de recopilación de datos. El punto final de recopilación (el dominio al que la implementación envía los datos) es una opción independiente que afecta a la forma en que los exploradores y las directivas de red tratan la solicitud en sí.

**Recopilación de origen** enruta las solicitudes de recopilación de datos a través de un dominio que controla su organización (por ejemplo, `data.example.com`), utilizando un CNAME que señala al Edge Network de Adobe. Como la solicitud permanece en el dominio, es menos probable que la bloqueen bloqueadores de anuncios o restricciones de red del explorador. La recopilación de origen también es un requisito previo para establecer [ID de dispositivos de origen](./fpid.md) desde su propia infraestructura de servidor, que es la estrategia de identidad más duradera disponible. Adobe recomienda usar el [programa de certificados administrado por Adobe](https://experienceleague.adobe.com/es/docs/core-services/interface/data-collection/adobe-managed-cert) para configurar la colección de origen para su implementación.

**La colección de terceros** envía solicitudes directamente a [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md), que pertenece a Adobe (como `example.data.adobedc.net`). Aunque las cookies de identidad siguen configurándose como cookies de origen en el dominio, la solicitud en sí misma va a un dominio de terceros, que algunos exploradores y bloqueadores de anuncios pueden restringir.

## Elija el patrón de identidad correcto {#choose-your-path}

* **Refuerce la persistencia de la identidad en las propiedades de propiedad**: Use [ID de dispositivos de origen](./fpid.md) cuando las restricciones del explorador acorten la duración de las cookies y necesite una continuidad más sólida para el análisis y la personalización en los sitios que controla.
* **Pasar la identidad de una aplicación a la web móvil**: Usa [el uso compartido de identidades de móvil a web](./mobile-to-web.md) cuando el visitante comience en tu aplicación móvil y continúe en una página web móvil o WebView.
* **Mantenga la identidad continua entre sus dominios**: Use el uso compartido entre dominios [cuando los visitantes se muevan entre las propiedades web de su organización y desee un sistema de informes y una personalización coherentes.](./cross-domain-sharing.md)
* **Combine persistencia de origen con activación de terceros**: use [Compatibilidad con identidad unificada](./unified-identity-support.md) cuando necesite una identificación de origen duradera junto con flujos de activación de terceros admitidos.
* **Enviar identificadores de nivel de persona**: Use [`identityMap`](./identity-map.md) para enviar ID de CRM, correos electrónicos con hash y otros identificadores de nivel de persona junto con el ECID para que los servicios descendentes puedan vincular la actividad a una persona conocida.
* **Comprenda cómo afecta el consentimiento a la identidad**: lea [Consentimiento e identidad](./consent.md) para saber cómo controlan `defaultConsent` y `setConsent` cuándo Web SDK genera un ECID, establece cookies y envía datos.

Para obtener ayuda para diagnosticar problemas de identidad, como inflación de visitantes, incoherencias de ECID o problemas de FPID, consulte [Solución de problemas de identidad](./troubleshooting.md).
