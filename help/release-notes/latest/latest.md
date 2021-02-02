---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 27 de enero de 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 74325dcfe9d7b117e3f812d88e0c4a980d44ef53
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 27%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de enero de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)
- [[!DNL Experience Platform Launch Server Side]](#launch)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones de expresión ordinarias | [!DNL Data Prep] Mapper ahora admite la coincidencia y extracción de parte del campo de entrada en función de expresiones regulares. |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Coincidencia de ID avanzada | Mejoras en las capacidades de la tasa de coincidencia de audiencias en [!DNL Facebook Custom Audiences] y [!DNL Google Customer Match], agregando compatibilidad para la coincidencia de identidades adicionales, como ID externos, números de teléfono e ID de dispositivos móviles. Consulte la siguiente documentación para obtener más información: <ul><li>[Destino de Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de Coincidencia de clientes de Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activar perfiles y segmentos en un destino](../../destinations/ui/activate-destinations.md)</li></ul> |

Para obtener más información, visite la [descripción general de destinos](../../destinations/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en el conector de origen de Adobe Audience Manager | Ahora puede filtrar y seleccionar segmentos individuales de origen de Audience Manager a ingesta en plataforma, así como filtrar las características de origen. Consulte el tutorial sobre [creación de un conector de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| [!DNL Google BigQuery] mejoras en los conectores de origen | Ahora puede ingerir archivos de más de 10 GB en una ejecución de flujo mediante el conector de origen [!DNL BigQuery]. Consulte la [[!DNL BigQuery] información general del conector de origen](../../sources/connectors/databases/bigquery.md) para obtener más información. |
| Compatibilidad con tipos de datos complejos para almacenamientos en la nube | Ahora puede ingestar tipos de datos complejos, como matrices en archivos JSON, al utilizar un conector de origen de almacenamiento de nube. Consulte los tutoriales sobre la creación de un flujo de datos de almacenamiento en la nube [en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [mediante la [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obtener más información. |
| Compatibilidad con la autenticación basada en claves principales de servicio para [!DNL Microsoft Dynamics] origen | Ahora puede autenticarse en su cuenta [!DNL Dynamics] mediante una clave principal de servicio como alternativa a la autenticación basada en contraseña. Consulte la [[!DNL Dynamics] información general del conector de origen](../../sources/connectors/crm/ms-dynamics.md) para obtener más información. |
| Compatibilidad de la interfaz de usuario con separadores personalizados en orígenes de almacenamiento en la nube | Ahora puede establecer un delimitador de columna personalizado, como una coma (`,`), una ficha (`\t`) o una barra vertical (`|`), para recopilar archivos delimitados en la interfaz de usuario. Consulte el tutorial sobre [creación de un flujo de datos con un conector de origen de almacenamiento de nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información |

Para obtener más información sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md).

## [!DNL Experience Platform Launch Server Side] {#launch}

Adobe Experience Platform Launch Server Side reduce el peso de páginas web y aplicaciones mediante Adobe Experience Platform Edge Network para ejecutar tareas que se realizan normalmente en el cliente. Las reglas de Platform Launch Server Side pueden transformar y enviar datos a nuevos destinos sin cambiar las implementaciones del lado del cliente.

Platform Launch Server Side, junto con los SDK móviles y web de Adobe Experience Platform, permite:

- Realizar una sola llamada desde la página que contiene una carga útil de datos y, a continuación, unificar este servidor de datos para reducir el tráfico de red del lado del servidor y ofrecer una experiencia más rápida a los clientes.
- Reducir la cantidad de tiempo que tardan las páginas web en cargarse para que el sitio se ajuste a las prácticas recomendadas del sector en cuanto a rendimiento.
- Aumentar la transparencia y el control sobre los tipos de datos que se envían a todas las propiedades del lado del cliente.
- Crear una regla del lado del servidor para enviar los datos rastreados anteriormente a un nuevo destino.

Para obtener más información, consulte la [documentación de inicio de plataforma](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html?lang=en).