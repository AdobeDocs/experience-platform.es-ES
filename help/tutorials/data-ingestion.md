---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Tutoriales sobre ingesta de datos
topic-legacy: tutorial
type: Tutorial
description: La ingesta de datos incluye la ingesta por lotes, la ingesta de transmisión por secuencias y la ingesta mediante conectores de origen.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 4%

---

# Ingesta de datos en [!DNL Experience Platform]

Adobe Experience Platform reúne datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. El Adobe [!DNL Experience Platform Data Ingestion] representa los múltiples métodos mediante los cuales [!DNL Platform] incorpora datos de estas fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso por flujo [!DNL Platform services] descendente. [!DNL Data Ingestion] incluye ingesta por lotes, ingesta de flujo continuo e ingesta mediante conectores de origen. Para obtener más información, lea la [Información general sobre la ingesta de datos](../ingestion/home.md) o diríjase directamente a la [Documentación de fuentes](../sources/home.md).

## Crear una conexión de origen en la interfaz de usuario y la API

Los conectores de origen le permiten introducir datos de varias fuentes, donde después se pueden etiquetar, estructurar y mejorar con [!DNL Platform services]. Para empezar a crear un conector de origen, consulte la [información general de las fuentes](../sources/home.md).

## Ingesta de datos de lote

Adobe Experience Platform permite importar fácilmente datos en [!DNL Platform] como archivos por lotes. Algunos ejemplos de datos que se van a introducir pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido [!DNL Experience Data Model] (XDM) en el Registro de esquemas. Para empezar, visite el [tutorial de ingesta de datos en Platform](../ingestion/tutorials/ingest-batch-data.md).

## Asignación de un archivo CSV a un esquema XDM

Para poder introducir datos CSV en Adobe Experience Platform, los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Para ver los pasos que muestran cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario [!DNL Experience Platform], siga el [asignar un archivo CSV a un tutorial de esquema XDM](../ingestion/tutorials/map-a-csv-file.md).

## Creación de una conexión de flujo continuo

Para iniciar la transmisión de datos a [!DNL Experience Platform], primero debe solicitar un extremo HTTP. Tiene la opción de configurar este extremo para aplicar el comportamiento autenticado. Esto se puede hacer mediante la interfaz de usuario [!DNL Platform] o las API [!DNL Experience Platform]. Para obtener más información, siga los tutoriales para [crear una conexión de flujo continuo mediante la IU](../ingestion/tutorials/create-streaming-connection-ui.md) o [crear una conexión de flujo continuo mediante API](../ingestion/tutorials/create-streaming-connection.md).

## Creación de una conexión de flujo continuo autenticada

La recopilación de datos autenticados permite que los servicios de Adobe Experience Platform, como [!DNL Real-time Customer Profile] y [!DNL Identity], diferencien entre registros procedentes de fuentes de confianza y fuentes de confianza. Para empezar, siga el tutorial para [crear una conexión de flujo autenticada](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Registros de emisión y datos de series temporales

Con un conjunto de datos y conexiones de flujo continuo en su lugar, puede transmitir datos de registros o series temporales a [!DNL Platform]. Para empezar a transmitir datos de registro, siga el tutorial [stream record data into Platform](../ingestion/tutorials/streaming-record-data.md). Para empezar a transmitir datos de series temporales, siga los [datos de series temporales de flujo a Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Transmisión de varios mensajes en una única solicitud HTTP

Al transmitir datos a Adobe Experience Platform, hacer numerosas llamadas HTTP puede ser caro. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas útiles de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una única solicitud es una excelente manera de optimizar los datos que se envían a [!DNL Experience Platform]. Para aprender a enviar varios mensajes a [!DNL Experience Platform] dentro de una única solicitud HTTP mediante la ingesta de flujo continuo, siga el [tutorial de envío de varios mensajes](../ingestion/tutorials/streaming-multiple-messages.md).
