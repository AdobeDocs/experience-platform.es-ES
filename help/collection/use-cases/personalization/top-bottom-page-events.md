---
title: Configuración de la parte superior e inferior de los eventos de página en Web SDK
description: Este artículo explica cómo utilizar la parte superior e inferior de los eventos de página en Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Configuración de la parte superior e inferior de los eventos de página en Web SDK

Al ofrecer experiencias personalizadas, el tiempo de carga de una página web es esencial. Para minimizar el tiempo que un usuario espera contenido personalizado, Web SDK admite la configuración de los eventos superior e inferior de la página.

Los eventos superior e inferior de página describen un método para cargar de forma asíncrona varios elementos en la página, manteniendo al mismo tiempo el tiempo de carga de la página como mínimo:

* La parte superior del evento de página solicita personalización en cuanto la página empieza a cargarse.
* La parte inferior del evento de página registra una vista de página cuando la página termina de cargarse.

Adobe Analytics ignora la parte superior de los eventos de página, lo que lleva a un registro de métricas más preciso, ya que solo se registra una visita a la página (la parte inferior del evento de página).

Puede configurar los eventos superior e inferior de la página de dos maneras: llamando directamente a la biblioteca de JavaScript de Web SDK (`alloy()`) o utilizando la extensión de etiquetas de Web SDK en la interfaz de usuario de etiquetas de Adobe Experience Platform. La acción [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) de la extensión de etiqueta incluye una opción &#39;[!UICONTROL Use guided events]&#39; que preconfigura valores de campo para los escenarios &#39;[!UICONTROL Request personalization]&#39; (parte superior de la página) y &#39;[!UICONTROL Collect analytics]&#39; (parte inferior de la página). Cada ejemplo siguiente muestra ambas implementaciones.

## Evento de parte superior de la página {#top-of-page}

El ejemplo siguiente configura una parte superior del evento de página que solicita personalización pero suprime [eventos de visualización](display-events.md) para las propuestas procesadas automáticamente. Estos eventos de visualización se envían con la parte inferior del evento de página en su lugar.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parámetro | Obligatorio/Opcional | Descripción |
| --- | --- | --- |
| `type` | Requerido | Establezca este parámetro en `decisioning.propositionFetch`. Este tipo de evento especial indica a Adobe Analytics que elimine este evento. Al utilizar Customer Journey Analytics, también puede configurar un filtro para soltar estos eventos. Consulte [Tipos de eventos de Edge Network en Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types) para obtener más información. |
| `renderDecisions` | Requerido | Establezca este parámetro en `true`. Este parámetro indica a Web SDK que procese las decisiones devueltas por Edge Network. |
| `personalization.sendDisplayEvent` | Requerido | Establezca este parámetro en `false`. Este parámetro detiene el envío de eventos de visualización. |

>[!TAB Extensión de etiqueta Web SDK]

Configure una acción [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) en la regla que se active en la parte superior de la página. Habilite **[!UICONTROL Use guided events]** y luego seleccione **[!UICONTROL Request personalization]**. Esta opción bloquea &#39;[!UICONTROL Type]&#39; a &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;, &#39;[!UICONTROL Render visual personalization decisions]&#39; a habilitado y &#39;[!UICONTROL Automatically send a display event]&#39; a deshabilitado.

Para establecer estos campos manualmente, deje **[!UICONTROL Use guided events]** deshabilitado y configure cada campo usted mismo.

>[!ENDTABS]

## Final de ejemplos de eventos de página {#bottom-of-page}

### Proposiciones procesadas automáticamente {#bottom-auto-rendered}

