---
title: Notas de la versión de Adobe Experience Platform, agosto de 2020
description: Notas de la versión de agosto de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 12 de agosto de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para extraer perspectivas de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones utilizando los recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se ha mejorado la estabilidad de larga duración [!DNL JupyterLab notebook] máquinas virtuales. |

Para obtener más información, consulte [!DNL JupyterLab], consulte la [[!DNL JupyterLab] guía del usuario](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match le permite utilizar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades que Google posee y gestiona, como: [!DNL Search], [!DNL Shopping], Gmail y YouTube. <br><br> Visite la [!DNL Google Customer Match] [página](../../destinations/catalog/advertising/google-customer-match.md) en el catálogo de destinos para obtener más información sobre el destino y cómo configurarlo en Real-Time CDP. |

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Editor de nombres de archivo personalizado | Actualice al flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que le permiten editar el nombre de los archivos exportados. Para obtener más información, consulte [ Configurar paso](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |
| Atributos recomendados | Actualice al flujo de trabajo de activación de datos para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube que muestran los atributos recomendados para que los agregue a los archivos exportados. Para obtener más información, consulte [Paso Seleccionar atributos](../../destinations/ui/activate-batch-profile-destinations.md) en el flujo de trabajo de activación. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basado en el Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes en todo el recorrido de clientes. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos descendentes para ofrecer experiencias personalizadas de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con IAB TCF 2.0 | [!DNL Real-Time CDP] es ahora un proveedor registrado para la versión 2.0 de la variable [!DNL Transparency & Consent Framework] (TCF), tal como se describe en la [!DNL Interactive Advertising Bureau] (IAB). Puede configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por una CMP y aplicar las preferencias de consentimiento de los clientes al activar segmentos en destinos descendentes. |

Para obtener más información, consulte [!DNL Real-Time CDP], consulte la [[!DNL Real-Time CDP] información general](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Supervisión de la ejecución del flujo | Los usuarios pueden supervisar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y las métricas. Consulte la [monitorización de flujos de datos](../../sources/tutorials/ui/monitor.md) documento para obtener más información. |
| Notificaciones de ejecución de flujo | Los usuarios pueden suscribirse a eventos y registrar vínculos web para recibir notificaciones en tiempo real sobre el estado, las métricas y los errores relacionados con las ejecuciones de flujo. |
| Mejoras en el catálogo de la interfaz de usuario | Actualizaciones en la pantalla del catálogo de fuentes para facilitar el acceso a las acciones principales de los objetos seleccionados. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
