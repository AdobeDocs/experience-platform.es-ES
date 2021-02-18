---
title: Uso de Adobe Target con el SDK web de plataforma
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web Experience Platform mediante Adobe Target
keywords: destinatario;destinatario de adobe;actividad.id;experiencia.id;decisionesDeprocesamiento;ámbitosDeDecisión;fragmento de código de ocultación previa;vec;Compositor de experiencias basadas en formularios;xdm;audiencias;decisiones;ámbito;esquema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---


# Uso de Adobe Target con el SDK web de plataforma

Adobe Experience Platform [!DNL Web SDK] puede entregar y procesar experiencias personalizadas administradas en Adobe Target en el canal web. Puede utilizar un editor WYSIWYG, denominado [Compositor de experiencias visuales](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), para crear, activar y entregar sus actividades y experiencias de personalización.

## Activación de Adobe Target

Para habilitar [!DNL Target], debe hacer lo siguiente:

1. Habilite el destinatario en la [configuración de Edge](../../fundamentals/edge-configuration.md) con el código de cliente apropiado.
1. Añada la opción `renderDecisions` a sus eventos.

A continuación, opcionalmente, también puede:

* Añada `decisionScopes` a sus eventos para recuperar actividades específicas (útil para actividades creadas con el compositor basado en formularios).
* Añada el [fragmento de ocultamiento previo](../manage-flicker.md) para ocultar solo ciertas partes de la página.

## Uso del VEC de Adobe Target

Para utilizar el VEC con una implementación de SDK web de plataforma, debe instalar y activar la extensión de ayuda de [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

## Actividades de VEC de procesamiento automático

El SDK web de Adobe Experience Platform tiene la capacidad de procesar automáticamente las experiencias definidas mediante el VEC de Adobe Target en la web para los usuarios. Para indicar al SDK web de Adobe Experience Platform que procese automáticamente actividades VEC, envíe un evento con `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Uso del Compositor basado en formularios

El Compositor de experiencias basadas en formularios es una interfaz no visual que resulta útil para configurar pruebas A/B, [!DNL Experience Targeting], Automated Personalization y actividades de Recommendations con diferentes tipos de respuesta, como JSON, HTML, Image, etc. Según el tipo de respuesta o la decisión devuelta por Adobe Target, se puede ejecutar la lógica principal de su negocio. Para recuperar las decisiones de las actividades del Compositor basado en formularios, envíe un evento con todos los &quot;temas de decisión&quot; para los que desee recuperar una decisión.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Ámbitos de decisión

`decisionScopes` define las secciones, ubicaciones o partes de las páginas en las que desea representar una experiencia personalizada. Estos `decisionScopes` son personalizables y definidos por el usuario. Para los clientes actuales [!DNL Target], `decisionScopes` también se conocen como &quot;mboxes&quot;. En la interfaz de usuario [!DNL Target], `decisionScopes` aparece como &quot;ubicaciones&quot;.

## El ámbito `__view__`

El SDK web de Adobe Experience Platform proporciona funciones que permiten recuperar acciones de VEC sin necesidad de depender del SDK para procesar las acciones de VEC por usted. Envíe un evento con `__view__` definido como `decisionScopes`.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Audiencias en XDM

Al definir Audiencias para las actividades de Destinatario que se enviarán mediante Adobe Experience Platform Web SDK, se debe definir y utilizar [XDM](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/home.html). Después de definir esquemas, clases y mezclas XDM, puede crear una regla de audiencia de Destinatario definida por los datos XDM para la segmentación. En Destinatario, los datos XDM se muestran en el Generador de Audiencias como un parámetro personalizado. El XDM se serializa mediante notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene actividades de Destinatario con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, tenga en cuenta que no se enviarán correctamente a través del SDK. En lugar de utilizar parámetros personalizados o el perfil del usuario, debe utilizar XDM en su lugar. Sin embargo, hay campos de objetivo de audiencia predeterminados que se admiten mediante el SDK web de Adobe Experience Platform y que no requieren XDM. Estos son los campos disponibles en la interfaz de usuario de Destinatario que no requieren XDM:

* Biblioteca de segmentos
* Geografía 
* Red
* Operating System
* Páginas del sitio
* Explorador
* Fuentes de tráfico
* Lapso de tiempo

## Terminología

__Decisiones:__ En  [!DNL Target], se correlacionan con la experiencia seleccionada de una Actividad.

__Esquema:__ El esquema de una decisión es el tipo de oferta en  [!DNL Target].

__Ámbito de aplicación:__ El ámbito de aplicación de la decisión. En [!DNL Target], este es el mBox. El mBox global es el ámbito `__view__`.

__XDM:__ El XDM se serializa en notación de puntos y luego se coloca  [!DNL Target] como parámetros de mBox.
