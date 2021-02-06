---
keywords: Experience Platform;inicio;temas populares;ECID;ecid
solution: Experience Platform
title: Datos de identidad para solicitudes de privacidad
topic: overview
description: Este documento proporciona una guía general sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---


# Datos de identidad para solicitudes de privacidad

Para que Adobe Experience Platform [!DNL Privacy Service] procese las solicitudes de los clientes para sus datos privados (incluidas las solicitudes de acceso, eliminación o exclusión de la venta), se le deben proporcionar identificadores únicos que vinculen a un cliente específico con sus datos privados almacenados en las aplicaciones habilitadas para Adobe Experience Cloud. [!DNL Privacy Service] a continuación, utiliza estos identificadores para recopilar todos los datos almacenados bajo la identidad del cliente  [!DNL Experience Cloud]y procesarlos según la solicitud del cliente.

Este documento proporciona una guía general sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.

## Identidades y Áreas de nombres

Cuando un cliente puede interactuar con su marca a través de varios canales diferentes, puede resultar difícil reconciliar los identificadores dispares que se registran a partir de esas muchas interacciones. Esto a su vez puede dificultar la determinación de los datos que pertenecen a una persona en particular en sus aplicaciones [!DNL Experience Cloud].

Por ejemplo, al administrar solicitudes de datos de clientes en [!DNL Privacy Service], una identidad puede representar un valor de cookie establecido en un dominio controlado por Adobes, un valor de cookie bajo un dominio de terceros y compartido con Adobe o un identificador personalizado que usted defina explícitamente en su organización de IMS.

Por lo tanto, es necesario que cada identidad enviada a [!DNL Privacy Service] vaya acompañada de una Área de nombres que proporcione contexto al relacionar el valor de identidad con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service mantiene un almacén de Áreas de nombres de identidad definidas globalmente y definidas por el usuario. Para obtener información más detallada sobre Áreas de nombres, consulte la [información general de la Área de nombres de identidad](../identity-service/namespaces.md). Para obtener una lista de Áreas de nombres estándar y calificadores de Área de nombres que se utilizan comúnmente en [!DNL Privacy Service], consulte la [sección del apéndice](api/appendix.md) en la guía para desarrolladores.

## ECID y servicio de inclusión

Adobe Experience Cloud [!DNL Identity Service] sirve como un marco de identificación común para [!DNL Experience Cloud] y asigna una ID única y persistente a cada visitante del sitio. El [!DNL Experience Cloud] ID (ECID) hace un seguimiento de la actividad de un cliente mediante el uso de una cookie de origen, puede identificar de forma exclusiva un dispositivo en varias aplicaciones y le permite identificar el mismo visitante del sitio y sus datos en diferentes aplicaciones [!DNL Experience Cloud]. Consulte la [información general del servicio de identidad de Experience Cloud](https://docs.adobe.com/content/help/es-ES/id-service/using/intro/overview.html) para obtener más información.

El servicio de inclusión, una extensión de [!DNL Experience Cloud Identity Service], le permite configurar protocolos en la aplicación para que los visitantes puedan determinar si puede configurar una cookie en el dispositivo o explorador del visitante. Para obtener información más detallada sobre el servicio de inclusión, incluido cómo configurar el servicio para su aplicación, consulte la [documentación del servicio de inclusión](https://docs.adobe.com/content/help/es-ES/id-service/using/implementation/opt-in-service/optin-overview.html).

Una vez que se han asignado los ECID a los visitantes del sitio, puede utilizar el Adobe [!DNL Privacy JavaScript Library] para recuperar esos ID para utilizarlos en solicitudes de privacidad, como se describe en la siguiente sección.

## [!DNL Privacy JS Library]

El [!DNL Adobe Privacy JavaScript Library] proporciona varias funciones que le permiten recuperar y eliminar identidades de cliente almacenadas en el explorador. La biblioteca se puede configurar para recuperar información de identidad de varias aplicaciones de Adobe, incluido ECID. Mediante el uso de rellamadas o promesas, puede administrar mediante programación ID recuperados correctamente y enviarlos a la API [!DNL Privacy Service].

Para obtener más información sobre [!DNL Privacy JS Library], incluyendo ejemplos de código para varios casos de uso común, consulte la [información general de la Biblioteca de JS de privacidad](js-library.md).

## Pasos siguientes

Este documento proporciona una breve descripción general de los conceptos centrales involucrados en la recuperación de datos de identidad del cliente para su uso en solicitudes de privacidad. Se recomienda revisar los vínculos de documentación proporcionados en cada sección para obtener información más detallada sobre estos conceptos y servicios. Para ver los pasos sobre cómo enviar los ID recuperados a [!DNL Privacy Service] para crear solicitudes de acceso, eliminación o exclusión de venta, consulte la [guía para desarrolladores de Privacy Service](api/getting-started.md).