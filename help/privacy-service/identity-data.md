---
keywords: Experience Platform;inicio;temas populares;ECID;ecid
solution: Experience Platform
title: Datos de identidad para solicitudes de privacidad
description: Este documento proporciona orientación general sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad de los clientes.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Datos de identidad para solicitudes de privacidad

Para que Adobe Experience Platform [!DNL Privacy Service] procese las solicitudes de los clientes relativas a sus datos privados (incluidas las solicitudes de acceso, eliminación o exclusión de la venta), debe contar con identificadores únicos que vinculen a un cliente específico a sus datos privados almacenados en las aplicaciones habilitadas para Adobe Experience Cloud. [!DNL Privacy Service] utiliza estos identificadores para recopilar todos los datos almacenados bajo la identidad del cliente en [!DNL Experience Cloud] y procesarlos de acuerdo con la solicitud del cliente.

Este documento proporciona orientación general sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad de los clientes.

## Identidades y áreas de nombres

Cuando un cliente puede interactuar con su marca a través de varios canales diferentes, puede ser difícil reconciliar los identificadores dispares que se registran a partir de esas muchas interacciones. Esto, a su vez, puede dificultar la determinación de qué datos pertenecen a una persona en particular en sus aplicaciones [!DNL Experience Cloud].

Por ejemplo, al administrar solicitudes de datos de clientes en [!DNL Privacy Service], una identidad puede representar un valor de cookie establecido en un dominio controlado por Adobe, un valor de cookie bajo un dominio de terceros y compartido con Adobe o un identificador personalizado que defina explícitamente dentro de su organización.

Por lo tanto, es necesario que cada identidad enviada a [!DNL Privacy Service] vaya acompañada de un área de nombres que proporcione contexto al relacionar el valor de identidad con su sistema de origen. Un área de nombres puede representar un concepto genérico como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad de Adobe Experience Platform mantiene un almacén de áreas de nombres de identidad definidas globalmente y por el usuario. Para obtener información más detallada sobre las áreas de nombres, vea la [descripción general del área de nombres de identidad](../identity-service/features/namespaces.md). Para obtener una lista de los calificadores de área de nombres y áreas de nombres estándar que se utilizan normalmente en [!DNL Privacy Service], vea la [sección del apéndice](api/appendix.md) en la guía de la API.

## Servicio de inclusión y ECID

Adobe Experience Cloud [!DNL Identity Service] sirve como marco de identificación común para [!DNL Experience Cloud] y asigna un identificador único y persistente a cada visitante del sitio. El ID de [!DNL Experience Cloud] (ECID) hace un seguimiento de la actividad de un cliente mediante el uso de una cookie de origen, puede identificar de forma exclusiva un dispositivo en varias aplicaciones y le permite identificar al mismo visitante del sitio y sus datos en distintas aplicaciones de [!DNL Experience Cloud]. Consulte la [descripción general del servicio de identidad del Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) para obtener más información.

El servicio de inclusión (Opt-in), una extensión de [!DNL Experience Cloud Identity Service], le permite configurar protocolos en su aplicación para que los visitantes puedan determinar si puede establecer una cookie en el dispositivo o el explorador del visitante. Para obtener información más detallada sobre el servicio Opt-in, incluyendo cómo configurar el servicio para su aplicación, consulte [Documentación del servicio Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es).

Una vez que se hayan asignado ECID a los visitantes del sitio, puede utilizar el Adobe [!DNL Privacy JavaScript Library] para recuperar esos ID y utilizarlos en solicitudes de privacidad, tal como se describe en la sección siguiente.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] proporciona varias funciones que le permiten recuperar y quitar identidades de clientes almacenadas en el explorador. La biblioteca se puede configurar para recuperar información de identidad de varias aplicaciones de Adobe, incluido ECID. Mediante llamadas de retorno o promesas, puede controlar mediante programación los ID recuperados correctamente y enviarlos a la API [!DNL Privacy Service].

Para obtener más información sobre [!DNL Privacy JS Library], incluidas muestras de código para varios casos de uso comunes, consulte [Información general sobre la biblioteca JS de privacidad](js-library.md).

## Pasos siguientes

Este documento proporciona una breve descripción de los conceptos centrales implicados en la recuperación de datos de identidad del cliente para su uso en solicitudes de privacidad. Se recomienda revisar los vínculos de documentación proporcionados en cada sección para obtener información más detallada acerca de estos conceptos y servicios. Para ver los pasos de cómo enviar los ID recuperados a [!DNL Privacy Service] para crear solicitudes de acceso, eliminación o exclusión de la venta, consulte la [guía de API de Privacy Service](api/overview.md).
