---
title: personalización
description: Procesar contenido diferente para diferentes usuarios y crear una experiencia personalizada para ellos.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

El objeto `personalization` configura qué decisiones de personalización (ofertas o propuestas) se solicitan y cómo se administran en la solicitud y la respuesta. Resulta especialmente útil en implementaciones de Adobe Target o Adobe Journey Optimizer, ya que es la fuerza motriz que permite personalizar el contenido mostrado por usuario.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

El objeto `personalization` contiene las siguientes propiedades:

## `personalization.decisionScopes`

La propiedad `decisionScopes` es una matriz de cadenas que indica a Web SDK que recupere y devuelva decisiones de personalización. Cada elemento de la matriz identifica una ubicación, contexto o ubicación lógica donde se desea obtener contenido personalizado.

Esta propiedad es útil cuando desea recuperar explícitamente contenido personalizado para áreas o componentes específicos de una página. Resulta especialmente útil en aplicaciones de una sola página que pueden requerir diferentes conjuntos de ofertas a medida que cambia la navegación o la vista del usuario. También puede utilizar esta propiedad para optimizar el rendimiento recuperando únicamente ofertas para los elementos de la interfaz de usuario relevantes para el usuario.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

En Adobe Target, cada ámbito de decisión se asigna a un mbox o actividad. En Adobe Journey Optimizer, cada ámbito de decisión se asigna a ubicaciones o campañas de contenido web basadas en decisiones. En Offer Decisioning, los ámbitos de decisión se asignan a qué ofertas o propuestas debe recibir el visitante.

>[!TIP]
>
>Si desea solicitar (o bloquear) el ámbito global, utilice [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) en lugar de especificarlo aquí en `decisionScopes`.

## `personalization.surfaces`

La propiedad `surfaces` es una matriz de cadenas [surface URI](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) que definen manualmente el canal, dispositivo o contexto para el que se solicita la personalización. Permiten distinguir entre diferentes experiencias digitales, como dominios, aplicaciones o plataformas de dispositivos, dentro del ecosistema de canales cruzados. De forma predeterminada, la biblioteca infiere la superficie por defecto de la página actual. Puede utilizar esta propiedad para anular la superficie deducida automáticamente para la página actual.

Esta propiedad es útil cuando desea utilizar la personalización entre canales y debe distinguir cómo funciona la personalización entre canales independientes. Permite crear ofertas distintas para sitios diferentes bajo la misma organización de Adobe Experience Platform.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Esta propiedad se utiliza fundamentalmente con Adobe Journey Optimizer, ya que coincide con las superficies configuradas en campañas de Journey Optimizer y en la administración de superficies.

## `personalization.schemas`

La propiedad `schemas` es una matriz de cadenas de URI de esquema que filtra los tipos de contenido de personalización solicitado a Edge Network. Al establecer esta propiedad, se restringe la respuesta que recibe de Adobe para incluir únicamente ofertas que coincidan con las definiciones de tipo de contenido especificadas. Si se omite, la biblioteca solicita ofertas de todos los esquemas disponibles para los ámbitos o superficies coincidentes.

Esta propiedad ayuda a optimizar el tamaño de la respuesta y se asegura de que el sitio web o la aplicación solo reciban los tipos de oferta que puede gestionar. También resulta útil cuando se utiliza con aplicaciones de una sola página que procesan contenido personalizado de una manera específica (como utilizar solo acciones DOM o solo objetos JSON).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Se admiten los siguientes URI de esquema:

* **`https://ns.adobe.com/personalization/dom-action`**: ofertas que son acciones DOM directas, generadas generalmente por el Compositor de experiencias visuales en Adobe Target. Contienen instrucciones para manipular automáticamente los elementos de la página sin código adicional. Es el estándar de la personalización web procesada automáticamente.
* **`https://ns.adobe.com/personalization/html-content-item`**: ofertas que contienen HTML sin procesar entregado como cadena. Su implementación suele insertar este contenido en la ubicación deseada en la página, lo que le proporciona más control que las acciones del DOM. Normalmente se utiliza para titulares, fragmentos o contenido modal.
* **`https://ns.adobe.com/personalization/json-content-item`**: ofertas que tienen el formato de objeto JSON. Normalmente se utiliza en implementaciones basadas en API o front-end que esperan datos estructurados en lugar de cambios de HTML o DOM.
* **`https://ns.adobe.com/personalization/redirect-item`**: ofertas que redirigen a una dirección URL diferente. Se utiliza para llevar al usuario a una nueva página en función de la lógica de segmentación o de toma de decisiones, como páginas de aterrizaje o flujos de incorporación.
* **`https://ns.adobe.com/personalization/ruleset-item`**: entrega un bloque de lógica empresarial para activar un motor de reglas del lado del cliente. Contiene un conjunto de reglas con versiones que define las condiciones lógicas y las consecuencias (si es necesario, lógica de personalización).
* **`https://ns.adobe.com/personalization/message/in-app`**: ofertas formateadas específicamente para mensajes en la aplicación de Adobe Journey Optimizer, normalmente se representan como modelos, titulares, ventanas emergentes o superposiciones.
* **`https://ns.adobe.com/personalization/message/content-card`**: ofertas con formato específico para tarjetas de contenido de Adobe Journey Optimizer, diseñadas para fuentes persistentes o de estilo bandeja de entrada en aplicaciones web o móviles.
* **`https://ns.adobe.com/personalization/message/native-alert`**: ofertas formateadas específicamente para alertas nativas de Adobe Journey Optimizer, lo que activa cuadros de diálogo de notificación nativos de la plataforma.
* **`https://ns.adobe.com/personalization/measurement`**: se usa para rastrear clics e interacciones en ofertas personalizadas. No incluye contenido que se pueda procesar.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: esquema para modificar el historial de eventos de un visitante en el almacenamiento local. Los SDK los utilizan internamente para rastrear qué experiencias se han entregado o bloqueado. No incluye contenido que se pueda procesar.
* **`https://ns.adobe.com/personalization/default-content-item`**: contenido alternativo o predeterminado, normalmente cuando no se admite ninguna oferta personalizada. Garantiza que los usuarios que no cumplan los requisitos sigan recibiendo contenido, lo que mantiene la experiencia coherente.

