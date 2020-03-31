---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servicio de Consulta de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Visión general del servicio de Consulta

Adobe Experience Platform transfiere datos de una amplia variedad de fuentes. Un desafío importante para los especialistas en mercadotecnia es darle sentido a estos datos para obtener perspectivas sobre sus clientes. El servicio de Consulta de la plataforma Adobe Experience Platform facilita esto al permitirle utilizar SQL estándar para la consulta de datos en la plataforma. Con el servicio de Consulta, puede unirse a cualquier conjunto de datos en Data Lake y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, aprendizaje automático o para su inserción en el Perfil del cliente en tiempo real. Este documento proporciona una visión general de la función del servicio de Consulta en la plataforma de experiencias.

## Uso del servicio de Consulta

El servicio de Consulta proporciona una interfaz de usuario y una API RESTful desde la que puede crear consultas SQL para analizar mejor los datos. Con la interfaz de usuario, puede escribir y ejecutar consultas, vista de consultas ejecutadas anteriormente y acceso a consultas guardadas por usuarios dentro de la organización de IMS. La interfaz de usuario está pensada para utilizarse como un simulador para probar sus consultas antes de ejecutarlas en un conjunto de datos más amplio. Puede encontrar más información sobre el uso del servicio interactivo en Platform en la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. La API de RESTful ofrece una experiencia similar, que le permite escribir y ejecutar consultas mediante programación, programar consultas para uso y repetición futuros, así como crear plantillas para consultas que desee escribir. Encontrará más información sobre el uso de la API de servicio de Consulta en la guía [para desarrolladores de](api/getting-started.md)Consulta Service.

## Servicios de Consulta y de plataforma de experiencia

El servicio de Consulta interactúa y se puede utilizar junto con varios servicios de la plataforma de experiencias. Para aprovechar al máximo las capacidades del Servicio de Consulta, se recomienda familiarizarse con estos servicios y con la forma en que interactúan con el Servicio de Consulta.

### Área de trabajo de ciencia de datos

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados en la plataforma de experiencia. Data Science Workspace permite a los científicos de datos crear fórmulas basadas en datos de registros y series temporales sobre los clientes y sus actividades, lo que facilita predicciones como la propensión a comprar y ofertas recomendadas que el individuo probablemente apreciará y utilizará. Puede utilizar SQL en el área de trabajo de Data Science integrando el servicio de Consulta en JupyterLab, lo que le permite explorar, transformar y analizar datos de Adobe Analytics. Lea la información general de Área de trabajo de ciencia de datos para obtener más información sobre Área de trabajo de ciencia de datos y la guía de integración de servicio de Consulta para obtener más información sobre cómo interactúa Área de trabajo de ciencia de datos con el servicio de Consulta.

### Servicio de segmentación

El servicio de segmentación de plataformas de Adobe Experience Manager permite a los usuarios dividir a sus clientes en grupos más pequeños que comparten características similares. Estos segmentos se pueden evaluar posteriormente para proporcionar una mejor análisis en los datos de Perfil del cliente en tiempo real. El servicio de Consulta se puede utilizar para proporcionar esta análisis mediante la ejecución de consultas en los datos de este segmento dentro del Data Lake. Lea la descripción general del servicio de segmentación para obtener más información sobre la segmentación y la guía del lenguaje de Consulta de Perfil (PQL) para obtener más información sobre cómo analizar los segmentos.

## Pasos siguientes

Al leer este documento, se le ha presentado el servicio de Consulta y cómo funciona dentro del bueno ámbito de la plataforma de experiencias. Para obtener más información sobre la interacción con varios extremos dentro de la API de servicio de Consulta, lea la guía [para desarrolladores de](api/getting-started.md)Consulta Service. Para obtener más información sobre el uso del servicio interactivo en Platform, lea la guía [de interfaz de usuario del servicio de](ui/overview.md)Consulta. Para obtener una lista completa sobre la conexión de clientes externos con el servicio de Consulta, lea la descripción general [de los clientes del servicio de](clients/overview.md)Consulta.
