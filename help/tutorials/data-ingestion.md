---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales de inserción de datos
topic: tutorial
type: Tutorial
description: La ingestión de datos incluye la ingestión por lotes, la ingestión por flujo continuo y la ingestión mediante conectores de origen.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Ingest data into [!DNL Experience Platform]

Adobe Experience Platform reúne los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. Adobe [!DNL Experience Platform Data Ingestion] representa los múltiples métodos mediante los cuales se [!DNL Platform] ingieren datos de estas fuentes, así como la forma en que se conservan esos datos dentro del Data Lake para su uso en la etapa posterior [!DNL Platform services]. [!DNL Data Ingestion] incluye la ingestión por lotes, la ingestión por flujo continuo y la ingestión mediante conectores de origen. Para obtener más información, lea la descripción general [de la ingestión de](../ingestion/home.md) datos o vaya directamente a la documentación [de](../sources/home.md)las fuentes.

## Creación de un conector de origen en la interfaz de usuario y la API

Los conectores de origen le permiten ingestar datos de varias fuentes, donde se pueden etiquetar, estructurar y mejorar mediante [!DNL Platform services]. Para empezar a crear un conector de origen, consulte la descripción general [de](../sources/home.md)las fuentes.

## Ingestar datos de lote

Adobe Experience Platform permite importar fácilmente datos en [!DNL Platform] archivos por lotes. Algunos ejemplos de datos que se van a ingerir pueden incluir datos de perfil de un archivo plano en un sistema CRM (como un archivo parquet) o datos que se ajustan a un esquema conocido [!DNL Experience Data Model] (XDM) en el Registro de Esquemas. Para empezar, visite el tutorial [de](../ingestion/tutorials/ingest-batch-data.md)ingestión de datos en la plataforma.

## Asignación de un archivo CSV a un Esquema XDM

Para poder ingerir datos CSV en Adobe Experience Platform, los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Para ver los pasos que se siguen para asignar un archivo CSV a un esquema XDM mediante la interfaz del [!DNL Experience Platform] usuario, siga el [mapa de un archivo CSV a un tutorial](../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

## Creación de una conexión de flujo continuo

Para inicio de datos de flujo continuo a [!DNL Experience Platform], primero debe solicitar un extremo HTTP. Tiene la opción de configurar este extremo para aplicar un comportamiento autenticado. Esto se puede hacer mediante la interfaz de usuario [!DNL Platform] o [!DNL Experience Platform] las API. Para obtener más información, siga los tutoriales sobre la [creación de una conexión de flujo mediante la interfaz de usuario](../ingestion/tutorials/create-streaming-connection-ui.md) o la [creación de una conexión de flujo mediante API](../ingestion/tutorials/create-streaming-connection.md).

## Creación de una conexión de flujo autenticada

La recopilación de datos autenticada permite a los servicios de Adobe Experience Platform, como [!DNL Real-time Customer Profile] y [!DNL Identity], diferenciar entre registros procedentes de fuentes de confianza y fuentes de confianza. Para empezar, siga el tutorial para [crear una conexión](../ingestion/tutorials/create-authenticated-streaming-connection.md)de flujo autenticada.

## Datos de series temporales y registros de flujo

Con un conjunto de datos y conexiones de flujo continuo implementadas, puede transmitir datos de registros o series temporales a [!DNL Platform]. Para empezar a transmitir datos de registro, siga los datos de registro de [flujo en el tutorial](../ingestion/tutorials/streaming-record-data.md)Plataforma. Para empezar a transmitir datos de series temporales, siga los datos de series temporales de [flujo en la plataforma](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir varios mensajes en una sola solicitud HTTP

Al transmitir datos a Adobe Experience Platform, realizar numerosas llamadas HTTP puede resultar costoso. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una excelente manera de optimizar los datos que se envían a [!DNL Experience Platform]. Para obtener información sobre cómo enviar varios mensajes a [!DNL Experience Platform] una sola solicitud HTTP mediante la ingesta de flujo continuo, siga el tutorial [de](../ingestion/tutorials/streaming-multiple-messages.md)envío de varios mensajes.



