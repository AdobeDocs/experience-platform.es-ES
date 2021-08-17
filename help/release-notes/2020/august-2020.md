---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 12 de agosto de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para extraer perspectivas de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se ha mejorado la estabilidad de las [!DNL JupyterLab notebook] máquinas virtuales de larga duración. |

Para obtener más información sobre [!DNL JupyterLab], consulte la [[!DNL JupyterLab] guía del usuario](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

En la [Plataforma de datos del cliente en tiempo real](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a esos socios de una manera transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match le permite utilizar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en las propiedades de Google y en las que opera, como: [!DNL Search], [!DNL Shopping], Gmail y YouTube. <br><br> Visite la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) página del catálogo de destinos para obtener más información sobre el destino y cómo configurarlo en CDP en tiempo real. |

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Editor de nombres de archivo personalizado | Actualice al flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que le permiten editar el nombre de los archivos exportados. Para obtener más información, consulte el [ paso Configurar](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |
| Atributos recomendados | Actualice al flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que muestran los atributos recomendados para que los agregue a los archivos exportados. Para obtener más información, consulte el paso [Select attributes](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Integrada en el Experience Platform, la plataforma de datos del cliente en tiempo real ([!DNL Real-time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles del cliente con decisiones inteligentes en todo el recorrido del cliente. [!DNL Real-time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos descendentes para ofrecer experiencias personalizadas de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con IAB TCF 2.0 | [!DNL Real-time CDP] es ahora un proveedor registrado para la versión 2.0 del  [!DNL Transparency & Consent Framework] (TCF), como lo describe el  [!DNL Interactive Advertising Bureau] (IAB). Puede configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por una CMP y aplicar las preferencias de consentimiento de los clientes al activar segmentos en destinos descendentes. |

Para obtener más información sobre [!DNL Real-time CDP], consulte [[!DNL Real-time CDP] overview](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Supervisión de la ejecución del flujo | Los usuarios pueden supervisar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y las métricas. Consulte el documento [monitorización de flujos de datos](../../sources/tutorials/ui/monitor.md) para obtener más información. |
| Notificaciones de ejecución de flujo | Los usuarios pueden suscribirse a eventos y registrar vínculos web para recibir notificaciones en tiempo real sobre el estado, las métricas y los errores relacionados con las ejecuciones de flujo. |
| Mejoras en el catálogo de la interfaz de usuario | Actualizaciones en la pantalla del catálogo de fuentes para facilitar el acceso a las acciones principales de los objetos seleccionados. |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
