---
title: Cifrado de datos en Adobe Experience Platform
description: Descubra cómo se cifran los datos en tránsito y en reposo en Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Cifrado de datos en Adobe Experience Platform

Adobe Experience Platform es un sistema potente y ampliable que centraliza y estandariza los datos de experiencia del cliente en todas las soluciones empresariales. Todos los datos que utiliza Experience Platform se cifran en tránsito y en reposo para mantener sus datos seguros. Este documento describe los procesos de cifrado de Experience Platform en un nivel superior.

El siguiente diagrama de flujo de proceso ilustra cómo Experience Platform ingiere, cifra y mantiene los datos:

![Diagrama que ilustra cómo Experience Platform ingiere, cifra y mantiene los datos.](../images/governance-privacy-security/encryption/flow.png)

## Datos en tránsito {#in-transit}

Todos los datos en tránsito entre Experience Platform y cualquier componente externo se realizan a través de conexiones seguras y cifradas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En general, los datos se introducen en Experience Platform de tres maneras:

- Las funcionalidades de [recopilación de datos](../../collection/home.md) permiten que los sitios web y las aplicaciones móviles envíen datos al Edge Network de Experience Platform para su ensayo y preparación para la ingesta.
- [Conectores de Source](../../sources/home.md) transmiten datos directamente a Experience Platform desde aplicaciones de Adobe Experience Cloud y otras fuentes de datos empresariales.
- Las herramientas que no son de ETL de Adobe (extraer, transformar, cargar) envían datos a la [API de ingesta por lotes](../../ingestion/batch-ingestion/overview.md) para su consumo.

Una vez que los datos se han introducido en el sistema y se han [cifrado en reposo](#at-rest), los servicios de Experience Platform enriquecen y exportan los datos de las siguientes maneras:

- [Destinos](../../destinations/home.md) le permiten activar datos en aplicaciones de Adobe y aplicaciones de socios.
- Las aplicaciones nativas de Experience Platform como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/ajo-home) también pueden usar los datos.

### Compatibilidad con el protocolo mTLS {#mtls-protocol-support}

Ahora puede usar la seguridad de la capa de transporte mutuo (mTLS) para garantizar una seguridad mejorada en las conexiones salientes al [destino de la API HTTP](../../destinations/catalog/streaming/http-destination.md) y a las [acciones personalizadas](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) de Adobe Journey Optimizer. mTLS es un método de seguridad de extremo a extremo para la autenticación mutua que garantiza que ambas partes que comparten información son quienes dicen ser antes de que se compartan los datos. mTLS incluye un paso adicional en comparación con TLS, en el que el servidor también solicita el certificado del cliente y lo verifica al final.

Si desea [usar mTLS con acciones personalizadas de Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) y flujos de trabajo de destino de API HTTP de Experience Platform, la dirección del servidor que coloque en la interfaz de usuario de acción del cliente de Adobe Journey Optimizer o en la interfaz de usuario de destinos debe tener los protocolos TLS deshabilitados y solo mTLS habilitado. Si el protocolo TLS 1.2 sigue habilitado en ese extremo, no se envía ningún certificado para la autenticación del cliente. Esto significa que, para usar mTLS con estos flujos de trabajo, el extremo del servidor de &quot;recepción&quot; debe ser un extremo de conexión mTLS **solo** habilitado.

>[!IMPORTANT]
>
>No se requiere ninguna configuración adicional en la acción personalizada de Adobe Journey Optimizer o en el destino de la API HTTP para activar mTLS; este proceso se produce automáticamente cuando se detecta un punto de conexión habilitado para mTLS. El nombre común (CN) y los nombres alternativos del sujeto (SAN) de cada certificado están disponibles en la documentación como parte del certificado y se pueden utilizar como una capa adicional de validación de propiedad si desea hacerlo.
>
>RFC 2818, publicado en mayo de 2000, anula el uso del campo Nombre común (CN) en certificados HTTPS para la verificación del nombre del sujeto. En su lugar, recomienda utilizar la extensión &quot;Nombre alternativo del sujeto&quot; (SAN) del tipo &quot;nombre DNS&quot;.

### Descargar certificados {#download-certificates}

>[!NOTE]
>
>Usted es responsable de garantizar que sus sistemas utilicen un certificado público válido. Revise regularmente los certificados, especialmente a medida que se acerca la fecha de caducidad. Utilice la API para recuperar y actualizar certificados antes de que caduquen.

Ya no se proporcionan vínculos de descarga directa para certificados mTLS públicos. En su lugar, use el [extremo de certificado público](../../data-governance/mtls-api/public-certificate-endpoint.md) para recuperar los certificados. Este es el único método admitido para acceder a los certificados públicos actuales. Garantiza que siempre reciba certificados válidos y actualizados para sus integraciones.

Las integraciones que dependen del cifrado basado en certificados deben actualizar sus flujos de trabajo para admitir la recuperación automatizada de certificados mediante la API. El uso de vínculos estáticos o actualizaciones manuales puede dar como resultado el uso de certificados caducados o revocados, lo que provoca integraciones fallidas.

#### Automatización del ciclo vital de certificados {#certificate-lifecycle-automation}

Adobe ahora automatiza el ciclo de vida del certificado para las integraciones mTLS a fin de mejorar la fiabilidad y evitar interrupciones en el servicio. Los certificados públicos son:

- Reemitido 60 días antes del vencimiento.
- Revocado 30 días antes de la caducidad.

Estos intervalos se seguirán acortando según las [directrices del foro CA/B en evolución](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), cuyo objetivo es reducir la duración del certificado a un máximo de 47 días.

Si anteriormente utilizaba vínculos en esta página para descargar certificados, actualice el proceso para recuperarlos exclusivamente a través de la API.

## Datos en reposo {#at-rest}

Los datos que Experience Platform ingiere y utiliza se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por el sistema, independientemente del origen o el formato de archivo. Todos los datos que persisten en el lago de datos se cifran, almacenan y administran en una instancia de [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) aislada que es única para su organización.

Para obtener detalles sobre cómo se cifran los datos en reposo en Azure Data Lake Storage, consulte la [documentación oficial de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Pasos siguientes

Este documento proporciona información general de alto nivel sobre cómo se cifran los datos en Experience Platform. Para obtener más información sobre los procedimientos de seguridad en Experience Platform, consulta la descripción general de [gobernanza, privacidad y seguridad](./overview.md) en Experience League o mira el [documento técnico de seguridad de Experience Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
