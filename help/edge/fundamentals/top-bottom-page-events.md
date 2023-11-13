---
title: Uso de los eventos superior e inferior de la página
description: Este artículo explica cómo utilizar la parte superior e inferior de los eventos de página en el SDK web.
source-git-commit: 5322156774388a19788529aee554424b2fb5d91b
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---


# Uso de los eventos superior e inferior de página en el SDK web

Cuando se desea ofrecer experiencias personalizadas a los clientes, es esencial disponer de una página web a la hora de cargarla.

Para optimizar los tiempos de carga y ofrecer personalización lo más rápido posible, el SDK web admite la configuración de los eventos superior e inferior de la página.

Los eventos Top e Bottom of page describen un método para cargar de forma asíncrona varios elementos en la página, manteniendo al mismo tiempo el tiempo de carga de la página al mínimo.

Esta configuración minimiza el tiempo que un usuario tiene que esperar hasta que se cargue el contenido personalizado.

En cuanto a la precisión de las métricas, Adobe Analytics puede ignorar los eventos de la parte superior de la página, lo que lleva a un registro de métricas más preciso, ya que solo se registra una visita a la página (la parte inferior del evento de la página).

## Casos de uso {#use-cases}

Un minorista de ropa deportiva quiere ofrecer experiencias personalizadas a sus compradores, minimizando al mismo tiempo la fricción del usuario al visitar su sitio web, y todo ello sin dejar de poder recopilar métricas de visitantes con precisión.

Mediante los eventos superior e inferior de página del SDK web, el equipo de marketing puede configurar su envío de personalización de la forma más óptima:

* El SDK web envía una solicitud de personalización que se carga en cuanto la página empieza a cargarse. Este es un evento de la parte superior de la página.
* Cuando termina de cargarse la página, se registra un evento de vista de página. Esto sucede más adelante en el proceso de carga de página. Esta es una parte inferior del evento de la página.

## Ejemplo del evento de la parte superior de la página {#top-of-page}

El siguiente ejemplo de código ejemplifica una parte superior de la configuración de evento de página que solicita personalización, pero no envía notificaciones de visualización para propuestas procesadas automáticamente. Las notificaciones de visualización se envían como parte del evento de final de página.

>[!BEGINTABS]

>[!TAB Evento de parte superior de la página]

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
|---|---|---|
| `type` | Requerido | Establezca este parámetro en `decisioning.propositionFetch`. Este tipo de evento especial indica a Adobe Analytics que elimine este evento. Al utilizar Customer Journey Analytics, también puede configurar un  para soltar estos eventos. |
| `renderDecisions` | Requerido | Establezca este parámetro en `true`. Este parámetro indica al SDK web que procese las decisiones devueltas por la red perimetral. |
| `personalization.sendDisplayEvent` | Requerido | Establezca este parámetro en `false`. Esto evita que se envíen notificaciones de visualización. |

>[!ENDTABS]

## Final de ejemplos de eventos de página {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Proposiciones procesadas automáticamente]

El siguiente ejemplo de código ejemplifica una parte inferior de la configuración de evento de página que envía notificaciones de visualización para propuestas que se procesaron automáticamente en la página, pero para las que se suprimieron las notificaciones de visualización en [principio de página](#top-of-page) evento.

>[!NOTE]
>
>En este escenario, debe llamar a la parte inferior del evento de página _después_ la parte superior de la página uno. Sin embargo, no es necesario esperar a la parte inferior del evento de página hasta que se haya completado la parte superior de la página uno.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parámetro | Obligatorio/Opcional | Descripción |
|---|---|---|
| `personalization.includeRenderedPropositions` | Requerido | Establezca este parámetro en `true`. Esto permite enviar notificaciones de visualización que se suprimieron en la parte superior del evento de página. |
| `xdm` | Opcional | Utilice esta sección para incluir todos los datos necesarios para la parte inferior del evento de página. |

>[!TAB Proposiciones procesadas manualmente]

El ejemplo de código siguiente ejemplifica una parte inferior de la configuración de eventos de página que envía notificaciones de visualización para propuestas que se procesaron manualmente en la página (es decir, para ámbitos o superficies de decisión personalizados).

>[!NOTE]
>
>En esta situación, el evento de la parte inferior de la página debe esperar hasta que la parte superior del evento de la página se haya completado para procesar las propuestas y registrar la parte inferior del evento de la página.

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
|---|---|---|
| `xdm._experience.decisioning.propositions` | Requerido | Esta sección define las propuestas procesadas manualmente. Debe incluir la propuesta `ID`, `scope`, y `scopeDetails`. Consulte la documentación sobre cómo [personalización del procesamiento manual](../personalization/rendering-personalization-content.md#manually) para obtener más información sobre cómo registrar las notificaciones de visualización para el contenido procesado manualmente. El contenido de personalización procesado manualmente debe incluirse en la parte inferior de la visita individual a la página. |
| `xdm._experience.decisioning.propositionEventType` | Requerido | Establezca este parámetro en `display: 1`. |
| `xdm` | Opcional | Utilice esta sección para incluir todos los datos necesarios para la parte inferior del evento de página. |

>[!ENDTABS]


## Aplicación de una sola página con visitas individuales a las páginas superior e inferior {#spa-example}


>[!BEGINTABS]

>[!TAB Primera vista de página]

El ejemplo siguiente incluye la adición del requerido `xdm.web.webPageDetails.viewName` parámetro. Esto es lo que la convierte en una aplicación de una sola página. El `viewName` en este ejemplo es la vista que se carga al cargar la página.

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

// Bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

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

>[!TAB Segunda vista de página (opción 1)]

En este ejemplo, no es necesario realizar una división superior/inferior de la página porque ya se ha recuperado la personalización de la página.

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


>[!TAB Segunda vista de página (opción 2)]

Si todavía necesita retrasar la parte inferior de la visita individual a la página, puede utilizar `applyPropositions` para la parte superior de la visita individual a la página. Dado que no es necesario recuperar ninguna personalización ni registrar ningún dato de Analytics, no es necesario realizar una solicitud a la red de Edge.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
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

>[!ENDTABS]

## Ejemplo de GitHub {#github-sample}

La muestra se encuentra en [esta dirección](https://github.com/adobe/alloy-samples/tree/main/top-and-bottom) muestra cómo utilizar el Experience Platform y el SDK web para solicitar personalización en la parte superior de la página y enviar métricas de análisis en la parte inferior. Puede descargar el ejemplo y ejecutarlo localmente para comprender cómo funcionan los eventos superior e inferior de la página.
