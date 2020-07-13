---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servicio de Consulta de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Visión general del servicio de Consulta

Adobe Experience Platform ingesta datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en mercadotecnia es darle sentido a estos datos para obtener perspectivas sobre sus clientes. El servicio de Consulta de Adobe Experience Platform facilita esto al permitirle utilizar SQL estándar para la consulta de datos en Platform. Con el servicio de Consulta, puede unirse a cualquier conjunto de datos en Data Lake y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, aprendizaje automático o para su inserción en el Perfil del cliente en tiempo real. Este documento proporciona una visión general de la función del servicio de Consulta dentro del Experience Platform.

El servicio de Consulta permite que las marcas conecten el viaje de los clientes en línea a fuera de línea y comprendan la atribución de omni-canal. El siguiente vídeo muestra cómo un negocio de experiencia puede aprovechar el servicio de Consulta para abordar casos de uso clave y cómo funciona el servicio de Consulta.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso del servicio de Consulta

El servicio de Consulta proporciona una interfaz de usuario y una API RESTful desde la que puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. La interfaz de usuario está pensada para utilizarse como un simulador para probar sus consultas antes de ejecutarlas en un conjunto de datos más amplio. Puede encontrar más información sobre el uso del servicio interactivo en Platform en la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. La API de RESTful ofrece una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Encontrará más información sobre el uso de la API de servicio de Consulta en la guía [para desarrolladores de](api/getting-started.md)Consulta Service.

## Servicios de Consulta y servicios de Experience Platform

El servicio de Consulta interactúa y puede utilizarse junto con varios servicios de Experience Platform. Para aprovechar al máximo las capacidades del Servicio de Consulta, se recomienda familiarizarse con estos servicios y con la forma en que interactúan con el Servicio de Consulta.

### Área de trabajo de ciencia de datos

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados en el Experience Platform. Data Science Workspace permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre los clientes y sus actividades, lo que facilita predicciones como la propensión a comprar y ofertas recomendadas que el individuo probablemente apreciará y utilizará. Puede utilizar SQL dentro de Data Science Workspace integrando el servicio de Consulta en JupyterLab, lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea la información general de Área de trabajo de ciencia de datos para obtener más información sobre Área de trabajo de ciencia de datos y la guía de integración de servicio de Consulta para obtener más información sobre cómo interactúa Área de trabajo de ciencia de datos con el servicio de Consulta.

### Servicio de segmentación

El servicio de segmentación por Adobe Experience Platform permite a los usuarios dividir a sus clientes en grupos más pequeños que comparten características similares. Estos segmentos se pueden evaluar posteriormente para proporcionar una mejor análisis en los datos de Perfil del cliente en tiempo real. El servicio de Consulta se puede utilizar para proporcionar esta análisis mediante la ejecución de consultas en los datos de este segmento dentro del Data Lake. Lea la descripción general del servicio de segmentación para obtener más información sobre la segmentación y la guía del lenguaje de Consulta de Perfil (PQL) para obtener más información sobre cómo analizar los segmentos.

### Caso de uso de BI de buscador

Con Adobe Experience Platform, puede ingerir, almacenar, estructurar y extraer todos los conjuntos de datos almacenados. incluyendo datos de comportamiento, CRM y puntos de venta. Con [!DNL Experience Platform's Query Service], puede realizar consultas en estos conjuntos de datos y responder preguntas específicas sobre el negocio y luego generar perspectivas de impacto en los inicios. En el siguiente vídeo se muestra el valor de crear paneles en las herramientas de inteligencia empresarial (BI) mediante [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximos pasos y recursos adicionales

Al leer este documento, usted ha sido presentado al Servicio de Consulta y cómo funciona dentro del bueno ámbito de Experience Platform. Para obtener más información sobre la interacción con varios extremos dentro de la API de servicio de Consulta, lea la guía [para desarrolladores de](api/getting-started.md)Consulta Service. Para obtener más información sobre el uso del servicio interactivo en Platform, lea la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. Para obtener una lista completa sobre la conexión de clientes externos con el servicio de Consulta, lea la descripción general [de los clientes del servicio de](clients/overview.md)Consulta.

Para prepararse mejor para ejecutar consultas, vea el siguiente vídeo. Este vídeo comparte consejos y prácticas recomendadas para ejecutar consultas en la interfaz del editor de consultas, los clientes PSQL, las soluciones de inteligencia empresarial (BI) y la API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
