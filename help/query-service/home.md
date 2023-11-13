---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consulta
solution: Experience Platform
title: Información general del servicio de consultas
description: Este documento proporciona información general sobre la función que desempeña el servicio de consultas dentro del Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Información general del [!DNL Query Service]

Adobe Experience Platform ingiere datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en marketing es dar sentido a estos datos para obtener perspectivas sobre sus clientes. Adobe Experience Platform [!DNL Query Service] facilita esto al permitirle utilizar SQL estándar para consultar datos en [!DNL Platform]. Uso de [!DNL Query Service], puede unirse a cualquier conjunto de datos de [!DNL Data Lake] y capture los resultados de la consulta como un nuevo conjunto de datos para utilizarlo en la creación de informes, el aprendizaje automático o para su incorporación en [!DNL Real-Time Customer Profile]. Este documento proporciona información general sobre la función de [!DNL Query Service] dentro [!DNL Experience Platform].

[!DNL Query Service] permite a las marcas conectar el recorrido del cliente con conexión y comprender la atribución omnicanal. El siguiente vídeo muestra cómo puede aprovechar una empresa de experiencias [!DNL Query Service] para tratar casos de uso clave y cómo [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso de [!DNL Query Service]

[!DNL Query Service] proporciona una interfaz de usuario y una API RESTful desde la cual puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario de, puede escribir y ejecutar consultas, ver consultas ejecutadas anteriormente y acceder a las guardadas por usuarios de su organización. La interfaz de usuario está diseñada para utilizarse como zona protegida para probar las consultas antes de ejecutarlas en el conjunto de datos más amplio. Más información sobre el uso del servicio interactivo en [!DNL Platform] se puede encontrar en la [Guía de la interfaz de usuario del servicio de consultas](ui/overview.md). La API de RESTful proporciona una experiencia similar, lo que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para las consultas que desee escribir. Más información sobre el uso de [!DNL Query Service] La API se encuentra en [Guía para desarrolladores de Query Service](api/getting-started.md).

## [!DNL Query Service] y [!DNL Experience Platform] servicios

[!DNL Query Service] interactúa y se puede utilizar junto con varios [!DNL Experience Platform] servicios. Para sacar el máximo partido a [!DNL Query Service's] funciones, se recomienda que se familiarice con estos servicios y con cómo interactúan con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener perspectivas de los datos almacenados en [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales acerca de los clientes y sus actividades, lo que facilita predicciones como la tendencia a comprar y ofertas recomendadas que el individuo probablemente aprecie y utilice. Puede usar SQL en [!DNL Data Science Workspace] al integrar [!DNL Query Service] en [!DNL JupyterLab], lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea el [!DNL Data Science Workspace] información general para obtener más información acerca de [!DNL Data Science Workspace], y el [!DNL Query Service] guía de integración para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permite a los usuarios dividir sus clientes en grupos más pequeños que comparten características similares. Estas audiencias pueden evaluarse posteriormente para proporcionar un mejor análisis de su [!DNL Real-Time Customer Profile] datos. [!DNL Query Service] se puede usar para proporcionar este análisis ejecutando consultas sobre estos datos de audiencia en el [!DNL Data Lake]. Lea el [!DNL Segmentation Service] información general para obtener más información sobre la segmentación y la [!DNL Profile Query Language] Guía de (PQL) para obtener más información sobre cómo analizar audiencias.

## Casos de uso

[!DNL Query Service] proporciona un enfoque flexible al procesamiento de datos que sirve para muchos fines. Entre otros, puede aliviar la carga de segmentación de los especialistas en marketing y ayudar a generar audiencias procesables y perspectivas comerciales significativas. Los siguientes casos de uso ofrecen ejemplos más detallados del poder de [!DNL Query Service].

### Abandono de exploración de Adobe Analytics

Esta [el ejemplo de abandono de la exploración se centra en el uso del Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) datos para crear una audiencia procesable concreta. [!DNL Query Service] admite una lógica compleja para la segmentación a fin de calcular varios atributos personalizados para su uso descendente o para simplificar en gran medida la forma de crear audiencias.

### Paneles de Looker BI

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados, incluidos los datos de comportamiento, CRM y de punto de venta. Uso de [!DNL Experience Platform's Query Service], puede consultar estos conjuntos de datos y responder preguntas específicas sobre el negocio y, a continuación, empezar a generar perspectivas impactantes. El siguiente vídeo muestra el valor de crear paneles en las herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Pasos siguientes y recursos adicionales

Al leer este documento, se le ha presentado a [!DNL Query Service] y cómo funciona dentro del ámbito más amplio de [!DNL Experience Platform]. Para obtener más información sobre cómo interactuar con varios extremos dentro de la variable [!DNL Query Service] API, lea la [Guía para desarrolladores de Query Service](api/getting-started.md). Para obtener más información sobre el uso del servicio interactivo en [!DNL Platform], lea la [Guía de la interfaz de usuario del servicio de consultas](ui/overview.md). Para obtener una lista completa de cómo conectar clientes externos con [!DNL Query Service], lea la [Información general sobre clientes de Query Service](clients/overview.md).

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte sugerencias y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes SQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
