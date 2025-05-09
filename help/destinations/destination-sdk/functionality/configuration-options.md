---
description: El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos. Descubra cómo estos componentes combinados permiten a Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital.
title: Opciones de configuración en Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Opciones de configuración en Destination SDK

El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos.

Combinados, estos componentes permiten a Experience Platform conectarse a plataformas de destino, enviar mensajes personalizados, exportar archivos personalizados y activar datos de perfil en todo el ecosistema digital.

El diagrama siguiente muestra información general de alto nivel sobre los componentes que puede configurar a través de Destination SDK para crear su propio destino. Estos componentes se describen más adelante.

>[!BEGINSHADEBOX]

![Diagrama que muestra los componentes de Destination SDK, los extremos de configuración y las operaciones admitidas.](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## Configuración del servidor {#server-configuration}

La configuración del servidor de destino une información sobre las especificaciones de su servidor y la plantilla utilizada por Adobe para entregar cargas útiles en su destino.

Por ejemplo, aquí es donde especifica los puntos finales de API del lado al que Experience Platform debe conectarse, así como los encabezados y el formato de las llamadas de API que Experience Platform realizará.

En el caso de los destinos basados en archivos, esta configuración también incluye los formatos de compresión y formato de archivo admitidos para el destino. Puede configurar las funcionalidades que se describen a continuación a través del [extremo de servidores de destino](../authoring-api/destination-server/create-destination-server.md).

* [Especificaciones del servidor](destination-server/server-specs.md): Una plantilla de configuración que contiene información sobre la ubicación de almacenamiento o el extremo HTTP al que se envían los datos.
* [Especificaciones de la plantilla](destination-server/templating-specs.md): en esta plantilla, puede definir cómo estructurar la solicitud de API HTTP para su extremo, incluido cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite su plataforma. Use esta información junto con la documentación de [formato de mensaje](destination-server/message-format.md).
* [Formato del mensaje](destination-server/message-format.md): Esta sección trata información detallada sobre los idiomas de plantilla admitidos, los formatos de mensaje y la información requerida por Adobe para configurar la integración con su plataforma. Use esta información junto con la documentación de [especificaciones de plantilla](destination-server/templating-specs.md).
* [Especificaciones de archivo](destination-server/file-formatting.md): Una plantilla de configuración que incluye las opciones de formato y compresión de archivos para el destino del lote.

## Configuración de destino {#destination-configuration}

Este punto de conexión de configuración contiene información básica y avanzada sobre el destino. Por ejemplo, aquí es donde se especifican los tipos de identidad que puede admitir el destino, el formato deseado de los archivos exportados (para destinos basados en archivos) y varios atributos de interfaz de usuario para la tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.

Consulte la documentación siguiente para obtener detalles sobre cada uno de los componentes de configuración de destino. Puede configurar las funcionalidades descritas a continuación a través del [extremo de destinos](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuración de autenticación del cliente](destination-configuration/customer-authentication.md): seleccione el mecanismo de autenticación que Experience Platform debe usar para conectarse a su destino. Esta configuración genera la página [Configurar nuevo destino](../../ui/connect-destination.md) en la interfaz de usuario de Experience Platform, donde los usuarios conectan Experience Platform a las cuentas que tienen con el destino.
* [Autorización de OAuth2](destination-configuration/oauth2-authorization.md): Obtenga información acerca de todos los flujos de autenticación de [!DNL OAuth2] admitidos por Destination SDK y obtenga instrucciones para configurar la autenticación de [!DNL OAuth2] para su destino.
* [Campos de datos del cliente](destination-configuration/customer-data-fields.md): Aprenda a crear campos de entrada en la interfaz de usuario de Experience Platform que permitan a los usuarios especificar información diversa relacionada con la forma de conectar y exportar datos a su destino.
* [Atributos de interfaz de usuario](destination-configuration/ui-attributes.md): Obtenga información sobre cómo configurar los atributos de la interfaz de usuario, como el vínculo a la documentación, la categoría de la tarjeta de destino, y el tipo y la frecuencia de conexión de destino, para los destinos creados con Destination SDK.
* [Configuración de esquema](destination-configuration/schema-configuration.md): Aprenda a definir el esquema de destino al que los usuarios pueden asignar atributos e identidades de perfil.
* [Configuración del área de nombres de identidad](destination-configuration/identity-namespace-configuration.md): Aprenda a configurar las identidades admitidas en el destino. Esta configuración rellena las identidades de destino en el [paso de asignación](../../ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario de Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema del destino.
* [Envío de destino](destination-configuration/destination-delivery.md): Aprenda a configurar a dónde van exactamente los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que aterrizarán los datos.
* [Configuración de metadatos de audiencia](destination-configuration/audience-metadata-configuration.md): descubra cómo los metadatos de audiencia, como nombres de audiencia o ID, deben compartirse entre Experience Platform y su destino.
* [Directiva de agregación](destination-configuration/aggregation-policy.md): Aprenda a configurar una directiva de agregación para determinar cómo se deben agrupar y agrupar las solicitudes HTTP a su destino.
* [Configuración por lotes](destination-configuration/batch-configuration.md): configure varias opciones de nomenclatura de archivos y programación de exportación disponibles para los usuarios al conectarse a su destino en la interfaz de usuario de Experience Platform.
* [Calificaciones de perfil históricas](destination-configuration/historical-profile-qualifications.md): obtenga información acerca de las clasificaciones de perfil históricas admitidas por los destinos creados con Destination SDK.

## Configuración de metadatos de audiencia {#audience-metadata-configuration}

Este componente le permite configurar cómo se crean, actualizan o eliminan las audiencias en el destino mediante programación. En el caso de los destinos basados en archivos, permite configurar una notificación cada vez que los archivos se envían correctamente al destino. Puede configurar esta funcionalidad a través del extremo [audience-templates](../metadata-api/create-audience-template.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora tiene una visión general de la funcionalidad proporcionada por Destination SDK y de las páginas que se deben leer para obtener más información acerca de configuraciones específicas. A continuación, puedes leer las guías que incluyen todos los pasos para [configurar una transmisión por secuencias](../guides/configure-destination-instructions.md) o un [destino basado en archivos](../guides/configure-file-based-destination-instructions.md) mediante Destination SDK.
