---
title: Resumen de ingesta de datos
description: Este documento presenta las tres formas principales de introducir los datos en Experience Platform, con vínculos a su documentación general respectiva para obtener información más detallada.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---

# Resumen de ingesta de datos

En Adobe Experience Platform, la ingesta de datos consiste en el transporte de datos desde fuentes diversas a un medio de almacenamiento al que una organización puede acceder, utilizar y analizar. La ingesta de datos en Experience Platform se puede agrupar en dos categorías principales: **ingesta de transmisión** y **ingesta por lotes**.

En la transmisión por secuencias y la ingesta por lotes hay una serie de métodos diferentes que puede utilizar para introducir los datos en Experience Platform. Estos métodos incluyen el uso de una variedad de **orígenes** y la conexión a estos orígenes para luego introducir datos en Experience Platform.

Lea este documento para obtener una descripción general de las muchas formas diferentes en que se pueden ingerir datos en Experience Platform.

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## Ingesta por streaming {#streaming}

Puede utilizar la introducción por transmisión continua para enviar datos desde dispositivos del cliente y del lado del servidor a Experience Platform en tiempo real. Experience Platform admite el uso de entradas de datos para transmitir datos de experiencia entrantes, que persisten en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos provengan de una fuente de confianza.

Para obtener más información, lea la [descripción general de la ingesta de transmisión](./streaming-ingestion/overview.md).

## Ingesta por lotes {#batch}

En Experience Platform, un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los conjuntos de datos están formados por lotes. Puede utilizar la ingesta por lotes para introducir datos en Experience Platform como archivos por lotes. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros introducidos correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como los archivos CSV planos (asignados a esquemas XDM) y archivos de parquet, se deben introducir mediante este método.

Para obtener más información, lea la [descripción general de la ingesta por lotes](./batch-ingestion/overview.md).

## Fuentes {#sources}

También puede introducir datos conectándose a fuentes de Experience Platform. Experience Platform mantiene un catálogo de una variedad de fuentes de datos a las que puede conectarse e introducir datos. Estas fuentes pueden ser aplicaciones nativas de Adobe, como la fuente de Adobe Analytics o la fuente de Marketo Engage. También puede conectarse a orígenes de terceros como el origen [!DNL Amazon S3] y el origen [!DNL Google Cloud Storage].

Las fuentes se agrupan en diferentes categorías, como almacenamiento en la nube, bases de datos y sistemas CRM. Una fuente determinada puede admitir la ingesta por lotes o de flujo continuo.

Con las fuentes, puede introducir datos de una serie de fuentes de datos diferentes y de diferentes categorías de casos de uso. Además, la ingesta de datos a través de una fuente le ofrece la oportunidad de autenticarse con la fuente de datos externa, configurar una programación de ingesta y administrar el rendimiento de la ingesta.

Para obtener más información, lea la [descripción general de orígenes](../sources/home.md).

### Creación de esquemas asistidos por ML {#ml-assisted-schema-creation}

Para integrar rápidamente nuevas fuentes de datos, ahora puede utilizar algoritmos de aprendizaje automático para generar un esquema a partir de datos de ejemplo. Esta automatización simplifica la creación de esquemas precisos, reduce los errores y acelera el proceso desde la recopilación de datos hasta el análisis y las perspectivas.

Consulte la [guía de creación de esquemas asistidos por ML](../xdm/ui/ml-assisted-schema-creation.md) para obtener más información sobre este flujo de trabajo.

## Preparación de los datos {#data-prep}

Aunque la preparación de datos no es un método de ingesta, es una parte importante del proceso de ingesta de datos. Utilice las funciones de preparación de datos para asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM) antes de crear un flujo de datos para introducir los datos en Experience Platform. La preparación de datos aparece como el paso &quot;Asignación&quot; en la interfaz de usuario de Experience Platform durante el proceso de ingesta de datos.

Para obtener más información, lea la [descripción general de la preparación de datos](../data-prep/home.md).

## Métodos de ingesta por streaming {#streaming-ingestion-methods}

