---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: fd6516d1c1d3792b41de65d0f44d78af1124ccc7
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Guía para desarrolladores de API de Perfil para clientes en tiempo real

El Perfil del cliente en tiempo real le permite ver una vista holística de cada uno de sus clientes individuales dentro del Adobe Experience Platform. Perfil le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente.

La API de Perfil del cliente en tiempo real incluye varios extremos, que se describen a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la guía [de](getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, la lectura de llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, consulte el marcador de referencia de la API de Perfil del cliente en tiempo [real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alfa) Atributos calculados

>[!IMPORTANT]
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Puede crear, vista, editar y eliminar atributos calculados mediante el `config/computedAttributes` punto final. Para obtener información sobre cómo utilizar este extremo, visite la guía del extremo de atributos [calculados](computed-attributes.md).

## Proyecciones de Edge

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La API de Perfil del cliente en tiempo real proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde se debe enrutar una proyección. Para obtener información detallada sobre cómo trabajar con proyecciones de borde, visite la guía [de configuraciones de](edge-projections.md)proyección y puntos finales de destinos.

## Entidades

A través de Adobe Experience Platform puede acceder a los datos de Perfil del cliente en tiempo real mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la guía [de extremo de](entities.md)las entidades. Para acceder a perfiles mediante la interfaz de usuario de Platform, consulte la guía del usuario de [Perfil](../ui/user-guide.md).

## Combinar directivas

Al reunir datos de varias fuentes en Experience Platform, las políticas de combinación son las reglas que Platform utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Mediante la API de Perfil del cliente en tiempo real, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre cómo trabajar con políticas de combinación mediante la API, visite la guía [de extremo de directivas de](merge-policies.md)combinación.

Para obtener una guía sobre cómo trabajar con políticas de combinación mediante la interfaz de usuario de Platform, consulte la guía [del usuario](../ui/merge-policies.md)Combinar directivas.

## Trabajos del sistema de Perfil

Los datos ingeridos en Platform se almacenan en Data Lake y en el almacén de datos de Perfil del cliente en tiempo real. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del almacén de Perfiles para eliminar los datos que ya no necesite o que se agregaron por error. Esto requiere el uso de la API para crear un trabajo de sistema de Perfil, conocido como &quot;solicitud de eliminación&quot;, que también se puede modificar, supervisar o eliminar si es necesario. Para aprender a trabajar con solicitudes de eliminación mediante el `/system/jobs` punto final de la API de Perfil de clientes en tiempo real, siga los pasos descritos en la guía [de extremo de trabajos del sistema de](profile-system-jobs.md)perfil.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Perfil del cliente en tiempo real, lea la guía [de](getting-started.md) introducción y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos relacionados con el Perfil. Para obtener más información sobre el trabajo con datos de Perfil mediante la interfaz de usuario de Platform, consulte la guía [de usuario de Perfil para clientes en tiempo](../ui/user-guide.md)real.