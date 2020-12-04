---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Servicio de Consulta de Adobe Experience Platform
topic: overview
description: Este documento proporciona una visión general de la función del servicio de Consulta dentro del Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# [!DNL Query Service]sobre validación

Adobe Experience Platform ingesta datos desde una amplia variedad de fuentes. Un desafío importante para los especialistas en mercadotecnia es darle sentido a estos datos para obtener perspectivas sobre sus clientes. Adobe Experience Platform [!DNL Query Service] lo facilita al permitirle utilizar SQL estándar para la consulta de datos en [!DNL Platform]. Con [!DNL Query Service], puede unir cualquier conjunto de datos en el [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en el sistema de informes, el aprendizaje automático o la ingestión en [!DNL Real-time Customer Profile]. Este documento proporciona una visión general de la función de [!DNL Query Service] dentro de [!DNL Experience Platform].

[!DNL Query Service] permite que las marcas conecten el viaje de los clientes en línea y sin conexión y comprendan la atribución de omni-canal. El siguiente vídeo muestra cómo un negocio de experiencia puede aprovechar [!DNL Query Service] para abordar casos de uso clave y cómo [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] proporciona una interfaz de usuario y una API RESTful desde la cual puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. La interfaz de usuario está pensada para utilizarse como un simulador para probar sus consultas antes de ejecutarlas en un conjunto de datos más amplio. Encontrará más información sobre el uso del servicio interactivo en [!DNL Platform] la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. La API de RESTful ofrece una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Encontrará más información sobre el uso de la [!DNL Query Service] API en la guía [para desarrolladores de](api/getting-started.md)Consulta Service.

## [!DNL Query Service] y [!DNL Experience Platform] servicios

[!DNL Query Service] interactúa y puede utilizarse junto con varios [!DNL Experience Platform] servicios. Para aprovechar al máximo [!DNL Query Service's] las capacidades, se recomienda familiarizarse con estos servicios y con cómo interactúan con ellos [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados en [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre los clientes y sus actividades, lo que facilita predicciones como la propensión a comprar y ofertas recomendadas que el individuo probablemente apreciará y utilizará. Puede utilizar SQL en [!DNL Data Science Workspace] la integración [!DNL Query Service] en [!DNL JupyterLab], lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea la [!DNL Data Science Workspace] información general para obtener más información sobre [!DNL Data Science Workspace]y la guía de [!DNL Query Service] integración para obtener más información sobre cómo [!DNL Data Science Workspace] interactúa con [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permite a los usuarios dividir a sus clientes en grupos más pequeños que comparten características similares. Estos segmentos pueden evaluarse posteriormente para proporcionar una mejor análisis en sus [!DNL Real-time Customer Profile] datos. [!DNL Query Service] se puede utilizar para proporcionar esta análisis ejecutando consultas en los datos de este segmento dentro del [!DNL Data Lake]. Lea la información general [!DNL Segmentation Service] para obtener más información sobre la segmentación y la guía [!DNL Profile Query Language] (PQL) para obtener más información sobre cómo analizar los segmentos.

### Caso de uso de BI de buscador

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados. incluyendo datos de comportamiento, CRM y puntos de venta. Con [!DNL Experience Platform's Query Service], puede realizar consultas en estos conjuntos de datos y responder preguntas específicas sobre el negocio y luego generar perspectivas de impacto en los inicios. En el siguiente vídeo se muestra el valor de crear paneles en las herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximos pasos y recursos adicionales

Al leer este documento, se le ha presentado [!DNL Query Service] y cómo funciona dentro del bueno ámbito de [!DNL Experience Platform]. Para obtener más información sobre la interacción con varios extremos dentro de la [!DNL Query Service] API, consulte la guía [para desarrolladores de](api/getting-started.md)Consulta Service. Para obtener más información sobre el uso del servicio interactivo en [!DNL Platform], lea la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. Para obtener una lista completa sobre la conexión de clientes externos con [!DNL Query Service], lea la descripción general [de los clientes del servicio de](clients/overview.md)Consulta.

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte consejos y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes PSQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
