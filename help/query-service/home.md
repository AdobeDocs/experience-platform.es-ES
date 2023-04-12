---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta
solution: Experience Platform
title: Información general del servicio de consultas
description: Este documento proporciona una descripción general de la función del servicio de consultas dentro del Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Información general del [!DNL Query Service]

Adobe Experience Platform incorpora datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en marketing es dar sentido a estos datos para obtener información sobre sus clientes. Adobe Experience Platform [!DNL Query Service] facilita esto al permitirle utilizar SQL estándar para consultar datos en [!DNL Platform]. Uso [!DNL Query Service], puede unirse a cualquier conjunto de datos en la [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en sistemas de informes, aprendizaje automático o para su incorporación a [!DNL Real-Time Customer Profile]. Este documento proporciona una visión general de la función de [!DNL Query Service] en [!DNL Experience Platform].

[!DNL Query Service] permite a las marcas conectar el recorrido de cliente en línea a sin conexión y comprender la atribución omnicanal. El siguiente vídeo muestra cómo puede aprovechar una experiencia empresarial [!DNL Query Service] para abordar casos de uso clave y cómo [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso de [!DNL Query Service]

[!DNL Query Service] proporciona una interfaz de usuario y una API RESTful desde la cual puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a consultas guardadas por los usuarios de la organización. La interfaz de usuario está diseñada para utilizarse como simulador de pruebas para probar las consultas antes de ejecutarlas en un conjunto de datos más amplio. Más información sobre el uso del servicio interactivo en [!DNL Platform] se encuentra en la variable [Guía de la interfaz de usuario del servicio de consulta](ui/overview.md). La API de RESTful proporciona una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Más información sobre el uso de la variable [!DNL Query Service] La API se puede encontrar en la [Guía para desarrolladores de Query Service](api/getting-started.md).

## [!DNL Query Service] y [!DNL Experience Platform] servicios

[!DNL Query Service] interactúa y se puede utilizar junto con varios [!DNL Experience Platform] servicios. Para sacar el máximo partido a [!DNL Query Service's] , se recomienda que se familiarice con estos servicios y con cómo interactúan con ellos [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados dentro de [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre clientes y sus actividades, facilitando predicciones como la compra de propensión y ofertas recomendadas que el individuo probablemente aprecie y use. Puede utilizar SQL en [!DNL Data Science Workspace] integrando [!DNL Query Service] into [!DNL JupyterLab], lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea el [!DNL Data Science Workspace] información general para obtener más información [!DNL Data Science Workspace]y [!DNL Query Service] guía de integración para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permite a los usuarios dividir sus clientes en grupos más pequeños que compartan características similares. Estos segmentos pueden evaluarse posteriormente para proporcionar un mejor análisis sobre su [!DNL Real-Time Customer Profile] datos. [!DNL Query Service] se puede usar para proporcionar este análisis ejecutando consultas sobre estos datos de segmento dentro del [!DNL Data Lake]. Lea el [!DNL Segmentation Service] información general para obtener más información sobre segmentación y [!DNL Profile Query Language] (PQL) para obtener más información sobre cómo analizar segmentos.

## Casos de uso

[!DNL Query Service] proporciona un enfoque flexible para el procesamiento de datos que sirve para muchos fines. Entre otros, puede aliviar la carga de la segmentación de los especialistas en marketing y ayudar a generar audiencias procesables y perspectivas comerciales significativas. Los siguientes casos de uso ofrecen ejemplos más profundos del poder de [!DNL Query Service].

### Abandono de exploración de Adobe Analytics

Esta [el ejemplo de abandono de exploración se centra en el uso del Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) datos para crear una audiencia procesable concreta. [!DNL Query Service] incorpora lógica compleja para la segmentación con el fin de calcular varios atributos personalizados para utilizarlos de forma descendente o para simplificar en gran medida la forma en que genera sus segmentos.

### Tableros BI de consulta

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados, incluidos los datos de comportamiento, CRM y puntos de venta. Uso [!DNL Experience Platform's Query Service], puede consultar estos conjuntos de datos y responder preguntas específicas sobre el negocio y luego empezar a generar perspectivas impactantes. En el siguiente vídeo se muestra el valor de crear paneles en las herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Pasos siguientes y recursos adicionales

Al leer este documento, se le ha introducido [!DNL Query Service] y su funcionamiento dentro del bueno ámbito de aplicación [!DNL Experience Platform]. Para obtener más información sobre cómo interactuar con distintos puntos finales dentro de la variable [!DNL Query Service] API, lea la [Guía para desarrolladores de Query Service](api/getting-started.md). Para obtener más información sobre el uso del servicio interactivo en [!DNL Platform], lea la [Guía de la interfaz de usuario del servicio de consulta](ui/overview.md). Para obtener una lista completa sobre la conexión de clientes externos con [!DNL Query Service], lea la [Información general sobre los clientes del servicio de consultas](clients/overview.md).

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. En este vídeo se comparten sugerencias y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, clientes PSQL, soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
