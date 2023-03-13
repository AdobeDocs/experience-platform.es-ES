---
description: El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos. Combinados, estos componentes permiten a Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital.
title: Opciones de configuración en Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Opciones de configuración en Destination SDK

## Información general {#overview}

El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos. Combinados, estos componentes permiten a Experience Platform conectarse a las plataformas de destino, enviar mensajes personalizados, exportar archivos personalizados y activar datos de perfil en todo el ecosistema digital. Las configuraciones utilizadas en el Adobe Experience Platform Destination SDK son las siguientes:

* **Configuración de destino**: contiene información básica sobre el destino. Esta configuración incluye los tipos de identidad que puede admitir el destino, el formato deseado de los archivos exportados (para destinos basados en archivos) y varios atributos de interfaz de usuario para la tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.
* **Especificaciones de servidor, archivo y plantilla**: Vincula información sobre las especificaciones del servidor y la plantilla utilizada por el Adobe para entregar cargas útiles en el destino. En el caso de los destinos basados en archivos, esta configuración también incluye los formatos de compresión y formato de archivo admitidos para el destino.
   * **Especificaciones del servidor**: una plantilla de configuración que contiene información sobre la ubicación de almacenamiento o el extremo HTTP al que se envían los datos.&quot;
   * **Especificaciones de archivo**: Una plantilla de configuración que incluye las opciones de formato y compresión de archivos para el destino del lote.
   * **Especificaciones de plantilla**: En esta plantilla, puede definir cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite la plataforma. Para obtener información detallada sobre los lenguajes de plantilla compatibles, los formatos de mensaje y la información requerida por Adobe para configurar la integración con su , lea [Formato del mensaje](./message-format.md).
* **Configuración de autenticación**: esta configuración define cómo se conectan los usuarios de Adobe Experience Platform al destino.
* **Configuración de metadatos de audiencia**: este punto de conexión de configuración le permite configurar cómo se crean, actualizan o eliminan las audiencias o los segmentos en el destino mediante programación. En el caso de los destinos por lotes, le permite configurar una notificación cada vez que los archivos se envíen correctamente al destino.

![Diagrama que muestra los extremos de configuración del Destination SDK y cómo se utilizan juntos.](./assets/self-service-configuration.png)

## Vínculos relacionados {#related-links}

Las páginas siguientes proporcionan más detalles sobre la funcionalidad y las opciones de configuración disponibles en Destination SDK, así como las operaciones de API correspondientes que puede realizar.

| Descripción de la funcionalidad (destinos de flujo continuo) | Descripción de la funcionalidad (destinos por lotes) | Referencia de API |
|--- |--- |--- |
| [Opciones de configuración de destino](./destination-configuration.md) | [Opciones de configuración de destino basadas en archivos](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Operaciones de extremo de API de destinos](./destination-configuration-api.md) |
| [Especificaciones de servidor y plantilla](./server-and-template-configuration.md) | [Especificaciones de configuración del servidor y del archivo](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Operaciones de extremo de API de servidores de destino](./destination-server-api.md) |
| [Configuración de autenticación](./authentication-configuration.md) | Igual que para los destinos de flujo continuo. | Puede configurar la información de autenticación del destino mediante el `customerAuthenticationConfigurations` parámetros del `/destinations` punto final. Más información para [transmisión](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) y [lote](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinos. |
| [Gestión de metadatos de audiencia](./audience-metadata-management.md) | Igual que para streaming. Consulte [ejemplo basado en archivos](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) para comprender cómo se pueden utilizar los metadatos de audiencia en un contexto de destino por lotes. | [Operaciones de API de extremo de metadatos de audiencia](./audience-metadata-api.md) |
| [Configuración de OAuth 2](./oauth2-authentication.md) | Igual que para los destinos de flujo continuo | Configure con el `customerAuthenticationConfigurations` en el campo [Extremo de API /targets](./destination-configuration-api.md). |
| [Formato del mensaje](./message-format.md) | - | - |
| [Herramientas de prueba para destinos de flujo continuo](./test-destination.md) | [Herramientas de prueba para destinos basados en archivos](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Operaciones de API de prueba de destino](./destination-testing-api.md) |
| [Publicación de destino](./configure-destination-instructions.md#publish-destination) | Igual que para los destinos de flujo continuo | [Operaciones de API de publicación de destino](./destination-publish-api.md) |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora tiene una visión general de la funcionalidad proporcionada por Destination SDK y qué páginas leer para obtener más información acerca de configuraciones específicas. A continuación, puede leer las guías que incluyen todos los pasos para [configuración de una transmisión por secuencias](/help/destinations/destination-sdk/configure-destination-instructions.md) o una [destino basado en archivos](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) mediante el uso de Destination SDK.
