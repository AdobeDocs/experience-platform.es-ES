---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consulta
solution: Experience Platform
title: Introducción al servicio de consultas
description: Obtenga información acerca de la función del servicio de consultas dentro del Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Introducción al servicio de consultas

Adobe Experience Platform ingiere datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en marketing es dar sentido a estos datos para obtener perspectivas sobre sus clientes. Para consultar datos en Platform, puede utilizar SQL estándar y Adobe Experience Platform Query Service. Puede utilizar el servicio de consulta para unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, el aprendizaje automático o para su inserción en [!DNL Real-Time Customer Profile]. Este documento proporciona información general sobre la función que desempeña el servicio de consultas dentro del Experience Platform.

Puede utilizar el servicio de consultas para conectar el recorrido del cliente con conexión y comprender la atribución omnicanal de su marca. El siguiente vídeo muestra cómo una empresa de experiencia puede utilizar el servicio de consultas para tratar casos de uso clave y cómo funciona el servicio de consultas.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso del servicio de consultas {#usage}

Para analizar los datos, cree y ejecute consultas SQL con la interfaz de usuario del servicio de consultas o la API de RESTful.
Con la interfaz de usuario del servicio de consultas puede escribir, ejecutar y programar consultas, ver consultas ejecutadas anteriormente y acceder a las guardadas por usuarios de su organización. También puede probar las consultas antes de ejecutarlas en su conjunto de datos más amplio con el Editor de consultas. Consulte la [Guía de IU del servicio de consultas](ui/overview.md) para obtener información general sobre la funcionalidad de la interfaz de usuario.

La API de RESTful proporciona una experiencia similar. Puede utilizar la API del servicio de consultas para escribir y ejecutar consultas mediante programación, crear y guardar plantillas para consultas que desee adaptar o programar consultas para ejecución automatizada. Consulte la [Guía para desarrolladores de Query Service](api/getting-started.md) para obtener más información sobre el uso de la API del servicio de consultas.

Para empezar a utilizar rápidamente las funciones del servicio de consultas, se recomienda leer los siguientes documentos:

- [Directrices generales para la ejecución de consultas](./best-practices/writing-queries.md)
- [Sintaxis SQL en el servicio de consultas](./sql/syntax.md)
- [Crear conjuntos de datos derivados con SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Servicio de consultas y servicios de Experience Platform {#experience-platform-services}

El servicio de consulta interactúa y se puede utilizar con varios servicios de Experience Platform. Para sacar el máximo partido a las capacidades del servicio de consultas, debe familiarizarse con estos servicios y con cómo interactúan con él. El [Página de aterrizaje de documentación del Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=es) proporciona resúmenes y vínculos a las funcionalidades de la plataforma.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener perspectivas de los datos almacenados en Experience Platform. Los científicos de datos pueden usar el [!DNL Data Science Workspace] para crear fórmulas basadas en datos de registros y series temporales acerca de los clientes y sus actividades. Estas recetas facilitan las predicciones, como la tendencia a comprar y las ofertas recomendadas que el individuo probablemente aprecie y utilice. Puede usar SQL en [!DNL Data Science Workspace] integrando el servicio de consultas en [!DNL JupyterLab] para explorar, transformar y analizar datos de Adobe Analytics. Lea el [[!DNL Data Science Workspace] descripción general](../data-science-workspace/home.md) y el [Guía de conexión de Jupyter Notebook](./clients/jupyter-notebook.md) para obtener más información acerca de cómo [!DNL Data Science Workspace] interactúa con el servicio de consultas.

### [!DNL Segmentation Service] {#segmentation}

Utilice el servicio de segmentación de Adobe Experience Platform para dividir los clientes en grupos más pequeños que compartan características similares. Estas audiencias se pueden evaluar para proporcionar un mejor análisis de los datos del perfil del cliente en tiempo real. Puede utilizar el servicio de consultas para ejecutar consultas sobre estos datos de audiencia dentro del lago de datos y proporcionar el análisis. Lea el [Resumen del servicio de segmentación](../segmentation/home.md) y el [[!DNL Profile Query Language] Guía de (PQL)](../segmentation/pql/overview.md) para obtener más información sobre cómo analizar audiencias.

## Casos de uso {#use-cases}

El servicio de consultas ofrece un enfoque flexible para el procesamiento de datos que cumple muchos propósitos. Entre otros, puede aliviar la carga de segmentación de los especialistas en marketing y ayudar a generar audiencias procesables y perspectivas comerciales significativas. Los siguientes casos de uso ofrecen ejemplos más detallados de la potencia del servicio de consultas.

### Abandono de exploración de Adobe Analytics {#abandon-browse}

Esta [el ejemplo de abandono de la exploración se centra en el uso del Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) datos para crear una audiencia procesable concreta. El servicio de consulta admite una lógica compleja para la segmentación a fin de calcular varios atributos personalizados para su uso descendente o para simplificar en gran medida la forma en que se crean las audiencias.

## Generación de perspectivas con paneles personalizados {#custom-dashboards}

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados, incluidos los datos de comportamiento, CRM y de punto de venta. Uso de [!DNL Experience Platform's Query Service], puede consultar estos conjuntos de datos y responder preguntas específicas sobre el negocio y, a continuación, empezar a generar perspectivas impactantes. Obtenga información sobre cómo crear y administrar paneles personalizados, donde puede crear, añadir y editar widgets personalizados para visualizar métricas clave con [paneles definidos por el usuario](../dashboards/user-defined-dashboards.md). Incluso puede [personalizar sus propios informes de Real-Time CDP](../dashboards/data-models/cdp-insights-data-model-b2c.md) para los casos de uso de marketing y KPI mediante consultas SQL con los modelos de datos de Real-time Customer Data Platform Insights.

## Pasos siguientes y recursos adicionales

Al leer este documento, se le ha presentado el Servicio de consultas y cómo funciona dentro del ámbito más amplio de Experience Platform. Para continuar aprendiendo sobre las funciones del servicio de consultas, se recomienda leer los siguientes documentos:

- El [Guía para desarrolladores de Query Service](api/getting-started.md): para obtener más información sobre cómo interactuar con varios extremos dentro de la API del servicio de consultas.
- El [Guía de la interfaz de usuario del servicio de consultas](ui/overview.md): para obtener más información sobre el uso del Editor de consultas y la IU.
- El [Información general sobre clientes de Query Service](clients/overview.md): Para obtener una lista completa de clientes externos para conectarse con el servicio de consultas.

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte sugerencias y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes SQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
