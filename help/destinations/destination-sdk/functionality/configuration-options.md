---
description: El servicio de destinos en Adobe Experience Platform utiliza extremos de configuración para varios componentes que crean la funcionalidad de destinos. Descubra cómo estos componentes combinados permiten al Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en el ecosistema digital.
title: Opciones de configuración en el Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Opciones de configuración en el Destination SDK

El servicio de destinos en Adobe Experience Platform utiliza extremos de configuración para varios componentes que crean la funcionalidad de destinos.

Estos componentes combinados permiten al Experience Platform conectarse a plataformas de destino, enviar mensajes personalizados, exportar archivos personalizados y activar datos de perfil en el ecosistema digital.

El diagrama siguiente muestra una descripción general de alto nivel de los componentes que puede configurar mediante Destination SDK para crear su propio destino. Estos componentes se describen más adelante.

![Diagrama que muestra los componentes del Destination SDK, los extremos de configuración y las operaciones que admiten.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuración de servidor {#server-configuration}

La configuración del servidor de destino combina información sobre las especificaciones del servidor y la plantilla utilizada por Adobe para entregar cargas útiles al destino.

Por ejemplo, aquí es donde especifica los extremos de la API que el Experience Platform debe conectar, así como los encabezados y el formato de las llamadas de API que Platform realizará.

Para los destinos basados en archivos, esta configuración también incluye los formatos de formato y compresión de archivos admitidos para el destino. Puede configurar las funcionalidades que se describen a continuación mediante la [extremo de los servidores de destino](../authoring-api/destination-server/create-destination-server.md).

* [Especificaciones del servidor](destination-server/server-specs.md): Una plantilla de configuración que contiene información sobre la ubicación de almacenamiento o el extremo HTTP al que se envían los datos.
* [Especificaciones de plantilla](destination-server/templating-specs.md): En esta plantilla, puede definir cómo estructurar la solicitud de API HTTP al extremo, incluido cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite la plataforma. Use esta información junto con la variable [formato del mensaje](destination-server/message-format.md) documentación.
* [Formato del mensaje](destination-server/message-format.md): En esta sección se trata la información detallada sobre los idiomas de plantilla admitidos, los formatos de mensaje y la información requerida por Adobe para configurar la integración con su plataforma. Use esta información junto con la variable [especificaciones de plantilla](destination-server/templating-specs.md) documentación.
* [Especificaciones del archivo](destination-server/file-formatting.md): Una plantilla de configuración que incluye las opciones de formato y compresión de archivos para el destino del lote.

## Configuración de destino {#destination-configuration}

Este extremo de configuración contiene información básica y avanzada sobre el destino. Por ejemplo, aquí es donde especifica los tipos de identidad que su destino puede admitir, el formato deseado de archivos exportados (para destinos basados en archivos) y varios atributos de interfaz de usuario para su tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.

Consulte la documentación siguiente para obtener detalles sobre cada uno de los componentes de configuración de destino. Puede configurar las funcionalidades que se describen a continuación mediante la [extremo de destinos](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuración de autenticación de cliente](destination-configuration/customer-authentication.md): Seleccione el mecanismo de autenticación que el Experience Platform debe utilizar para conectarse al destino. Esta configuración genera la variable [Configurar nuevo destino](../../ui/connect-destination.md) en la interfaz de usuario del Experience Platform, donde los usuarios se conectan Experience Platform a las cuentas que tienen con el destino.
* [Autenticación OAuth2](destination-configuration/oauth2-authentication.md): Obtenga información sobre todas las [!DNL OAuth2] flujos de autenticación admitidos por el Destination SDK y obtener instrucciones para configurar [!DNL OAuth2] autenticación para el destino.
* [Campos de datos del cliente](destination-configuration/customer-data-fields.md): Aprenda a crear campos de entrada en la interfaz de usuario del Experience Platform que permitan a los usuarios especificar información relevante para la conexión y exportación de datos al destino.
* [Atributos de interfaz de usuario](destination-configuration/ui-attributes.md): Obtenga información sobre cómo configurar los atributos de la interfaz de usuario, como el vínculo de documentación, la categoría de tarjeta de destino y el tipo y la frecuencia de conexión de destino, para los destinos creados con el Destination SDK.
* [Configuración del esquema](destination-configuration/schema-configuration.md): Obtenga información sobre cómo definir el esquema de destino al que los usuarios pueden asignar atributos e identidades de perfil.
* [Configuración del área de nombres de identidad](destination-configuration/identity-namespace-configuration.md): Obtenga información sobre cómo configurar las identidades admitidas por su destino. Esta configuración rellena las identidades de destino en la variable [paso de asignación](../../ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario del Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema en el destino.
* [Entrega de destino](destination-configuration/destination-delivery.md): Obtenga información sobre cómo configurar dónde se dirigen exactamente los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que llegan los datos.
* [Configuración de metadatos de audiencia](destination-configuration/audience-metadata-configuration.md): Descubra cómo los metadatos de segmentos, como los nombres o ID de segmentos, deben compartirse entre el Experience Platform y el destino.
* [Política de agregación](destination-configuration/aggregation-policy.md): Aprenda a configurar una directiva de agregación para determinar cómo se deben agrupar y agrupar las solicitudes HTTP al destino.
* [Configuración por lotes](destination-configuration/batch-configuration.md): Configure varios ajustes de nomenclatura de archivos y programación de exportación disponibles para los usuarios al conectarse al destino en la interfaz de usuario del Experience Platform.
* [Calificaciones históricas de perfil](destination-configuration/historical-profile-qualifications.md): Obtenga información sobre las cualificaciones de perfil históricas admitidas por los destinos creados con Destination SDK.

## Configuración de metadatos de audiencia {#audience-metadata-configuration}

Este componente le permite configurar cómo se crean, actualizan o eliminan las audiencias y segmentos mediante programación en el destino. Para los destinos basados en archivos, le permite configurar una notificación cada vez que los archivos se envíen correctamente a su destino. Puede configurar esta funcionalidad a través de la [extremo audience-templates](../metadata-api/create-audience-template.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora tiene una visión general de la funcionalidad proporcionada por el Destination SDK y qué páginas leer para obtener más información sobre configuraciones específicas. A continuación, puede leer las guías que incluyen todos los pasos para [configuración de una transmisión](../guides/configure-destination-instructions.md) o [destino basado en archivos](../guides/configure-file-based-destination-instructions.md) mediante Destination SDK.
