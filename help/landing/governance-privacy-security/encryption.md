---
title: Cifrado de datos en Adobe Experience Platform
topic-legacy: data protection
description: Descubra cómo se cifran los datos en tránsito y en reposo en Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: d99a9081edc483831d56af3d838b67d9aba25bea
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# Cifrado de datos en Adobe Experience Platform

Adobe Experience Platform es un sistema potente y ampliable que centraliza y estandariza los datos de experiencia del cliente en todas las soluciones empresariales. Todos los datos utilizados por Platform se cifran en tránsito y en reposo para mantener sus datos seguros. Este documento describe los procesos de encriptación de Platform en un alto nivel.

El siguiente diagrama de flujo de proceso ilustra cómo se introducen, cifran y mantienen los datos [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Datos en tránsito {#in-transit}

Todos los datos en tránsito entre Platform y cualquier componente externo se realizan a través de conexiones seguras y cifradas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En general, los datos se introducen en Platform de tres maneras:

* [Recopilación de datos](../../collection/home.md) las funcionalidades permiten que los sitios web y las aplicaciones móviles envíen datos a Platform Edge Network para su ensayo y preparación para la ingesta.
* [Conectores de origen](../../sources/home.md) transmitir datos directamente a Platform desde aplicaciones de Adobe Experience Cloud y otras fuentes de datos empresariales.
* Las herramientas de ETL (extracción, transformación, carga) que no son de Adobe envían datos al [API de ingesta por lotes](../../ingestion/batch-ingestion/overview.md) para consumo.

Una vez introducidos los datos en el sistema y [cifrado en reposo](#at-rest), luego puede ser enriquecido por los servicios de Platform y sacado del sistema de las siguientes maneras:

* [Destinos](../../destinations/home.md) permite activar datos en aplicaciones de Adobe y aplicaciones de socios.
* Aplicaciones nativas de la plataforma, como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) también puede utilizar los datos.

## Datos en reposo {#at-rest}

Los datos que Platform ingesta y utiliza se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por el sistema, independientemente del origen o el formato de archivo. Todos los datos almacenados en el lago de datos se cifran, almacenan y administran en un entorno aislado [[!DNL Microsoft Azure Data Lake] Almacenamiento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que es única para su organización.

Para obtener más información sobre cómo se cifran los datos en reposo en el almacenamiento de Azure Data Lake, consulte [documentación oficial de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Pasos siguientes

Este documento proporciona información general de alto nivel sobre cómo se cifran los datos en Platform. Para obtener más información sobre los procedimientos de seguridad en Platform, consulte la descripción general de [administración, privacidad y seguridad](./overview.md) en el Experience League, o eche un vistazo a la [Documento técnico sobre seguridad de plataforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
