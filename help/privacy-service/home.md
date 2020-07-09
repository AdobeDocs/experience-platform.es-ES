---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Adobe Experience Platform Privacy Service general

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan.

El Adobe Experience Platform Privacy Service se desarrolló en respuesta a un cambio fundamental en la manera en que las empresas deben administrar los datos personales de sus clientes. El objetivo central del Privacy Service es automatizar el cumplimiento de las regulaciones de privacidad de datos que, cuando se violan, pueden resultar en importantes multas y interrumpir las operaciones de datos de su empresa.

Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. Con Privacy Service, puede enviar solicitudes para acceder a los datos personales de los clientes y eliminarlos de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas de privacidad legales y de la organización.

## Introducción a Privacy Service {#getting-started}

Para poder utilizar el Privacy Service, es necesario tomar varias decisiones clave en cuanto a los requisitos de privacidad de su organización, los tipos de datos de identidad que recopila de sus clientes y la mejor manera de interconectar su sistema CRM con el servicio.

Estas decisiones pueden resumirse en las siguientes preguntas:

1. **¿Qué información recopilo de mis clientes?**
   * Para aprovechar al máximo a los Privacy Service, debe tener una comprensión detallada de los tipos de datos que recopila de sus clientes y de los que están sujetos a las normas de privacidad. Consulte la sección sobre [determinación de los requisitos](#requirements) de privacidad para obtener más información.
1. **¿He etiquetado correctamente mis datos?**
   * Los datos deben etiquetarse correctamente para que el servicio pueda determinar a qué campos acceder o eliminar durante los trabajos de privacidad. Consulte la sección sobre [etiquetado de datos](#label) para obtener más información.
1. **¿Sé qué ID se deben enviar al Privacy Service?**
   * Al enviar solicitudes de privacidad, se deben proporcionar ID de cliente individuales específicos de determinadas aplicaciones de Adobe. Consulte las secciones sobre [proporcionar datos](#identity) de identidad y [realizar solicitudes](#requests) de privacidad para obtener más información.
1. **¿Cómo rastreo mis trabajos de privacidad?**
   * Una vez que haya realizado las solicitudes de privacidad, hay varias opciones para rastrear su estado y los resultados. Consulte la sección sobre [supervisión de trabajos](#monitor) de privacidad para obtener más información.

En las secciones que figuran a continuación se proporciona orientación general sobre estas importantes medidas previas, y también se proporcionan vínculos a la documentación adicional del Privacy Service para obtener más detalles.

### Determinar los requisitos de privacidad de su organización {#requirements}

Dependiendo de la naturaleza de su negocio y de las jurisdicciones bajo las que opera, sus operaciones de datos pueden estar sujetas a regulaciones legales de privacidad. Estas regulaciones a menudo otorgan a sus clientes el derecho de solicitar acceso a los datos que recopila de ellos, y el derecho de solicitar la eliminación de esos datos almacenados. Estas solicitudes de datos personales de los clientes se denominan &quot;solicitudes de privacidad&quot; en toda la documentación.

La siguiente tabla describe las regulaciones legales de privacidad que Privacy Service administra las solicitudes, incluidos los vínculos a la documentación para obtener más información:

| Reglamento | Descripción |
| --- | --- |
| CCPA (California) | La Ley de Privacidad del Consumidor de California (CCPA) mejora los derechos de privacidad y la protección del consumidor para los residentes de California, Estados Unidos. La CCPA otorga nuevos derechos de privacidad de datos a los residentes de California, incluido el derecho a acceder y eliminar sus datos personales, a saber si sus datos personales se venden o revelan (y a quién) y a exclusión que sus datos se venden a terceros.<br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://oag.ca.gov/privacy/ccpa)</li><li>[Preguntas más frecuentes sobre CCPA](ccpa/faq.md)</li></ul> |
| RGPD (Unión Europea) | El Reglamento General de Protección de Datos (RGPD) incluyó nuevos derechos sobre privacidad de datos para los miembros de la Unión Europea, como el **derecho de acceso** y el **derecho al olvido**. Esto implica que cualquier ciudadano de la UE cuyos datos personales hayan sido recopilados por su empresa puede solicitar el acceso o la supresión de sus datos en cualquier momento. <br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://gdpr-info.eu/)</li><li>[Preguntas más frecuentes sobre el RGPD](gdpr/faq.md)</li><li>[Terminología del RGPD](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Tailandia) | La Ley de Protección de Datos Personales de Tailandia (PDPA, por sus siglas en inglés) se introdujo para proteger a los propietarios tailandeses de los datos de la recopilación, el uso o la revelación ilegales de sus datos personales. Inspirado en el RGPD de la Unión Europea, el reglamento otorga a los ciudadanos tailandeses el derecho de solicitar el acceso a sus datos personales almacenados o la eliminación de los mismos.<br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Preguntas más frecuentes sobre PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminología PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Si sus operaciones de datos son de la competencia de cualquiera de las regulaciones anteriores, revise su documentación para obtener información importante, como los derechos de privacidad específicos que otorgan a sus clientes y las ventanas de cumplimiento para cumplir con las solicitudes de privacidad. Esta información debe tenerse en cuenta a la hora de determinar cómo integrar a un Privacy Service en su sistema CRM y cómo los clientes deben interactuar con su sitio Web para realizar solicitudes de privacidad.

Además de las regulaciones legales, cualquier norma organizativa o industrial aplicable a su organización también debe ser considerada al tomar estas decisiones.

### Datos de etiqueta para solicitudes de privacidad {#label}

Según las aplicaciones Experience Cloud que utilice, debe etiquetar los campos de datos específicos a los que se debe acceder o eliminar en respuesta a las solicitudes de privacidad. El proceso de etiquetado de datos varía según la aplicación. Para obtener información sobre cómo etiquetar datos para cada aplicación de Adobe admitida, consulte el documento en aplicaciones [](./experience-cloud-apps.md)Experience Cloud.

### Determinar los tipos de datos de identidad que se envían al Privacy Service {#identity}

Para que el Privacy Service pueda procesar una solicitud de privacidad de un cliente, se debe proporcionar al menos un valor de identidad único para ese cliente en la propia solicitud. Un valor de identidad único es cualquier dato que puede utilizarse para identificar a una persona individual y sus datos personales almacenados en los almacenes de datos de su Experience Cloud. El Privacy Service utiliza esta información de identidad para localizar y procesar los datos personales del cliente según la naturaleza de la solicitud (acceso, eliminación o exclusión).

Según las aplicaciones Experience Cloud que utilice su sistema CRM, variarán el tipo y la cantidad de valores de identidad que debe proporcionar a cada cliente. Algunas aplicaciones utilizan sus propios valores de ID de cliente internos (como ID de Adobe Target), mientras que otras soluciones dependen de identificadores globales de Adobe Experience Cloud Identity Service (ECID) que rastrean la actividad de los clientes en todas las aplicaciones de Experience Cloud. Además, la información personal genérica como una dirección de correo electrónico o un número de teléfono también puede servir como datos de identidad válidos.

El documento sobre datos de [identidad para solicitudes](./identity-data.md) de privacidad proporciona información más detallada sobre los tipos de información de identidad que se aceptan para el Privacy Service. El documento también proporciona instrucciones sobre cómo aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada de sus clientes a medida que interactúan con su sitio web y enviar esos datos al Privacy Service en solicitudes de API.

### Inicio que realiza solicitudes de privacidad {#requests}

Una vez que haya determinado las necesidades de privacidad de su empresa y haya decidido qué valores de identidad se enviarán al Privacy Service, podrá realizar inicios para realizar solicitudes de privacidad. Privacy Service le permite enviar solicitudes de privacidad a través de la API o la interfaz de usuario.

>[!IMPORTANT]
>
>Las secciones siguientes proporcionan vínculos a documentación que explica cómo realizar solicitudes de privacidad genéricas en la API o la interfaz de usuario. Sin embargo, según las aplicaciones Experience Cloud que utilice, los campos que debe enviar en la carga útil de la solicitud pueden ser diferentes de los ejemplos que se muestran en estas guías.
>
>A medida que vaya siguiendo las guías de API o de interfaz de usuario, consulte el documento sobre aplicaciones [de](./experience-cloud-apps.md) Privacy Service y Experience Cloud para obtener más información sobre cómo dar formato a las solicitudes de privacidad de las aplicaciones de Experience Cloud en particular.

#### Uso de la API

La API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service proporciona varios extremos para crear y administrar trabajos de privacidad mediante llamadas a la API RESTful, lo que le permite abordar mediante programación la conformidad con la normativa de privacidad de sus aplicaciones Experience Cloud. Para ver los pasos detallados sobre cómo utilizar la API, consulte la guía [para desarrolladores de la API de](api/getting-started.md)Privacy Service.

#### Uso de la interfaz de usuario

>[!NOTE]
>
>Actualmente, la interfaz de usuario del Privacy Service solo admite solicitudes de acceso y eliminación. Todas las solicitudes de exclusión deben realizarse a través de la API.

La interfaz de usuario del Privacy Service le permite crear y supervisar trabajos de privacidad mediante una interfaz gráfica. La interfaz de usuario incluye un widget de informe **de** estado que proporciona una representación visual del estado de todas las solicitudes activas y le permite crear nuevas solicitudes mediante el creador **de** solicitudes integrado o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario, consulte la guía [del usuario del](ui/overview.md)Privacy Service.

### Supervisión de trabajos de privacidad {#monitor}

Una vez que haya realizado trabajos de privacidad, tiene varias opciones para supervisar su estado y sus resultados:

| Método de supervisión | Descripción |
| --- | --- |
| IU de Privacy Service | La interfaz de usuario del Privacy Service proporciona un panel de supervisión que le permite realizar una vista de una representación visual del estado de todas las solicitudes activas. Consulte la guía [del usuario del](ui/overview.md) Privacy Service para obtener más información. |
| API de Privacy Service | Puede supervisar mediante programación el estado de los trabajos de privacidad mediante los extremos de búsqueda proporcionados por la API de Privacy Service. Consulte la guía [para desarrolladores de](./api/getting-started.md) Privacy Service para ver los pasos detallados sobre cómo utilizar la API. |
| Eventos de privacidad | Los Eventos de privacidad aprovechan los Eventos de E/S de Adobe enviados a un enlace web configurado para facilitar la automatización eficaz de las solicitudes de trabajos. Reducen o eliminan la necesidad de sondear la API de Privacy Service para comprobar si un trabajo se ha completado o si se ha alcanzado un determinado hito en un flujo de trabajo. Consulte el tutorial sobre la [suscripción a Eventos](./privacy-events.md) de privacidad para obtener más información. |

## Pasos siguientes

Este documento proporcionó una visión general de alto nivel del Privacy Service y de los principales pasos necesarios para el inicio mediante las capacidades del servicio. Consulte la documentación relacionada a lo largo de la descripción general para obtener información más detallada sobre los diversos aspectos del trabajo con Privacy Service.
