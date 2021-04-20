---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 21 de abril de 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 73ecf6e6f9796088e2d14f9dc3d9667104b22a8e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 14%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 21 de abril de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la edición de asignación para flujos de datos existentes | Ahora puede actualizar los conjuntos de asignación de un flujo de datos existente. No se pueden actualizar conjuntos de asignaciones para flujos de datos programados para una ingesta única. Esta función no es compatible con la API HTTP, Adobe Analytics, Adobe Audience Manager y [!DNL Marketo Engage]. Para obtener más información, consulte el tutorial sobre la [actualización de flujos de datos de fuentes en la interfaz de usuario](../../sources/tutorials/ui/update-dataflows.md). |
| Compatibilidad con la transmisión por secuencias de ingesta | Ahora puede utilizar funciones de preparación de datos al crear una conexión de origen de flujo continuo. Para obtener más información, consulte el tutorial sobre la [creación de una conexión de origen de flujo en la interfaz de usuario](../../sources/tutorials/ui/create/streaming/http.md). |

Para obtener más información, consulte [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en los casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren predicciones específicas de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos.

### Customer AI

Customer AI disponible en la plataforma de datos del cliente en tiempo real, se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Se ha actualizado la funcionalidad para que admita conjuntos de datos de Adobe Analytics mediante el conector de origen de Analytics sin necesidad de ETL para que los datos se ajusten al esquema de Evento de experiencia del consumidor (EEC). |
| Compatibilidad con datos de Adobe Audience Manager | Se ha actualizado la funcionalidad para admitir conjuntos de datos de Adobe Audience Manager a través del conector de origen del Audience Manager sin necesidad de ETL para los datos de modo que se ajusten al esquema de Evento de experiencia del consumidor (CEE). |
| Resumen de rendimiento del modelo | La AI del cliente ahora tiene una [pestaña de resumen del rendimiento del modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) dentro de la página de perspectivas de instancias de servicio. La pestaña de rendimiento del modelo muestra todas las tasas de conversión y pérdida reales. Esto le permite descifrar y comprender lo que está sucediendo en cada uno de sus bloques de propensión. |

Para obtener más información sobre conjuntos de datos compatibles, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Se ha actualizado la funcionalidad para que admita conjuntos de datos de Adobe Analytics mediante el conector de origen de Analytics sin necesidad de ETL para que los datos se ajusten al esquema de Evento de experiencia del consumidor (EEC). |

Para obtener más información sobre conjuntos de datos compatibles, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ahora puede crear una [!DNL Marketo Engage] conexión de origen utilizando la interfaz de usuario para llevar datos B2B a Platform y mantener estos datos actualizados mediante aplicaciones conectadas a la plataforma. Para obtener más información, consulte la [[!DNL Marketo Engage] documentación del conector de origen](../../sources/connectors/adobe-applications/marketo/marketo.md). |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
