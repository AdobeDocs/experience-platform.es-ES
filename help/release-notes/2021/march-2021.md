---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2021'
description: Las notas de la versión de marzo de 2021 de Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 38%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 31 de marzo de 2021**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

| Función | Descripción |
| ------- | ----------- |
| Función `add_to_array` | Se ha actualizado la funcionalidad para admitir matrices como parámetro. |
| Función `to_array` | Se ha actualizado la funcionalidad para admitir objetos como parámetro. |

Para obtener más información, consulte [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API RESTful que le permiten generar segmentos y audiencias a partir de los datos de [!DNL Real-Time Customer Profile]. Estos segmentos se configuran centralmente y se mantienen en [!DNL Experience Platform], lo que hace que cualquier aplicación de Adobe pueda acceder a ellos fácilmente.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| (Beta) Segmentación de Edge | La segmentación de Edge evalúa los segmentos en tiempo real, lo que permite casos de uso de personalización de la misma página y de la siguiente. Encontrará más información sobre la segmentación de Edge en la [descripción general de la IU de segmentación](../../segmentation/ui/overview.md). |
| (Beta) Segmentación incremental | Aumenta la actualización de las definiciones de segmentos existentes evaluadas en la segmentación por lotes hasta una hora. |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Fuentes de Beta que se trasladan a GA | Las siguientes fuentes se han promocionado de beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Compatibilidad con API para la ingesta de archivos comprimidos | Ahora puede obtener una vista previa e ingerir archivos JSON comprimidos o delimitados mediante fuentes de almacenamiento en la nube. Para obtener más información, consulte el tutorial sobre [recopilación de datos de almacenamiento en la nube mediante API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Compatibilidad de IU para la carga recursiva de archivos | Ahora puede introducir carpetas completas de forma recursiva al utilizar una fuente de almacenamiento en la nube. Al ingerir una carpeta completa, debe asegurarse de que su contenido comparta el mismo esquema. Para obtener más información, consulte el tutorial sobre [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
