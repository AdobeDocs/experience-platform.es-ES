---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Guía para desarrolladores de API de Perfil para clientes en tiempo real

El Perfil del cliente en tiempo real le permite ver una vista holística de cada uno de sus clientes individuales dentro de Adobe Experience Platform. Perfil le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente.

## Primeros pasos {#getting-started}

Mediante la API de Perfil de cliente en tiempo real, puede realizar operaciones CRUD básicas con recursos de Perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos de Perfil y la eliminación de conjuntos de datos o lotes innecesarios.

El uso de esta guía para desarrolladores requiere conocer los distintos servicios de Adobe Experience Platform que intervienen en el trabajo con datos de Perfil. Antes de comenzar a trabajar con la API de Perfil del cliente en tiempo real, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [Servicio](../../identity-service/home.md)de identidad de Adobe Experience Platform: Obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [Servicio](../../segmentation/home.md)de segmentación de la plataforma Adobe Experience: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a extremos de la API de Perfil con éxito.

### Leer llamadas de API de muestra

La documentación de la API de Perfil del cliente en tiempo real proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a extremos de plataforma. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como las llamadas POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## (Alfa) Atributos calculados

>[!IMPORTANT]
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos.

Cada atributo calculado contiene una expresión, o &#39;regla&#39;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información.

Puede crear, vista, editar y eliminar atributos calculados mediante los `config/computedAttributes` extremos. Para aprender a utilizar estos extremos, visite la subguía [Atributos](computed-attributes.md)calculados.

## Proyecciones de Edge

Adobe Experience Platform permite la personalización en tiempo real de las experiencias de los clientes al facilitar el acceso a los datos en servidores estratégicamente ubicados llamados &quot;bordes&quot;. La API de Perfil del cliente en tiempo real proporciona puntos finales para trabajar con bordes a través de componentes llamados &quot;proyecciones&quot;. Esto incluye configuraciones de proyección para determinar qué datos se deben proyectar a cada borde, así como destinos de proyección para definir dónde se debe enrutar una proyección.

Para obtener información detallada sobre el trabajo con proyecciones de los bordes, consulte la subguía [Proyecciones de los](edge-projections.md)bordes.

## Entidades

A través de Adobe Experience Platform puede acceder a los datos de Perfil del cliente en tiempo real mediante las API de RESTful o la interfaz de usuario. Para aprender a acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API, siga los pasos descritos en la subguía [](entities.md)de entidades.

## Combinar directivas

Al reunir datos de varias fuentes en la plataforma de experiencia, las políticas de combinación son las reglas que utiliza la plataforma para determinar cómo se priorizarán los datos y qué datos se combinarán para crear perfiles de clientes individuales.

Mediante la API de Perfil del cliente en tiempo real, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre cómo trabajar con políticas de combinación mediante la API, visite la subguía [de políticas de](merge-policies.md)combinación.

Para obtener una guía sobre cómo trabajar con políticas de combinación mediante la interfaz de usuario de la plataforma, consulte la guía [del usuario](../ui/merge-policies.md)Combinar directivas.

## Búsqueda de Perfiles

La búsqueda por Perfil se utiliza para buscar e indexar los campos configurables contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para empezar a trabajar con la búsqueda por Perfil, consulte la subguía [de búsqueda](profile-search.md)

## Trabajos del sistema de Perfil

Los datos ingeridos en Platform se almacenan en Data Lake y en el almacén de datos de Perfil del cliente en tiempo real. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del almacén de Perfiles para eliminar los datos que ya no necesite o que se agregaron por error. Esto requiere el uso de la API para crear un trabajo de sistema de Perfil, conocido como &quot;solicitud de eliminación&quot;, que también se puede modificar, supervisar o eliminar si es necesario.

Para aprender a trabajar con solicitudes de eliminación mediante los `/system/jobs` extremos de la API de Perfil de clientes en tiempo real, siga los pasos descritos en la subguía [de trabajos del sistema de](profile-system-jobs.md)perfil.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Perfil del cliente en tiempo real, seleccione una de las subguías para aprender a utilizar los extremos específicos relacionados con el Perfil. Para obtener más información sobre cómo trabajar con datos de Perfil mediante la interfaz de usuario de la plataforma, consulte la guía [de usuario de Perfil para clientes en tiempo](../ui/user-guide.md)real.