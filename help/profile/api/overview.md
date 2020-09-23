---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
description: La API de Perfil del cliente en tiempo real incluye varios extremos, que se describen a continuación.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guía para desarrolladores de API

[!DNL Real-time Customer Profile] le permite ver una vista holística de cada uno de sus clientes individuales dentro de Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente.

La [!DNL Real-time Customer Profile] API incluye varios extremos, como se describe a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la guía [de](getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, la lectura de llamadas de API de muestra y mucho más.

Para realizar la vista de todos los extremos disponibles y de las operaciones de CRUD, visite el marcador Referencia de la API de Perfil del cliente en tiempo [real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Para obtener una guía sobre cómo trabajar con [!DNL Real-time Customer Profile] datos en la [!DNL Experience Platform] interfaz de usuario, consulte la guía [del usuario de](../ui/user-guide.md)Perfil.

## (Alfa) Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Puede crear, vista, editar y eliminar atributos calculados mediante el `config/computedAttributes` punto final. Para obtener información sobre cómo utilizar este extremo, visite la guía del extremo de atributos [calculados](computed-attributes.md).

## Proyecciones de Edge {#edge-projections}

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La [!DNL Real-time Customer Profile] API proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde se debe enrutar una proyección. Para obtener información detallada sobre cómo trabajar con proyecciones de borde, visite la guía [de configuraciones de](edge-projections.md)proyección y puntos finales de destinos.

## Entidades ([!DNL Profile] acceso) {#entities}

A través de Adobe Experience Platform puede acceder a [!DNL Real-time Customer Profile] los datos mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la guía [de extremo de](entities.md)las entidades. Para acceder a perfiles mediante la [!DNL Platform] IU, consulte la guía [del usuario de](../ui/user-guide.md)Perfil.

## Trabajos de exportación ([!DNL Profile] exportación) {#profile-export}

[!DNL Real-time Customer Profile] los datos se pueden exportar a un conjunto de datos para un procesamiento posterior, como exportar segmentos de audiencia para activación o atributos de perfil para sistema de informes. Los trabajos de exportación para segmentos de audiencia forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Lea la guía [de extremo de trabajos de exportación de](../../profile/api/export-jobs.md) segmentación para obtener más información. Para obtener instrucciones paso a paso sobre cómo crear y administrar trabajos de exportación para atributos de perfil, visite la guía de extremo de trabajos de [exportación](export-jobs.md).

## Combinar directivas {#merge-policies}

Al reunir datos de varias fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Con la API, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. [!DNL Real-time Customer Profile] Para obtener más información sobre cómo trabajar con políticas de combinación mediante la API, visite la guía [de extremo de directivas de](merge-policies.md)combinación.

Para obtener una guía sobre cómo trabajar con políticas de combinación mediante la [!DNL Platform] interfaz de usuario, consulte la guía [del usuario de directivas de](../ui/merge-policies.md)combinación.

## Estado de muestra de previsualización ([!DNL Profile] previsualización) {#profile-preview}

Como los datos habilitados para Perfil se ingieren en Experience Platform, se almacenan en el almacén de datos de Perfil. A medida que aumenta o disminuye el número de registros en el almacén de Perfiles, se ejecuta un trabajo de muestra que incluye información sobre cuántos fragmentos de perfil y perfiles combinados hay en el almacén de datos. Mediante la API de Perfil puede realizar previsualizaciones de la muestra más reciente de éxito, así como de la distribución de perfiles de lista por conjunto de datos y por Área de nombres de identidad. Para empezar a usar el punto final, consulte la guía `/profilepreviewstatus` de extremo de estado de muestra de [previsualización](preview-sample-status.md).

## Trabajos del sistema de perfil {#profile-system-jobs}

Los datos ingeridos en [!DNL Platform] se almacenan tanto en el almacén [!DNL Data Lake] como en el [!DNL Real-time Customer Profile] almacén de datos. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del [!DNL Profile] almacén para eliminar los datos que ya no necesite o que se agregaron por error. Esto requiere utilizar la API para crear una [!DNL Profile System Job], conocida como &quot;[!DNL delete request]&quot;, que también se puede modificar, supervisar o eliminar si es necesario. Para aprender a trabajar con solicitudes de eliminación mediante el `/system/jobs` punto final de la [!DNL Real-time Customer Profile] API, siga los pasos descritos en la guía [de extremo de trabajos del sistema de](profile-system-jobs.md)perfil.

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas mediante la [!DNL Real-time Customer Profile] API, lea la guía [de](getting-started.md) introducción y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales [!DNL Profile]relacionados específicos. Para trabajar con [!DNL Profile] datos mediante la [!DNL Experience Platform] IU, consulte la guía [de usuario de Perfil de clientes en tiempo](../ui/user-guide.md)real.