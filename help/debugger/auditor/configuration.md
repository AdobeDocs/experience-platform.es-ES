---
title: Referencia de prueba de configuración
description: Descubra cómo Auditor comprueba las características de las configuraciones en Adobe Experience Platform Debugger.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 50%

---

# Referencia de prueba de configuración

Esta referencia proporciona más información sobre cómo la función auditor de Adobe Experience Platform Debugger ejecuta las pruebas de configuración.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Experience Platform Debugger, consulte [descripción general de la función de auditor](./overview.md).

Las pruebas de configuración analizan la configuración, los valores o los posibles conflictos específicos de la implementación. Experience Platform Auditor evalúa las etiquetas comparándolas con otras normas y prácticas recomendadas.

| Prueba | Grosor | Criterios | Recomendación |
| --- | --- | --- | --- |
| Advertising Cloud: Los nombres de conversión solo utilizan caracteres alfanuméricos | 3 | El parámetro `ev_conversion_property_name` solo debe contener valores numéricos y decimales, EXCEPTO el parámetro `ev_transid`, que puede contener valores numéricos o de texto. Busque `everesttech.net` píxeles que contengan un parámetro de dirección URL que comience por `ev_`. | Compruebe que los parámetros de la propiedad de transacción solo contienen valores numéricos y decimales.<br><br>Advertencia: Cualquier otro tipo de valor puede causar pérdida de datos. |
| Advertising Cloud: Los nombres de conversión utilizan caracteres seguros para URL | 3 | Los nombres de propiedades de conversión no deben contener un signo &amp; o un signo de interrogación. | Compruebe que los parámetros de propiedad de transacción no contienen un signo &amp; o un signo de interrogación no codificado. Estos signos rompen el formato de la dirección URL.<br><br>Advertencia: Los parámetros de propiedad que contienen un signo &amp; o un signo de interrogación no codificado (por ejemplo: `ev_formComplete?=1` o `ev_formComplete&Submit=1`), pueden causar la pérdida de datos. |
| Advertising Cloud: ID de transacción implementado correctamente | 1 | El nombre de propiedad `ev_transid=` no debe estar vacío. | El nombre de propiedad `ev_transid=` no debe quedar sin valor. Si no se introduce un valor, puede causar la pérdida de datos de transacción. Asigne un valor a `ev_transid=` o quite el parámetro del píxel. |
| Analytics: Instanciado en DOM | 5 | El código de Adobe Analytics no está instalado o no puede ejecutarse. Devuelve el valor 0 cuando no se encuentra ningún código de Analytics en la página web. | Compruebe que la etiqueta de Analytics está implementada en la página y no está bloqueada por las siguientes actividades de script.<br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |
| Analytics: Instanciado una vez | 5 | El código de Adobe Analytics se ha detectado más de una vez en la página. Devuelve el valor 0 cuando no se encuentra ningún código de A-Analytics en la página web. | Compruebe que solo hay una etiqueta de Analytics en la página.<br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |
| Analytics: Última versión | 3 | Las páginas no ejecutan la última versión de la biblioteca de códigos de Analytics. Las bibliotecas de códigos que alimentan las tecnologías de Experience Cloud se actualizan y modifican constantemente para aprovechar las mejoras de rendimiento y ofrecer las últimas funciones. Devuelve el valor 0 cuando no se encuentra ningún código de Analytics en la página web. | Instale la última versión de la biblioteca de Analytics.<br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es) |
| Launch: Las etiquetas de terceros se cargan asincrónicamente después de DOM ready | 3 | Para lograr un equilibrio entre una buena experiencia de usuario y la recopilación de datos precisos, las etiquetas de terceros deben activarse en DOM ready. Esto garantizará que las secuencias de comandos de seguimiento se ejecuten sin afectar a la funcionalidad del sitio. | Resuelva este problema ajustando todas las reglas que ejecutan píxeles de terceros para que se activen en DOM Ready.<br><br>[Más información](../../tags/ui/managing-resources/rules.md) |
| Servicio de Experience Cloud ID: Última versión | 2 | Las páginas no ejecutan la última versión de la biblioteca de códigos del servicio de ID de visitante, visitorAPI.js. Las bibliotecas de códigos que alimentan las tecnologías de Experience Cloud se actualizan y modifican constantemente para aprovechar las mejoras de rendimiento y ofrecer las últimas funciones. | Instale la última versión de la biblioteca del servicio de ID de visitante.<br><br>[Más información](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html?lang=es) |
| Launch: Última versión | 2 | Estas páginas no ejecutan la última versión de la biblioteca de códigos de etiquetas (Turbine). Las bibliotecas de códigos que alimentan las tecnologías de Experience Cloud se actualizan y modifican constantemente para aprovechar las mejoras de rendimiento y ofrecer las últimas funciones. | Vuelva a compilar y publique la biblioteca de etiquetas.<br><br>[Más información](../../tags/quick-start/quick-start.md) |
| Target: Última versión | 2 | Las páginas no ejecutan la última versión de la biblioteca de códigos de Target. Las bibliotecas de códigos que alimentan las tecnologías de Experience Cloud se actualizan y modifican constantemente para aprovechar las mejoras de rendimiento y ofrecer las últimas funciones. | Instale la última versión de la biblioteca de Target.<br><br>[Más información](https://developer.adobe.com/target/implement/client-side/) |
| Target: mboxDefault precede a mboxCreate | 5 | El uso correcto de mboxCreate es similar al siguiente:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Asegúrese de incluir una etiqueta `<div class="mboxDefault"></div>` antes de invocar mboxCreate(). at.js no añadirá una para usted.<br><br>[Más información](https://developer.adobe.com/target/implement/client-side/) |
| Target: DOCTYPE válido | 5 | Se ha detectado un DOCTYPE no válido. En este escenario no se activará ningún mbox.  Para at.js, DOCTYPE debe estar en modo Estándares o Target no funcionará. | Actualice DOCTYPE en la página.<br><br>[Más información](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
