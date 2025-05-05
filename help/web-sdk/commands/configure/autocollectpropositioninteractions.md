---
title: autoCollectPropositionInteractions
description: Obtenga información sobre cómo configurar Experience Platform Web SDK para que recopile automáticamente datos de vínculos.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: 55c656e7fd08e98b75c20f0688a6697baf533291
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

La propiedad `autoCollectPropositionInteractions` es una configuración opcional que determina si Web SDK debe recopilar automáticamente interacciones de propuestas.

El valor es un mapa de proveedores de decisiones, cada uno con un valor que indica cómo se deben gestionar las interacciones de propuestas automáticas.

## Valores compatibles {#supported-values}

De manera predeterminada, las interacciones automáticas de propuestas se recopilan _siempre_ para Adobe Journey Optimizer (`AJO`) y _nunca_ para Adobe Target (`TGT`).

A continuación se muestra el valor predeterminado de `autoTrackPropositionInteractions`.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Consulte la tabla siguiente para conocer los valores de configuración admitidos para cada proveedor de decisiones.

| Valor | Descripción |
| --- | --- |
| `always` | [!DNL Web SDK] siempre recopilará automáticamente `interact` eventos para cualquier elemento asociado con una propuesta. |
| `never` | [!DNL Web SDK] nunca recopilará automáticamente `interact` eventos para los elementos asociados con una propuesta. |
| `decoratedElementsOnly` | [!DNL Web SDK] recopilará automáticamente `interact` eventos para elementos asociados con una propuesta, pero solo si el elemento incluye atributos de datos que especifican una etiqueta o token. |

## Seguimiento automático de la interacción de propuestas {#logic}

Cuando habilita el seguimiento automático de interacción de propuestas, el [!DNL Web SDK] recopila automáticamente cualquier clic dentro de un elemento de propuesta procesado en el DOM. Esto incluye cualquier experiencia procesada automáticamente en el DOM por [!DNL Web SDK] y las experiencias procesadas en el DOM mediante el comando [`applyPropositions`](../applypropositions.md).

### Atributos de datos {#data-attributes}

Puede utilizar atributos de datos en elementos para añadir especificidad a una interacción.

| Nombre | Atributo de datos | Descripción |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Cuando el atributo de datos de etiqueta está presente en un elemento donde se hizo clic, se incluye con los detalles de interacción enviados a [!DNL Edge Network]. [!DNL Web SDK] busca un atributo de datos de etiqueta que comience por el elemento donde se hizo clic y que suba por el árbol DOM. [!DNL Web SDK] utiliza la primera etiqueta que encuentra. |
| [!DNL Token] | `data-aep-click-token` | Use este token al aprovechar las directivas de decisión en [campañas basadas en código de Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Puede utilizar el token para distinguir en qué elemento de directiva de decisión se hizo clic. Cuando el atributo de datos de token está presente en un elemento en el que se hizo clic, se incluye con los detalles de interacción enviados al Edge Network. [!DNL Web SDK] busca un atributo de datos de token que comience por el elemento donde se hizo clic y que suba por el árbol DOM. [!DNL Web SDK] utiliza el primer token que encuentra. |
| [!DNL Interact ID] | `data-aep-interact-id` | [!DNL Web SDK] agrega automáticamente este ID único a los elementos contenedores al procesar propuestas. Web SDK utiliza este identificador para correlacionar [!DNL DOM] elementos con propuestas. Como se trata de un ID requerido por [!DNL Web SDK], no debe modificarlo en modo alguno. Puede ignorarlo con seguridad. |

**Ejemplo**

Consulte el siguiente fragmento de código para ver un ejemplo de uso de atributos de datos.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### El comando `applyPropositions` {#apply-propositions}

Consulte la documentación de [`applyPropositions`](../applypropositions.md) para saber cómo funciona este comando.

El comando `applyPropositions` es una forma cómoda de procesar propuestas para [!DNL DOM]. Sin embargo, en el caso de las campañas basadas en código con `JSON`, puede utilizar este comando para correlacionar un elemento [!DNL DOM] existente (o el que el código de su aplicación procesó en la pantalla en función de los valores `JSON`) con una propuesta.

Esta correlación activa el seguimiento automático de interacciones para ese elemento y asigna a ese elemento la propuesta adecuada. Para lograrlo, establezca `actionType` en `track`.

**Ejemplo**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Habilite propuestas automáticas e interacciones mediante el rastreo de clics a través de la extensión de etiquetas de Web SDK {#tag-extension}

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **Recopilación de datos** > **Etiquetas**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **Extensiones** y, a continuación, seleccione **Configurar** en la tarjeta de Adobe Experience Platform Web SDK.
1. Desplácese hacia abajo hasta la sección **[!UICONTROL Recopilación de datos]** y, a continuación, active la casilla de verificación **Habilitar propuestas y el seguimiento de vínculos de interacción**.
1. Seleccione **Guardar** y luego publique los cambios.

## Habilite el seguimiento automático de propuestas e interacciones de vínculos a través de la biblioteca JavaScript de Web SDK {#library}

El seguimiento de propuestas está habilitado de manera predeterminada en [!DNL Web SDK]. Sin embargo, puede seguir configurándolo con el valor `autoCollectPropositionInteractions` al ejecutar el comando [`configure`](../configure/overview.md).

Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `{"AJO": "always", "TGT": "never"}`. Si prefiere no rastrear automáticamente las interacciones de propuestas, establezca el valor en `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoCollectPropositionInteractions": {"AJO": "always", "TGT": "never"}
});
```
