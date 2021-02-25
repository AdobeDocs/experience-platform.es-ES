---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Expresiones PQL de muestra para atributos calculados
topic: guía
type: Documentación
description: Los atributos calculados son funciones que se utilizan para acumulados datos de nivel de evento en atributos de nivel de perfil. Estas funciones requieren el uso de expresiones válidas del lenguaje de Consulta de Perfil (PQL). Esta guía describe algunas de las expresiones PQL más utilizadas para los atributos calculados.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# expresiones PQL de muestra para atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

En Adobe Experience Platform, los atributos calculados son funciones utilizadas para acumulados datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Cada atributo calculado se define con información básica, como un nombre y una descripción, la clase de esquema y la ruta al campo en el que se retendrá el valor y una expresión, cuyo valor calculado es el valor que se desea almacenar en el atributo calculado.

Las expresiones utilizadas en los atributos calculados se crean mediante [!DNL Profile Query Language] (PQL), un lenguaje de consulta compatible con el modelo de datos de experiencia (XDM) diseñado para admitir la definición y ejecución de consultas para datos de Perfil de clientes en tiempo real.

Los atributos calculados actualmente admiten las siguientes funciones: sum, count, min, max y booleano. Esta guía describe algunas de las expresiones PQL más utilizadas que puede utilizar al definir sus propios atributos calculados para su organización. Para obtener más información sobre PQL y vínculos a directrices de formato adicionales y muestras de consultas admitidas, visite [información general de PQL](../../segmentation/pql/overview.md).

## Expresiones de flujo continuo

En la tabla siguiente se proporcionan detalles sobre las expresiones de consulta más utilizadas que se admiten en el modo de flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Perfil o Evento de experiencias (EE[]) | Tipo de resultado |
|---|---|---|---|
| Recuento de descargas de imágenes en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot; y contentType = &quot;image&quot;].count() | Perfil y EE[] | Número entero |
| Suma del gasto de los clientes en productos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y categoría = &quot;productos deportivos&quot;].sum(commerce.order.priceTotal) | Perfil y EE[] | Entero o Doble |
| Gasto promedio de los clientes en productos deportivos en los últimos 7 días.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(la marca de tiempo se produce  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Perfil y EE[] | Duplicada |
| ¿Ha gastado el cliente más de 100 dólares en productos deportivos los últimos 7 días?<br/><br/>**Nota:** Requiere la creación de dos atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Perfil y EE[] | Booleano |
| ¿Ha realizado el cliente una compra en los últimos 7 días? | chain(xEvent, timestamp, [A: QUÉ(eventType = &quot;transaction&quot;) CUANDO(&lt; 7 días antes de ahora)]) | Perfil y EE[] | Booleano |
| El menor gasto de los usuarios en artículos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y categoría = &quot;productos deportivos&quot;].min(commerce.order.priceTotal) | Perfil y EE[] | Entero o Doble |
| El mayor gasto de los usuarios en artículos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y categoría = &quot;productos deportivos&quot;].max(commerce.order.priceTotal) | Perfil y EE[] | Entero o Doble |
| Recuento de descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil y EE[] | Map[String, Integer] |
| Suma de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Perfil y EE[] | Map[String, Integer] o Map[String, Doble] |
| Promedio de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(la marca de tiempo se produce  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.count())))<br/><br/>**ca3:** ca2 / ca1]] | Perfil y EE[] | Map[String, Doble] |
| Mínimo de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Perfil y EE[] | Map[String, Integer] o Map[String, Doble] |
| Máximo de propiedades numéricas sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Perfil y EE[] | Map[String, Integer] o Map[String, Doble] |
| Expresión numérica en perfil, no eventos de referencia. | if(people.gender = &quot;women&quot;, 60, 65) | Perfil | Entero o Doble |
| Expresión booleana en perfil, no en eventos de referencia. | people.bornYear >= 2000 | Perfil | Booleano |
| Expresión de cadena en perfil, no en eventos de referencia. | if(homeAddress.countryCode en [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Perfil | Cadena |

## Expresiones por lotes

La siguiente tabla proporciona detalles para las expresiones de consulta que solo están disponibles en modo de lote, lo que significa que no están disponibles en flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Perfil o Evento de experiencias (EE[]) | Tipo de resultado |
|---|---|---|---|
| Indica si la suma de la expresión numérica sobre las descargas de productos en los últimos 7 días supera los 100, indexada por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Map[String, Boolean] |
| Indica si el promedio de expresión numérica sobre las descargas de productos en los últimos 7 días es superior a 100, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Map[String, Boolean] |
| Acumulación de varias métricas para cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Perfil y EE[] | Map[String, Object] donde Object es un tipo XDM personalizado |