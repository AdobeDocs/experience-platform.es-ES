---
title: Notas de la versión de Adobe Experience Platform, agosto de 2021
description: Notas de la versión de agosto de 2021 de Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
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

Los destinos son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | El destino de Atributos del dirigible, anteriormente en fase beta, ya está disponible de forma general. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | El destino Etiquetas de dirigibles, anteriormente en fase beta, ya está disponible de forma general. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | El destino de Braze, que anteriormente estaba en fase beta, ya está disponible de forma general. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Con el destino Lista de clientes de Pinterest, puede crear audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Dirija su actividad a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de una manera segura, automatizada y escalable. |

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de  para que Experience Platform envíe datos de audiencia y perfil a su punto final, en función de los datos y los formatos de autenticación de su elección. Las configuraciones se almacenan en el Experience Platform y se pueden recuperar mediante API para actualizaciones adicionales. |
| [Mejoras de uso en Destinos](../../destinations/ui/activation-overview.md) | Las mejoras de uso en los destinos permiten a los especialistas en marketing activar segmentos sin problemas en destinos existentes. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Perspectivas de la capacidad de observación {#observability}

Observability Insights le permite monitorizar las actividades de Platform mediante el uso de métricas estadísticas y notificaciones de eventos.

**Nuevas características**

| Función | Descripción |
| --- | --- |
| Alertas | ahora puede suscribirse a alertas importantes relacionadas con los flujos de trabajo que se ejecutan en Platform. Después de suscribirse a reglas de alerta específicas, recibirá notificaciones en la interfaz de usuario y correos electrónicos cuando se produzca un evento importante del ciclo vital (como una ingesta de datos correcta) o si hay problemas que requieren su atención (como un error en el flujo de ingesta o un trabajo de segmento que tarde más de lo esperado). Para obtener más información, consulte la [información general sobre alertas](../../observability/alerts/overview.md). |

Consulte la [Resumen de Observability Insights](../../observability/home.md) para obtener más información sobre el servicio.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Examinar perfiles por política de combinación o identidad | Al examinar los perfiles en Experience Platform, ahora puede examinar por política de combinación para obtener una vista previa de 20 perfiles de muestra basados en la política de combinación seleccionada. También puede examinar por identidad para buscar un perfil específico utilizando un área de nombres de identidad y un valor de identidad relacionado. Para obtener más información, consulte la [Guía de la IU del perfil del cliente en tiempo real](../../profile/ui/user-guide.md). |

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, comience por leer el [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Conector de origen de carga de archivos locales | Se ha cambiado el nombre de la categoría de ingesta de archivos a sistema local, lo que permite llevar los archivos locales directamente a Platform mediante el conector de carga de archivos local. Los datos introducidos a través de este conector se pueden monitorizar mediante el panel de monitorización. Consulte la [información general sobre el origen de carga de archivos locales](../../sources/connectors/local-system/local-file-upload.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
