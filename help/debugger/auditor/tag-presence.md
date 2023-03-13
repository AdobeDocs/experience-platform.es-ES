---
title: Referencia de prueba de presencia de etiquetas
description: Descubra cómo la función auditor prueba la presencia de etiquetas en Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 34%

---

# Referencia de prueba de presencia de etiquetas

Esta referencia proporciona más información sobre cómo el auditor de Adobe Experience Platform Debugger comprueba la presencia de etiquetas.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Platform Debugger, consulte la [información general sobre auditor feature](./overview.md).

Las pruebas de presencia de etiquetas evalúan si existen determinadas etiquetas en la página y si están en el lugar correcto en el código de la página.

| Prueba | Peso | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Presencia de código | 5 | La etiqueta de Advertising Cloud no está disponible en el DOM. | Implemente la etiqueta Advertising Cloud con la variable [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Píxel de segmento implementado | 5 | Actualice los píxeles del segmento de Advertising Cloud con las nuevas etiquetas de solo imagen de Advertising Cloud. El uso de etiquetas de segmento AMO no soportadas puede causar la pérdida de datos. | Implemente el píxel del segmento de Advertising Cloud con la variable [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics: cargado en DOM | 5 | No se ha detectado la etiqueta de Adobe Analytics. | Instale la última versión de Analytics. <br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |
| Launch: biblioteca cargada | 5 | A `global _satellite` no se ha encontrado el objeto en el DOM, lo que significa que la biblioteca de etiquetas no está instalada o no se puede ejecutar. | Compruebe que la biblioteca de etiquetas está implementada en la página y que no está bloqueada por las actividades de script posteriores. |
| Launch: no hay varios scripts incrustados | 5 | Los sitios de producción solo deben cargar un código incrustado por página. | Compruebe que solo se está cargando la biblioteca de producción en la página. |
| Lanzamiento - `pageBottom` la devolución de llamada existe en `<body>` | 5 | El requerido `_satellite.pageBottom()` no se ha encontrado la devolución de llamada dentro de `<body>` de la página. Esta prueba falla si `pageBottom` La llamada de no se encuentra en la página o si está en el `<head>` (u otra ubicación inesperada). Solo funcionará correctamente si `pageBottom` se encuentra en algún lugar dentro de `<body>` etiqueta. | Añada la secuencia de comandos en línea inmediatamente antes de la `</body>` para garantizar la correcta funcionalidad de las etiquetas.<br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Lanzamiento - `pageBottom` la devolución de llamada no debe existir cuando se implementa asincrónicamente | 5 | El `_satellite.pageBottom()` la llamada de retorno se ha encontrado en la página, cosa que no debería suceder cuando las etiquetas se implementan de forma asíncrona. | Retire el `_satellite.pageBottom()` para habilitar la correcta funcionalidad de las etiquetas. <br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Servicio de Experience Cloud ID: presencia de código | 5 | No se ha encontrado el código del servicio de Experience Cloud ID. Se recomienda encarecidamente el uso de ID de Experience Cloud (ECID) para garantizar que se obtiene el máximo valor de las soluciones de Experience Cloud, y es fundamental para la administración de ID en todas las soluciones de Experience Cloud. | Instale la versión más reciente de ECID.<br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) |
| Servicio de Experience Cloud ID: presencia de cookies | 5 | El `AMCV_` no se ha encontrado la cookie. Debe crear una instancia de un objeto visitante desde el código`VisitorAPI.js` . | Si se trata de una implementación de etiquetas, compruebe que el ID de AdobeOrg se ha introducido correctamente en la herramienta ECID. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es) |
| Servicio de Experience Cloud ID: Valor de MID presente | 5 | No se ha encontrado el valor MID en `AMCV_` cookie. | Vuelva a realizar la prueba para comprobar si hay latencia de API de ECID. Si esta situación persiste, póngase en contacto con el Servicio de atención al cliente de Adobe. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es) |
| Target: presencia de código | 5 | Adobe Target debe definirse en el DOM. | Instale la última versión de Target (at.js). <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target: biblioteca cargada en `<head>` | 4 | La biblioteca de Target debe cargarse en `<head>` etiqueta. | Compruebe que la biblioteca de Target se carga en la `<head>` etiqueta. <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
