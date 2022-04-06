---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;unificado;perfil;rtcp;habilitar perfil;Activar perfil
title: Guía de API del perfil del cliente en tiempo real
description: La API de perfil de cliente en tiempo real permite a los desarrolladores explorar y trabajar con datos de perfil, incluidos la visualización de perfiles, la creación y actualización de políticas de combinación, la exportación o la muestra de datos de perfil y la eliminación de datos de perfil que ya no son necesarios o que se añadieron por error. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Guía de la API de [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] le permite ver una vista holística de cada uno de sus clientes en Adobe Experience Platform. [!DNL Profile] le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

La variable [!DNL Real-time Customer Profile] La API incluye varios extremos, descritos a continuación. Visite las guías de puntos de conexión individuales para obtener más información y consulte la [guía de introducción](getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Intercambio de referencias de la API del perfil del cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Para obtener una guía sobre cómo trabajar con [!DNL Real-time Customer Profile] los datos de [!DNL Experience Platform] Interfaz de usuario, consulte [Guía del usuario del perfil](../ui/user-guide.md).

## (Alpha) Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con elementos como el valor de compra de por vida, el tiempo entre compras o el número de aperturas de aplicaciones, sin que sea necesario realizar cálculos complejos manualmente cada vez que se necesite la información. Estos valores de atributo calculados se pueden ver en un perfil, utilizarse para crear un segmento o acceder a ellos a través de una serie de patrones de acceso diferentes.

Puede crear, ver, editar y eliminar atributos calculados mediante la variable `config/computedAttributes` punto final. Para aprender a utilizar atributos calculados, consulte la [información general sobre atributos calculados](../computed-attributes/overview.md). Para las operaciones de API, visite [guía de extremo de API de atributos calculados](../computed-attributes/ca-api.md).

## Proyecciones perimetrales {#edge-projections}

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La variable [!DNL Real-time Customer Profile] La API de proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde enrutar una proyección. Para obtener información detallada sobre cómo trabajar con proyecciones de Edge, visite el [guía de configuraciones de proyección y extremos de destino](edge-projections.md).

## Entidades ([!DNL Profile] access) {#entities}

A través de Adobe Experience Platform puede acceder a [!DNL Real-time Customer Profile] datos mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la sección [guía de extremo de entidades](entities.md). Para acceder a los perfiles mediante la variable [!DNL Platform] Interfaz de usuario, consulte [Guía del usuario del perfil](../ui/user-guide.md).

## Exportar trabajos ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] los datos se pueden exportar a un conjunto de datos para un procesamiento posterior, como la exportación de segmentos de audiencia para su activación o atributos de perfil para la creación de informes. Los trabajos de exportación para segmentos de audiencia forman parte del [!DNL Adobe Experience Platform Segmentation Service] API, lea la [guía de extremo de trabajos de exportación de segmentación](../../profile/api/export-jobs.md) para obtener más información. Para obtener instrucciones paso a paso sobre cómo crear y administrar trabajos de exportación para atributos de perfil, visite [exportar guía de extremo de trabajos](export-jobs.md).

## Combinar directivas {#merge-policies}

Al unir datos de varias fuentes en [!DNL Experience Platform], las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales. Al usar la variable [!DNL Real-time Customer Profile] , puede crear nuevas directivas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para trabajar con políticas de combinación usando la API, visite [guía de extremo de directivas de combinación](merge-policies.md).

Para obtener más información sobre las políticas de combinación y su función dentro de Platform, comience leyendo el [información general sobre políticas de combinación](../merge-policies/overview.md).

## Vista previa del estado de muestra ([!DNL Profile] preview) {#profile-preview}

A medida que los datos se incorporan en Platform, se ejecuta un trabajo de muestra para actualizar el recuento de perfiles y otras métricas relacionadas con los datos del perfil del cliente en tiempo real. Los resultados de este trabajo de muestra se pueden ver utilizando la variable `/previewsamplestatus` , que forma parte de la API del perfil del cliente en tiempo real. Este extremo también se puede usar para enumerar distribuciones de perfiles tanto por conjunto de datos como por área de nombres de identidad, así como para generar múltiples informes con el fin de ganar visibilidad en la composición del Almacenamiento de perfiles de su organización.  Para empezar a usar la variable `/profilepreviewstatus` , consulte [vista previa de la guía de extremo del estado de muestra](preview-sample-status.md).

## Trabajos del sistema de perfiles {#profile-system-jobs}

Datos con perfil habilitado que se incorporan en [!DNL Platform] se almacena en la variable [!DNL Data Lake] , así como el [!DNL Real-time Customer Profile] almacén de datos. En ocasiones puede ser necesario eliminar un conjunto de datos o lote del [!DNL Profile] almacenar para eliminar los datos que ya no necesita o que se añadieron por error. Esto requiere el uso de la API para crear un [!DNL Profile System Job], también conocido como &quot;[!DNL delete request]&quot;, que pueden modificarse, supervisarse o eliminarse si es necesario. Para aprender a trabajar con solicitudes de eliminación mediante la variable `/system/jobs` en la variable [!DNL Real-time Customer Profile] , siga los pasos descritos en la sección [guía de extremo de trabajos del sistema de perfiles](profile-system-jobs.md).

## Actualizar atributos de perfiles {#update-profile}

En ocasiones puede ser necesario actualizar los datos en el Almacenamiento de perfiles de su organización. Por ejemplo, es posible que necesite corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para Perfil configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial para [activación de un conjunto de datos para Perfil y actualizar](../../catalog/datasets/enable-upsert.md).

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas con [!DNL Real-time Customer Profile] API, lea la [guía de introducción](getting-started.md) a continuación, seleccione una de las guías de punto final para aprender a utilizar las [!DNL Profile]extremos relacionados. Para trabajar con [!DNL Profile] los datos que utilizan la variable [!DNL Experience Platform] Interfaz de usuario, consulte [Guía del usuario del perfil del cliente en tiempo real](../ui/user-guide.md).