## `personalization.sendDisplayEvent`

La propiedad `sendDisplayEvent` es un booleano que determina si un evento de notificación de visualización se envía automáticamente a Edge Network inmediatamente después de que se represente contenido personalizado en la página. Si se omite, su valor predeterminado es `true`. Establezca esta variable en `false` si no desea indicar que el contenido personalizado se procesó para el seguimiento de impresiones.

El caso de uso más común para establecer esta variable en `false` es cuando planea enviar otro comando a otra parte de la implementación que indique un evento de visualización. Algunas implementaciones tienen eventos de impresión y de Analytics; esta propiedad le proporciona control total sobre los comandos `sendEvent` que incrementan las impresiones.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Las versiones anteriores de Web SDK (versiones 2.12.0 y anteriores) usan `sendDisplayNotifications` en su lugar.

## `personalization.includePendingDisplayNotifications`

La propiedad `includePendingDisplayNotifications` es un booleano que controla si alguna notificación de visualización pendiente está incluida en la llamada actual `sendEvent`. Las notificaciones de visualización pendientes son impresiones de contenido personalizado que se han representado, pero que aún no se han notificado a Edge Network como evento de visualización. Esta propiedad es útil cuando se utilizan aplicaciones de una sola página, ya que el procesamiento de contenido personalizado y las llamadas a `sendEvent` pueden ser asíncronas entre sí.

El valor predeterminado de esta propiedad es `false`. Establezca esta propiedad en `true` si desea procesar por lotes y vaciar las notificaciones de visualización pendientes para que sus impresiones se registren con precisión. La implementación sincrónica, como los sitios web tradicionales, no suele necesitar establecer esta propiedad.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

La propiedad `defaultPersonalizationEnabled` es un booleano que le proporciona un control explícito sobre cómo Web SDK solicita el ámbito de personalización predeterminado de toda la página (`__view__`) y la superficie para este comando `sendEvent`. De forma predeterminada, en el primer comando `sendEvent` después de una carga de página, Web SDK solicita ofertas para el ámbito de personalización predeterminado de toda la página y las superficies asociadas. Los comandos `sendEvent` posteriores no solicitan la personalización predeterminada. Puede utilizar esta propiedad para anular ese comportamiento. Resulta útil en implementaciones de aplicaciones de una sola página en las que es posible que desee volver a solicitar la personalización predeterminada a medida que el usuario navega por el sitio. También puede usar esta propiedad cuando quiera _solamente_ enviar un evento de visualización sin duplicar la recuperación de ofertas.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Esta propiedad utiliza la siguiente lógica en función de cómo se establezca:

* **No establecido**: Solicitar personalización predeterminada cuando aún no se ha solicitado. La personalización predeterminada generalmente se solicita en los primeros `sendEvent` después de la carga de una página y, a continuación, no se solicita de nuevo en las llamadas a `sendEvent` subsiguientes en la misma página. Al establecer esta propiedad, se anula este comportamiento.
* **`true`**: solicite explícitamente el ámbito de página y la superficie predeterminada, incluso si este comando `sendEvent` no es el primero después de cargar una página. Los momentos ideales para establecer esta propiedad en `true` son cuando necesite forzar una solicitud de personalización predeterminada, como en escenarios de aplicación de una sola página.
* **`false`**: suprime explícitamente la solicitud para el ámbito de página y la superficie predeterminada, incluso si este comando `sendEvent` es el primero después de cargar una página. Los momentos ideales para establecer esta propiedad en `false` son cuando desea que un comando de `sendEvent` determinado no solicite nuevas ofertas y, en su lugar, envíe datos a Analytics o envíe un evento de visualización.

## Componentes de Personalization que utilizan la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a esta propiedad es la sección [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) al configurar una acción &#39;[!UICONTROL Send event]&#39;.
