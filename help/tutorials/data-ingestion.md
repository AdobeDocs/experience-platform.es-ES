---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales de inserción de datos
topic: tutorial
translation-type: tm+mt
source-git-commit: e4da80338dbfbad70dfb3cf7df9fe589e949e788

---


# Ingestar datos en la plataforma de experiencia

Adobe Experience Platform aúna los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingestión de datos de la plataforma de experiencia de Adobe representa los múltiples métodos mediante los cuales la plataforma ingesta datos de estas fuentes, así como la forma en que se mantienen los datos dentro del lago de datos para su uso por los servicios de plataforma descendente. La ingestión de datos incluye la ingestión por lotes, la ingestión por flujo continuo y la ingestión mediante conectores de origen. Para obtener más información, lea la descripción general [de la ingestión de](../ingestion/home.md) datos o vaya directamente a la documentación [de](../sources/home.md)las fuentes.

## Creación de un conector de origen en la interfaz de usuario y la API

Los conectores de origen le permiten ingestar datos de varias fuentes, donde se pueden etiquetar, estructurar y mejorar mediante los servicios de plataforma. Para empezar a crear un conector de origen, consulte la descripción general [de](../sources/home.md)las fuentes.

## Ingestar datos de lote

Adobe Experience Platform le permite importar fácilmente datos en Platform como archivos por lotes. Algunos ejemplos de datos que se van a ingerir pueden incluir datos de perfil de un archivo plano en un sistema CRM (como un archivo parquet) o datos que se ajustan a un esquema conocido del Modelo de datos de experiencia (XDM) en el Registro de Esquemas. Para empezar, visite el tutorial [de](../ingestion/tutorials/ingest-batch-data.md)ingestión de datos en la plataforma.

## Asignación de un archivo CSV a un Esquema XDM

Para poder transferir datos CSV a la plataforma de Adobe Experience, los datos deben asignarse a un esquema del modelo de datos de experiencia (XDM). Para ver los pasos que se siguen para asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario de la plataforma de experiencia, siga el [mapa de un archivo CSV a un tutorial](../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

## Creación de una conexión de flujo continuo

Para inicio de datos de flujo continuo a la plataforma de experiencia, primero debe crear una conexión HTTP de flujo. Al crear una conexión de flujo continuo, debe proporcionar detalles clave como, por ejemplo, el origen de los datos de flujo continuo y si desea o no enviar datos desde un origen de confianza (autenticado) o no de confianza (no autenticado). Esto se puede hacer mediante la interfaz de usuario de la plataforma o las API de la plataforma de experiencia. Para obtener más información, siga los tutoriales sobre la [creación de una conexión de flujo mediante la interfaz de usuario](../ingestion/tutorials/create-streaming-connection-ui.md) o la [creación de una conexión de flujo mediante API](../ingestion/tutorials/create-streaming-connection.md).

## Creación de una conexión de flujo autenticada

La recopilación de datos autenticada permite a los servicios de Adobe Experience Platform, como Perfil e identidad del cliente en tiempo real, diferenciar entre registros procedentes de fuentes de confianza y orígenes que no son de confianza. Para empezar, siga el tutorial para [crear una conexión](../ingestion/tutorials/create-authenticated-streaming-connection.md)de flujo autenticada.

## Datos de series temporales y registros de flujo

Con un conjunto de datos y conexiones de flujo continuo implementadas, puede transmitir datos de registros o series temporales a la plataforma. Para empezar a transmitir datos de registro, siga los datos de registro de [flujo en el tutorial](../ingestion/tutorials/streaming-record-data.md)Plataforma. Para empezar a transmitir datos de series temporales, siga los datos de series temporales de [flujo en la plataforma](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir varios mensajes en una sola solicitud HTTP

Cuando se transmiten datos a Adobe Experience Platform, puede resultar caro realizar numerosas llamadas HTTP. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes en una sola solicitud es una manera excelente de optimizar los datos que se envían a la plataforma de experiencia. Para obtener información sobre cómo enviar varios mensajes a la plataforma de experiencias en una sola solicitud HTTP mediante la transmisión de flujo continuo, siga el tutorial [de](../ingestion/tutorials/streaming-multiple-messages.md)envío de varios mensajes.



