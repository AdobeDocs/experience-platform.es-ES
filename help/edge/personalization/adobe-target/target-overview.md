---
title: Uso de Adobe Target con el SDK web de Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Experience Platform mediante Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;fragmento de ocultamiento previo;vec;Compositor de experiencias basadas en formularios;xdm;audiencias;decisiones;ámbito;esquema;diagrama del sistema;diagrama
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c99bc94226b296463e92340723d1318e0775f6a7
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 5%

---

# Uso de [!DNL Adobe Target] con el [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] puede entregar y procesar experiencias personalizadas administradas en  [!DNL Adobe Target] el canal web. Puede utilizar un editor WYSIWYG, denominado [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para crear, activar y ofrecer sus actividades y experiencias de personalización.

Las siguientes funciones se han probado y actualmente son compatibles con [!DNL Target]:

* [Pruebas A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Creación de informes de conversión e impresión de A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es)
* [Actividades de Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Pruebas multivariable (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Actividades de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Informes de impresión y conversión de Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Compatibilidad con VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] diagrama del sistema

El diagrama siguiente le ayuda a comprender el flujo de trabajo de las decisiones de borde [!DNL Target] y [!DNL Platform Web SDK].

![Diagrama de la toma de decisiones perimetrales de Adobe Target con el SDK web de Platform](./assets/target-platform-web-sdk.png)

| La llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga el [!DNL Platform Web SDK]. El [!DNL Platform Web SDK] envía una solicitud a la red perimetral con datos XDM, el ID de entorno de Datastreams, los parámetros transferidos y el ID de cliente (opcional). La página (o los contenedores) está oculta previamente. |
| 2 | La red perimetral envía la solicitud a los servicios Edge para enriquecerla con el ID del visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | La red perimetral envía la solicitud de personalización enriquecida al perímetro [!DNL Target] con el ID de visitante y los parámetros transferidos. |
| 4 | Los scripts de perfil se ejecutan y luego se alimentan en el almacenamiento de perfiles [!DNL Target]. El almacenamiento de perfiles obtiene segmentos de la [!UICONTROL Biblioteca de audiencias] (por ejemplo, segmentos compartidos desde [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | En función de los parámetros de solicitud de URL y los datos de perfil, [!DNL Target] determina qué actividades y experiencias se mostrarán para el visitante en la vista de página actual y para futuras vistas de recuperación previa. [!DNL Target] a continuación, lo devuelve a la red perimetral. |
| 6 | a. La red perimetral envía la respuesta de personalización a la página, incluyendo de forma opcional los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br>b. El contenido personalizado para las vistas que se muestran como resultado de las acciones del usuario en una aplicación de una sola página (SPA) se almacena en caché para que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. &#x200B;<br>c. La red perimetral envía el ID de visitante y otros valores en cookies, como consentimiento, ID de sesión, identidad, comprobación de cookies, personalización, etc. |
| 7 | La red perimetral reenvía los detalles de [!UICONTROL Analytics for Target] (A4T) (actividad, experiencia y metadatos de conversión) al &#x200B; perimetral [!DNL Analytics]. |

## Habilitación de [!DNL Adobe Target]

Para habilitar [!DNL Target], haga lo siguiente:

1. Habilite [!DNL Target] en su [conjunto de datos](../../fundamentals/datastreams.md) con el código de cliente apropiado.
1. Agregue la opción `renderDecisions` a los eventos.

A continuación, opcionalmente, también puede añadir las siguientes opciones:

* **`decisionScopes`**: Recupere actividades específicas (útil para actividades creadas con el compositor basado en formularios) añadiendo esta opción a los eventos.
* **[Ocultamiento previo del fragmento](../manage-flicker.md)**: Oculte solo ciertas partes de la página.

## Uso del VEC de Adobe Target

Para utilizar el VEC con una implementación [!DNL Platform Web SDK], instale y active la extensión [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Para obtener más información, consulte [Visual Experience Composer Helper extension](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) en la *Guía de Adobe Target*.

## Actividades de VEC de procesamiento automático

El [!DNL Adobe Experience Platform Web SDK] tiene el poder de procesar automáticamente las experiencias definidas mediante el VEC de [!DNL Adobe Target] en la web para los usuarios. Para indicar a [!DNL Experience Platform Web SDK] que procese automáticamente las actividades del VEC, envíe un evento con `renderDecisions = true`:

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

El [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) es una interfaz no visual que resulta útil para configurar [!UICONTROL Pruebas A/B], [!UICONTROL Segmentación de experiencias], [!UICONTROL Automated Personalization] y [!UICONTROL Recommendations] con diferentes tipos de respuestas, como JSON, HTML, Imagen, etc . Según el tipo de respuesta o la decisión devuelta por [!DNL Target], se puede ejecutar la lógica principal del negocio. Para recuperar decisiones para las actividades del Compositor basado en formularios, envíe un evento con todos los &quot;decisionScopes&quot; para los que desee recuperar una decisión.

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

`decisionScopes` defina secciones, ubicaciones o partes de las páginas en las que desea procesar una experiencia personalizada. Estos `decisionScopes` son personalizables y están definidos por el usuario. Para los clientes actuales de [!DNL Target] , `decisionScopes` también se conocen como &quot;mboxes&quot;. En la interfaz de usuario de [!DNL Target], `decisionScopes` aparece como &quot;ubicaciones&quot;.

## El ámbito `__view__`

El [!DNL Experience Platform Web SDK] proporciona funcionalidad para recuperar acciones del VEC sin depender del SDK para procesar las acciones del VEC por usted. Envíe un evento con `__view__` definido como `decisionScopes`.

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

Al definir audiencias para las actividades [!DNL Target] que se entregan mediante [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es) debe definirse y utilizarse. Después de definir esquemas XDM, clases y grupos de campos de esquema, puede crear una regla de audiencia [!DNL Target] definida por los datos XDM para la segmentación. Dentro de [!DNL Target], los datos XDM se muestran en el [!UICONTROL Audience Builder] como un parámetro personalizado. El XDM se serializa mediante notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene [!DNL Target] actividades con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, no se entregan correctamente mediante el SDK. En lugar de usar parámetros personalizados o el perfil de usuario, debe utilizar XDM en su lugar. Sin embargo, hay campos de objetivo de audiencia integrados compatibles con el [!DNL Platform Web SDK] que no requieren XDM. Estos campos están disponibles en la interfaz de usuario [!DNL Target] que no requieren XDM:

* Biblioteca de segmentos
* Geografía
* Red
* Operating System
* Páginas del sitio
* Explorador
* Fuentes de tráfico
* Lapso de tiempo

Para obtener más información, consulte [Categorías para audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) en la *Guía de Adobe Target*.

### Actualización de perfil único

El [!DNL Platform Web SDK] permite actualizar el perfil al perfil [!DNL Target] y al [!DNL Platform Web SDK] como evento de experiencia.

Para actualizar un perfil [!DNL Target], asegúrese de que los datos de perfil se pasan con lo siguiente:

* En `“data {“`
* En `“__adobe.target”`
* Prefijo `“profile.”`, por ejemplo, como se muestra a continuación

| Clave | Tipo | Descripción |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente de personalización si debe interpretar las acciones DOM |
| `decisionScopes` | Matriz `<String>` | Una lista de ámbitos para recuperar decisiones |
| `xdm` | Objeto | Datos formateados en XDM que llegan al SDK web de plataforma como evento de experiencia |
| `data` | Objeto | Pares de clave/valor arbitrarios enviados a soluciones [!DNL Target] en la clase de destino. |

El código [!DNL Platform Web SDK] típico que utiliza este comando tiene el siguiente aspecto:

**`sendEvent`con datos de perfil**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Envío de atributos de perfil a Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Solicitar recomendaciones

La siguiente tabla enumera los atributos [!DNL Recommendations] y si cada uno es compatible a través de [!DNL Platform Web SDK]:

| Categoría | Atributo | Estado de asistencia |
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
| Página o categoría de elemento para la afinidad de la categoría | user.categoryId | Admitido |

**Envío de atributos de Recommendations a Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Depuración

mboxTrace y mboxDebug ya no se utilizan. Utilice [[!DNL Platform Web SDK] depuración](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminología

__Decisiones:__ en  [!DNL Target], las decisiones se correlacionan con la experiencia seleccionada en una actividad.

__Esquema:__ el esquema de una decisión es el tipo de oferta en  [!DNL Target].

__Ámbito de aplicación:__ el ámbito de aplicación de la decisión. En [!DNL Target], el ámbito es el mBox. El mBox global es el ámbito `__view__`.

__XDM:__ el XDM se serializa en notación de puntos y luego se coloca en  [!DNL Target] como parámetros mBox.
