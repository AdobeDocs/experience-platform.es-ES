---
title: Notas de la versión de Adobe Experience Platform, abril de 2021
description: Las notas de la versión de abril de 2021 de Adobe Experience Platform.
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
| Compatibilidad con la edición de asignación para flujos de datos existentes | Ahora puede actualizar los conjuntos de asignaciones de un flujo de datos existente. No puede actualizar los conjuntos de asignaciones para flujos de datos programados para una ingesta única. Esta función no es compatible con la API HTTP, Adobe Analytics, Adobe Audience Manager y [!DNL Marketo Engage]. Para obtener más información, consulte el tutorial sobre [actualización de flujos de datos de origen en la IU](../../sources/tutorials/ui/update-dataflows.md). |
| Compatibilidad con la ingesta por streaming | Ahora puede utilizar las funciones de preparación de datos al crear una conexión de origen de flujo continuo. Para obtener más información, consulte el tutorial sobre [creación de una conexión de origen de flujo continuo en la IU](../../sources/tutorials/ui/create/streaming/http.md). |

Para obtener más información, consulte la [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

| Función | Descripción |
| --- | --- |
| Recomendaciones de esquemas por sector | Al seleccionar clases y grupos de campos de esquema en la interfaz de usuario del Editor de esquemas, puede utilizar un nuevo filtro para ver los componentes estándar recomendados en función de su sector específico. Consulte la documentación sobre [modelos de datos del sector](https://www.adobe.com/go/xdm-industry-erds-en) para obtener más información sobre cómo se relacionan entre sí estos componentes para diferentes casos de uso del sector. |

## [!DNL Intelligent Services] {#intelligent-services}

Los servicios inteligentes permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones concretas de las necesidades de una compañía mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos.

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Funcionalidad actualizada para admitir conjuntos de datos de Adobe Analytics a través del conector de origen de Analytics sin necesidad de extraer los datos para cumplir con el esquema de Evento de experiencia del consumidor (CEE). |
| Compatibilidad con datos de Adobe Audience Manager | Funcionalidad actualizada para admitir conjuntos de datos de Adobe Audience Manager a través del conector de origen del Audience Manager sin necesidad de extraer los datos para cumplir con el esquema de Evento de experiencia del consumidor (CEE). |
| Resumen de rendimiento del modelo | La inteligencia artificial aplicada al cliente ahora tiene un [pestaña resumen de rendimiento del modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) en la página de información de la instancia de servicio. La pestaña de rendimiento del modelo muestra todas las tasas de conversión y de pérdida reales. Esto le permite descifrar y comprender qué está pasando en cada uno de sus bloques de tendencia. |

Para obtener más información sobre los conjuntos de datos admitidos, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con datos de Adobe Analytics | Funcionalidad actualizada para admitir conjuntos de datos de Adobe Analytics a través del conector de origen de Analytics sin necesidad de extraer los datos para cumplir con el esquema de Evento de experiencia del consumidor (CEE). |

Para obtener más información sobre los conjuntos de datos admitidos, consulte la [[!DNL Intelligent Services] documentación de preparación de datos](../../intelligent-services/data-preparation.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de [!DNL Real-Time Customer Profile] datos. Estos segmentos se configuran y mantienen de forma centralizada en Platform, lo que hace que cualquier aplicación de Adobe pueda acceder fácilmente a ellos.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones de agregación adicionales | Se han añadido funciones de recuento en el Generador de segmentos. Las funciones de recuento permiten contar el número de veces que se ha realizado el evento especificado. Encontrará más información sobre las funciones de recuento en la sección de funciones de recuento de [Guía del Generador de segmentos](../../segmentation/ui/segment-builder.md#count-functions) |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ahora puede crear un [!DNL Marketo Engage] conexión de origen mediante la interfaz de usuario para llevar los datos B2B a Platform y mantenerlos actualizados mediante aplicaciones conectadas a Platform. Para obtener más información, consulte la [[!DNL Marketo Engage] documentación del conector de origen](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Fuentes beta que se trasladan a GA | Las siguientes fuentes se han promocionado de beta a GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
