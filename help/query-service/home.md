---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;consulta
solution: Experience Platform
title: Información general del servicio de consulta
topic: overview
description: Este documento proporciona una visión general de la función del servicio de Consulta dentro del Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Información general del [!DNL Query Service]

Adobe Experience Platform ingesta datos desde una amplia variedad de fuentes. Un desafío importante para los especialistas en mercadotecnia es darle sentido a estos datos para obtener perspectivas sobre sus clientes. Adobe Experience Platform [!DNL Query Service] facilita esto al permitirle utilizar SQL estándar para la consulta de datos en [!DNL Platform]. Mediante [!DNL Query Service], puede unir cualquier conjunto de datos en [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, aprendizaje automático o para su ingestión en [!DNL Real-time Customer Profile]. Este documento proporciona una visión general de la función de [!DNL Query Service] dentro de [!DNL Experience Platform].

[!DNL Query Service] permite que las marcas conecten el recorrido del cliente en línea con otro sin conexión y comprendan la atribución de omni-canal. El siguiente video muestra cómo un negocio de experiencia puede aprovechar [!DNL Query Service] para abordar casos de uso clave y cómo [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso de [!DNL Query Service]

[!DNL Query Service] proporciona una interfaz de usuario y una API RESTful desde la cual puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. La interfaz de usuario está pensada para utilizarse como un simulador para probar sus consultas antes de ejecutarlas en un conjunto de datos más amplio. Encontrará más información sobre el uso del servicio interactivo en [!DNL Platform] en la [Guía de interfaz de usuario del servicio de Consulta](ui/overview.md). La API de RESTful ofrece una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Encontrará más información sobre el uso de la API [!DNL Query Service] en la [guía para desarrolladores de servicios de Consulta](api/getting-started.md).

## [!DNL Query Service] y  [!DNL Experience Platform] servicios

[!DNL Query Service] interactúa y puede utilizarse junto con varios  [!DNL Experience Platform] servicios. Para aprovechar al máximo las capacidades de [!DNL Query Service's], se recomienda familiarizarse con estos servicios y con cómo interactúan con [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados dentro de [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre los clientes y sus actividades, lo que facilita predicciones como la propensión a comprar y ofertas recomendadas que el individuo probablemente apreciará y utilizará. Puede utilizar SQL dentro de [!DNL Data Science Workspace] integrando [!DNL Query Service] en [!DNL JupyterLab], lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea la [!DNL Data Science Workspace] información general para obtener más información sobre [!DNL Data Science Workspace] y la [!DNL Query Service] guía de integración para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permite a los usuarios dividir a sus clientes en grupos más pequeños que comparten características similares. Estos segmentos se pueden evaluar posteriormente para proporcionar una mejor análisis en los datos [!DNL Real-time Customer Profile]. [!DNL Query Service] se puede utilizar para proporcionar esta análisis ejecutando consultas en los datos de este segmento dentro del  [!DNL Data Lake]. Lea la [!DNL Segmentation Service] información general para obtener más información sobre la segmentación y la [!DNL Profile Query Language] guía (PQL) para obtener más información sobre cómo analizar los segmentos.

### Caso de uso de BI de buscador

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados. incluyendo datos de comportamiento, CRM y puntos de venta. Al utilizar [!DNL Experience Platform's Query Service], puede realizar consultas en estos datasets y responder preguntas específicas sobre el negocio y luego generar perspectivas impactantes para el inicio. El siguiente vídeo muestra el valor de crear paneles en herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximos pasos y recursos adicionales

Al leer este documento, se le ha presentado a [!DNL Query Service] y cómo funciona dentro del bueno ámbito de [!DNL Experience Platform]. Para obtener más información sobre cómo interactuar con varios extremos dentro de la API [!DNL Query Service], lea la [guía para desarrolladores de servicios de Consulta](api/getting-started.md). Para obtener más información sobre el uso del servicio interactivo en [!DNL Platform], lea la [Guía de interfaz de usuario del servicio de Consulta](ui/overview.md). Para obtener una lista completa sobre la conexión de clientes externos con [!DNL Query Service], lea la [información general de los clientes del servicio de Consulta](clients/overview.md).

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte consejos y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes PSQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
