---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2022
description: Notas de la versión de septiembre de 2022 para Adobe Experience Platform.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 28 de septiembre de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Servicio de identidad](#identity-service)
- [Fuentes](#sources)

## Servicio de identidad {#identity-service}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente parezca tener múltiples &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales y impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la eliminación de conjuntos de datos | El servicio de identidad ahora admite la eliminación de conjuntos de datos al solicitar a través de la variable [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), la interfaz de usuario o la higiene de los datos. Lea la guía de [eliminación de conjuntos de datos en la interfaz de usuario](../../catalog/datasets/user-guide.md#delete-a-dataset) para obtener más información. |

Para obtener más información sobre el servicio de identidad, lea la [Información general del servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Impacto de la población del segmento del Audience Manager en el perfil del cliente en tiempo real | La ingesta de grandes poblaciones de segmentos de Audience Manager tiene un impacto directo en el recuento total de perfiles cuando envía por primera vez un segmento de Audience Manager a Platform mediante la fuente de Audience Manager. Esto significa que si selecciona todos los segmentos, es posible que se produzca un recuento de perfiles superior a su derecho de uso de licencia. Para obtener más información, lea la [Información general de la fuente del Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obtener información sobre el uso de las licencias, consulte la documentación de [uso del panel de uso de licencias](../../dashboards/guides/license-usage.md). |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).