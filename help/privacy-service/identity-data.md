---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datos de identidad para solicitudes de privacidad
topic: overview
translation-type: tm+mt
source-git-commit: f2fe9c01c8355d0b312a0236f76085d1743aa8cc

---


# Datos de identidad para solicitudes de privacidad

Para que Adobe Experience Platform Privacy Service pueda procesar las solicitudes de los clientes de sus datos privados (incluidas las solicitudes de acceso, eliminación o exclusión de la venta), se le deben proporcionar identificadores únicos que vinculen a un cliente específico con sus datos privados almacenados en las aplicaciones habilitadas para Adobe Experience Cloud. A continuación, Privacy Service utiliza estos identificadores para recopilar todos los datos almacenados bajo la identidad del cliente en Experience Cloud y procesarlos según la solicitud del cliente.

Este documento proporciona una guía general sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.

## Identidades y Áreas de nombres

Cuando un cliente puede interactuar con su marca a través de varios canales diferentes, puede resultar difícil reconciliar los identificadores dispares que se registran a partir de esas muchas interacciones. Esto a su vez puede dificultar la determinación de los datos que pertenecen a una persona en particular en las aplicaciones de Experience Cloud.

Por ejemplo, al administrar solicitudes de datos de clientes en Privacy Service, una identidad puede representar un valor de cookie establecido en un dominio controlado por Adobe, un valor de cookie bajo un dominio de terceros y compartido con Adobe o un identificador personalizado que usted defina explícitamente en su organización de IMS.

Por lo tanto, cada identidad enviada al Servicio de Privacidad debe ir acompañada de una **Área de nombres** que proporcione contexto al relacionar el valor de identidad con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Destinatario ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service mantiene una tienda de Áreas de nombres de identidad definidas globalmente y definidas por el usuario. Para obtener información más detallada sobre Áreas de nombres, consulte la descripción general [de la Área de nombres de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)identidad. Para obtener una lista de Áreas de nombres estándar y calificadores de Área de nombres que se utilizan comúnmente en Privacy Service, consulte la sección [del](api/appendix.md) apéndice en la guía para desarrolladores.

## ECID y servicio de inclusión

El servicio de identidad de Adobe Experience Cloud sirve como marco común de identificación para Experience Cloud y asigna un ID único y persistente a cada visitante del sitio. El ID de Experience Cloud (ECID) rastrea la actividad de un cliente mediante el uso de una cookie de origen, puede identificar de forma exclusiva un dispositivo en varias aplicaciones y le permite identificar el mismo visitante de sitio y sus datos en diferentes aplicaciones de Experience Cloud. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) for more information.

El servicio de inclusión, una extensión del servicio de identidad de Experience Cloud, le permite configurar protocolos en la aplicación para que los visitantes puedan determinar si puede configurar una cookie en el dispositivo o explorador del visitante. Para obtener información más detallada sobre el servicio de inclusión, incluido cómo configurar el servicio para su aplicación, consulte la documentación [del servicio de](https://docs.adobe.com/content/help/en/id-service/using/implementation/opt-in-service/optin-overview.html)inclusión.

Una vez que se han asignado los ECID a los visitantes del sitio, puede utilizar la biblioteca JavaScript de privacidad de Adobe para recuperar dichos ID y utilizarlos en solicitudes de privacidad, tal como se describe en la siguiente sección.

## Biblioteca JS de privacidad

La biblioteca JavaScript de privacidad de Adobe proporciona varias funciones que le permiten recuperar y eliminar identidades de cliente almacenadas en el explorador. La biblioteca se puede configurar para recuperar información de identidad de varias aplicaciones de Adobe, incluido ECID. Mediante el uso de rellamadas o promesas, puede gestionar mediante programación los ID recuperados correctamente y enviarlos a la API de Privacy Service.

Para obtener más información acerca de la Biblioteca de JS de privacidad, incluyendo ejemplos de código para varios casos de uso común, consulte la información general [de la Biblioteca de JS de](js-library.md)privacidad.

## Pasos siguientes

Este documento proporciona una breve descripción general de los conceptos centrales involucrados en la recuperación de datos de identidad del cliente para su uso en solicitudes de privacidad. Se recomienda revisar los vínculos de documentación proporcionados en cada sección para obtener información más detallada sobre estos conceptos y servicios. Para ver los pasos sobre cómo enviar los ID recuperados a Privacy Service para crear solicitudes de acceso, eliminación o exclusión de venta, consulte la guía para desarrolladores de [Privacy Service](api/getting-started.md).