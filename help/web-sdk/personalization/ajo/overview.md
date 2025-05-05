---
title: Uso de Adobe Journey Optimizer con Experience Platform Web SDK
description: Obtenga información sobre cómo procesar contenido personalizado con Experience Platform Web SDK mediante Adobe Journey Optimizer
keywords: ajo;ajo web;adobe recorrido optimizer;renderDecisions;superficies;decisiones;propuestas;ámbito;esquema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Usando [!DNL Adobe Journey Optimizer] con [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] puede entregar y procesar experiencias personalizadas administradas en [!DNL Adobe Journey Optimizer] al canal web. Puede usar un editor de WYSIWYG, [!DNL Adobe Journey Optimizer] [Canal web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=es), o una interfaz no visual, [Canal de experiencia basado en código](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/code-based-experience/get-started-code-based) para crear, activar y entregar sus campañas y experiencias de personalización de [!DNL Journey Optimizer Web].

>[!IMPORTANT]
>
>Lea la [Documentación del canal web de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=es) para obtener información sobre cómo empezar a crear y generar informes con [!DNL Journey Optimizer Web] experiencias.

## Terminología {#terminology}

**[!UICONTROL Superficie]**: Una superficie web es una página web o ubicación en una página identificada por un URI donde se enviará el contenido de experiencia [!DNL Adobe Journey Optimizer].

**[!UICONTROL Propuestas]**: en [!DNL Adobe Journey Optimizer], las propuestas se correlacionan con la experiencia seleccionada de entre [!DNL Journey Optimizer Campaign].

## Habilitando [!DNL Adobe Journey Optimizer] {#enable-ajo}

Para empezar a usar [!DNL Adobe Journey Optimizer], siga los pasos a continuación.

1. Consulte los [requisitos previos](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=es#prerequesites) de la [!DNL Adobe Journey Optimizer] [Guía de experiencias web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=es), en concreto:
   * Configuró [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Habilite [!DNL Adobe Journey Optimizer] en su [secuencia de datos](../../../datastreams/overview.md).
   * Habilite la opción [!UICONTROL Política de combinación activa en Edge].

2. Agregue la opción `renderDecisions` a los eventos. Establezca `renderDecisions` en `true` para el procesamiento automático de las propuestas de contenido de Journey Optimizer enviadas en las superficies de página web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Si lo desea, puede especificar superficies adicionales en los eventos. De forma predeterminada, Web SDK genera automáticamente la superficie web para la página web actual y la incluye en la solicitud a Edge Network. Si es necesario, se pueden incluir superficies adicionales en la solicitud especificándolas en la opción `personalization.surfaces` del comando `sendEvent` o en la configuración **[!UICONTROL Superficies]** [[!UICONTROL Enviar evento] acción](../../../tags/extensions/client/web-sdk/action-types.md#send-event) correspondiente de la extensión de Web SDK.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Las superficies de evento se incluyen en el campo de solicitud `query.personalization.surfaces`:

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

4. Al igual que otras características de personalización, puede agregar un **[fragmento preocultado](../manage-flicker.md)** para ocultar solo ciertas partes de la página al recuperar experiencias.

## Creación de experiencias web de Adobe Journey Optimizer {#create-ajo-web-experiences}

Siga las instrucciones de [creación de campañas web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=es#create-web-campaign) de la [!DNL Adobe Journey Optimizer] [Guía de experiencias web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=es) para crear [!DNL Journey Optimizer Web] campañas y experiencias.

## Representación de contenido personalizado {#rendering-personalized-content}

Consulte la documentación sobre [procesamiento de contenido personalizado](../rendering-personalization-content.md) para obtener más información.

Las propuestas de Adobe Journey Optimizer para superficies web se procesan de manera similar a las propuestas de ámbito de decisión `__view__`. Específicamente, cuando la opción `renderDecisions` se establece en `true` en el comando `sendEvent`, Web SDK la procesará automáticamente.

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

Para depurar las implementaciones de personalización de Adobe Journey Optimizer, use [Depuración de Web SDK](/help/web-sdk/use-cases/debugging.md). Hay disponibles [!DNL Adobe Journey Optimizer] seguimientos de depuración al solucionar problemas con [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Buscar eventos con el prefijo `AJO:`.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
