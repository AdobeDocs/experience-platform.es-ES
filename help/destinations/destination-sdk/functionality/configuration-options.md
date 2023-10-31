---
description: El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos. Descubra cómo estos componentes combinados permiten a Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital.
title: Opciones de configuración en Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Opciones de configuración en Destination SDK

El servicio de destinos de Adobe Experience Platform utiliza puntos finales de configuración para varios componentes que crean la funcionalidad de destinos.

Combinados, estos componentes permiten a Experience Platform conectarse a las plataformas de destino, enviar mensajes personalizados, exportar archivos personalizados y activar datos de perfil en todo el ecosistema digital.

El diagrama siguiente muestra información general de alto nivel sobre los componentes que puede configurar mediante Destination SDK para crear su propio destino. Estos componentes se describen más adelante.

![Diagrama que muestra los componentes del Destination SDK, los extremos de configuración y las operaciones admitidas.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuración de servidor {#server-configuration}

La configuración del servidor de destino une información sobre las especificaciones de su servidor y la plantilla utilizada por Adobe para entregar cargas útiles en su destino.

Por ejemplo, aquí es donde especifica los puntos finales de API del lado al que el Experience Platform debe conectarse, así como los encabezados y el formato de las llamadas de API que Platform realizará.

En el caso de los destinos basados en archivos, esta configuración también incluye los formatos de compresión y formato de archivo admitidos para el destino. Puede configurar las funcionalidades que se describen a continuación a través de la [extremo de servidores de destino](../authoring-api/destination-server/create-destination-server.md).

* [Especificaciones del servidor](destination-server/server-specs.md): Una plantilla de configuración que contiene información sobre la ubicación de almacenamiento o el extremo HTTP al que se envían los datos.
* [Especificaciones de plantilla](destination-server/templating-specs.md): en esta plantilla, puede definir cómo estructurar la solicitud de API HTTP a su punto de conexión, incluido cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite su plataforma. Utilice esta información junto con el [formato del mensaje](destination-server/message-format.md) documentación.
* [Formato del mensaje](destination-server/message-format.md): Esta sección trata información detallada sobre los lenguajes de plantilla admitidos, los formatos de mensaje y la información requerida por Adobe para configurar la integración con la plataforma. Utilice esta información junto con el [especificaciones de plantilla](destination-server/templating-specs.md) documentación.
* [Especificaciones de archivo](destination-server/file-formatting.md): Una plantilla de configuración que incluye las opciones de formato y compresión de archivos para el destino del lote.

## Configuración de destino {#destination-configuration}

Este punto de conexión de configuración contiene información básica y avanzada sobre el destino. Por ejemplo, aquí es donde se especifican los tipos de identidad que puede admitir el destino, el formato deseado de los archivos exportados (para destinos basados en archivos) y varios atributos de interfaz de usuario para la tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.

Consulte la documentación siguiente para obtener detalles sobre cada uno de los componentes de configuración de destino. Puede configurar las funcionalidades que se describen a continuación a través de la [extremo de destinos](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuración de autenticación del cliente](destination-configuration/customer-authentication.md): seleccione el mecanismo de autenticación que el Experience Platform debe utilizar para conectarse al destino. Esta configuración genera el [Configurar nuevo destino](../../ui/connect-destination.md) página de la interfaz de usuario de Experience Platform, donde los usuarios se conectan con Experience Platform a las cuentas que tienen con el .
* [Autenticación OAuth2](destination-configuration/oauth2-authentication.md): Obtenga información acerca de todos los [!DNL OAuth2] flujos de autenticación admitidos por el Destination SDK y obtenga instrucciones para configurarlos [!DNL OAuth2] para su destino..
* [Campos de datos del cliente](destination-configuration/customer-data-fields.md): Aprenda a crear campos de entrada en la interfaz de usuario de Experience Platform que permitan a los usuarios especificar información diversa relevante para cómo conectar y exportar datos a su destino.
* [Atributos de IU](destination-configuration/ui-attributes.md): Obtenga información sobre cómo configurar los atributos de la interfaz de usuario, como el vínculo de documentación, la categoría de la tarjeta de destino, el tipo de conexión de destino y la frecuencia, para los destinos creados con Destination SDK.
* [Configuración del esquema](destination-configuration/schema-configuration.md): Aprenda a definir el esquema de destino al que los usuarios pueden asignar atributos e identidades de perfil.
* [Configuración del área de nombres de identidad](destination-configuration/identity-namespace-configuration.md): Obtenga información sobre cómo configurar las identidades admitidas en el destino. Esta configuración rellena las identidades de destinatario en la variable [paso de asignación](../../ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario de Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema de destino.
* [Envío de destino](destination-configuration/destination-delivery.md): Obtenga información sobre cómo configurar a dónde van exactamente los datos exportados y qué regla de autenticación se utiliza en la ubicación donde aterrizarán los datos.
* [Configuración de metadatos de audiencia](destination-configuration/audience-metadata-configuration.md): Descubra cómo los metadatos de audiencia, como nombres de audiencias o ID, deben compartirse entre el Experience Platform y el destino.
* [Política de agregación](destination-configuration/aggregation-policy.md): Obtenga información sobre cómo configurar una directiva de agregación para determinar cómo se deben agrupar y agrupar las solicitudes HTTP al destino.
* [Configuración por lotes](destination-configuration/batch-configuration.md): configure los distintos ajustes de nomenclatura de archivos y programación de exportación disponibles para los usuarios al conectarse al destino en la interfaz de usuario del Experience Platform.
* [Cualificaciones históricas del perfil](destination-configuration/historical-profile-qualifications.md): obtenga información acerca de las cualificaciones de perfil históricas admitidas por los destinos creados con Destination SDK.

## Configuración de metadatos de audiencia {#audience-metadata-configuration}

Este componente le permite configurar cómo se crean, actualizan o eliminan las audiencias en el destino mediante programación. En el caso de los destinos basados en archivos, permite configurar una notificación cada vez que los archivos se envían correctamente al destino. Puede configurar esta funcionalidad mediante las opciones [extremo de audience-templates](../metadata-api/create-audience-template.md).

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora tiene una visión general de la funcionalidad proporcionada por Destination SDK y qué páginas leer para obtener más información acerca de configuraciones específicas. A continuación, puede leer las guías que incluyen todos los pasos para [configuración de una transmisión por secuencias](../guides/configure-destination-instructions.md) o una [destino basado en archivos](../guides/configure-file-based-destination-instructions.md) mediante el uso de Destination SDK.
