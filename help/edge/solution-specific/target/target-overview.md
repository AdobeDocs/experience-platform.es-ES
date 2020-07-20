---
title: 'Adobe Target y el SDK web de Adobe Experience Platform. '
seo-title: SDK web de Adobe Experience Platform y uso de Adobe Target
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web Experience Platform mediante Adobe Target
seo-description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web Experience Platform mediante Adobe Target
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 3%

---


# [!DNL Target] Información general

El Adobe Experience Platform [!DNL Web SDK] puede ofrecer y procesar experiencias personalizadas administradas en Adobe Target con el canal web. Puede utilizar un editor WYSIWYG, denominado Compositor [de experiencias](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) visuales (VEC), o una interfaz no visual, el Compositor [de experiencias basadas en](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)formularios, para crear, activar y ofrecer sus actividades y experiencias de personalización.

## Habilitar Adobe Target

Para habilitar [!DNL Target], debe hacer lo siguiente:

1. Active los tokens de respuesta actividad.id y experience.id en la [!DNL Target] interfaz de usuario.

![destinatario_reponse_token](../../solution-specific/target/assets/target_response_token.png)

1. Habilite el destinatario en la configuración [de](../../fundamentals/edge-configuration.md) Edge con el código de cliente adecuado.
1. Añada la `renderDecisions` opción a sus eventos.

A continuación, opcionalmente, también puede:

* Añada `decisionScopes` a sus eventos para recuperar actividades específicas (útil para actividades creadas con el compositor basado en formularios).
* Añada el [fragmento](../../solution-specific/target/flicker-management.md) de ocultamiento previo para ocultar solo determinadas partes de la página.

## Uso del Adobe Target VEC

Con el SDK, puede utilizar el VEC normalmente con una excepción: necesita tener instalada y activa la extensión [auxiliar de VEC de](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) destinatario.

## Actividades de VEC de procesamiento automático

El SDK web de AEP tiene la capacidad de procesar automáticamente las experiencias definidas mediante el VEC de Adobe Target en la web para los usuarios. Para indicar al SDK web de AEP que procese automáticamente actividades VEC, envíe un evento con `renderDecisions = true`:

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

El Compositor de experiencias basadas en formularios es una interfaz no visual que resulta útil para configurar pruebas A/B, [!DNL Experience Targeting]Personalización automatizada y actividades de Recomendaciones con diferentes tipos de respuesta, como JSON, HTML, Image, etc. Según el tipo de respuesta o la decisión devuelta por Adobe Target, se puede ejecutar la lógica de negocio principal. Para recuperar las decisiones de las actividades del Compositor basado en formularios, envíe un evento con todos los &quot;temas de decisión&quot; para los que desee recuperar una decisión.

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

`decisionScopes` define las secciones, ubicaciones o partes de las páginas en las que desea representar una experiencia personalizada. Son `decisionScopes` personalizables y están definidas por el usuario. Para [!DNL Target] los clientes actuales, `decisionScopes` también se conocen como &quot;mboxes&quot;. En la [!DNL Target] interfaz de usuario, `decisionScopes` aparezca como &quot;ubicaciones&quot;.

## __Ámbito de vista__

AEP [!DNL Web SDK] proporciona una funcionalidad en la que puede recuperar acciones de VEC sin depender de AEP [!DNL Web SDK] para procesar las acciones de VEC. Envíe un evento con `__view__` la definición de `decisionScopes`.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Audiencias en XDM

Al definir Audiencias para las actividades de Destinatario que se enviarán mediante el SDK web de AEP, se debe definir y utilizar [XDM](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/home.html) . Después de definir esquemas, clases y mezclas XDM, puede crear una regla de audiencia de Destinatario definida por los datos XDM para la segmentación. En Destinatario, los datos XDM se muestran en el Generador de Audiencias como un parámetro personalizado. El XDM se serializa mediante notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene actividades de Destinatario con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, tenga en cuenta que no se enviarán correctamente a través del SDK web de AEP. En lugar de utilizar parámetros personalizados o el perfil del usuario, debe utilizar XDM en su lugar. Sin embargo, hay campos de objetivo de audiencia predeterminados que se admiten mediante el SDK web de AEP y que no requieren XDM. Estos son los campos disponibles en la interfaz de usuario de Destinatario que no requieren XDM:

* Biblioteca de segmentos
* Geografía 
* Red
* Operating System
* Páginas del sitio
* Browser
* Fuentes de tráfico
* Periodo de tiempo

## Terminología

__Decisiones__ : En [!DNL Target], se correlacionan con la experiencia seleccionada de una Actividad.

__Ámbito__ : el ámbito de aplicación de la decisión. En [!DNL Target], este es el mBox. El mbox global es el `__view__` ámbito.

__Esquema__ - El esquema de una decisión es el tipo de oferta en [!DNL Target].

__XDM__ : el XDM se serializa en notación de puntos y luego se coloca [!DNL Target] como parámetros de mBox.
