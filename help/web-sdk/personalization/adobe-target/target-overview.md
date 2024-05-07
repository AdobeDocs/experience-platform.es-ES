---
title: Uso de Adobe Target con SDK web para la personalización
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Experience Platform mediante Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 69406293dce5fdfc832adff801f1991626dafae0
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 4%

---

# Uso [!DNL Adobe Target] y [!DNL Web SDK] para personalización

[!DNL Adobe Experience Platform] [!DNL Web SDK] puede entregar y procesar experiencias personalizadas gestionadas en [!DNL Adobe Target] al canal web. Puede utilizar un editor WYSIWYG, llamado [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), o una interfaz no visual, la variable [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para crear, activar y ofrecer sus actividades y experiencias de personalización.

>[!IMPORTANT]
>
>Obtenga información sobre cómo migrar la implementación de Target al SDK web de Platform con [Migración de Target de at.js 2.x al SDK web de Platform](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=es) tutorial.
>
>Obtenga información sobre cómo implementar Target por primera vez con [Implementar Adobe Experience Cloud con SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) tutorial. Para obtener información específica de Target, consulte la sección del tutorial titulada [Configuración de Target con el SDK web de Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Las siguientes funciones se han probado y actualmente son compatibles con [!DNL Target]:

* [Pruebas A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Informes de impresión y conversión de A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es)
* [Actividades de Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Pruebas multivariable (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Actividades de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=es)
* [Informes de conversión e impresión de Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Compatibilidad con VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] diagrama del sistema

El diagrama siguiente le ayuda a comprender el flujo de trabajo de [!DNL Target] y [!DNL Web SDK] edge decisioning.

![Diagrama de Adobe Target Edge Decisioning con el SDK web de Platform](assets/target-platform-web-sdk-new.png)

| La llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga el [!DNL Web SDK]. El [!DNL Web SDK] envía una solicitud al Edge Network con datos XDM, el ID de entorno de flujos de datos, los parámetros transferidos y el ID de cliente (opcional). La página (o los contenedores) está oculta previamente. |
| 2 | El Edge Network envía la solicitud a los servicios Edge para enriquecerla con el ID del visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | El Edge Network envía la solicitud de personalización enriquecida a [!DNL Target] Edge con el ID de visitante y los parámetros proporcionados. |
| 4 | Se ejecutan los scripts de perfil y se incluyen en [!DNL Target] almacenamiento de perfiles. El almacenamiento de perfiles recupera segmentos del [!UICONTROL Biblioteca de audiencias] (por ejemplo, segmentos compartidos desde [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], el [!DNL Adobe Experience Platform]). |
| 5 | En función de los parámetros de solicitud de URL y los datos de perfil, [!DNL Target] determina qué actividades y experiencias se mostrarán al visitante en la vista de página actual y en futuras vistas previamente recuperadas. [!DNL Target] a continuación, lo devuelve al Edge Network. |
| 6 | a. El Edge Network devuelve la respuesta de personalización a la página, incluyendo, de forma opcional, los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br>SPA b. El contenido personalizado para vistas que se muestran como resultado de acciones del usuario en una aplicación de una sola página () se almacena en caché para que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. <br>c. El Edge Network envía el ID de visitante y otros valores en cookies, como el consentimiento, el ID de sesión, la identidad, la comprobación de cookies y la personalización. |
| 7 | El SDK web envía la notificación del dispositivo al Edge Network. |
| 8 | El Edge Network reenvía [!UICONTROL Analytics for Target] (A4T) detalla (actividad, experiencia y metadatos de conversión) en [!DNL Analytics] edge. |

## Habilitando [!DNL Adobe Target]

Para habilitar [!DNL Target], haga lo siguiente:

1. Activar [!DNL Target] en su [secuencia de datos](../../../datastreams/overview.md) con el código de cliente adecuado.
1. Añada el `renderDecisions` a sus eventos.

A continuación, de forma opcional, también puede añadir las siguientes opciones:

* **`decisionScopes`**: Recupere actividades específicas (útiles para actividades creadas con el compositor basado en formularios) añadiendo esta opción a los eventos.
* **[Preocultando fragmento](../manage-flicker.md)**: oculta solo ciertas partes de la página.

## Uso del VEC de Adobe Target

Para utilizar el VEC con un [!DNL Web SDK] implementación, instale y active el [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extensión de VEC Helper.

Para obtener más información, consulte [Extensión de ayuda del Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) en el *Guía de Adobe Target*.

## Representación de contenido personalizado

Consulte [Representación de contenido de personalización](../rendering-personalization-content.md) para obtener más información.

## Audiencias en XDM

Al definir audiencias para su [!DNL Target] actividades que se entregan a través de [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es) debe definirse y utilizarse. Después de definir esquemas XDM, clases y grupos de campos de esquema, puede crear un [!DNL Target] regla de audiencia definida por los datos XDM para la segmentación. En [!DNL Target], los datos XDM se muestran en [!UICONTROL Generador de audiencias] como parámetro personalizado. El XDM se serializa con notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene [!DNL Target] actividades con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, no se entregan correctamente a través del SDK. En lugar de utilizar parámetros personalizados o el perfil de usuario, debe utilizar XDM. Sin embargo, hay campos de segmentación de audiencia listos para usar compatibles con el [!DNL Web SDK] que no requieren XDM. Estos campos están disponibles en la variable [!DNL Target] IU que no requieren XDM:

* Biblioteca de segmentos
* Geografía
* Red
* Sistema operativo
* Páginas del sitio
* Explorador
* Fuentes de tráfico
* Lapso de tiempo

Para obtener más información, consulte [Categorías para audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) en el *Guía de Adobe Target*.

### Tokens de respuesta

Los tokens de respuesta se utilizan para enviar metadatos a terceros, como Google o Facebook. Los tokens de respuesta se devuelven en `meta` campo dentro de `propositions` -> `items`. Este es un ejemplo:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Para recopilar los tokens de respuesta de, debe suscribirse a `alloy.sendEvent` prometer, iterar `propositions`y extraiga los detalles de `items` -> `meta`.

Cada `proposition` tiene un `renderAttempted` campo booleano que indica si la variable `proposition` se ha procesado o no. Consulte el siguiente ejemplo:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Cuando se habilita la representación automática, la matriz de propuestas contiene:

#### Al cargar la página:

* Basado en Compositor basado en formularios `propositions` con `renderAttempted` indicador establecido en `false`
* Propuestas basadas en el Compositor de experiencias visuales con `renderAttempted` indicador establecido en `true`
* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con `renderAttempted` indicador establecido en `true`

#### Al ver - cambiar (para vistas en caché):

* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con `renderAttempted` indicador establecido en `true`

Cuando la representación automática está desactivada, la matriz de propuestas contiene:

#### Al cargar la página:

* [!DNL Form-based Composer]basado en `propositions` con `renderAttempted` indicador establecido en `false`
* [!DNL Visual Experience Composer]propuestas basadas en con `renderAttempted` indicador establecido en `false`
* [!DNL Visual Experience Composer]Propuestas basadas en para una vista de aplicación de una sola página con `renderAttempted` indicador establecido en `false`

#### Al ver - cambiar (para vistas en caché):

* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con `renderAttempted` indicador establecido en `false`

### Actualización de perfil único

El [!DNL Web SDK] permite actualizar el perfil a [!DNL Target] y a la [!DNL Web SDK] como un evento de experiencia.

Para actualizar una [!DNL Target] , asegúrese de que los datos de perfil se pasan con lo siguiente:

* En `"data {"`
* En `"__adobe.target"`
* Prefijo `"profile."`

| Clave | Tipo | Descripción |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente de personalización si debe interpretar las acciones del DOM |
| `decisionScopes` | Matriz `<String>` | Una lista de ámbitos para los que recuperar decisiones |
| `xdm` | Objeto | Datos con formato XDM que aterrizan en el SDK web como un evento de experiencia |
| `data` | Objeto | Pares arbitrarios de clave/valor enviados a [!DNL Target] soluciones en la clase de destino. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Retraso al guardar los parámetros de perfil o entidad hasta que se muestre contenido al usuario final**

Para retrasar el registro de atributos en el perfil hasta que se haya mostrado el contenido, establezca `data.adobe.target._save=false` en su solicitud.

Por ejemplo: su sitio web contiene tres ámbitos de decisión que corresponden a tres vínculos de categoría en el sitio web (hombres, mujeres y niños) y desea rastrear la categoría que visitó finalmente el usuario. Envíe estas solicitudes con el `__save` indicador establecido en `false` para evitar que la categoría persista en el momento en que se solicita el contenido. Una vez visualizado el contenido, envíe la carga útil adecuada (incluido el `eventToken` y `stateToken`) para que se registren los atributos correspondientes.

<!--Save profile or entity attributes by default with:

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "__save" : true // Optional. __save=true is the default 
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt",
        "entity.id" : "1234",
      }
    }
  }
} ) ; 
```
-->

El ejemplo siguiente envía un mensaje de estilo trackEvent, ejecuta scripts de perfil, guarda atributos y registra inmediatamente el evento.

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt" ,
        "entity.id" : "1234" ,
        "track": {
          "scopes": [ "mbox1", "mbox2"],
          "type": "display|click|..."
        }
      }
    }
  }
} ) ;
```

