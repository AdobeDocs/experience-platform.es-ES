---
title: Notas de la versión de Adobe Experience Platform, enero de 2021
description: Notas de la versión de enero de 2021 para Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de enero de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones de expresión regular | [!DNL Data Prep] Mapper ahora admite la coincidencia y extracción de parte del campo de entrada basada en expresiones regulares. |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] es la solución de almacenamiento de objetos de Microsoft para la nube. |

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Coincidencia de ID avanzada | Mejoras en las capacidades de la tasa de coincidencia de audiencia en [!DNL Facebook Custom Audiences] y [!DNL Google Customer Match], al agregar compatibilidad con coincidencias de identidad adicionales, como ID externos, números de teléfono e ID de dispositivos móviles. Consulte la siguiente documentación para obtener más información: <ul><li>[Destino de facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de coincidencia del cliente de Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Para obtener más información, visite [información general sobre destinos](../../destinations/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Eliminar conjunto de datos del almacén de perfiles | Cuando elimine un conjunto de datos del lago de datos del Experience Platform, también se eliminará automáticamente del almacén de perfiles. Ya no es necesario usar el extremo de la API de trabajos del sistema de perfiles para realizar una solicitud de eliminación para eliminar el conjunto de datos del almacén de perfiles explícitamente. Para obtener más información, consulte la [guía de extremo de la API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md). |
| Recuento estimado del espacio de nombres de ID para un segmento determinado | Para recuentos de perfiles estimados, la API de vista previa ahora informa:<ul><li>Recuento total de perfiles estimados en un segmento para un área de nombres determinada.</li><li>Recuento total de perfiles estimados en el esquema de unión de perfiles para un área de nombres determinada.</li></ul>Para obtener más información, consulte [guía de extremo de API de vista previa de perfil](../../profile/api/preview-sample-status.md). |

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] datos, comience leyendo el [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en el conector de origen de Adobe Audience Manager | Ahora puede filtrar y seleccionar segmentos individuales de origen de Audience Manager a ingesta en Platform, así como filtrar los rasgos de origen. Consulte el tutorial en [creación de un conector de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| [!DNL Google BigQuery] mejoras en el conector de origen | Ahora puede ingerir archivos de más de 10 GB en una ejecución de flujo mediante la función [!DNL BigQuery] conector de origen. Consulte la [[!DNL BigQuery] información general del conector de origen](../../sources/connectors/databases/bigquery.md) para obtener más información. |
| Compatibilidad con tipos de datos complejos para almacenamiento en la nube | Ahora puede introducir tipos de datos complejos, como matrices en archivos JSON, al utilizar un conector de origen de almacenamiento en la nube. Consulte los tutoriales sobre la creación de un flujo de datos de almacenamiento en la nube [en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [usando la variable [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obtener más información. |
| Compatibilidad con la autenticación basada en claves principales del servicio para [!DNL Microsoft Dynamics] source | Ahora puede autenticarse en su [!DNL Dynamics] cuenta que utiliza una clave principal de servicio como alternativa a la autenticación basada en contraseña. Consulte la [[!DNL Dynamics] información general del conector de origen](../../sources/connectors/crm/ms-dynamics.md) para obtener más información. |
| Compatibilidad de la interfaz de usuario con separadores personalizados en fuentes de almacenamiento en la nube | Ahora puede establecer un delimitador de columna personalizado, como una coma (`,`), pestaña (`\t`) o una barra vertical (`|`), para recopilar archivos delimitados en la interfaz de usuario. Consulte el tutorial en [creación de un flujo de datos con un conector de origen de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
