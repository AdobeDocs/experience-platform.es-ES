---
title: Ajustes de configuración de Personalization
description: Configure las opciones de personalización en la extensión de etiquetas Web SDK.
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Ajustes de configuración de Personalization

Esta sección de configuración le permite determinar cómo desea ocultar determinadas partes de la página mientras se carga el contenido personalizado. Cuando se configura correctamente, estos ajustes garantizan que los visitantes vean el contenido personalizado adecuado.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Personalization]**.

![Imagen que muestra la configuración de personalización de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/web-sdk-ext-personalization.png)

Las opciones disponibles son las siguientes:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Utilice esta opción para permitir que Web SDK lea y escriba las cookies heredadas `mbox` y `mboxEdgeCluster` que utilizan las bibliotecas `at.js` 1.x o 2.x. Esta configuración ayuda a mantener intactos los perfiles de los visitantes al moverlos entre páginas mediante Web SDK o `at.js` en el mismo sitio web. Si no tiene `at.js` implementado en ninguna parte del sitio, no necesita habilitar esta casilla de verificación. La biblioteca JavaScript equivalente a esta casilla es [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

Al habilitar esta opción, asegúrese de habilitar también [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) en `targetGlobalSettings()`.

## [!UICONTROL Prehiding style] {#prehiding-style}

El editor de estilos preocultado permite definir reglas CSS personalizadas para ocultar secciones específicas de una página. Cuando se carga la página, Web SDK utiliza este estilo para ocultar las secciones que deben personalizarse, recupera la personalización y, a continuación, muestra las secciones de página personalizadas. Este flujo de trabajo permite a los visitantes ver contenido personalizado sin ver cómo se carga o parpadea el proceso de recuperación de la personalización. El equivalente de la biblioteca JavaScript para este editor de código es [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Esta sección no es una configuración directa, sino una ubicación práctica para obtener código de implementación. Implemente este fragmento preocultado dentro de la etiqueta `<head>` en su sitio para ocultar el contenido deseado mientras se carga la biblioteca de Web SDK.

>[!IMPORTANT]
>
>Al utilizar el fragmento preocultado, Adobe recomienda utilizar la misma regla CSS entre el fragmento preocultado y el estilo preocultado.

## [!UICONTROL Enable personalization storage]

Casilla de verificación que permite a Web SDK almacenar eventos de personalización. en el almacenamiento local del explorador. Resulta útil cuando desea realizar un seguimiento de las experiencias que el visitante ha visto en las cargas de página.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Menú desplegable que determina cuándo Web SDK recopila automáticamente los clics en el contenido devuelto desde Adobe Journey Optimizer.

* **[!UICONTROL Always]**: recopile todas las interacciones con propuestas.
* **[!UICONTROL Decorated elements only]**: recopilar solamente interacciones en elementos con `data-aep-click-label` o `data-aep-click-token` atributos de HTML.
* **[!UICONTROL Never]**: no recopile interacciones con propuestas.

La biblioteca JavaScript equivalente a este menú desplegable es [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Su valor predeterminado es [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

Menú desplegable que determina cuándo Web SDK recopila automáticamente los clics en el contenido devuelto desde Adobe Target.

* **[!UICONTROL Always]**: recopile todas las interacciones con propuestas.
* **[!UICONTROL Decorated elements only]**: recopilar solamente interacciones en elementos con `data-aep-click-label` o `data-aep-click-token` atributos de HTML.
* **[!UICONTROL Never]**: no recopile interacciones con propuestas.

La biblioteca JavaScript equivalente a este menú desplegable es [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Su valor predeterminado es [!UICONTROL Never].
