---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;perfil unificado;perfil unificado;rtcp;habilitar perfil;habilitar perfil
title: Guía de la API del perfil del cliente en tiempo real
description: La API de perfil del cliente en tiempo real permite a los desarrolladores explorar y trabajar con datos de perfil, incluidos los perfiles de vista, crear y actualizar políticas de combinación, exportar o muestrear datos de perfil y eliminar datos de perfil que ya no sean necesarios o que se hayan añadido por error. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---

# Guía de la API de [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] le permite ver una vista integral de cada uno de sus clientes individuales dentro de Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

La API [!DNL Real-Time Customer Profile] incluye varios extremos, que se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de muestra y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite el [Swagger de referencia de la API del perfil del cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Para obtener una guía para trabajar con datos de [!DNL Real-Time Customer Profile] en la interfaz de usuario de [!DNL Experience Platform], consulte la [guía de usuario de perfil](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative} Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
La funcionalidad de atributos calculados está en versión beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin que sea necesario realizar manualmente cálculos complejos cada vez que se necesite la información. Estos valores de atributo calculados se pueden ver en un perfil, utilizarse para crear una audiencia o acceder a ellos a través de una serie de patrones de acceso diferentes.

Puede crear, ver, editar y eliminar atributos calculados mediante el extremo `ca/attributes/`. Para aprender a utilizar los atributos calculados, consulte la [descripción general de los atributos calculados](../computed-attributes/overview.md). Para operaciones API, visite la [guía de extremo API de atributos calculados](../computed-attributes/api.md).

## Entidades (acceso de [!DNL Profile]) {#entities}

A través de Adobe Experience Platform, puede acceder a los datos de [!DNL Real-Time Customer Profile] mediante las API de RESTful o la interfaz de usuario de. Para obtener información sobre cómo acceder a entidades, más conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la guía de extremo de [entidades](entities.md). Para obtener acceso a los perfiles mediante la interfaz de usuario de [!DNL Platform], consulte la [Guía del usuario del perfil](../ui/user-guide.md).

## Trabajos de exportación ([!DNL Profile] exportar) {#profile-export}

Los datos de [!DNL Real-Time Customer Profile] se pueden exportar a un conjunto de datos para un procesamiento posterior, como la exportación de audiencias para su activación o de atributos de perfil para la creación de informes. Los trabajos de exportación para audiencias forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Lea la [guía de extremo de trabajos de exportación de segmentación](../../profile/api/export-jobs.md) para obtener más información. Para obtener instrucciones paso a paso acerca de cómo crear y administrar trabajos de exportación para atributos de perfil, visite la [guía de extremo de trabajos de exportación](export-jobs.md).

## Políticas de combinación {#merge-policies}

Al unir datos de varias fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Con la API [!DNL Real-Time Customer Profile], puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Para trabajar con políticas de combinación mediante la API, visite la [guía de extremo de políticas de combinación](merge-policies.md).

Para obtener más información sobre las políticas de combinación y su función en Platform, lea la [descripción general de las políticas de combinación](../merge-policies/overview.md).

## Previsualizar estado de muestra ([!DNL Profile] vista previa) {#profile-preview}

A medida que los datos se incorporan a Platform, se ejecuta un trabajo de muestra para actualizar el recuento de perfiles y otras métricas relacionadas con los datos del perfil del cliente en tiempo real. Los resultados de este trabajo de ejemplo se pueden ver mediante el extremo `/previewsamplestatus`, parte de la API del perfil del cliente en tiempo real. Este extremo también se puede utilizar para enumerar distribuciones de perfil por conjunto de datos y área de nombres de identidad, así como para generar varios informes con el fin de obtener visibilidad sobre la composición del almacén de perfiles de su organización.  Para empezar a usar el extremo `/profilepreviewstatus`, consulte la [guía de extremo de estado de muestra de vista previa](preview-sample-status.md).

## Trabajos del sistema de perfil {#profile-system-jobs}

Los datos con perfil habilitado que se han ingerido en [!DNL Platform] se almacenan en [!DNL Data Lake] y en el almacén de datos de [!DNL Real-Time Customer Profile]. En ocasiones, puede ser necesario eliminar datos de perfil asociados con un conjunto de datos del almacén de perfiles para eliminar datos que ya no son necesarios o que se añadieron por error. Esto requiere el uso de la API para crear un(a) [!DNL Profile System Job], también conocido como &quot;[!DNL delete request]&quot;, que se puede modificar, supervisar o eliminar si es necesario. Para obtener información sobre cómo trabajar con solicitudes de eliminación mediante el extremo `/system/jobs` en la API [!DNL Real-Time Customer Profile], siga los pasos descritos en la [guía de extremo de trabajos del sistema de perfiles](profile-system-jobs.md).

## Actualización de atributos de perfiles {#update-profile}

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para el perfil y configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial de [habilitar un conjunto de datos para Perfil y actualizar](../../catalog/datasets/enable-upsert.md).

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas mediante la API [!DNL Real-Time Customer Profile], lea la [guía de introducción](getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos relacionados con [!DNL Profile]. Para trabajar con datos de [!DNL Profile] usando la interfaz de usuario de [!DNL Experience Platform], consulte la [guía del usuario del perfil del cliente en tiempo real](../ui/user-guide.md).
