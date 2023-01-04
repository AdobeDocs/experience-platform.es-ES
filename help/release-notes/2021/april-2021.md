---
title: Notas de la versión de Adobe Experience Platform, abril de 2021
description: Notas de la versión de abril de 2021 para Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 21 de abril de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la edición de asignación para flujos de datos existentes | Ahora puede actualizar los conjuntos de asignación de un flujo de datos existente. No se pueden actualizar conjuntos de asignaciones para flujos de datos programados para una ingesta única. Esta función no es compatible con la API HTTP, Adobe Analytics, Adobe Audience Manager y [!DNL Marketo Engage]. Para obtener más información, consulte el tutorial sobre [actualización de flujos de datos de fuentes en la interfaz de usuario](../../sources/tutorials/ui/update-dataflows.md). |
| Compatibilidad con la transmisión por secuencias de ingesta | Ahora puede utilizar funciones de preparación de datos al crear una conexión de origen de flujo continuo. Para obtener más información, consulte el tutorial sobre [creación de una conexión de origen de flujo continuo en la interfaz de usuario](../../sources/tutorials/ui/create/streaming/http.md). |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

| Función | Descripción |
| --- | --- |
| Recomendaciones de esquema por sector | Al seleccionar clases y grupos de campos de esquema en la interfaz de usuario del Editor de esquemas, puede utilizar un nuevo filtro para ver los componentes estándar recomendados según su sector específico. Consulte la documentación sobre [modelos de datos del sector](https://www.adobe.com/go/xdm-industry-erds-en) para obtener más información sobre cómo se relacionan estos componentes entre sí para diferentes casos de uso del sector. |

## [!DNL Intelligent Services] {#intelligent-services}

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en los casos de uso de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones concretas de las necesidades de una compañía mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos.

### Customer AI

La AI del cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Se ha actualizado la funcionalidad para que admita conjuntos de datos de Adobe Analytics mediante el conector de origen de Analytics sin necesidad de ETL para que los datos se ajusten al esquema de Evento de experiencia del consumidor (EEC). |
| Compatibilidad con datos de Adobe Audience Manager | Se ha actualizado la funcionalidad para admitir conjuntos de datos de Adobe Audience Manager a través del conector de origen del Audience Manager sin necesidad de ETL para los datos de modo que se ajusten al esquema de Evento de experiencia del consumidor (CEE). |
| Resumen de rendimiento del modelo | La AI del cliente ahora tiene un [ficha resumen de rendimiento del modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) en la página de perspectivas de instancias de servicio. La pestaña de rendimiento del modelo muestra todas las tasas de conversión y pérdida reales. Esto le permite descifrar y comprender lo que está sucediendo en cada uno de sus bloques de propensión. |

Para obtener más información sobre los conjuntos de datos compatibles, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Se ha actualizado la funcionalidad para que admita conjuntos de datos de Adobe Analytics mediante el conector de origen de Analytics sin necesidad de ETL para que los datos se ajusten al esquema de Evento de experiencia del consumidor (EEC). |

Para obtener más información sobre los conjuntos de datos compatibles, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-Time Customer Profile] datos. Estos segmentos están configurados y mantenidos de forma centralizada en Platform, lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones adicionales de agregación | Se han añadido funciones de recuento en el Generador de segmentos. Las funciones de recuento permiten contabilizar el número de veces que se ha realizado el evento especificado. Puede encontrar más información sobre las funciones de recuento en la sección funciones de recuento de la sección [Guía del Generador de segmentos](../../segmentation/ui/segment-builder.md#count-functions) |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ahora puede crear un [!DNL Marketo Engage] conexión de origen mediante la interfaz de usuario para llevar datos B2B a Platform y mantener estos datos actualizados mediante aplicaciones conectadas a la plataforma. Para obtener más información, consulte la [[!DNL Marketo Engage] documentación del conector de origen](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
