---
title: Notas de la versión de Adobe Experience Platform, enero de 2021
description: Las notas de la versión de enero de 2021 de Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 27%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 27 de enero de 2021**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones de expresión regular | El asignador [!DNL Data Prep] ahora admite la coincidencia y la extracción de parte del campo de entrada en función de expresiones regulares. |

Para obtener más información, consulte [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] es la solución de almacenamiento de objetos de Microsoft para la nube. |

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Coincidencia de ID avanzada | Mejoras en las capacidades de tasa de coincidencia de audiencia en [!DNL Facebook Custom Audiences] y [!DNL Google Customer Match], al agregar compatibilidad con coincidencia de identidad adicional, como ID externos, números de teléfono e ID de dispositivos móviles. Consulte la siguiente documentación para obtener más información: <ul><li>[Destino de Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Para obtener más información, visita la [descripción general de destinos](../../destinations/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Eliminar conjunto de datos del almacén de perfiles | Al eliminar un conjunto de datos del lago de datos de Experience Platform, también se eliminará automáticamente del almacén de perfiles. Ya no es necesario utilizar el punto de conexión de la API de trabajos del sistema de perfiles para realizar una solicitud de eliminación para eliminar explícitamente el conjunto de datos del almacén de perfiles. Para obtener más información, consulte la [guía de extremo de API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md). |
| Recuento estimado del área de nombres de ID para un segmento determinado | Para los recuentos de perfiles estimados, la API de previsualización ahora informa de lo siguiente:<ul><li>Recuento total de perfiles estimados en un segmento para un área de nombres determinada.</li><li>Recuento total de perfiles estimados en el esquema de unión de perfiles para un área de nombres determinada.</li></ul>Para obtener más información, consulte la [guía de extremo de API de vista previa de perfil](../../profile/api/preview-sample-status.md). |

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de [!DNL Profile], lea la [descripción general del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en el conector de origen de Adobe Audience Manager | Ahora puede filtrar y seleccionar segmentos de origen individuales de Audience Manager para introducirlos en Experience Platform, así como filtrar los rasgos de origen. Consulte el tutorial sobre [creación de un conector de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| [!DNL Google BigQuery] mejoras en el conector de origen | Ahora puede ingerir archivos de más de 10 GB en una ejecución de flujo utilizando el conector de origen [!DNL BigQuery]. Consulte la [[!DNL BigQuery] descripción general del conector de origen](../../sources/connectors/databases/bigquery.md) para obtener más información. |
| Compatibilidad con tipos de datos complejos para almacenamiento en la nube | Ahora puede introducir tipos de datos complejos, como matrices en archivos JSON, al utilizar un conector de origen de almacenamiento en la nube. Consulte los tutoriales sobre la creación de un flujo de datos de almacenamiento en la nube [en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [mediante la API [!DNL Flow Service] 4&rbrace; para obtener más información.](../../sources/tutorials/api/collect/cloud-storage.md) |
| Compatibilidad con la autenticación basada en claves principales de servicio para el origen [!DNL Microsoft Dynamics] | Ahora puede autenticarse en su cuenta de [!DNL Dynamics] mediante una clave principal de servicio como alternativa a la autenticación basada en contraseña. Consulte la [[!DNL Dynamics] descripción general del conector de origen](../../sources/connectors/crm/ms-dynamics.md) para obtener más información. |
| Compatibilidad de la IU con separadores personalizados en fuentes de almacenamiento en la nube | Ahora puede establecer un delimitador de columna personalizado, como una coma (`,`), una tabulación (`\t`) o una barra vertical (`|`), para recopilar archivos delimitados en la interfaz de usuario. Consulte el tutorial sobre [creación de un flujo de datos con un conector de origen de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
