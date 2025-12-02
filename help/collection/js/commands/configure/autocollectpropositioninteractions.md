---
title: autoCollectPropositionInteractions
description: Recopilar datos automáticamente cuando se hace clic en un vínculo.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

La propiedad `autoCollectPropositionInteractions` es una configuración opcional que determina si Web SDK recopila automáticamente interacciones de propuestas. El valor es un mapa de proveedores de decisiones, cada uno con un valor que indica cómo se deben gestionar las interacciones de propuestas automáticas.

Cuando se habilita el seguimiento automático de la interacción de propuestas, Web SDK recopila automáticamente cualquier clic dentro de un elemento de propuesta procesado en el DOM. Esta colección incluye todas las experiencias que Web SDK representa automáticamente en el DOM y las experiencias que se representan en el DOM mediante el comando [`applyPropositions`](../applypropositions.md).

Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `{"AJO": "always", "TGT": "never"}`. Si prefiere no rastrear automáticamente las interacciones de propuestas, establezca el valor en `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Entre las propiedades compatibles con este objeto se incluyen:

| Propiedad | Descripción |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Los valores posibles para cada propiedad incluyen:

| Valor | Descripción |
| --- | --- |
| **`always`** | Recopilar siempre automáticamente `interact` eventos para cualquier elemento asociado con una propuesta. |
| **`never`** | Nunca recopile automáticamente `interact` eventos para los elementos asociados con una propuesta. |
| **`decoratedElementsOnly`** | Recopilar automáticamente `interact` eventos para elementos asociados con una propuesta si el elemento incluye atributos de datos que especifiquen una etiqueta o un token. |

## Atributos de datos {#data-attributes}

Puede utilizar atributos de datos en elementos para añadir especificidad a una interacción.

| Nombre | Atributo de datos | Descripción |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Cuando el atributo de datos label está presente en un elemento en el que se hizo clic, se incluye con los detalles de interacción enviados a Edge Network. Web SDK busca un atributo de datos de etiqueta que comience por el elemento en el que se ha hecho clic y que suba por el árbol DOM. Web SDK utiliza la primera etiqueta que encuentra. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Use este token al aprovechar las directivas de decisión en [campañas basadas en código de Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Puede utilizar el token para distinguir en qué elemento de directiva de decisión se hizo clic. Cuando el atributo de datos de token está presente en un elemento en el que se hizo clic, se incluye con los detalles de interacción enviados a Edge Network. Web SDK busca un atributo de datos de token que comience por el elemento en el que se ha hecho clic y suba por el árbol DOM. Web SDK utiliza el primer token que encuentra. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Web SDK agrega automáticamente este ID único a los elementos contenedores al procesar las propuestas. Web SDK utiliza este ID para correlacionar elementos DOM con propuestas. Como se trata de un ID requerido por Web SDK, no debe modificarse de ninguna manera. Puede ignorarlo con seguridad. |

## Ejemplo

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Usando `autoCollectPropositionInteractions` con el comando `applyPropositions` {#apply-propositions}

El comando [`applyPropositions`](../applypropositions.md) es una forma cómoda de procesar propuestas al DOM. Sin embargo, en el caso de campañas basadas en código con JSON, puede utilizar este comando para correlacionar un elemento DOM existente (o el que el código de su aplicación procesó en la pantalla en función de los valores JSON) con una propuesta.

Esta correlación activa el seguimiento automático de interacciones para ese elemento y asigna a ese elemento la propuesta adecuada. Para lograrlo, establezca `actionType` en `track`.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Configuración de interacciones automáticas de propuestas para la extensión de etiquetas Web SDK

Los dos menús desplegables siguientes al configurar la extensión de etiquetas Web SDK son el equivalente de este objeto:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
