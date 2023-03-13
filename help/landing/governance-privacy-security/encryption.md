---
title: Cifrado de datos en Adobe Experience Platform
description: Descubra cómo se cifran los datos en tránsito y en reposo en Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# Cifrado de datos en Adobe Experience Platform

Adobe Experience Platform es un sistema potente y ampliable que centraliza y estandariza los datos de experiencia del cliente en todas las soluciones empresariales. Todos los datos utilizados por Platform se cifran en tránsito y en reposo para mantener sus datos seguros. Este documento describe los procesos de cifrado de Platform en un nivel superior.

El siguiente diagrama de flujo de proceso ilustra cómo ingiere, cifra y mantiene los datos [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Datos en tránsito {#in-transit}

Todos los datos en tránsito entre Platform y cualquier componente externo se dirigen a través de conexiones seguras y cifradas mediante HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En general, los datos se introducen en Platform de tres maneras:

* [Recopilación de datos](../../collection/home.md) Las funciones de permiten a los sitios web y las aplicaciones móviles enviar datos a Platform Edge Network para su ensayo y preparación para la ingesta.
* [Conectores de origen](../../sources/home.md) transmitir datos directamente a Platform desde aplicaciones de Adobe Experience Cloud y otras fuentes de datos empresariales.
* Las herramientas que no son de ETL (extracción, transformación, carga) de Adobe envían datos a [API de ingesta por lotes](../../ingestion/batch-ingestion/overview.md) para consumo.

Después de introducir los datos en el sistema y [cifrado en reposo](#at-rest)Por lo tanto, se puede enriquecer con servicios de Platform y sacarlo del sistema de las siguientes maneras:

* [Destinos](../../destinations/home.md) permite activar datos en aplicaciones de Adobe y aplicaciones de socios.
* Aplicaciones de plataforma nativas como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) también puede utilizar los datos de.

## Datos en reposo {#at-rest}

Los datos que Platform ingiere y utiliza se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por el sistema, independientemente del origen o el formato de archivo. Todos los datos que persisten en el lago de datos se cifran, almacenan y administran de forma aislada [[!DNL Microsoft Azure Data Lake] Almacenamiento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que es única para su organización.

Para obtener más información sobre cómo se cifran los datos en reposo en Azure Data Lake Storage, consulte la [documentación oficial de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Pasos siguientes

Este documento proporciona información general de alto nivel sobre cómo se cifran los datos en Platform. Para obtener más información sobre los procedimientos de seguridad en Platform, consulte la información general sobre [gobernanza, privacidad y seguridad](./overview.md) en el Experience League, o eche un vistazo a la [Documentación técnica de seguridad de Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
