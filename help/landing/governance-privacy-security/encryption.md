---
title: Cifrado de datos en Adobe Experience Platform
description: Descubra cómo se cifran los datos en tránsito y en reposo en Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Cifrado de datos en Adobe Experience Platform

Adobe Experience Platform es un sistema potente y ampliable que centraliza y estandariza los datos de experiencia del cliente en todas las soluciones empresariales. Todos los datos que utiliza Platform se cifran en tránsito y en reposo para mantener sus datos seguros. Este documento describe los procesos de cifrado de Platform en un nivel superior.

El siguiente diagrama de flujo de proceso ilustra cómo el Experience Platform ingiere, cifra y mantiene los datos:

![Diagrama que ilustra cómo el Experience Platform ingiere, cifra y mantiene los datos.](../images/governance-privacy-security/encryption/flow.png)

## Datos en tránsito {#in-transit}

Todos los datos en tránsito entre Platform y cualquier componente externo se dirigen a través de conexiones seguras y cifradas mediante HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En general, los datos se introducen en Platform de tres maneras:

- [Recopilación de datos](../../collection/home.md) Las funciones de permiten a los sitios web y las aplicaciones móviles enviar datos al Edge Network de Platform para su ensayo y preparación para la ingesta.
- [Conectores de origen](../../sources/home.md) transmitir datos directamente a Platform desde aplicaciones de Adobe Experience Cloud y otras fuentes de datos empresariales.
- Las herramientas que no son de ETL (extracción, transformación, carga) de Adobe envían datos a [API de ingesta por lotes](../../ingestion/batch-ingestion/overview.md) para consumo.

Después de introducir los datos en el sistema y [cifrado en reposo](#at-rest), los servicios de Platform enriquecen y exportan los datos de las siguientes maneras:

- [Destinos](../../destinations/home.md) permite activar datos en aplicaciones de Adobe y aplicaciones de socios.
- Aplicaciones de plataforma nativas como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/ajo-home) también puede utilizar los datos de.

### Compatibilidad con el protocolo mTLS {#mtls-protocol-support}

Ahora puede utilizar Mutual Transport Layer Security (mTLS) para garantizar una seguridad mejorada en las conexiones salientes a [Destino de API HTTP](../../destinations/catalog/streaming/http-destination.md) y ADOBE JOURNEY OPTIMIZER [acciones personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). mTLS es un método de seguridad de extremo a extremo para la autenticación mutua que garantiza que ambas partes que comparten información son quienes dicen ser antes de que se compartan los datos. mTLS incluye un paso adicional en comparación con TLS, en el que el servidor también solicita el certificado del cliente y lo verifica al final.

Si lo desea [usar mTLS con acciones personalizadas de Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) y flujos de trabajo de destino de la API HTTP del Experience Platform, la dirección del servidor que se coloque en la IU de acción del cliente de Adobe Journey Optimizer o en la IU de destinos debe tener los protocolos TLS deshabilitados y solo mTLS habilitado. Si el protocolo TLS 1.2 sigue habilitado en ese extremo, no se envía ningún certificado para la autenticación del cliente. Esto significa que, para utilizar mTLS con estos flujos de trabajo, el punto final del servidor de &quot;recepción&quot; debe ser un mTLS **solamente** extremo de conexión habilitado.

>[!IMPORTANT]
>
>No se requiere ninguna configuración adicional en la acción personalizada de Adobe Journey Optimizer o en el destino de la API HTTP para activar mTLS; este proceso se produce automáticamente cuando se detecta un punto de conexión habilitado para mTLS. El nombre común (CN) y los nombres alternativos del sujeto (SAN) de cada certificado están disponibles en la documentación como parte del certificado y se pueden utilizar como una capa adicional de validación de propiedad si desea hacerlo.
>
>RFC 2818, publicado en mayo de 2000, anula el uso del campo Nombre común (CN) en certificados HTTPS para la verificación del nombre del sujeto. En su lugar, recomienda utilizar la extensión &quot;Nombre alternativo del sujeto&quot; (SAN) del tipo &quot;nombre DNS&quot;.

### Descargar certificados {#download-certificates}

>[!NOTE]
>
>Es su responsabilidad mantener actualizado el certificado público. Asegúrese de revisar regularmente el certificado, especialmente a medida que se acerca su fecha de caducidad. Debe marcar esta página para mantener la última copia en su entorno.

Si desea comprobar el CN o SAN para realizar una validación adicional de terceros, puede descargar los certificados correspondientes aquí:

- [El certificado público de Adobe Journey Optimizer](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [El certificado público del servicio Destinations](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## Datos en reposo {#at-rest}

Los datos que Platform ingiere y utiliza se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por el sistema, independientemente del origen o el formato de archivo. Todos los datos que persisten en el lago de datos se cifran, almacenan y administran de forma aislada [[!DNL Microsoft Azure Data Lake] Almacenamiento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que es única para su organización.

Para obtener más información sobre cómo se cifran los datos en reposo en Azure Data Lake Storage, consulte la [documentación oficial de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Pasos siguientes

Este documento proporciona información general de alto nivel sobre cómo se cifran los datos en Platform. Para obtener más información sobre los procedimientos de seguridad en Platform, consulte la información general sobre [gobernanza, privacidad y seguridad](./overview.md) en el Experience League, o eche un vistazo a la [Documentación técnica de seguridad de Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
