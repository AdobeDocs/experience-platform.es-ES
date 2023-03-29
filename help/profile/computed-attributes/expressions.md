---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Expresiones PQL de muestra para atributos calculados
type: Documentation
description: Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones requieren el uso de expresiones válidas de lenguaje de consulta de perfil (PQL). Esta guía describe algunas de las expresiones PQL más utilizadas para los atributos calculados.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha) Ejemplo de expresiones PQL para atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo computado está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización. Cada atributo calculado se define con información básica, como un nombre y una descripción, la clase de esquema y la ruta al campo en el que se va a mantener el valor y una expresión, cuyo valor calculado es el valor que desea almacenar en el atributo calculado.

Las expresiones utilizadas en los atributos calculados se crean mediante [!DNL Profile Query Language] (PQL), un lenguaje de consulta compatible con el Modelo de datos de experiencia (XDM) diseñado para admitir la definición y ejecución de consultas para datos del Perfil del cliente en tiempo real.

Actualmente, los atributos calculados admiten las siguientes funciones: sum, count, min, max y booleano. Esta guía describe algunas de las expresiones de PQL más utilizadas que puede utilizar al definir sus propios atributos calculados para su organización. Para obtener más información sobre PQL y vínculos a directrices de formato adicionales y muestras de consultas admitidas, visite [Información general de PQL](../../segmentation/pql/overview.md).

## Expresiones de flujo continuo

La tabla siguiente proporciona detalles para las expresiones de consulta más utilizadas que se admiten en el modo de flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Perfil o evento de experiencia (EE[]) | Tipo de resultado |
|---|---|---|---|
| Recuento de descargas de imágenes en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot; y contentType = &quot;image&quot;].count() | Perfil y EE[] | Número entero |
| Suma del gasto de los clientes en productos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].sum(commerce.order.priceTotal) | Perfil y EE[] | Número entero o doble |
| Gasto promedio de los clientes en productos deportivos en los últimos 7 días.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].count()<br/><br/>**ca3:** ca1/ca2 | Perfil y EE[] | Doble |
| ¿El cliente ha gastado más de 100 dólares en artículos deportivos los últimos 7 días?<br/><br/>**Nota:** Requiere la creación de dos atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Perfil y EE[] | Booleano |
| ¿El cliente ha realizado una compra en los últimos 7 días? | chain(xEvent, timestamp, [A: QUÉ(eventType = &quot;transaction&quot;) CUANDO(&lt; 7 días antes)]) | Perfil y EE[] | Booleano |
| El menor gasto del usuario en productos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].min(commerce.order.priceTotal) | Perfil y EE[] | Número entero o doble |
| El mayor gasto del usuario en productos deportivos en los últimos 7 días. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;transaction&quot; y category = &quot;productos deportivos&quot;].max(commerce.order.priceTotal) | Perfil y EE[] | Número entero o doble |
| Recuento de descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil y EE[] | Mapa[Cadena, entero] |
| Suma de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G => mapEntry(K, G.sum(commerce.order.priceTotal))) | Perfil y EE[] | Mapa[Cadena, entero] o Mapa[Cadena, Doble] |
| Promedio de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto.<br/><br/>**Nota:** Requiere la creación de tres atributos calculados. | **ca1:** xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2/ca1 | Perfil y EE[] | Mapa[Cadena, Doble] |
| Mínimo de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G => mapEntry(K, G.min(commerce.order.priceTotal))) | Perfil y EE[] | Mapa[Cadena, entero] o Mapa[Cadena, Doble] |
| Máximo de propiedad numérica sobre las descargas de cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G => mapEntry(K, G.max(commerce.order.priceTotal))) | Perfil y EE[] | Mapa[Cadena, entero] o Mapa[Cadena, Doble] |
| Expresión numérica en el perfil, sin referencia a eventos. | if(person.gender = &quot;women&quot;, 60, 65) | Perfil | Número entero o doble |
| Expresión booleana en el perfil, sin referencia a eventos. | person.birthYear >= 2000 | Perfil | Booleano |
| Expresión de cadena en el perfil, sin referencia a eventos. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;FILA&quot;) | Perfil | Cadena |

## Expresiones por lotes

La siguiente tabla proporciona detalles para expresiones de consulta que solo están disponibles en modo por lotes, lo que significa que actualmente no están disponibles en flujo continuo.

| Descripción | Expresión PQL | Tipo de entrada:<br/>Perfil o evento de experiencia (EE[]) | Tipo de resultado |
|---|---|---|---|
| Indica si la suma de expresiones numéricas sobre las descargas de productos en los últimos 7 días supera los 100, indexados por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Mapa[Cadena, Booleano] |
| Indica si el promedio de expresión numérica sobre las descargas de productos en los últimos 7 días supera los 100, indexados por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil y EE[] | Mapa[Cadena, Booleano] |
| Acumulación de varias métricas para cada producto descargado, en los últimos 7 días, indexado por producto. | xEvent[(la marca de tiempo se produce &lt; 7 días antes) y eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Perfil y EE[] | Mapa[Cadena, Objeto] donde Object es un tipo XDM personalizado |
