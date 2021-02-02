---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API;perfil unificado;Perfil unificado;unificado;Perfil;rtcp;habilitar perfil;Habilitar perfil
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
description: La API de Perfil de cliente en tiempo real incluye varios extremos para explorar y trabajar con datos de Perfil, como ver perfiles, crear y actualizar políticas de combinación, exportar o muestrear datos de Perfil y eliminar datos de Perfil que ya no necesite o que se agregaron por error.
translation-type: tm+mt
source-git-commit: 823d89ab37156e775a2879e3a2c91bfd911b83bb
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guía para desarrolladores de API

[!DNL Real-time Customer Profile] le permite ver una vista holística de cada uno de sus clientes individuales dentro de Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente.

La API [!DNL Real-time Customer Profile] incluye varios extremos, que se describen a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la [guía de introducción](getting-started.md) para obtener información importante sobre los encabezados requeridos, leer llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, visite el [Intercambio de referencia de la API de Perfil del cliente en tiempo real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Para obtener una guía sobre cómo trabajar con [!DNL Real-time Customer Profile] datos en la interfaz de usuario de [!DNL Experience Platform], consulte la [guía del usuario de Perfil](../ui/user-guide.md).

## (Alfa) Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Puede crear, vista, editar y eliminar atributos calculados mediante el extremo `config/computedAttributes`. Para aprender a usar este extremo, visite la [guía de extremo de atributos calculados](computed-attributes.md).

## Proyecciones de Edge {#edge-projections}

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La API [!DNL Real-time Customer Profile] proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde se debe enrutar una proyección. Para obtener información detallada sobre cómo trabajar con proyecciones de Edge, visite la [guía de parámetros de destinos y configuraciones de proyección](edge-projections.md).

## Entidades ([!DNL Profile] acceso) {#entities}

A través de Adobe Experience Platform puede acceder a [!DNL Real-time Customer Profile] datos mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la [guía de extremo de las entidades](entities.md). Para acceder a perfiles mediante la [!DNL Platform] interfaz de usuario, consulte la [guía del usuario de Perfil](../ui/user-guide.md).

## Exportar trabajos ([!DNL Profile] exportar) {#profile-export}

[!DNL Real-time Customer Profile] los datos se pueden exportar a un conjunto de datos para un procesamiento posterior, como exportar segmentos de audiencia para activación o atributos de perfil para sistema de informes. Los trabajos de exportación para segmentos de audiencia forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Para obtener más información, lea la guía del extremo de trabajos de exportación de [segmentación](../../profile/api/export-jobs.md). Para obtener instrucciones paso a paso sobre cómo crear y administrar trabajos de exportación para atributos de perfil, visite la [guía de extremo de trabajos de exportación](export-jobs.md).

## Combinar directivas {#merge-policies}

Al reunir datos de múltiples fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Mediante la API [!DNL Real-time Customer Profile], puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre cómo trabajar con políticas de combinación mediante la API, visite la [guía de extremo de directivas de combinación](merge-policies.md).

Para obtener una guía sobre cómo trabajar con políticas de combinación mediante la [!DNL Platform] interfaz de usuario, consulte la [guía del usuario de directivas de combinación](../ui/merge-policies.md).

## Estado de muestra de previsualización ([!DNL Profile] previsualización) {#profile-preview}

Como los datos habilitados para Perfil se ingieren en Experience Platform, se almacenan en el almacén de datos de Perfil. A medida que aumenta o disminuye el número de registros en el almacén de Perfiles, se ejecuta un trabajo de muestra que incluye información sobre cuántos fragmentos de perfil y perfiles combinados hay en el almacén de datos. Mediante la API de Perfil puede realizar previsualizaciones de la muestra más reciente de éxito, así como de la distribución de perfiles de lista por conjunto de datos y por Área de nombres de identidad. Para empezar a utilizar el extremo `/profilepreviewstatus`, consulte la guía del extremo de estado de muestra de [previsualización](preview-sample-status.md).

## Trabajos del sistema de perfil {#profile-system-jobs}

Los datos habilitados para perfiles que se ingieren en [!DNL Platform] se almacenan en el [!DNL Data Lake], así como en el almacén de datos [!DNL Real-time Customer Profile]. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del almacén [!DNL Profile] para eliminar los datos que ya no necesite o que se agregaron por error. Esto requiere utilizar la API para crear un [!DNL Profile System Job], también conocido como &quot;[!DNL delete request]&quot;, que se puede modificar, supervisar o eliminar si es necesario. Para aprender a trabajar con solicitudes de eliminación mediante el extremo `/system/jobs` de la API [!DNL Real-time Customer Profile], siga los pasos descritos en la [guía del extremo de trabajos del sistema de perfil](profile-system-jobs.md).

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas mediante la API [!DNL Real-time Customer Profile], lea la [guía de introducción](getting-started.md) y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos relacionados con [!DNL Profile]. Para trabajar con datos [!DNL Profile] mediante la interfaz de usuario [!DNL Experience Platform], consulte la [Guía del usuario de Perfil del cliente en tiempo real](../ui/user-guide.md).