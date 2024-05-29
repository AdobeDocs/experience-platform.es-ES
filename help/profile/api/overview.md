---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;perfil unificado;perfil unificado;rtcp;habilitar perfil;habilitar perfil
title: Guía de la API del perfil del cliente en tiempo real
description: La API de perfil del cliente en tiempo real permite a los desarrolladores explorar y trabajar con datos de perfil, incluidos los perfiles de vista, crear y actualizar políticas de combinación, exportar o muestrear datos de perfil y eliminar datos de perfil que ya no sean necesarios o que se hayan añadido por error. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# Guía de la API de [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] le permite ver una vista integral de cada uno de sus clientes individuales dentro de Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable y con marca de hora de cada interacción de clientes.

El [!DNL Real-Time Customer Profile] La API incluye varios extremos, que se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Swagger de referencia de API de perfil de cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Para obtener una guía sobre cómo trabajar con [!DNL Real-Time Customer Profile] datos en la [!DNL Experience Platform] Interfaz de usuario, consulte la [Guía del usuario del perfil](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative} Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
La funcionalidad de atributos calculados está en versión beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin que sea necesario realizar manualmente cálculos complejos cada vez que se necesite la información. Estos valores de atributo calculados se pueden ver en un perfil, utilizarse para crear una audiencia o acceder a ellos a través de una serie de patrones de acceso diferentes.

Puede crear, ver, editar y eliminar atributos calculados mediante la variable `ca/attributes/` punto final. Para aprender a utilizar atributos calculados, consulte la [información general sobre atributos calculados](../computed-attributes/overview.md). Para operaciones de API, visite la [guía de extremo de API de atributos calculados](../computed-attributes/api.md).

## Entidades ([!DNL Profile] access) {#entities}

A través de Adobe Experience Platform puede acceder a [!DNL Real-Time Customer Profile] datos mediante las API de RESTful o la interfaz de usuario de. Para obtener información sobre cómo acceder a entidades, más conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la sección [guía de extremo de entidades](entities.md). Para acceder a los perfiles con [!DNL Platform] IU, consulte la [Guía del usuario del perfil](../ui/user-guide.md).

## Exportar trabajos ([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] los datos se pueden exportar a un conjunto de datos para un procesamiento posterior, como la exportación de audiencias para su activación o de atributos de perfil para la creación de informes. Los trabajos de exportación para audiencias forman parte de [!DNL Adobe Experience Platform Segmentation Service] API, lea la [guía de extremo de trabajos de exportación de segmentación](../../profile/api/export-jobs.md) para obtener más información. Para obtener instrucciones paso a paso sobre cómo crear y administrar trabajos de exportación para atributos de perfil, visite la [guía de extremo de trabajos de exportación](export-jobs.md).

## Políticas de combinación {#merge-policies}

Al unir datos de varias fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Uso del [!DNL Real-Time Customer Profile] API, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Para trabajar con políticas de combinación mediante la API, visite [guía de extremo de políticas de combinación](merge-policies.md).

Para obtener más información acerca de las políticas de combinación y su función dentro de Platform, comience por leer la [resumen de políticas de combinación](../merge-policies/overview.md).

## Previsualizar estado de muestra ([!DNL Profile] preview) {#profile-preview}

A medida que los datos se incorporan a Platform, se ejecuta un trabajo de muestra para actualizar el recuento de perfiles y otras métricas relacionadas con los datos del perfil del cliente en tiempo real. Los resultados de este trabajo de muestra se pueden ver mediante el `/previewsamplestatus` punto de conexión, parte de la API del perfil del cliente en tiempo real. Este extremo también se puede utilizar para enumerar distribuciones de perfil por conjunto de datos y área de nombres de identidad, así como para generar varios informes con el fin de obtener visibilidad sobre la composición del almacén de perfiles de su organización.  Para empezar a utilizar `/profilepreviewstatus` punto final, consulte la [vista previa guía de extremo de estado de muestra](preview-sample-status.md).

## Trabajos del sistema de perfil {#profile-system-jobs}

Datos con perfil habilitado que se incorporan a [!DNL Platform] se almacena en [!DNL Data Lake] así como el [!DNL Real-Time Customer Profile] almacén de datos. En ocasiones, puede ser necesario eliminar datos de perfil asociados con un conjunto de datos del almacén de perfiles para eliminar datos que ya no son necesarios o que se añadieron por error. Para ello, es necesario utilizar la API de para crear un [!DNL Profile System Job], también conocido como &quot;[!DNL delete request]&quot;, que se puede modificar, supervisar o eliminar si es necesario. Para obtener información sobre cómo trabajar con solicitudes de eliminación mediante `/system/jobs` punto final en la [!DNL Real-Time Customer Profile] API, siga los pasos descritos en la [guía de extremo de trabajos del sistema de perfil](profile-system-jobs.md).

## Actualización de atributos de perfiles {#update-profile}

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para el perfil y configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial de [habilitar un conjunto de datos para perfiles y actualizaciones](../../catalog/datasets/enable-upsert.md).

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas utilizando [!DNL Real-Time Customer Profile] API, lea la [guía de introducción](getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar [!DNL Profile]Puntos finales relacionados con. Para trabajar con [!DNL Profile] datos con el [!DNL Experience Platform] Interfaz de usuario, consulte la [Guía del usuario del Perfil del cliente en tiempo real](../ui/user-guide.md).
