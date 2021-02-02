---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Tutoriales de inserción de datos
topic: tutorial
type: Tutorial
description: La ingestión de datos incluye la ingestión por lotes, la ingestión por flujo continuo y la ingestión mediante conectores de origen.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Ingresar datos en [!DNL Experience Platform]

Adobe Experience Platform reúne los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. El Adobe [!DNL Experience Platform Data Ingestion] representa los múltiples métodos mediante los cuales [!DNL Platform] ingiere datos de estas fuentes, así como la forma en que se mantienen esos datos dentro del Data Lake para su uso por el flujo [!DNL Platform services]. [!DNL Data Ingestion] incluye la ingestión por lotes, la ingestión por flujo continuo y la ingestión mediante conectores de origen. Para obtener más información, lea la [información general sobre la ingestión de datos](../ingestion/home.md) o diríjase directamente a la [documentación de fuentes](../sources/home.md).

## Creación de un conector de origen en la interfaz de usuario y la API

Los conectores de origen le permiten ingestar datos de múltiples fuentes, donde luego se pueden etiquetar, estructurar y mejorar mediante [!DNL Platform services]. Para empezar a crear un conector de origen, consulte la información general de [orígenes](../sources/home.md).

## Ingestar datos de lote

Adobe Experience Platform permite importar fácilmente datos en [!DNL Platform] como archivos por lotes. Algunos ejemplos de datos que se van a ingerir pueden incluir datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o datos que se ajustan a un esquema conocido [!DNL Experience Data Model] (XDM) en el Registro de Esquemas. Para empezar, visite el [tutorial de ingestión de datos en el tutorial de plataforma](../ingestion/tutorials/ingest-batch-data.md).

## Asignación de un archivo CSV a un Esquema XDM

Para poder ingerir datos CSV en Adobe Experience Platform, los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Para ver los pasos que se siguen para asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario [!DNL Experience Platform], siga el [asignar un archivo CSV a un tutorial de esquema XDM](../ingestion/tutorials/map-a-csv-file.md).

## Creación de una conexión de flujo continuo

Para inicio de datos de flujo continuo a [!DNL Experience Platform], primero debe solicitar un extremo HTTP. Tiene la opción de configurar este extremo para aplicar un comportamiento autenticado. Esto se puede hacer mediante la interfaz de usuario [!DNL Platform] o las API [!DNL Experience Platform]. Para obtener más información, siga los tutoriales para [crear una conexión de flujo mediante la IU](../ingestion/tutorials/create-streaming-connection-ui.md) o [crear una conexión de flujo mediante API](../ingestion/tutorials/create-streaming-connection.md).

## Creación de una conexión de flujo autenticada

La recopilación de datos autenticada permite a los servicios de Adobe Experience Platform, como [!DNL Real-time Customer Profile] y [!DNL Identity], diferenciar entre registros provenientes de fuentes de confianza y fuentes de confianza. Para empezar, siga el tutorial para [crear una conexión de flujo autenticada](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Datos de series temporales y registros de flujo

Con un conjunto de datos y conexiones de flujo continuo implementadas, puede transmitir datos de registros o series temporales a [!DNL Platform]. Para empezar a transmitir datos de registro, siga el [flujo de datos de registro en el tutorial de plataforma](../ingestion/tutorials/streaming-record-data.md). Para empezar a transmitir datos de series temporales, siga los [datos de series temporales de flujo en la plataforma](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir varios mensajes en una sola solicitud HTTP

Al transmitir datos a Adobe Experience Platform, realizar numerosas llamadas HTTP puede resultar costoso. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una manera excelente de optimizar los datos que se envían a [!DNL Experience Platform]. Para aprender a enviar varios mensajes a [!DNL Experience Platform] dentro de una sola solicitud HTTP usando la ingesta de flujo, siga el [tutorial de envío de varios mensajes](../ingestion/tutorials/streaming-multiple-messages.md).



