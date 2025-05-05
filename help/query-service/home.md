---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consulta
solution: Experience Platform
title: Introducción al servicio de consultas
description: Obtenga información acerca de la función que desempeña el servicio de consultas en Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Introducción al servicio de consultas

Adobe Experience Platform ingiere datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en marketing es dar sentido a estos datos para obtener perspectivas sobre sus clientes. Para consultar datos en Experience Platform, puede utilizar SQL estándar y Adobe Experience Platform Query Service. Puede usar el Servicio de consultas para unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, el aprendizaje automático o para su inserción en [!DNL Real-Time Customer Profile]. Este documento proporciona información general sobre la función que desempeña el servicio de consultas en Experience Platform.

Puede utilizar el servicio de consultas para conectar el recorrido del cliente con conexión y comprender la atribución omnicanal de su marca. El siguiente vídeo muestra cómo una empresa de experiencia puede utilizar el servicio de consultas para tratar casos de uso clave y cómo funciona el servicio de consultas.

>[!VIDEO](https://video.tv.adobe.com/v/33590?quality=12&learn=on&captions=spa)

## Uso del servicio de consultas {#usage}

Para analizar los datos, cree y ejecute consultas SQL con la interfaz de usuario del servicio de consultas o la API de RESTful.
Con la interfaz de usuario del servicio de consultas puede escribir, ejecutar y programar consultas, ver consultas ejecutadas anteriormente y acceder a las guardadas por usuarios de su organización. También puede probar las consultas antes de ejecutarlas en su conjunto de datos más amplio con el Editor de consultas. Consulte la [guía de IU del servicio de consultas](ui/overview.md) para obtener una descripción general de la funcionalidad de la IU.

La API de RESTful proporciona una experiencia similar. Puede utilizar la API del servicio de consultas para escribir y ejecutar consultas mediante programación, crear y guardar plantillas para consultas que desee adaptar o programar consultas para ejecución automatizada. Consulte la [Guía para desarrolladores de Query Service](api/getting-started.md) para obtener más información sobre el uso de la API de Query Service.

Para empezar a utilizar rápidamente las funciones del servicio de consultas, se recomienda leer los siguientes documentos:

- [Directrices generales para la ejecución de consultas](./best-practices/writing-queries.md)
- [Sintaxis SQL en el servicio de consultas](./sql/syntax.md)
- [Crear conjuntos de datos derivados con SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Servicio de consultas y servicios de Experience Platform {#experience-platform-services}

El servicio de consulta interactúa y se puede utilizar con varios servicios de Experience Platform. Para sacar el máximo partido a las capacidades del servicio de consultas, debe familiarizarse con estos servicios y con cómo interactúan con él. La [página de aterrizaje de documentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es) proporciona resúmenes y vínculos a las capacidades de la plataforma.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener información de los datos almacenados en Experience Platform. Los científicos de datos pueden usar [!DNL Data Science Workspace] para generar fórmulas basadas en datos de registros y series temporales acerca de los clientes y sus actividades. Estas recetas facilitan las predicciones, como la tendencia a comprar y las ofertas recomendadas que el individuo probablemente aprecie y utilice. Puede usar SQL en [!DNL Data Science Workspace] integrando Query Service en [!DNL JupyterLab] para explorar, transformar y analizar datos de Adobe Analytics. Lea la [[!DNL Data Science Workspace] descripción general](../data-science-workspace/home.md) y la [guía de conexión de Jupyter Notebook](./clients/jupyter-notebook.md) para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con el servicio de consultas.

### [!DNL Segmentation Service] {#segmentation}

Utilice el servicio de segmentación de Adobe Experience Platform para dividir los clientes en grupos más pequeños que compartan características similares. Estas audiencias se pueden evaluar para proporcionar un mejor análisis de los datos del perfil del cliente en tiempo real. Puede utilizar el servicio de consultas para ejecutar consultas sobre estos datos de audiencia dentro del lago de datos y proporcionar el análisis. Lea la [descripción general del servicio de segmentación](../segmentation/home.md) y la guía [[!DNL Profile Query Language] (PQL)](../segmentation/pql/overview.md) para obtener más información sobre cómo analizar audiencias.

## Casos de uso {#use-cases}

El servicio de consultas ofrece un enfoque flexible para el procesamiento de datos que cumple muchos propósitos. Entre otros, puede aliviar la carga de segmentación de los especialistas en marketing y ayudar a generar audiencias procesables y perspectivas comerciales significativas. Los siguientes casos de uso ofrecen ejemplos más detallados de la potencia del servicio de consultas.

### Abandono de exploración de Adobe Analytics {#abandon-browse}

Este ejemplo de [abandono de exploración se centra en el uso de datos de Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) para crear una audiencia procesable en particular. El servicio de consulta admite una lógica compleja para la segmentación a fin de calcular varios atributos personalizados para su uso descendente o para simplificar en gran medida la forma en que se crean las audiencias.

## Generación de perspectivas con paneles personalizados {#custom-dashboards}

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados, incluidos los datos de comportamiento, CRM y de punto de venta. Con [!DNL Experience Platform's Query Service], puede consultar estos conjuntos de datos y responder preguntas específicas sobre la empresa y, a continuación, empezar a generar perspectivas impactantes. Aprenda a crear y administrar paneles personalizados, donde puede crear, agregar y editar widgets personalizados para visualizar métricas clave con [paneles definidos por el usuario](../dashboards/standard-dashboards.md). Incluso puede [personalizar sus propios informes de Real-Time CDP](../dashboards/data-models/cdp-insights-data-model-b2c.md) para los casos de uso de KPI y marketing mediante consultas SQL con los modelos de datos de Real-Time Customer Data Platform Insights.

## Pasos siguientes y recursos adicionales

Al leer este documento, se le ha presentado el Servicio de consultas y cómo funciona dentro del ámbito general de Experience Platform. Para continuar aprendiendo sobre las funciones del servicio de consultas, se recomienda leer los siguientes documentos:

- La [guía para desarrolladores de Query Service](api/getting-started.md): Para obtener más información sobre cómo interactuar con varios extremos dentro de la API de Query Service.
- La [guía de interfaz de usuario del servicio de consultas](ui/overview.md): Para obtener más información sobre cómo usar el Editor de consultas y la interfaz de usuario.
- Información general sobre los clientes de [Query Service](clients/overview.md): para obtener una lista completa de clientes externos para conectarse al servicio de consultas.

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte sugerencias y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes SQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/33588?quality=12&learn=on&captions=spa)
