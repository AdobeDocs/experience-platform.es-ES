---
title: Referencia de prueba de alerta
description: Descubra cómo la función auditor prueba las alertas en Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 12%

---

# Referencia de prueba de alerta

Esta referencia proporciona más información sobre cómo la función auditor de Adobe Experience Platform Debugger ejecuta pruebas de .

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Platform Debugger, consulte [descripción general de la función de auditor](./overview.md).

Las alertas muestran los problemas que deben tenerse en cuenta, aunque eso no afecta a la puntuación. Las siguientes son algunas prácticas recomendadas que, en algunos casos, no serán útiles para su aplicación.

| Prueba | Grosor | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Se ha implementado la etiqueta de conversión correcta | 0 | Compruebe si se utiliza la etiqueta de conversión correcta.<br><br>**Advertencia**: El uso de etiquetas de conversión TubeMogul obsoletas puede causar la pérdida de datos. | Actualice los píxeles de conversión con las nuevas etiquetas de conversión solo de imagen de Advertising Cloud. Esto se puede lograr fácilmente con la [extensión de etiquetas Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Etiqueta JS correcta utilizada | 0 | Advertising Cloud debe utilizar las últimas etiquetas de JavaScript. | Actualice el JavaScript de Advertising Cloud con la última versión. El uso de versiones de JavaScript obsoletas puede causar la pérdida de funcionalidad. Esto se puede lograr más fácilmente mediante la [extensión de etiquetas Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: etiqueta de solo imagen | 0 | El formato de píxel de imagen de Advertising Cloud debe tener uno de los siguientes formatos recomendados: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Actualice los píxeles de Advertising Cloud con las nuevas etiquetas de solo imagen de Advertising Cloud para garantizar que dispone de toda la funcionalidad de Advertising Cloud. Esto se puede lograr fácilmente con la [extensión de etiquetas Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud DSP - Píxeles de segmento sincronización habilitada | 0 | DSP Compruebe si el píxel del segmento TubeMogul contiene un ajuste de sincronización de segmentos y recomiende que el ajuste se añada al píxel. DSP La configuración de sincronización de datos se determina mediante el uso de un parámetro de cadena de consulta. Para resumir: <ul><li>SI la etiqueta se está activando en cualquiera de las siguientes ubicaciones:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>Y la etiqueta contiene el parámetro de URL `sid=`</li><li>ENTONCES, compruebe si existe el parámetro de dirección URL `cs=0` o `cs=1` y, en caso contrario, recomiende que `cs=1` se agregue a esos píxeles para que mejoren las tasas de coincidencia de audiencia.</li></ul> | Agregue el parámetro de dirección URL `cs=1` a los píxeles de Advertising Cloud DSP para que se produzca la sincronización de audiencias, lo que aumenta las tasas de coincidencia de audiencia. Esto se puede lograr fácilmente con la [extensión de etiquetas Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Servicio de ID de Experience Cloud: utilice solo un AdobeOrg | 0 | En una implementación ECID normal, debe utilizarse un único AdobeOrg. | Compruebe que existen varios ID de AdobeOrg para esta implementación. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch: ubicación de devolución de llamada `pageBottom` | 0 | La función `_satellite.pageBottom()` debe estar presente para que funcionen las etiquetas. Agregue el script en línea inmediatamente antes de la etiqueta de cierre `</body>` para garantizar la correcta funcionalidad de la DTM. Nota: Se recomienda que la etiqueta sea la última etiqueta en el `<body>`. Si se encuentra dentro de la etiqueta `<body>`, puede funcionar, pero como no es una práctica recomendada, podría funcionar incorrectamente o dar resultados inesperados o no deseados. | Agregue el script en línea inmediatamente antes de la etiqueta de cierre `</body>` para garantizar la correcta funcionalidad de la DTM. <br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch: autoalojado | 0 | La biblioteca de Adobes se aloja en la instancia de Akamai en `assets.adobedtm.com`. El hosting propio es el método recomendado para cargar etiquetas, ya que ofrece un mayor control del rendimiento del sitio web mediante el control de caché, la reducción de las dependencias de scripts de terceros y un mayor control durante el proceso de publicación. Las bibliotecas de etiquetas se pueden alojar y administrar a través de su propio alojamiento web o CDN. | Cambiar a un alojamiento propio es un método para cargar etiquetas en una página. Aunque el alojamiento a través de la CDN de Akamai funciona en la mayoría de los casos, el alojamiento propio mejora el rendimiento de la página. <br><br>Información adicional:<ul><li>[Guía de inicio rápido de etiquetas](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Implementación asíncrona](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch: Debe implementarse asincrónicamente | 0 | Las etiquetas deben implementarse asincrónicamente para obtener un rendimiento óptimo. | Incluya el parámetro `async` en el script en línea para garantizar la correcta funcionalidad de las etiquetas <br><br>[Información adicional](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target: contenido en `mboxDefault` | 0 | El contenido debe estar presente en `mboxDefault` al usar `at.js`. | Compruebe que el contenido está disponible. <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
