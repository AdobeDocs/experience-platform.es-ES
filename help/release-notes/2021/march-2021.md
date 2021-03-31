---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 31 de marzo de 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 523e09b9af19b1deb01a69be0673b9a17084b7e4
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 31 de marzo de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sandboxes]](#sandboxes)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

| Función | Descripción |
| ------- | ----------- |
| Función  de `add_to_array` | Se ha actualizado la funcionalidad para admitir matrices como parámetro. |
| Función  de `to_array` | Se ha actualizado la funcionalidad para admitir objetos como parámetro. |

Para obtener más información, consulte [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales.

Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

| Función | Descripción |
| ------- | ----------- |
| (Beta) Múltiples entornos limitados de producción | Ahora puede crear y administrar varios entornos limitados de producción en su organización de IMS y dedicar entornos limitados de producción específicos a distintas líneas de negocios, marcas, proyectos o regiones. Para obtener más información, consulte los tutoriales sobre la creación de un entorno limitado de producción [en la interfaz de usuario](../../sandboxes/ui/user-guide.md) o [con la API](../../sandboxes/api/create-sandbox.md) para obtener más información. |

Para obtener más información sobre los entornos limitados, consulte la [información general de los entornos limitados](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de sus datos [!DNL Real-time Customer Profile]. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| (Beta) Segmentación de Edge | La segmentación de Edge evalúa los segmentos en tiempo real, lo que permite casos de uso de personalización de la misma página y de la siguiente página. Puede encontrar más información sobre la segmentación de Edge en la [Descripción general de la interfaz de segmentación](../../segmentation/ui/overview.md). |
| (Beta) Segmentación incremental | Aumenta la frescura de las definiciones de segmentos existentes evaluadas en la segmentación por lotes hasta una hora. |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [información general de segmentación](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Compatibilidad de API para la ingesta de archivos comprimidos | Ahora puede obtener una vista previa e introducir archivos JSON comprimidos o delimitados mediante fuentes de almacenamiento en la nube. Para obtener más información, consulte el tutorial sobre [recopilación de datos de almacenamiento en la nube mediante API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Compatibilidad de la interfaz de usuario con la carga de archivos recursivos | Ahora puede ingerir carpetas enteras recursivamente al usar un origen de almacenamiento en la nube. Al ingerir una carpeta completa, debe asegurarse de que su contenido comparte el mismo esquema. Para obtener más información, consulte el tutorial sobre [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