>[!NOTE]
>
>Si la variable `__save` se omite, el guardado de los atributos profile y entity se produce inmediatamente, como si la solicitud se hubiera ejecutado, aunque el resto de la solicitud sea una recuperación previa de personalización. El `__save` solo es relevante para los atributos de perfil y entidad. Si el objeto track está presente, la variable `__save` se ignora la directiva. Los datos se guardan inmediatamente y se registra la notificación.

**`sendEvent`con datos de perfil**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Cómo enviar atributos de perfil a Adobe Target:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Solicitar recomendaciones

La siguiente tabla enumera [!DNL Recommendations] y si cada uno de ellos es compatible mediante los atributos [!DNL Web SDK]:

| Categoría | Atributo | Estado de soporte |
| --- | --- | --- |
| Recommendations: atributos de entidad predeterminados | entity.id | Admitido |
|  | entity.name | Admitido |
|  | entity.categoryId | Admitido |
|  | entity.pageUrl | Admitido |
|  | entity.thumbnailUrl | Admitido |
|  | entity.message | Admitido |
|  | entity.value | Admitido |
|  | entity.inventory | Admitido |
|  | entity.brand | Admitido |
|  | entity.margin | Admitido |
|  | entity.event.detailsOnly | Admitido |
| Recommendations: atributos de entidad personalizados | entity.yourCustomAttributeName | Admitido |
| Recommendations: parámetros de mbox/página reservados | Excludedids | Admitido |
|  | cartIds | Admitido |
|  | productPurchasedId | Admitido |
| Categoría de página o elemento para la afinidad de la categoría | user.categoryId | Admitido |

**Envío de atributos de Recommendations a Adobe Target:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Depuración

mboxTrace y mboxDebug han quedado obsoletos. Utilice un método de [Depuración del SDK web](/help/web-sdk/use-cases/debugging.md) en su lugar.

## Terminología

__Propuestas:__ Entrada [!DNL Adobe Target], las propuestas se correlacionan con la experiencia seleccionada de una actividad.

__Esquema:__ El esquema de una decisión es el tipo de oferta de [!DNL Adobe Target].

__Ámbito:__ Ámbito de la decisión. Entrada [!DNL Adobe Target], el ámbito es mBox. El mBox global es el `__view__` ámbito.

__XDM:__ El XDM se serializa en notación de puntos y luego se coloca en [!DNL Adobe Target] como parámetros mBox.