El ejemplo siguiente configura un evento de final de página que envía eventos de visualización para propuestas que se representaron automáticamente en la página pero se suprimieron en el evento [principio de página](#top-of-page).

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parámetro | Obligatorio/Opcional | Descripción |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Requerido | Establezca este parámetro en `true`. Este parámetro habilita el envío de eventos de visualización que se suprimieron en la parte superior del evento de página. |
| `xdm` | Opcional | Utilice este objeto para incluir todos los datos que desee para la parte inferior del evento de página. |

>[!TAB Extensión de etiqueta Web SDK]

Configure una acción [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) en la regla que se active en la parte inferior de la página. Habilite **[!UICONTROL Use guided events]** y luego seleccione **[!UICONTROL Collect analytics]**. Esta opción bloquea &#39;[!UICONTROL Include rendered propositions]&#39; para que esté habilitado.

Para establecer este campo manualmente, deje **[!UICONTROL Use guided events]** deshabilitado y habilite **[!UICONTROL Include rendered propositions]** directamente. De forma opcional, rellene el campo **[!UICONTROL XDM]** con un elemento de datos de [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que lleve los datos de su página.

>[!ENDTABS]

### Proposiciones procesadas manualmente {#bottom-manually-rendered}

El ejemplo siguiente configura una parte inferior de un evento de página que envía eventos de visualización para propuestas que se procesaron manualmente en la página (es decir, para ámbitos o superficies de decisión personalizados).

>[!NOTE]
>
>En esta situación, el evento de la parte inferior de la página debe esperar hasta que la parte superior del evento de la página se haya completado para que las propuestas se puedan procesar y registrar.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```

| Parámetro | Obligatorio/Opcional | Descripción |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Requerido | Esta sección define las propuestas procesadas manualmente. Debe incluir las propuestas `id`, `scope` y `scopeDetails`. Consulte [Administrar eventos de visualización](display-events.md) para obtener más información. El contenido de personalización procesado manualmente debe incluirse en la parte inferior del evento de la página. |
| `xdm._experience.decisioning.propositionEventType` | Requerido | Establezca este parámetro en `display: 1`. |
| `xdm` | Opcional | Utilice este objeto para incluir todos los datos que desee para la parte inferior del evento de página. |

>[!TAB Extensión de etiqueta Web SDK]

La opción &#39;[!UICONTROL Use guided events]&#39; no cubre este escenario, por lo que debe configurar la acción manualmente:

1. Cree un elemento de datos [XDM object](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (o [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)) que rellene `_experience.decisioning.propositions` con los `id`, `scope` y `scopeDetails` de cada propuesta procesada y establezca `_experience.decisioning.propositionEventType.display` en `1`. Consulte [Administrar eventos de visualización](display-events.md) para obtener más información.
1. En la acción [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) para la parte inferior de la regla de página, deje **[!UICONTROL Use guided events]** deshabilitado y haga referencia al elemento de datos del campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Aplicación de una sola página con eventos en la parte superior e inferior de la página {#spa-example}

En una aplicación de una sola página, debe especificar el nombre de la vista en cada cambio de vista para que Web SDK procese la personalización correcta en la parte superior de la página y registre la vista correcta en la parte inferior de la página.

### Primera vista de página {#spa-first-view}

En este ejemplo, `home` es la vista cargada en la carga inicial de la página.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

La llamada principal solicita personalización para la vista `home` sin registrar una visita de Analytics ni activar eventos de visualización. La llamada inferior registra la vista de página y activa los eventos de visualización suprimidos. Incluya el mismo `viewName` en ambas llamadas para que la vista se registre de manera consistente.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Extensión de etiqueta Web SDK]

1. Cree un elemento de datos [XDM object](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que establezca `web.webPageDetails.viewName` en el nombre de la vista (por ejemplo, `home`).
1. Configure una acción de parte superior de la página [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): habilite **[!UICONTROL Use guided events]**, seleccione **[!UICONTROL Request personalization]** y haga referencia al elemento de datos en el campo **[!UICONTROL XDM]**.
1. Configure una acción en la parte inferior de la página **[!UICONTROL Send event]**: habilite **[!UICONTROL Use guided events]**, seleccione **[!UICONTROL Collect analytics]** y haga referencia al mismo elemento de datos en el campo **[!UICONTROL XDM]** para que `viewName` coincida en ambos eventos.

>[!ENDTABS]

### Segunda vista de página: opción 1 {#spa-second-view-option-1}

En este ejemplo, un solo evento es suficiente porque ya se ha recuperado la personalización de la página.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

>[!TAB Extensión de etiqueta Web SDK]

1. Cree un elemento de datos [XDM object](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que establezca `web.webPageDetails.viewName` en el nombre de la nueva vista (por ejemplo, `cart`).
1. En el cambio de vista, configure una sola acción [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): deje **[!UICONTROL Use guided events]** deshabilitado, habilite **[!UICONTROL Render visual personalization decisions]** y haga referencia al elemento de datos en el campo **[!UICONTROL XDM]**.

>[!ENDTABS]

### Segunda vista de página: opción 2 {#spa-second-view-option-2}

Utilice este método cuando tenga que retrasar la parte inferior del evento de la página (por ejemplo, cuando los datos de análisis de la página no estén listos en el momento del cambio de vista). Gestionar el cambio de vista en dos pasos:

1. En la parte superior de la página, procese las propuestas ya recuperadas sin realizar una llamada de Edge Network.
1. Una vez que los datos de análisis estén listos, envíe la parte inferior del evento de página.

Incluya el mismo `viewName` en ambas llamadas para que la vista se registre de manera consistente.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

Llame a [`applyPropositions`](/help/collection/js/commands/applypropositions.md) en la parte superior de la página para procesar las propuestas almacenadas en caché para la nueva vista. A continuación, llame a `sendEvent` en la parte inferior de la página con `includeRenderedPropositions: true` para que se activen los eventos de visualización suprimidos.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!TAB Extensión de etiqueta Web SDK]

1. Cree un elemento de datos [XDM object](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que establezca `web.webPageDetails.viewName` en el nombre de la nueva vista (por ejemplo, `cart`).
1. Para la parte superior del evento de página, configure una acción [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) y establezca el campo **[!UICONTROL View name]** en el nombre de la vista (por ejemplo, `cart`). Esta acción procesa las propuestas ya recuperadas sin ponerse en contacto con Edge Network.
1. Para la parte inferior del evento de página, configure una acción de [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): habilite **[!UICONTROL Use guided events]**, seleccione **[!UICONTROL Collect analytics]** y haga referencia al elemento de datos en el campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Ejemplo de GitHub {#github-sample}

La [muestra superior e inferior en el repositorio alloy-samples](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) muestra cómo solicitar personalización en la parte superior de la página y enviar métricas de análisis en la parte inferior. Descargue el ejemplo y ejecútelo localmente para ver cómo funcionan la parte superior e inferior de los eventos de página. El ejemplo utiliza la biblioteca JavaScript directamente; los mismos patrones se aplican cuando se configuran reglas equivalentes en la extensión de etiquetas Web SDK.
