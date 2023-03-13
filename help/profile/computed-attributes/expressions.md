---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Expresiones PQL de muestra para atributos calculados
type: Documentation
description: Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones requieren el uso de expresiones válidas de lenguaje de consulta de perfil (PQL). Esta guía describe algunas de las expresiones PQL más utilizadas para los atributos calculados.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha) Expresiones PQL de muestra para atributos calculados

>[!IMPORTANT]
>
>Actualmente, la funcionalidad de atributos calculados está en formato alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Cada atributo calculado se define con información básica, como un nombre y una descripción, la clase de esquema y la ruta de acceso al campo en el que se mantendrá el valor, y una expresión, cuyo valor calculado es el valor que desea almacenar en el atributo calculado.

Las expresiones utilizadas en los atributos calculados se crean mediante [!DNL Profile Query Language] (PQL), un lenguaje de consulta compatible con el modelo de datos de experiencia (XDM) diseñado para admitir la definición y ejecución de consultas de datos del perfil del cliente en tiempo real.

Actualmente, los atributos calculados admiten las siguientes funciones: suma, recuento, mínimo, máximo y booleano. Esta guía describe algunas de las expresiones PQL más utilizadas que puede utilizar al definir sus propios atributos calculados para su organización. Para obtener más información sobre el PQL y vínculos a directrices de formato adicionales y ejemplos de consultas admitidas, visite la [Información general de PQL](../../segmentation/pql/overview.md).

## Expresiones de streaming

La siguiente tabla proporciona detalles sobre las expresiones de consulta más utilizadas admitidas en el modo de flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Evento de perfil o experiencia (EE)[]) | Tipo de resultado |
|---|---|---|---|
| Recuento de descargas de imágenes en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot; y contentType = &quot;image&quot;].count() | Perfil y EE[] | Número entero |
| Suma del gasto del cliente en artículos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].sum(commerce.order.priceTotal) | Perfil y EE[] | Entero o doble |
| Gasto promedio de los clientes en artículos deportivos en los últimos 7 días.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | Perfil y EE[] | Doble |
| ¿El cliente ha gastado más de 100 dólares en artículos deportivos los últimos 7 días?<br/><br/>**Nota:** Requiere la creación de dos atributos calculados. | **ca1:** xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Perfil y EE[] | Booleano |
| ¿El cliente ha realizado una compra en los últimos 7 días? | chain(xEvent, timestamp, [A: QUÉ(eventType = &quot;transaction&quot;) CUÁNDO(&lt; 7 días antes)]) | Perfil y EE[] | Booleano |
| Gasto más bajo de los usuarios en artículos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].min(commerce.order.priceTotal) | Perfil y EE[] | Entero o doble |
| Gasto más alto de los usuarios en artículos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo tiene lugar &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;sporting products&quot;].max(commerce.order.priceTotal) | Perfil y EE[] | Entero o doble |
| Recuento de descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil y EE[] | Mapa[Cadena, entero] |
| Suma de la propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Perfil y EE[] | Mapa[Cadena, entero] o mapa[Cadena, doble] |
| Promedio de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))<br/><br/>**ca2:** xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1 | Perfil y EE[] | Mapa[Cadena, doble] |
| Mínimo de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Perfil y EE[] | Mapa[Cadena, entero] o mapa[Cadena, doble] |
| Máximo de propiedad numérica sobre descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Perfil y EE[] | Mapa[Cadena, entero] o mapa[Cadena, doble] |
| Expresión numérica en el perfil, sin referencia a eventos. | if(person.gender = &quot;female&quot;, 60, 65) | Perfil | Entero o doble |
| Expresión booleana en el perfil, sin referencia a eventos. | person.birthYear >= 2000 | Perfil | Booleano |
| Expresión de cadena en el perfil, sin referencia a eventos. | if(homeAddress.countryCode en [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Perfil | Cadena |

## Expresiones por lotes

La siguiente tabla proporciona detalles para expresiones de consulta que solo están disponibles en el modo por lotes, lo que significa que actualmente no están disponibles en el flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Evento de perfil o experiencia (EE)[]) | Tipo de resultado |
|---|---|---|---|
| Si la suma de expresiones numéricas sobre descargas de productos en los últimos 7 días supera o no los 100, indizadas por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Mapa[Cadena, booleano] |
| Si el promedio de expresión numérica sobre las descargas de productos en los últimos 7 días supera o no los 100, indizado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Mapa[Cadena, booleano] |
| Acumulación de varias métricas para cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes de ahora) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Perfil y EE[] | Mapa[String, Object] donde Objeto es un tipo XDM personalizado |
