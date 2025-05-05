---
title: Referencia de prueba de presencia de etiquetas
description: Descubra cómo la función auditor prueba la presencia de etiquetas en Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 17%

---

# Referencia de prueba de presencia de etiquetas

Esta referencia proporciona más información sobre cómo auditor comprueba la presencia de etiquetas en Adobe Experience Platform Debugger.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Experience Platform Debugger, consulte [descripción general de la función de auditor](./overview.md).

Las pruebas de presencia de etiquetas evalúan si existen determinadas etiquetas en la página y si están en el lugar correcto en el código de la página.

| Prueba | Grosor | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Presencia de código | 5 | La etiqueta de Advertising Cloud no está disponible en el DOM. | Implemente la etiqueta Advertising Cloud con la [extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Píxel de segmento implementado | 5 | Actualice los píxeles del segmento de Advertising Cloud con las nuevas etiquetas de solo imagen de Advertising Cloud. El uso de etiquetas de segmento AMO no soportadas puede causar la pérdida de datos. | Implemente el píxel del segmento de Advertising Cloud con la [extensión de etiqueta de Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics: cargado en DOM | 5 | No se ha detectado la etiqueta de Adobe Analytics. | Instale la última versión de Analytics. <br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |
| Launch: biblioteca cargada | 5 | No se encontró un objeto `global _satellite` en el DOM, lo que significa que la biblioteca de etiquetas no está instalada o no se puede ejecutar. | Compruebe que la biblioteca de etiquetas está implementada en la página y que no está bloqueada por las actividades de script posteriores. |
| Launch: no hay varios scripts incrustados | 5 | Los sitios de producción solo deben cargar un código incrustado por página. | Compruebe que solo se está cargando la biblioteca de producción en la página. |
| Launch: la llamada de retorno `pageBottom` existe en `<body>` | 5 | No se encontró la llamada de retorno `_satellite.pageBottom()` necesaria dentro del `<body>` de la página. Esta prueba falla si no se encuentra la llamada de `pageBottom` en la página o si está en la etiqueta `<head>` (o en otra ubicación inesperada). Solo funcionará correctamente si `pageBottom` se encuentra en algún lugar dentro de la etiqueta `<body>`. | Agregue el script en línea inmediatamente antes de la etiqueta de cierre `</body>` para garantizar la correcta funcionalidad de las etiquetas.<br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch: la llamada de retorno `pageBottom` no debe existir cuando se implementa asincrónicamente | 5 | La llamada de retorno `_satellite.pageBottom()` se ha encontrado en la página, cosa que no debería suceder cuando las etiquetas se implementan de forma asíncrona. | Elimine el script `_satellite.pageBottom()` para habilitar la correcta funcionalidad de las etiquetas. <br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Servicio de Experience Cloud ID: presencia de código | 5 | No se ha encontrado el código del servicio de Experience Cloud ID. El uso de Experience Cloud ID (ECID) es muy recomendable para garantizar que se obtiene el máximo valor de las soluciones de Experience Cloud y es fundamental para la administración de ID en todas las soluciones de Experience Cloud. | Instale la versión más reciente de ECID.<br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) |
| Servicio de Experience Cloud ID: presencia de cookies | 5 | No se encontró la cookie `AMCV_`. Debe crear una instancia de un objeto visitante a partir del código `VisitorAPI.js`. | Si se trata de una implementación de etiquetas, compruebe que el ID de AdobeOrg se ha introducido correctamente en la herramienta ECID. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es) |
| Servicio de Experience Cloud ID: Valor de MID presente | 5 | No se encontró el valor MID en la cookie `AMCV_`. | Vuelva a realizar la prueba para comprobar si hay latencia de API de ECID. Si la condición persiste, póngase en contacto con el Servicio de atención al cliente de Adobe. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es) |
| Target: presencia de código | 5 | Adobe Target debe definirse en el DOM. | Instale la última versión de Target (at.js). <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) |
| Target: biblioteca cargada en `<head>` | 4 | La biblioteca de Target debe cargarse en la etiqueta `<head>`. | Compruebe que la biblioteca de Target se carga en la etiqueta `<head>`. <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=es) |

{style="table-layout:auto"}
