---
title: Uso de Adobe Target con el SDK web de Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Experience Platform mediante Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;fragmento de ocultamiento previo;vec;Compositor de experiencias basadas en formularios;xdm;audiencias;decisiones;ámbito;esquema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# Uso de Adobe Target con el SDK web de Platform

Adobe Experience Platform [!DNL Web SDK] puede entregar y renderizar experiencias personalizadas administradas en Adobe Target al canal web. Puede utilizar un editor WYSIWYG, denominado [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para crear, activar y ofrecer sus actividades y experiencias de personalización.

Las siguientes funciones se han probado y actualmente son compatibles con Target:

* Pruebas A/B
* Creación de informes de conversión e impresión de A4T
* Automated Personalization
* Segmentación de experiencias
* Pruebas multivariable
* Creación de informes de conversión e impresión de objetivos nativos
* Compatibilidad con VEC

## Habilitación de Adobe Target

Para habilitar [!DNL Target], haga lo siguiente:

1. Habilite Target en su [almacén de datos](../../fundamentals/datastreams.md) con el código de cliente apropiado.
1. Agregue la opción `renderDecisions` a los eventos.

A continuación, opcionalmente, también puede añadir las siguientes opciones:

* `decisionScopes`: Recupere actividades específicas (útil para actividades creadas con el compositor basado en formularios) añadiendo esta opción a los eventos.
* [Ocultamiento previo del fragmento](../manage-flicker.md): Oculte solo ciertas partes de la página.

## Uso del VEC de Adobe Target

Para utilizar el VEC con una implementación del SDK web de Platform, instale y active la extensión [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper.

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

El Compositor de experiencias basadas en formularios es una interfaz no visual que resulta útil para configurar pruebas A/B, [!DNL Experience Targeting], Automated Personalization y actividades de Recommendations con diferentes tipos de respuestas, como JSON, HTML, Image, etc. Según el tipo de respuesta o la decisión devuelta por Adobe Target, se puede ejecutar la lógica empresarial principal. Para recuperar decisiones para las actividades del Compositor basado en formularios, envíe un evento con todos los &quot;decisionScopes&quot; para los que desee recuperar una decisión.

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

`decisionScopes` define secciones, ubicaciones o partes de las páginas en las que desea mostrar una experiencia personalizada. Estos `decisionScopes` son personalizables y están definidos por el usuario. Para los clientes actuales de [!DNL Target] , `decisionScopes` también se conocen como &quot;mboxes&quot;. En la interfaz de usuario de [!DNL Target], `decisionScopes` aparece como &quot;ubicaciones&quot;.

## El ámbito `__view__`

El SDK web de Adobe Experience Platform proporciona una funcionalidad en la que puede recuperar acciones del VEC sin depender del SDK para representar las acciones del VEC por usted. Envíe un evento con `__view__` definido como `decisionScopes`.

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

Al definir Audiencias para las actividades de Target que se entregan mediante el SDK web de Adobe Experience Platform, [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es) debe definirse y utilizarse. Después de definir esquemas XDM, clases y grupos de campos de esquema, puede crear una regla de audiencia de Target definida por los datos XDM para la segmentación. En Target, los datos XDM se muestran en el Generador de audiencias como un parámetro personalizado. El XDM se serializa mediante notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene actividades de Target con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, no se entregan correctamente mediante el SDK. En lugar de usar parámetros personalizados o el perfil de usuario, debe utilizar XDM en su lugar. Sin embargo, hay campos de objetivo de audiencia integrados compatibles con el SDK web de Adobe Experience Platform que no requieren XDM. Estos campos están disponibles en la interfaz de usuario de Target y no requieren XDM:

* Biblioteca de segmentos
* Geografía 
* Red
* Operating System
* Páginas del sitio
* Explorador
* Fuentes de tráfico
* Lapso de tiempo

## Terminología

__Decisiones:__ en  [!DNL Target], las decisiones se correlacionan con la experiencia seleccionada en una actividad.

__Esquema:__ el esquema de una decisión es el tipo de oferta en  [!DNL Target].

__Ámbito de aplicación:__ el ámbito de aplicación de la decisión. En [!DNL Target], el ámbito es el mBox. El mBox global es el ámbito `__view__`.

__XDM:__ el XDM se serializa en notación de puntos y luego se coloca en  [!DNL Target] como parámetros mBox.
