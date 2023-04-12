---
keywords: Experience Platform;inicio;temas populares;ECID;ecid
solution: Experience Platform
title: Datos de identidad para solicitudes de privacidad
description: Este documento proporciona instrucciones generales sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# Datos de identidad para solicitudes de privacidad

En orden para Adobe Experience Platform [!DNL Privacy Service] para procesar las solicitudes de los clientes relativas a sus datos privados (incluidas las solicitudes de acceso, eliminación o exclusión de la venta), se deben proporcionar identificadores únicos que vinculen a un cliente específico con sus datos privados almacenados en las aplicaciones habilitadas para Adobe Experience Cloud. [!DNL Privacy Service] a continuación, utiliza estos identificadores para recopilar todos los datos almacenados bajo la identidad del cliente dentro de [!DNL Experience Cloud]y procesarlo según la solicitud del cliente.

Este documento proporciona instrucciones generales sobre cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.

## Identidades y áreas de nombres

Cuando un cliente puede interactuar con su marca a través de varios canales diferentes, puede resultar difícil reconciliar los identificadores dispares que se registran a partir de esas muchas interacciones. Esto a su vez puede dificultar la determinación de qué datos pertenecen a una persona en particular de su [!DNL Experience Cloud] aplicaciones.

Por ejemplo, al gestionar solicitudes de datos de clientes en [!DNL Privacy Service], una identidad puede representar un valor de cookie establecido en un dominio controlado por Adobe, un valor de cookie bajo un dominio de terceros y compartido con Adobe, o un identificador personalizado que defina explícitamente dentro de su organización.

Por lo tanto, es necesario que cada identidad se envíe a [!DNL Privacy Service] va acompañado de un área de nombres que proporcione contexto al relacionar el valor de identidad con su sistema de origen. Un área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad de Adobe Experience Platform mantiene un almacén de áreas de nombres de identidad definidas globalmente y definidas por el usuario. Para obtener información más detallada sobre las áreas de nombres, consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md). Para obtener una lista de áreas de nombres estándar y calificadores de área de nombres que se utilizan comúnmente en [!DNL Privacy Service], consulte la [apéndice, sección](api/appendix.md) en la guía de API.

## ECID y servicio de inclusión (Opt-in)

Adobe Experience Cloud [!DNL Identity Service] sirve como marco común de identificación para [!DNL Experience Cloud]y asigna un ID único y persistente a cada visitante del sitio. La variable [!DNL Experience Cloud] El ID (ECID) rastrea la actividad de un cliente mediante el uso de una cookie de origen, puede identificar de forma exclusiva un dispositivo en varias aplicaciones y le permite identificar al mismo visitante del sitio y sus datos en diferentes [!DNL Experience Cloud] aplicaciones. Consulte la [Resumen del servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) para obtener más información.

Servicio Opt-in, una extensión de [!DNL Experience Cloud Identity Service], permite configurar protocolos en la aplicación para que los visitantes puedan determinar si se puede configurar una cookie en el dispositivo o explorador del visitante. Para obtener información más detallada sobre el servicio de inclusión (Opt-in), incluido cómo configurar el servicio para su aplicación, consulte [Documentación del servicio Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es).

Una vez que se hayan asignado ECID a los visitantes del sitio, puede utilizar el Adobe [!DNL Privacy JavaScript Library] para recuperar esos ID para usarlos en solicitudes de privacidad, como se describe en la siguiente sección.

## [!DNL Privacy JS Library]

La variable [!DNL Adobe Privacy JavaScript Library] proporciona varias funciones que le permiten recuperar y eliminar identidades de clientes que están almacenadas en el explorador. La biblioteca se puede configurar para recuperar información de identidad de varias aplicaciones de Adobe, incluido ECID. Mediante llamadas de retorno o promesas, puede administrar mediante programación los ID recuperados correctamente y enviarlos al [!DNL Privacy Service] API.

Para obtener más información, consulte [!DNL Privacy JS Library], incluidas las muestras de código para varios casos de uso comunes, consulte la [Resumen de la biblioteca de Privacy JS](js-library.md).

## Pasos siguientes

Este documento ofrece una breve descripción general de los conceptos centrales involucrados en la recuperación de datos de identidad de los clientes para su uso en solicitudes de privacidad. Se recomienda revisar los vínculos de documentación proporcionados en cada sección para obtener información más detallada sobre estos conceptos y servicios. Para ver los pasos sobre cómo enviar los ID recuperados a [!DNL Privacy Service] para crear solicitudes de acceso, eliminación o exclusión de la venta, consulte [Guía de API del Privacy Service](api/overview.md).
