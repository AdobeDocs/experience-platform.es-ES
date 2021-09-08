---
description: El servicio de destinos en Adobe Experience Platform utiliza plantillas de configuración para varios componentes que crean la funcionalidad de destinos. Estos componentes combinados permiten al Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital.
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: Opciones de configuración en el SDK de destino
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 1%

---

# Opciones de configuración en el SDK de destino

## Información general {#overview}

El servicio de destinos en Adobe Experience Platform utiliza plantillas de configuración para varios componentes que crean la funcionalidad de destinos. Estos componentes combinados permiten al Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital. Las plantillas utilizadas en Adobe Experience Platform son:

* **Configuración** de destino: Contiene información básica sobre el destino. Esta configuración incluye los tipos de identidad que su destino puede admitir y varios atributos de interfaz de usuario para su tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.
* **Especificaciones** de servidor y plantilla: Une información sobre las especificaciones del servidor y la plantilla utilizada por Adobe para entregar cargas útiles a su destino.
   * **Especificaciones** del servidor: Una plantilla que almacena los detalles del punto final.
   * **Especificaciones de plantilla**: En esta plantilla, puede definir cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite su plataforma. Para obtener información detallada sobre los idiomas de plantilla admitidos, los formatos de mensaje y la información requerida por Adobe para configurar la integración con su plataforma, lea [Message format](./message-format.md).
* **Configuración** de autenticación: Estos ajustes definen cómo se conectan los usuarios de Adobe Experience Platform con el destino.
* **Configuración** de metadatos de audiencia: Esta plantilla le permite configurar la forma en que se crean, actualizan o eliminan las audiencias o segmentos mediante programación en el destino.

![Plantillas y configuraciones del SDK de destino](./assets/self-service-configuration.png)

## Vínculos relacionados {#related-links}

Las páginas siguientes proporcionan más detalles sobre la funcionalidad y las opciones de configuración disponibles en el SDK de destino, así como las operaciones de API correspondientes que puede realizar.

| Descripción de funcionalidad | Referencia de API |
|--- |--- |
| [Configuración de destino](./destination-configuration.md) | [Operaciones de extremo de la API de destinos](./destination-configuration-api.md) |
| [Especificaciones de servidor y plantilla](./server-and-template-configuration.md) | [Operaciones de extremo de API de servidores de destino](./destination-server-api.md) |
| [Configuración de autenticación](./credentials-configuration.md) | [Operaciones de API de extremo de credenciales](./credentials-configuration-api.md) |
| [Gestión de metadatos de audiencia](./audience-metadata-management.md) | [Operaciones de API de extremo de metadatos de audiencia](./audience-metadata-api.md) |
| [Configuración de OAuth 2](./oauth2-authentication.md) | Realice la configuración utilizando el parámetro `customerAuthenticationConfigurations` en el extremo [/API de destinos](./destination-configuration-api.md). |
| [Formato del mensaje](./message-format.md) | - |
| [Pruebas de destino](./test-destination.md) | [Operaciones de API de prueba de destino](./destination-testing-api.md) |
| [Publicación de destino](./configure-destination-instructions.md#publish-destination) | [Operaciones de API de publicación de destino](./destination-publish-api.md) |
