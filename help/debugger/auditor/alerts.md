---
title: Referencia de prueba de alerta
description: Obtenga información sobre cómo la función auditor prueba las alertas en Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 37%

---

# Referencia de prueba de alerta

Esta referencia proporciona más información sobre cómo la función auditor de Adobe Experience Platform Debugger ejecuta pruebas de alerta.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Platform Debugger, consulte la [información general sobre auditor feature](./overview.md).

Las alertas muestran los problemas que deben tenerse en cuenta, aunque eso no afecta a la puntuación. Las siguientes son algunas prácticas recomendadas que, en algunos casos, no serán útiles para su aplicación.

| Prueba | Peso | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Se ha implementado la etiqueta de conversión correcta | 0 | Compruebe si se utiliza la etiqueta de conversión correcta.<br><br>**Advertencia**: El uso de etiquetas de conversión TubeMogul obsoletas puede causar la pérdida de datos. | Actualice los píxeles de conversión a las nuevas etiquetas de conversión solo de imagen de Advertising Cloud. Esto se puede lograr fácilmente con el [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Se ha utilizado la etiqueta JS correcta | 0 | Advertising Cloud debe utilizar las últimas etiquetas JavaScript. | Actualice el JavaScript de Advertising Cloud con la última versión. El uso de versiones de JavaScript no compatibles puede causar la pérdida de funcionalidad. Esto puede realizarse más fácilmente mediante el uso del [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: Etiqueta de solo imagen | 0 | El formato de píxel de imagen de Advertising Cloud debe tener uno de los siguientes formatos recomendados: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Actualice los píxeles de Advertising Cloud con las nuevas etiquetas de solo imagen de Advertising Cloud para garantizar que dispone de toda la funcionalidad de Advertising Cloud. Esto se puede lograr fácilmente con el [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud: píxeles de segmento: sincronización DSP habilitada | 0 | Compruebe si el píxel del segmento TubeMogul contiene un ajuste de sincronización de DSP y recomiende que el ajuste se añada al píxel. DSP La configuración de sincronización de datos se determina mediante el uso de un parámetro de cadena de consulta. Para resumir: <ul><li>SI la etiqueta se está activando en cualquiera de las siguientes ubicaciones:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>Y la etiqueta contiene el parámetro de URL `sid=`</li><li>ENTONCES, compruebe si el parámetro de URL `cs=0` o `cs=1` existe y, si no lo recomienda, `cs=1` se añadirán a esos píxeles para que mejoren las tasas de coincidencia de audiencia.</li></ul> | Añadir el parámetro de URL `cs=1` a los píxeles de Advertising Cloud DSP para que se pueda producir la sincronización de segmentos, lo que aumenta los índices de coincidencia de audiencia. Esto se puede lograr fácilmente con el [Extensión de etiqueta Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Servicio de Experience Cloud ID: utilice solo un AdobeOrg | 0 | En una implementación ECID normal, debe utilizarse un único AdobeOrg. | Verifique que existen varios ID de AdobeOrg para esta implementación. <br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Lanzamiento - `pageBottom` ubicación de devolución de llamada | 0 | El `_satellite.pageBottom()` La función debe estar presente para que las etiquetas funcionen. Añada la secuencia de comandos en línea inmediatamente antes de la `</body>` para garantizar la correcta funcionalidad de la DTM. Nota: Se recomienda que la etiqueta sea la última etiqueta en el `<body>`. Si se encuentra dentro de `<body>` tiene la posibilidad de funcionar, pero como no es una práctica recomendada, podría funcionar incorrectamente o dar resultados inesperados o no deseados. | Añada la secuencia de comandos en línea inmediatamente antes de la `</body>` para garantizar la correcta funcionalidad de la DTM. <br><br>[Más información](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch: Autoalojado | 0 | La biblioteca de etiquetas se aloja en la instancia de Adobe de Akamai en `assets.adobedtm.com`. El hosting propio es el método recomendado para cargar etiquetas, ya que permite un bueno control del rendimiento del sitio web mediante el control de caché, la reducción de las dependencias de scripts de terceros y un bueno control durante el proceso de publicación. Las bibliotecas de etiquetas se pueden alojar y administrar a través de su propio alojamiento web o CDN. | Cambiar a un alojamiento propio es un método para cargar etiquetas en una página. Aunque el alojamiento de a través de la CDN de Akamai generalmente funciona, el hosting propio mejora el rendimiento de la página. <br><br>Más información:<ul><li>[Guía de inicio rápido de etiquetas](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Implementación asíncrona](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch: Debe implementarse asincrónicamente | 0 | Las etiquetas deben implementarse asincrónicamente para obtener un rendimiento óptimo. | Incluya el `async` en el script en línea para garantizar la correcta funcionalidad de las etiquetas <br><br>[Información adicional](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target: contenido en `mboxDefault` | 0 | El contenido debe existir en `mboxDefault` al usar `at.js`. | Compruebe que el contenido está disponible. <br><br>[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
