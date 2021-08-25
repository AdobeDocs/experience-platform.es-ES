---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 25 de agosto de 2021.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
source-git-commit: b1dca51264582788ccbde005b063c57e2f3edc8f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 8%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 25 de agosto de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Destinos](#destinations)
- [Perspectivas de la capacidad de observación](#observability)
- [Perfil del cliente en tiempo real](#profile)
- [Fuentes](#sources)

## Destinos {#destinations}

Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos desde Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| [Mejoras en el uso de los destinos](../../destinations/ui/activation-overview.md) | Las mejoras en el uso de los destinos permiten a los especialistas en marketing activar segmentos sin problemas en destinos existentes. |

Para obtener información más general sobre los destinos, consulte [información general sobre destinos](../../destinations/home.md).

## Perspectivas de la capacidad de observación {#observability}

Observability Insights permite supervisar las actividades de Platform mediante el uso de métricas estadísticas y notificaciones de eventos.

**Nuevas características**

| Función | Descripción |
| --- | --- |
| Alertas | Ahora puede suscribirse a alertas importantes relacionadas con flujos de trabajo que se ejecutan en Platform. Después de suscribirse a reglas de alerta específicas, recibirá notificaciones en la interfaz de usuario y correos electrónicos cuando se produzca un evento de ciclo de vida importante (como la incorporación de datos correcta) o si hay problemas que requieran su atención (como un error en el flujo de ingesta o un trabajo de segmento que tarde más de lo esperado). Para obtener más información, consulte la [descripción general de las alertas](../../observability/alerts/overview.md). |

Consulte [Observability Insights overview](../../observability/home.md) para obtener más información sobre el servicio.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Examinar perfiles por política de combinación o identidad | Al examinar perfiles en Experience Platform, ahora puede examinar por política de combinación para obtener una vista previa de 20 perfiles de muestra basados en la política de combinación seleccionada. También puede examinar por identidad para buscar un perfil específico mediante un área de nombres de identidad y un valor de identidad relacionado. Para obtener más información, consulte la [Guía de la interfaz de usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md). |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, lea en primer lugar la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Conector de origen de carga de archivos locales | Se ha cambiado el nombre de la categoría de ingesta de archivos a sistema local, lo que permite llevar los archivos locales directamente a Platform mediante el conector de carga de archivos local. Los datos introducidos a través de este conector se pueden supervisar mediante el panel de control. Consulte la [descripción general del origen de carga de archivos locales](../../sources/connectors/local-system/local-file-upload.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
