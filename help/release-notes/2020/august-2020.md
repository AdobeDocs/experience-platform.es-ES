---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
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

[!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones mediante el uso de sus recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se mejoró la estabilidad de las máquinas virtuales [!DNL JupyterLab notebook] de larga ejecución. |

Para obtener más información sobre [!DNL JupyterLab], consulte la [[!DNL JupyterLab] guía del usuario](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

En [Plataforma de datos del cliente en tiempo real](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a esos socios de manera transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| [!DNL Google Customer Match] | La coincidencia de clientes de Google le permite utilizar sus datos en línea y sin conexión para comunicarse con sus clientes y volver a interactuar con ellos en las propiedades que posee y opera Google, como: [!DNL Search], [!DNL Shopping], Gmail y YouTube. <br><br> Visite la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) página en el catálogo de destinos para obtener más información sobre el destino y cómo configurarlo en CDP en tiempo real. |

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Editor de nombres de archivo personalizado | Actualice el flujo de trabajo de activación de datos para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube que le permiten editar el nombre de los archivos exportados. Para obtener más información, consulte el [ paso Configurar](../../destinations/ui/activate-destinations.md#configure) en el flujo de trabajo de activación. |
| Atributos recomendados | Actualice el flujo de trabajo de activación de datos para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube que muestran los atributos recomendados para agregarlos a los archivos exportados. Para obtener más información, consulte el [paso Seleccionar atributos](../../destinations/ui/activate-destinations.md#select-attributes) en el flujo de trabajo de activación. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basada en la plataforma de datos del cliente en tiempo real ([!DNL Real-time CDP]) y Experience Platform, ayuda a las compañías a reunir datos conocidos y desconocidos para activar los perfiles del cliente con decisiones inteligentes en todo el recorrido del cliente. [!DNL Real-time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a los destinos de flujo descendente para proporcionar experiencias personalizadas individuales a los clientes en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con IAB TCF 2.0 | [!DNL Real-time CDP] es ahora un proveedor registrado para la versión 2.0 de la  [!DNL Transparency & Consent Framework] (TCF), como lo describe la  [!DNL Interactive Advertising Bureau] (IAB). Puede configurar las operaciones de datos y los esquemas de perfil para que acepten los datos de consentimiento del cliente generados por un CMP y para que apliquen las preferencias de consentimiento de los clientes al activar segmentos en destinos de flujo descendente. |

Para obtener más información sobre [!DNL Real-time CDP], consulte la [[!DNL Real-time CDP] información general](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante servicios [!DNL Platform]. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Supervisión de la ejecución de flujo | Los usuarios pueden supervisar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y las métricas. Consulte el documento [flujos de datos de monitoreo](../../sources/tutorials/ui/monitor.md) para obtener más información. |
| Notificaciones de ejecución de flujo | Los usuarios pueden suscribirse a los eventos y registrar los enlaces web para recibir notificaciones en tiempo real sobre el estado, las métricas y los errores relacionados con las ejecuciones de flujo. |
| Mejoras en el catálogo de la interfaz de usuario | Actualizaciones en la pantalla del catálogo de fuentes para facilitar el acceso a las acciones principales de los objetos seleccionados. |

Para obtener más información sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md).