---
keywords: Experience Platform;inicio;temas populares;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Información general de Privacy Service
topic: overview
description: Privacy Service le permite facilitar el cumplimiento automatizado de las normas legales de privacidad en las operaciones de datos de su Experience Cloud.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---


# Información general del [!DNL Privacy Service]

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan.

Adobe Experience Platform [!DNL Privacy Service] se desarrolló en respuesta a un cambio fundamental en la manera en que se requiere que las empresas administren los datos personales de sus clientes. El propósito central de [!DNL Privacy Service] es automatizar el cumplimiento de las regulaciones de privacidad de datos que, cuando se violan, pueden resultar en multas importantes y en interrumpir las operaciones de datos para su negocio.

[!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales de clientes desde las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas legales y de privacidad de la organización.

## Introducción a [!DNL Privacy Service] {#getting-started}

Para poder utilizar [!DNL Privacy Service], es necesario tomar varias decisiones clave en cuanto a los requisitos de privacidad de su organización, los tipos de datos de identidad que recopila de sus clientes y la mejor manera de interconectar su sistema CRM con el servicio.

Estas decisiones pueden resumirse en las siguientes preguntas:

1. **¿Qué información recopilo de mis clientes?**
   * Para hacer el mejor uso de [!DNL Privacy Service], debe tener una comprensión detallada de los tipos de datos que recopila de sus clientes y de los que está sujeto a las regulaciones de privacidad. Consulte la sección sobre [determinación de los requisitos de privacidad](#requirements) para obtener más información.
1. **¿He etiquetado correctamente mis datos?**
   * Los datos deben etiquetarse correctamente para que el servicio pueda determinar a qué campos acceder o eliminar durante los trabajos de privacidad. Consulte la sección sobre [etiquetado de datos](#label) para obtener más información.
1. **¿Sé a qué ID enviar  [!DNL Privacy Service]?**
   * Al enviar solicitudes de privacidad, se deben proporcionar ID de cliente individuales específicos de aplicaciones de Adobe específicas. Consulte las secciones sobre [proporcionar datos de identidad](#identity) y [realizar solicitudes de privacidad](#requests) para obtener más información.
1. **¿Cómo rastreo mis trabajos de privacidad?**
   * Una vez que haya realizado las solicitudes de privacidad, hay varias opciones para rastrear su estado y los resultados. Consulte la sección sobre [tareas de monitoreo de privacidad](#monitor) para obtener más información.

Las secciones que figuran a continuación proporcionan orientación general sobre estos importantes pasos previos y también proporcionan vínculos a más [!DNL Privacy Service] documentación para obtener más detalles.

### Determinar los requisitos de privacidad de su organización {#requirements}

Dependiendo de la naturaleza de su negocio y de las jurisdicciones bajo las que opera, sus operaciones de datos pueden estar sujetas a regulaciones legales de privacidad. Estas regulaciones a menudo otorgan a sus clientes el derecho de solicitar acceso a los datos que recopila de ellos, y el derecho de solicitar la eliminación de esos datos almacenados. Estas solicitudes de datos personales de los clientes se denominan &quot;solicitudes de privacidad&quot; en toda la documentación.

Para obtener más información sobre las diferentes regulaciones legales de privacidad que [!DNL Privacy Service] administra las solicitudes, incluyendo términos clave y respuestas a las preguntas más frecuentes, consulte la [documentación de regulaciones de privacidad](./regulations/overview.md).

Si sus operaciones de datos son de la competencia de cualquiera de las regulaciones admitidas, revise su documentación para obtener información importante, como los derechos de privacidad específicos que otorgan a sus clientes y las ventanas de cumplimiento para cumplir con las solicitudes de privacidad. Esta información debe tenerse en cuenta al determinar cómo integrar [!DNL Privacy Service] en su sistema CRM y cómo los clientes deben interactuar con su sitio Web para realizar solicitudes de privacidad.

Además de las regulaciones legales, cualquier norma organizativa o industrial aplicable a su organización también debe ser considerada al tomar estas decisiones.

### Datos de etiqueta para solicitudes de privacidad {#label}

Según las aplicaciones [!DNL Experience Cloud] que utilice, debe etiquetar los campos de datos específicos a los que se debe acceder o eliminar en respuesta a las solicitudes de privacidad. El proceso de etiquetado de datos varía según la aplicación. Para obtener información sobre cómo etiquetar datos para cada aplicación de Adobe admitida, consulte el documento en [aplicaciones de Experience Cloud](./experience-cloud-apps.md).

### Determinar los tipos de datos de identidad que se enviarán a [!DNL Privacy Service] {#identity}

Para que [!DNL Privacy Service] procese una solicitud de privacidad de un cliente, se debe proporcionar al menos un valor de identidad único para ese cliente en la propia solicitud. Un valor de identidad único es cualquier información que se puede utilizar para identificar a una persona individual y sus datos personales almacenados en los [!DNL Experience Cloud] almacenes de datos. [!DNL Privacy Service] utiliza esta información de identidad para localizar y procesar los datos personales del cliente según la naturaleza de la solicitud (acceso, eliminación o exclusión).

Según las [!DNL Experience Cloud] aplicaciones que utilice su sistema CRM, el tipo y la cantidad de valores de identidad que debe proporcionar para cada cliente variarán. Algunas aplicaciones utilizan sus propios valores de ID de cliente internos (como Adobe Target ID), mientras que otras soluciones dependen de identificadores globales de Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastrean la actividad del cliente en todas las aplicaciones [!DNL Experience Cloud]. Además, la información personal genérica como una dirección de correo electrónico o un número de teléfono también puede servir como datos de identidad válidos.

El documento sobre [datos de identidad para solicitudes de privacidad](./identity-data.md) proporciona información más detallada sobre los tipos de información de identidad que se aceptan para [!DNL Privacy Service]. El documento también proporciona instrucciones sobre cómo aprovechar las tecnologías de Adobe para recuperar de manera efectiva la información de identidad adecuada de sus clientes a medida que interactúan con su sitio web y enviar esos datos a [!DNL Privacy Service] en solicitudes de API.

### Inicio que realiza solicitudes de privacidad {#requests}

Una vez que haya determinado las necesidades de privacidad de su negocio y haya decidido a qué valores de identidad enviar a [!DNL Privacy Service], puede realizar inicios para realizar solicitudes de privacidad. [!DNL Privacy Service] le permite enviar solicitudes de privacidad a través de la API o la interfaz de usuario.

>[!IMPORTANT]
>
>Las secciones siguientes proporcionan vínculos a documentación que explica cómo realizar solicitudes de privacidad genéricas en la API o la interfaz de usuario. Sin embargo, según las aplicaciones [!DNL Experience Cloud] que utilice, los campos que debe enviar en la carga útil de la solicitud pueden ser diferentes de los ejemplos que se muestran en estas guías.
>
>A medida que vaya siguiendo las guías de API o UI, consulte el documento de [aplicaciones de Privacy Service y Experience Cloud](./experience-cloud-apps.md) para obtener más información sobre cómo dar formato a las solicitudes de privacidad de sus [!DNL Experience Cloud] aplicaciones en particular.
>
>También es importante tener en cuenta que las solicitudes de privacidad se procesan asincrónicamente en las aplicaciones Experience Cloud. Una vez que el Privacy Service recibe una solicitud, cada aplicación puede tardar entre minutos y semanas en completarse. La cantidad de tiempo que se tarda en completar cada solicitud es específica a la aplicación con la que se está trabajando y la cantidad de datos que se deben procesar.

#### Uso de la API

El [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) proporciona varios extremos para crear y administrar trabajos de privacidad mediante llamadas de API RESTful, lo que le permite abordar mediante programación el cumplimiento de la normativa de privacidad para sus aplicaciones [!DNL Experience Cloud]. Para ver los pasos detallados sobre cómo utilizar la API, consulte la [guía para desarrolladores de API de Privacy Service](api/getting-started.md).

#### Uso de la interfaz de usuario

>[!NOTE]
>
>La interfaz de usuario [!DNL Privacy Service] actualmente solo admite solicitudes de acceso y eliminación. Todas las solicitudes de exclusión deben realizarse a través de la API.

La interfaz de usuario [!DNL Privacy Service] le permite crear y supervisar trabajos de privacidad mediante una interfaz gráfica. La interfaz de usuario incluye una utilidad **[!UICONTROL Informe de estado]** que proporciona una representación visual del estado de todas las solicitudes activas y le permite crear nuevas solicitudes mediante el **[!UICONTROL Generador de solicitudes]** integrado o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario, consulte la [guía del usuario del Privacy Service](ui/overview.md).

### Monitorear trabajos de privacidad {#monitor}

Una vez que haya realizado trabajos de privacidad, tiene varias opciones para supervisar su estado y sus resultados:

| Método de supervisión | Descripción |
| --- | --- |
| [!DNL Privacy Service] IU | La [!DNL Privacy Service] interfaz de usuario proporciona un panel de supervisión que le permite realizar una vista visual del estado de todas las solicitudes activas. Consulte la [guía del usuario del Privacy Service](ui/overview.md) para obtener más información. |
| [!DNL Privacy Service] API | Puede monitorear mediante programación el estado de los trabajos de Privacidad mediante los extremos de búsqueda proporcionados por la API [!DNL Privacy Service]. Consulte la [guía para desarrolladores de Privacy Service](./api/getting-started.md) para obtener pasos detallados sobre cómo utilizar la API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveche los Eventos de Adobe I/O enviados a un enlace web configurado para facilitar una automatización eficaz de las solicitudes de trabajos. Reducen o eliminan la necesidad de sondear la API [!DNL Privacy Service] para comprobar si se ha completado un trabajo o si se ha alcanzado un determinado hito en un flujo de trabajo. Consulte el tutorial sobre [suscripción a Eventos de privacidad](./privacy-events.md) para obtener más información. |

## Pasos siguientes

Este documento proporcionó una visión general de alto nivel de [!DNL Privacy Service] y los pasos principales requeridos para el inicio usando las capacidades del servicio. Consulte la documentación vinculada a lo largo de la descripción general para obtener información más detallada sobre los diversos aspectos del trabajo con [!DNL Privacy Service].
