---
title: Referencia de prueba de presencia de etiquetas
description: Descubra cómo comprueba la función de auditor la presencia de etiquetas en Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 34%

---

# Referencia de prueba de presencia de etiquetas

Esta referencia proporciona más información sobre la función de auditor en las pruebas de presencia de etiquetas de Adobe Experience Platform Debugger.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Platform Debugger, consulte la [información general sobre la función del auditor](./overview.md).

Las pruebas de presencia de etiquetas evalúan si ciertas etiquetas existen en la página y si están en el lugar correcto en el código de la página.

| Prueba | Peso | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Presencia de código | 5 | La etiqueta de Advertising Cloud no está disponible en el DOM. | Implemente la etiqueta Advertising Cloud utilizando la variable [Extensión de etiqueta de Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Píxel de segmento implementado | 5 | Actualice los píxeles del segmento de Advertising Cloud con las nuevas etiquetas de solo imagen de Advertising Cloud. El uso de etiquetas de segmento AMO no soportadas puede causar la pérdida de datos. | Implemente el píxel del segmento de Advertising Cloud utilizando la variable [Extensión de etiqueta de Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics: cargado en DOM | 5 | No se ha detectado la etiqueta de Adobe Analytics. | Instale la última versión de Analytics. <br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |
| Launch: biblioteca cargada | 5 | A `global _satellite` no se ha encontrado el objeto en el DOM, lo que significa que la biblioteca de etiquetas no está instalada o no se puede ejecutar. | Compruebe que la biblioteca de etiquetas está implementada en la página y que no está bloqueada por las actividades de script posteriores. |
| Launch: no hay varios scripts incrustados | 5 | Los sitios de producción solo deben cargar un código incrustado por página. | Compruebe que solo se está cargando la biblioteca de producción en la página. |
| Launch: `pageBottom` la rellamada existe en `<body>` | 5 | El `_satellite.pageBottom()` no se ha encontrado la rellamada dentro de la variable `<body>` de la página. Esta prueba falla si la variable `pageBottom` llamada de no se encuentra en la página o si está en la `<head>` (o cualquier otra ubicación inesperada). Solo pasará si `pageBottom` se encuentra en algún lugar dentro de la variable `<body>` etiqueta. | Añada la secuencia de comandos en línea inmediatamente antes del cierre `</body>` para garantizar la correcta funcionalidad de las etiquetas.<br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch: `pageBottom` la llamada de retorno no debe existir cuando se implementa asincrónicamente | 5 | La variable `_satellite.pageBottom()` se ha encontrado una llamada de retorno en la página, cosa que no debería suceder cuando las etiquetas se implementan asincrónicamente. | Elimine el `_satellite.pageBottom()` para habilitar la funcionalidad correcta de las etiquetas. <br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Servicio de Experience Cloud ID: presencia de código | 5 | No se ha encontrado el código del servicio de Experience Cloud ID. Se recomienda usar ID de Experience Cloud (ECID) para garantizar que se obtiene el máximo valor de las soluciones de Experience Cloud y es fundamental para la administración de ID en todas las soluciones de Experience Cloud. | Instale la versión más reciente de ECID.<br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) |
| Servicio de Experience Cloud ID: presencia de cookies | 5 | La variable `AMCV_` no se ha encontrado la cookie. Debe crear una instancia de un objeto visitante desde el código`VisitorAPI.js` . | Si se trata de una implementación de etiquetas, compruebe que el ID de AdobeOrg se ha introducido correctamente en la herramienta ECID. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es) |
| Servicio de Experience Cloud ID: Valor de MID presente | 5 | No se ha encontrado el valor MID en la variable `AMCV_` cookie. | Vuelva a realizar la prueba para comprobar la latencia de la API de ECID. Si esta situación persiste, póngase en contacto con el Servicio de atención al cliente de Adobe. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target: presencia de código | 5 | Adobe Target debe definirse en el DOM. | Instale la última versión de Target (at.js). <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target: biblioteca cargada en `<head>` | 4 | La biblioteca de Target debe cargarse en la variable `<head>` etiqueta. | Compruebe que la biblioteca de Target se carga en la variable `<head>` etiqueta. <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
