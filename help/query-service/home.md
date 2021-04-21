---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta
solution: Experience Platform
title: Información general del servicio de consultas
topic-legacy: overview
description: Este documento proporciona una descripción general de la función del servicio de consultas dentro del Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Información general del [!DNL Query Service]

Adobe Experience Platform incorpora datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en marketing es dar sentido a estos datos para obtener información sobre sus clientes. Adobe Experience Platform [!DNL Query Service] lo facilita al permitirle utilizar SQL estándar para consultar los datos en [!DNL Platform]. Con [!DNL Query Service], puede unirse a cualquier conjunto de datos en [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en sistemas de informes, aprendizaje automático o para ingerirlos en [!DNL Real-time Customer Profile]. Este documento proporciona información general sobre la función de [!DNL Query Service] dentro de [!DNL Experience Platform].

[!DNL Query Service] permite a las marcas conectar el recorrido de cliente en línea a sin conexión y comprender la atribución omnicanal. El siguiente vídeo muestra cómo un negocio de experiencia puede aprovechar [!DNL Query Service] para abordar casos de uso clave y cómo funciona [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso de [!DNL Query Service]

[!DNL Query Service] proporciona una interfaz de usuario y una API RESTful desde la cual puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios dentro de su organización de IMS. La interfaz de usuario está diseñada para utilizarse como simulador de pruebas para probar las consultas antes de ejecutarlas en un conjunto de datos más amplio. Puede encontrar más información sobre el uso del servicio interactivo dentro de [!DNL Platform] en la [Guía de la interfaz de usuario del servicio de consulta](ui/overview.md). La API de RESTful proporciona una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Puede encontrar más información sobre el uso de la API [!DNL Query Service] en la [Guía para desarrolladores del servicio de consulta](api/getting-started.md).

## [!DNL Query Service] y  [!DNL Experience Platform] servicios

[!DNL Query Service] interactúa y se puede utilizar junto con varios  [!DNL Experience Platform] servicios. Para aprovechar al máximo las capacidades de [!DNL Query Service's], se recomienda que se familiarice con estos servicios y con cómo interactúan con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados dentro de [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre clientes y sus actividades, facilitando predicciones como la compra de propensión y ofertas recomendadas que el individuo probablemente aprecie y use. Puede utilizar SQL en [!DNL Data Science Workspace] integrando [!DNL Query Service] en [!DNL JupyterLab], lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea la [!DNL Data Science Workspace] información general para obtener más información sobre [!DNL Data Science Workspace] y la guía de integración [!DNL Query Service] para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permite que los usuarios dividan a sus clientes en grupos más pequeños que compartan características similares. Estos segmentos pueden evaluarse posteriormente para proporcionar un mejor análisis de sus datos [!DNL Real-time Customer Profile]. [!DNL Query Service] para proporcionar este análisis, ejecute consultas sobre estos datos de segmento dentro de  [!DNL Data Lake]. Lea la [!DNL Segmentation Service] información general para obtener más información sobre la segmentación y la guía [!DNL Profile Query Language] (PQL) para obtener más información sobre cómo analizar los segmentos.

### Caso de uso de Lookéter BI

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados, incluidos los datos de comportamiento, CRM y puntos de venta. Con [!DNL Experience Platform's Query Service], puede consultar estos conjuntos de datos y responder preguntas específicas sobre el negocio y luego empezar a generar perspectivas impactantes. En el siguiente vídeo se muestra el valor de crear tableros en las herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Pasos siguientes y recursos adicionales

Al leer este documento, se le ha introducido [!DNL Query Service] y cómo funciona dentro del bueno ámbito de [!DNL Experience Platform]. Para obtener más información sobre la interacción con varios extremos dentro de la API [!DNL Query Service], lea la [Guía para desarrolladores del servicio de consulta](api/getting-started.md). Para obtener más información sobre el uso del servicio interactivo en [!DNL Platform], lea la [Guía de la interfaz de usuario del servicio de consulta](ui/overview.md). Para obtener una lista completa sobre la conexión de clientes externos con [!DNL Query Service], lea la [información general de clientes del servicio de consulta](clients/overview.md).

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. En este vídeo se comparten sugerencias y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, clientes PSQL, soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