En la tabla siguiente se describen los distintos métodos que se pueden utilizar para introducir datos de flujo continuo en Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Fuentes de streaming</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación de datos de sitios web y aplicaciones móviles.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método preferido para la colección del lado del cliente.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implemente varias aplicaciones de Adobe aprovechando un solo SDK.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">Conector de API HTTP</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación de fuentes de flujo continuo, transacciones, eventos y señales relevantes de clientes.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Los datos sin procesar o XDM se transmiten directamente al concentrador, sin segmentación de Edge en tiempo real ni reenvío de eventos.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Recopilación de fuentes de flujo continuo, transacciones, eventos relevantes de clientes y señales de [!DNL Edge Network] distribuidos globalmente.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Los datos se transmiten a través de [!DNL Edge Network]. Compatibilidad con la segmentación en tiempo real y el reenvío de eventos en Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en" style="color:#0563c1; text-decoration:underline">Aplicaciones Adobe</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta de datos desde aplicaciones como Adobe Analytics, Marketo Engage, Adobe Campaign Managed Services, Adobe Target, Adobe Audience Manager</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Conectores push y Source y API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">El método recomendado es migrar al SDK web/móvil en lugar de utilizar los SDK de aplicaciones tradicionales.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Fuentes de streaming</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta de un flujo de eventos empresarial, que generalmente se utiliza para compartir datos empresariales con varias aplicaciones de flujo descendente. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API de REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Los datos se transmiten en formato JSON y se pueden asignar al esquema XDM.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">SDK de fuentes de streaming</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Utilice las funciones de autoservicio de fuentes de autoservicio de SDK de streaming para integrar su propia fuente de datos en el catálogo de fuentes de Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Algunos ejemplos de fuentes de streaming integradas por socios son: Braze, Pendo y RainFocus.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## Métodos de ingesta por lotes {#batch-ingestion-methods}

En la tabla siguiente se describen los distintos métodos que se pueden utilizar para introducir datos por lotes en Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Orígenes de lotes</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Método</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Casos de uso comunes</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocolos</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Consideraciones</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">API de ingesta por lotes</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta desde una cola administrada por la empresa. Utilice la ingesta por lotes si es necesario preparar y formatear los datos antes de la ingesta.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, JSON o Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Debe administrar lotes y archivos para la ingesta.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">Orígenes de lotes</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Enfoque común para la ingesta de datos desde el almacenamiento en la nube, CRM y aplicaciones de automatización de marketing.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal para ingerir grandes cantidades de datos históricos.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Extraer, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingesta de Source en función de intervalos programados preconfigurados.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=en" style="color:#0563c1; text-decoration:underline">Zona de aterrizaje de datos</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Almacenamiento de archivos basado en la nube aprovisionado por Adobe. Tiene acceso a un contenedor de zona de aterrizaje de datos por zona protegida.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inserte sus archivos en la zona de aterrizaje de datos para su posterior ingesta en Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform aplica un plazo de caducidad estricto de siete días a todos los archivos y carpetas cargados en un contenedor de zona de aterrizaje de datos. Todos los archivos y carpetas se eliminan pasados siete días.</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">SDK de fuentes por lotes</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Utilice las funciones de autoservicio de SDK por lotes de fuentes de autoservicio para integrar su propia fuente de datos en el catálogo de fuentes de Experience Platform.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal para conectores de socios o para una experiencia de flujo de trabajo adaptada para configurar un conector empresarial.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Extracción, API de REST, CSV o JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Algunos ejemplos de fuentes por lotes integradas por socios son: Mailchimp, OneTrust, Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## Pasos siguientes y recursos adicionales

Este documento proporciona una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] en [!DNL Experience Platform]. Continúe leyendo la documentación de información general de cada método de ingesta para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingesta. Para obtener información sobre cómo [!DNL Experience Platform] realiza el seguimiento de los metadatos de los registros ingeridos, consulte la [descripción general del servicio de catálogo](../catalog/home.md).

>[!WARNING]
>
>El término &quot;perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] son los términos correctos utilizados en la documentación de [!DNL Experience Platform]. Consulte la documentación para obtener la funcionalidad más reciente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
