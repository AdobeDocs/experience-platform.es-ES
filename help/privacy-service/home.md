---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: f3872d433949e6c14c28c6833b8498d4d01b8de3
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 2%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan.

Adobe Experience Platform [!DNL Privacy Service] se desarrolló en respuesta a un cambio fundamental en la manera en que se requiere que las empresas gestionen los datos personales de sus clientes. El objetivo central de [!DNL Privacy Service] es automatizar el cumplimiento de las regulaciones de privacidad de datos que, cuando se violan, pueden resultar en importantes multas y interrumpir las operaciones de datos de su empresa.

[!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales de clientes desde las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas legales y de privacidad de la organización.

## Getting started with [!DNL Privacy Service] {#getting-started}

Para hacer uso de [!DNL Privacy Service], es necesario tomar varias decisiones clave en términos de los requisitos de privacidad de su organización, los tipos de datos de identidad que recopila de sus clientes y la mejor manera de interconectar su sistema CRM con el servicio.

Estas decisiones pueden resumirse en las siguientes preguntas:

1. **¿Qué información recopilo de mis clientes?**
   * Para aprovechar al máximo [!DNL Privacy Service], debe tener una comprensión detallada de los tipos de datos que recopila de sus clientes y de los que está sujeto a las normas de privacidad. Consulte la sección sobre [determinación de los requisitos](#requirements) de privacidad para obtener más información.
1. **¿He etiquetado correctamente mis datos?**
   * Los datos deben etiquetarse correctamente para que el servicio pueda determinar a qué campos acceder o eliminar durante los trabajos de privacidad. Consulte la sección sobre [etiquetado de datos](#label) para obtener más información.
1. **¿Sé a qué ID enviar [!DNL Privacy Service]?**
   * Al enviar solicitudes de privacidad, se deben proporcionar ID de cliente individuales específicos de aplicaciones de Adobe específicas. Consulte las secciones sobre [proporcionar datos](#identity) de identidad y [realizar solicitudes](#requests) de privacidad para obtener más información.
1. **¿Cómo rastreo mis trabajos de privacidad?**
   * Una vez que haya realizado las solicitudes de privacidad, hay varias opciones para rastrear su estado y los resultados. Consulte la sección sobre [supervisión de trabajos](#monitor) de privacidad para obtener más información.

En las secciones que figuran a continuación se proporciona orientación general sobre estas importantes medidas previas, y también se proporcionan vínculos a documentación adicional para obtener más información [!DNL Privacy Service] .

### Determinar los requisitos de privacidad de su organización {#requirements}

Dependiendo de la naturaleza de su negocio y de las jurisdicciones bajo las que opera, sus operaciones de datos pueden estar sujetas a regulaciones legales de privacidad. Estas regulaciones a menudo otorgan a sus clientes el derecho de solicitar acceso a los datos que recopila de ellos, y el derecho de solicitar la eliminación de esos datos almacenados. Estas solicitudes de datos personales de los clientes se denominan &quot;solicitudes de privacidad&quot; en toda la documentación.

La siguiente tabla describe las regulaciones legales de privacidad que [!DNL Privacy Service] administran las solicitudes, incluyendo vínculos a la documentación para obtener más información:

| Reglamento | Descripción |
| --- | --- |
| CCPA (California) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. La CCPA otorga nuevos derechos de privacidad de datos a los residentes de California, incluido el derecho a acceder y eliminar sus datos personales, a saber si sus datos personales se venden o revelan (y a quién) y a exclusión que sus datos se venden a terceros.<br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://oag.ca.gov/privacy/ccpa)</li><li>[Preguntas más frecuentes sobre CCPA](ccpa/faq.md)</li></ul> |
| RGPD (Unión Europea) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. Esto implica que cualquier ciudadano de la UE cuyos datos personales hayan sido recopilados por su empresa puede solicitar el acceso o la supresión de sus datos en cualquier momento. <br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://gdpr-info.eu/)</li><li>[Preguntas más frecuentes sobre el RGPD](gdpr/faq.md)</li><li>[Terminología del RGPD](gdpr/terminology.md)</li></ul> |
| LGPD (Brasil) | El objetivo [!DNL Lei Geral de Proteção de Dados] (LGPD) es regular el tratamiento de los datos personales de todas las personas físicas o físicas en el Brasil. La LGPD otorga a los ciudadanos brasileños el derecho a acceder y eliminar sus datos personales, a saber si se venden o revelan sus datos personales (y a quién), y el derecho a exclusión que sus datos se vendan a terceros.<br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://gdpr.eu/gdpr-vs-lgpd/)</li></ul> |
| PDPA (Tailandia) | El [!DNL Personal Data Protection Act] de Tailandia (PDPA) se introdujo para proteger a los propietarios de datos tailandeses de la recopilación, el uso o la revelación ilegales de sus datos personales. Inspirado en el RGPD de la Unión Europea, el reglamento otorga a los ciudadanos tailandeses el derecho de solicitar el acceso a sus datos personales almacenados o la eliminación de los mismos.<br/><br/>Vínculos para más documentación: <ul><li>[Visión general de la legislación](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Preguntas más frecuentes sobre PDPA](pdpa-tha/faq.md)</li><li>[Terminología de PDPA](pdpa-tha/terminology.md)</li></ul> |

Si sus operaciones de datos son de la competencia de cualquiera de las regulaciones anteriores, revise su documentación para obtener información importante, como los derechos de privacidad específicos que otorgan a sus clientes y las ventanas de cumplimiento para cumplir con las solicitudes de privacidad. Esta información debe tenerse en cuenta a la hora de determinar cómo se integra [!DNL Privacy Service] en el sistema CRM y cómo los clientes deben interactuar con el sitio web para realizar solicitudes de privacidad.

Además de las regulaciones legales, cualquier norma organizativa o industrial aplicable a su organización también debe ser considerada al tomar estas decisiones.

### Datos de etiqueta para solicitudes de privacidad {#label}

Según las [!DNL Experience Cloud] aplicaciones que utilice, debe etiquetar los campos de datos específicos a los que se debe acceder o eliminar en respuesta a las solicitudes de privacidad. El proceso de etiquetado de datos varía según la aplicación. Para obtener información sobre cómo etiquetar datos para cada aplicación de Adobe admitida, consulte el documento en aplicaciones [de](./experience-cloud-apps.md)Experience Cloud.

### Determinar los tipos de datos de identidad a los que enviar [!DNL Privacy Service] {#identity}

Para [!DNL Privacy Service] procesar una solicitud de privacidad de un cliente, se debe proporcionar al menos un valor de identidad único para ese cliente en la propia solicitud. Un valor de identidad único es cualquier dato que puede utilizarse para identificar a una persona individual y sus datos personales almacenados en sus almacenes [!DNL Experience Cloud] de datos. [!DNL Privacy Service] utiliza esta información de identidad para localizar y procesar los datos personales del cliente según la naturaleza de la solicitud (acceso, eliminación o exclusión).

Según las [!DNL Experience Cloud] aplicaciones que utilice su sistema CRM, el tipo y la cantidad de valores de identidad que debe proporcionar para cada cliente variarán. Algunas aplicaciones utilizan sus propios valores de ID de cliente internos (como Adobe Target ID), mientras que otras soluciones dependen de identificadores globales de Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastrean la actividad de los clientes en todas [!DNL Experience Cloud] las aplicaciones. Además, la información personal genérica como una dirección de correo electrónico o un número de teléfono también puede servir como datos de identidad válidos.

El documento sobre datos de [identidad para solicitudes](./identity-data.md) de privacidad proporciona información más detallada sobre los tipos de información de identidad que se aceptan para [!DNL Privacy Service]. El documento también proporciona instrucciones sobre cómo aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada de sus clientes a medida que interactúan con su sitio web y enviar esos datos a [!DNL Privacy Service] las solicitudes de API.

### Inicio que realiza solicitudes de privacidad {#requests}

Una vez que haya determinado las necesidades de privacidad de su empresa, y haya decidido a qué valores de identidad enviar [!DNL Privacy Service], puede realizar inicios para realizar solicitudes de privacidad. [!DNL Privacy Service] le permite enviar solicitudes de privacidad a través de la API o la interfaz de usuario.

>[!IMPORTANT]
>
>Las secciones siguientes proporcionan vínculos a documentación que explica cómo realizar solicitudes de privacidad genéricas en la API o la interfaz de usuario. Sin embargo, según las [!DNL Experience Cloud] aplicaciones que utilice, los campos que debe enviar en la carga útil de la solicitud pueden ser diferentes de los ejemplos que se muestran en estas guías.
>
>A medida que vaya siguiendo las guías de API o IU, consulte el documento sobre aplicaciones [de](./experience-cloud-apps.md) Privacy Service y Experience Cloud para obtener más información sobre cómo dar formato a las solicitudes de privacidad de sus [!DNL Experience Cloud] aplicaciones en particular.
>
>También es importante tener en cuenta que las solicitudes de privacidad se procesan asincrónicamente en las aplicaciones Experience Cloud. Una vez que el Privacy Service recibe una solicitud, cada aplicación puede tardar entre minutos y semanas en completarse. La cantidad de tiempo que se tarda en completar cada solicitud es específica a la aplicación con la que se está trabajando y la cantidad de datos que se deben procesar.

#### Uso de la API

El [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) proporciona varios extremos para crear y administrar trabajos de privacidad mediante llamadas de API RESTful, lo que le permite abordar mediante programación el cumplimiento de la normativa de privacidad de sus [!DNL Experience Cloud] aplicaciones. Para ver los pasos detallados sobre cómo utilizar la API, consulte la guía [para desarrolladores de la API de](api/getting-started.md)Privacy Service.

#### Uso de la interfaz de usuario

>[!NOTE]
>
>Actualmente, la interfaz de usuario [!DNL Privacy Service] solo admite solicitudes de acceso y eliminación. Todas las solicitudes de exclusión deben realizarse a través de la API.

La interfaz de usuario le permite crear y supervisar trabajos de privacidad mediante una interfaz gráfica. [!DNL Privacy Service] La interfaz de usuario incluye un widget de informe **[!UICONTROL de]** estado que proporciona una representación visual del estado de todas las solicitudes activas y le permite crear nuevas solicitudes mediante el creador **[!UICONTROL de]** solicitudes integrado o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario, consulte la guía [del usuario del](ui/overview.md)Privacy Service.

### Supervisión de trabajos de privacidad {#monitor}

Una vez que haya realizado trabajos de privacidad, tiene varias opciones para supervisar su estado y sus resultados:

| Método de supervisión | Descripción |
| --- | --- |
| [!DNL Privacy Service] IU | La interfaz de usuario [!DNL Privacy Service] proporciona un panel de supervisión que le permite realizar una vista de una representación visual del estado de todas las solicitudes activas. Consulte la guía [del usuario del](ui/overview.md) Privacy Service para obtener más información. |
| [!DNL Privacy Service] API | Puede supervisar mediante programación el estado de los trabajos de privacidad mediante los extremos de búsqueda proporcionados por la [!DNL Privacy Service] API. Consulte la guía [para desarrolladores de](./api/getting-started.md) Privacy Service para ver los pasos detallados sobre cómo utilizar la API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveche los Eventos de E/S de Adobe enviados a un enlace web configurado para facilitar la automatización eficaz de las solicitudes de trabajos. Reducen o eliminan la necesidad de sondear la [!DNL Privacy Service] API para comprobar si se ha completado un trabajo o si se ha alcanzado un determinado hito en un flujo de trabajo. Consulte el tutorial sobre la [suscripción a Eventos](./privacy-events.md) de privacidad para obtener más información. |

## Pasos siguientes

Este documento proporcionó una visión general de alto nivel de [!DNL Privacy Service] y los principales pasos necesarios para el inicio mediante las capacidades del servicio. Consulte la documentación vinculada a lo largo de la descripción general para obtener información más detallada sobre los diversos aspectos del trabajo con [!DNL Privacy Service].
