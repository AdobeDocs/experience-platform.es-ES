---
description: El servicio de destinos en Adobe Experience Platform utiliza plantillas de configuración para varios componentes que crean la funcionalidad de destinos. Estos componentes combinados permiten al Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital.
title: Opciones de configuración en el Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Opciones de configuración en el Destination SDK

## Información general {#overview}

El servicio de destinos en Adobe Experience Platform utiliza plantillas de configuración para varios componentes que crean la funcionalidad de destinos. Estos componentes combinados permiten al Experience Platform conectarse a socios de destino, enviar mensajes personalizados y activar datos de perfil en todo el ecosistema digital. Las plantillas utilizadas en Adobe Experience Platform son:

* **Configuración de destino**: Contiene información básica sobre el destino. Esta configuración incluye los tipos de identidad que su destino puede admitir y varios atributos de interfaz de usuario para su tarjeta de destino en la interfaz de usuario de Adobe Experience Platform.
* **Especificaciones de servidor y plantilla**: Une información sobre las especificaciones del servidor y la plantilla utilizada por Adobe para entregar cargas útiles a su destino.
   * **Especificaciones del servidor**: Una plantilla que almacena los detalles del punto final.
   * **Especificaciones de plantilla**: En esta plantilla, puede definir cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite su plataforma. Para obtener información detallada sobre los idiomas de plantilla admitidos, los formatos de mensaje y la información requerida por Adobe para configurar la integración con su plataforma, lea [Formato del mensaje](./message-format.md).
* **Configuración de autenticación**: Estos ajustes definen cómo se conectan los usuarios de Adobe Experience Platform con el destino.
* **Configuración de metadatos de audiencia**: Esta plantilla le permite configurar la forma en que se crean, actualizan o eliminan las audiencias o segmentos mediante programación en el destino.

![Plantillas y configuraciones de Destination SDK](./assets/self-service-configuration.png)

## Vínculos relacionados {#related-links}

Las páginas siguientes proporcionan más detalles sobre la funcionalidad y las opciones de configuración disponibles en Destination SDK, así como las operaciones de API correspondientes que puede realizar.

| Descripción de funcionalidad | Referencia de API |
|--- |--- |
| [Configuración de destino](./destination-configuration.md) | [Operaciones de extremo de la API de destinos](./destination-configuration-api.md) |
| [Especificaciones de servidor y plantilla](./server-and-template-configuration.md) | [Operaciones de extremo de API de servidores de destino](./destination-server-api.md) |
| [Configuración de autenticación](./authentication-configuration.md) | [Operaciones de API de extremo de credenciales](./credentials-configuration-api.md) |
| [Gestión de metadatos de audiencia](./audience-metadata-management.md) | [Operaciones de API de extremo de metadatos de audiencia](./audience-metadata-api.md) |
| [Configuración de OAuth 2](./oauth2-authentication.md) | Configure usando la variable `customerAuthenticationConfigurations` en el [punto final de la API /destinos](./destination-configuration-api.md). |
| [Formato del mensaje](./message-format.md) | - |
| [Pruebas de destino](./test-destination.md) | [Operaciones de API de prueba de destino](./destination-testing-api.md) |
| [Publicación de destino](./configure-destination-instructions.md#publish-destination) | [Operaciones de API de publicación de destino](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
