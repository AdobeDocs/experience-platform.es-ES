---
title: Uso de Adobe Journey Optimizer con el SDK web de Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Experience Platform mediante Adobe Journey Optimizer
keywords: ajo;ajo web;adobe recorrido optimizer;renderDecisions;superficies;decisiones;propuestas;ámbito;esquema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Uso de [!DNL Adobe Journey Optimizer] con el [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] puede entregar y procesar experiencias personalizadas gestionadas en [!DNL Adobe Journey Optimizer] al canal web. Puede utilizar un editor WYSIWYG, [!DNL Adobe Journey Optimizer] [IU de Campaña web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), para crear, activar y enviar su [!DNL Journey Optimizer Web] campañas y experiencias de personalización.

>[!IMPORTANT]
>
>Lea el [Documentación del canal web de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) para obtener información sobre cómo empezar a usar [!DNL Journey Optimizer Web] creación de experiencias e informes.

## Terminología {#terminology}

**[!UICONTROL Superficie]**: una superficie web es una propiedad web identificada por una dirección URL donde la variable [!DNL Adobe Journey Optimizer] se enviará el contenido de la experiencia.

**[!UICONTROL Propuestas]**: en [!DNL Adobe Journey Optimizer], las propuestas se correlacionan con la experiencia seleccionada de una [!DNL Journey Optimizer Campaign].

## Habilitando [!DNL Adobe Journey Optimizer] {#enable-ajo}

Para empezar a utilizar [!DNL Adobe Journey Optimizer], siga los pasos a continuación.

1. Consulte la sección [requisitos previos](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) desde el [!DNL Adobe Journey Optimizer] [Guía de experiencias web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), específicamente:
   * Configuración de [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Activar [!DNL Adobe Journey Optimizer] en su [secuencia de datos](../../datastreams/overview.md).
   * Habilite la [!UICONTROL Política de combinación activa en Edge] opción.

2. Añada el `renderDecisions` a sus eventos. Establecer `renderDecisions` hasta `true` para el procesamiento automático de propuestas de contenido de Journey Optimizer enviadas en las superficies de página web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Si lo desea, puede especificar superficies adicionales en los eventos. De forma predeterminada, el SDK web generará automáticamente la superficie web para la página web actual e la incluirá en la solicitud a la red perimetral. Si es necesario, se pueden incluir superficies adicionales en la solicitud especificándolas en el `personalization.surfaces` de la opción `sendEvent` o en el comando correspondiente **[!UICONTROL Superficies]** [[!UICONTROL Enviar evento] acción](../../../tags/extensions/client/web-sdk/action-types.md#send-event) configuración de la extensión del SDK web.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Las superficies de evento se incluyen en `query.personalization.surfaces` campo de solicitud:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Al igual que otras funciones de personalización, puede añadir una **[preocultar fragmento](../manage-flicker.md)** para ocultar solo ciertas partes de la página al recuperar experiencias.

## Creación de experiencias web de Adobe Journey Optimizer {#create-ajo-web-experiences}

Siga las [creación de campañas web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instrucciones de la [!DNL Adobe Journey Optimizer] [Guía de experiencias web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) para crear [!DNL Journey Optimizer Web] campañas y experiencias.

## Representación de contenido personalizado {#rendering-personalized-content}

Consulte la documentación sobre [representación de contenido de personalización](../rendering-personalization-content.md) para obtener más información.

Las propuestas de Adobe Journey Optimizer para superficies web se procesan de forma similar a la `__view__` propuestas del ámbito de decisión. En concreto, cuando `renderDecisions` se establece en `true` en el `sendEvent` comando: el SDK web las procesará automáticamente.

Ejemplo de propuesta de contenido de Journey Optimizer:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Depuración {#debugging}

Para depurar las implementaciones de personalización de Adobe Journey Optimizer, utilice [[!DNL Web SDK] depuración](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] los seguimientos de depuración están disponibles cuando se soluciona el problema utilizando [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Compruebe los eventos con `AJO:` prefijo.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
