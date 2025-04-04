---
title: Notas de la versión de Adobe Experience Platform, agosto de 2020
description: Las notas de la versión de agosto de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: jueves, 12 de agosto de 2020**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener información de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a hacer predicciones utilizando sus activos de contenido y datos en todas las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se mejoró la estabilidad de [!DNL JupyterLab notebook] máquinas virtuales de larga ejecución. |

Para obtener más información sobre [!DNL JupyterLab], consulte la [[!DNL JupyterLab] guía del usuario](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

En [Real-Time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera perfecta.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación para obtener más información:

| Destino | Descripción |
|--- | ---|
| [!DNL Google Customer Match] | Customer Match de Google le permite utilizar sus datos con y sin conexión para llegar a sus clientes y volver a interactuar con ellos en las propiedades de Google que posee y gestiona, como: [!DNL Search], [!DNL Shopping], Gmail y YouTube. <br><br> Visite la [!DNL Google Customer Match] [página](../../destinations/catalog/advertising/google-customer-match.md) en el catálogo de destinos para obtener más información acerca del destino y cómo configurarlo en Real-Time CDP. |

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Editor de nombres de archivo personalizado | Actualización del flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que le permite editar el nombre de los archivos exportados. Para obtener más información, consulte [Configurar paso](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |
| Atributos recomendados | Actualice el flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que muestra atributos recomendados para que los agregue a los archivos exportados. Para obtener más información, consulte el [paso Seleccionar atributos](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

El compilado en Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido del cliente. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con IAB TCF 2.0 | [!DNL Real-Time CDP] es ahora un proveedor registrado para la versión 2.0 de [!DNL Transparency & Consent Framework] (TCF), como lo describe [!DNL Interactive Advertising Bureau] (IAB). Puede configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por una CMP y aplicar las preferencias de consentimiento de los clientes al activar segmentos en destinos descendentes. |

Para obtener más información sobre [!DNL Real-Time CDP], consulte la [[!DNL Real-Time CDP] información general](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Monitorización de ejecución de flujo | Los usuarios pueden monitorizar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y las métricas. Consulte el documento [monitorización de flujos de datos](../../sources/tutorials/ui/monitor.md) para obtener más información. |
| Notificaciones de ejecución de flujo | Los usuarios pueden suscribirse a eventos y registrar webhooks para recibir notificaciones en tiempo real sobre el estado, las métricas y los errores relacionados con las ejecuciones de flujo. |
| Mejoras del catálogo de IU | Se actualiza la pantalla del catálogo de fuentes para facilitar el acceso a las acciones principales de los objetos seleccionados. |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
