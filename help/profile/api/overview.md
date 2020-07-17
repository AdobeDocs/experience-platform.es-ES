---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guía para desarrolladores de API

[!DNL Real-time Customer Profile] le permite ver una vista holística de cada uno de sus clientes individuales dentro del Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente.

La [!DNL Real-time Customer Profile] API incluye varios extremos, como se describe a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la guía [de](getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, la lectura de llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, consulte el marcador de referencia de la API de Perfil del cliente en tiempo [real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alfa) Atributos calculados

>[!IMPORTANT]
>
>
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Puede crear, vista, editar y eliminar atributos calculados mediante el `config/computedAttributes` punto final. Para obtener información sobre cómo utilizar este extremo, visite la guía del extremo de atributos [calculados](computed-attributes.md).

## Proyecciones de Edge

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La [!DNL Real-time Customer Profile] API proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde se debe enrutar una proyección. Para obtener información detallada sobre cómo trabajar con proyecciones de borde, visite la guía [de configuraciones de](edge-projections.md)proyección y puntos finales de destinos.

## Entidades (acceso a Perfil) {#entities}

Mediante Adobe Experience Platform puede acceder a [!DNL Real-time Customer Profile] los datos mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la guía [de extremo de](entities.md)las entidades. Para acceder a perfiles mediante la [!DNL Platform] IU, consulte la guía [del usuario de](../ui/user-guide.md)Perfil.

## Combinar directivas

Al reunir datos de varias fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Con la API, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. [!DNL Real-time Customer Profile] Para obtener más información sobre cómo trabajar con políticas de combinación mediante la API, visite la guía [de extremo de directivas de](merge-policies.md)combinación.

Para obtener una guía sobre cómo trabajar con políticas de combinación mediante la [!DNL Platform] interfaz de usuario, consulte la guía [del usuario](../ui/merge-policies.md)Combinar directivas.

## Trabajos del sistema de Perfil

Los datos ingeridos en [!DNL Platform] se almacenan tanto en el almacén [!DNL Data Lake] como en el [!DNL Real-time Customer Profile] almacén de datos. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del [!DNL Profile] almacén para eliminar los datos que ya no necesite o que se agregaron por error. Esto requiere utilizar la API para crear una [!DNL Profile System Job], conocida como &quot;[!DNL delete request]&quot;, que también se puede modificar, supervisar o eliminar si es necesario. Para aprender a trabajar con solicitudes de eliminación mediante el `/system/jobs` punto final de la [!DNL Real-time Customer Profile] API, siga los pasos descritos en la guía [de extremo de trabajos del sistema de](profile-system-jobs.md)perfil.

## Pasos siguientes

Para empezar a realizar llamadas mediante la [!DNL Real-time Customer Profile] API, lea la guía [de](getting-started.md) introducción y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales [!DNL Profile]relacionados específicos. Para obtener más información sobre cómo trabajar con [!DNL Profile] datos mediante la [!DNL Platform] interfaz de usuario, consulte la guía [de usuario de Perfil para clientes en tiempo](../ui/user-guide.md)real.