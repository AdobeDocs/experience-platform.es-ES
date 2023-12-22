---
keywords: Experience Platform;inicio;temas populares;RGPD;rgpd;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Resumen del Privacy Service
description: Descubra cómo Privacy Service puede facilitar el cumplimiento automatizado de las regulaciones legales de privacidad en las operaciones de datos de sus Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 5%

---

# Información general de Privacy Service

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan.

Adobe Experience Platform Privacy Service se desarrolló en respuesta a un cambio fundamental en la forma en que se requiere que las empresas administren los datos personales de sus clientes. El propósito central de Privacy Service es automatizar el cumplimiento de las regulaciones de privacidad de datos que, cuando se infringen, pueden resultar en multas importantes e interrumpir las operaciones de datos de su negocio.

Privacy Service proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. Puede utilizar Privacy Service para enviar solicitudes para acceder a datos personales de clientes y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

>[!IMPORTANT]
>
>El Privacy Service solo está diseñado para solicitudes de derechos de los interesados y consumidores. No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos. El Adobe tiene la obligación legal de cumplirlos en el momento oportuno. Como tal, no se permiten las pruebas de carga en el Privacy Service, ya que es un entorno de solo producción y crea un registro de solicitudes de privacidad válidas innecesarias.
>
>Ahora se establece un límite diario de carga estricto para ayudar a evitar el abuso del servicio. Si se detecta que algún usuario abusa del sistema, se deshabilitará el acceso al servicio. Luego se celebrará una reunión posterior con ellos para abordar sus acciones y discutir el uso aceptable de Privacy Service.

## Introducción a Privacy Service {#getting-started}

Para hacer un uso óptimo de Privacy Service, se deben tomar varias decisiones clave en términos de los requisitos de privacidad de su organización, los tipos de datos de identidad que recopila de sus clientes y la mejor manera de interconectar su sistema CRM con el servicio.

Estas decisiones pueden resumirse a través de las siguientes preguntas:

1. **¿Qué información recopilo de mis clientes?**
   * Para sacar el máximo partido a Privacy Service, debe tener una comprensión detallada de los tipos de datos que recopila de sus clientes y de cuál de ellos está sujeto a las normas de privacidad. Consulte la sección sobre [determinación de requisitos de privacidad](#requirements) para obtener más información.
1. **¿He etiquetado correctamente mis datos?**
   * Los datos deben etiquetarse correctamente para que el servicio determine a qué campos acceder o eliminar durante los trabajos de privacidad. Consulte la sección sobre [etiquetado de datos](#label) para obtener más información.
1. **¿Sé qué ID enviar al Privacy Service?**
   * Al enviar solicitudes de privacidad, se deben proporcionar ID de cliente individuales específicos de aplicaciones de Adobe concretas. Consulte las secciones sobre [proporcionar datos de identidad](#identity)  y [realización de solicitudes de privacidad](#requests) para obtener más información.
1. **¿Cómo realizo el seguimiento de mis trabajos de privacidad?**
   * Una vez que haya realizado solicitudes de privacidad, existen varias opciones para rastrear su estado y resultados. Consulte la sección sobre [supervisión de trabajos de privacidad](#monitor) para obtener más información.

Las secciones siguientes proporcionan directrices generales sobre estos pasos importantes para cumplir los requisitos previos, y también proporcionan enlaces a documentación adicional del Privacy Service para obtener más detalles.

### Determine los requisitos de privacidad de su organización {#requirements}

Según la naturaleza de su negocio y las jurisdicciones bajo las que actúa, sus operaciones de datos pueden estar sujetas a regulaciones legales de privacidad. Estas regulaciones, a menudo, otorgan a sus clientes el derecho de solicitar acceso a los datos que se recopilan de ellos, así como de solicitar la eliminación de esos datos almacenados. Estas solicitudes de datos personales de los clientes se denominan &quot;solicitudes de privacidad&quot; en toda la documentación.

Para obtener más información sobre las distintas regulaciones legales de privacidad en las que Privacy Service gestiona las solicitudes de, incluidos los términos clave y las respuestas a las preguntas más frecuentes, consulte la [documentación sobre normas de privacidad](./regulations/overview.md).

Si las operaciones de datos caen dentro del ámbito de cualquiera de las regulaciones admitidas, revise su documentación para obtener información importante, como los derechos de privacidad específicos que otorgan a sus clientes y las ventanas de cumplimiento para cumplir con las solicitudes de privacidad. Esta información debe tenerse en cuenta a la hora de determinar cómo integrar Privacy Service en el sistema CRM y cómo deben interactuar los clientes con el sitio web para realizar solicitudes de privacidad.

Además de las regulaciones legales, también debe tener en cuenta cualquier estándar organizativo o industrial aplicable a su organización al tomar estas decisiones.

### Etiquetado de datos para solicitudes de privacidad {#label}

Según la variable [!DNL Experience Cloud] Para las aplicaciones que utilice, debe etiquetar los campos de datos específicos a los que se debe acceder o eliminar en respuesta a las solicitudes de privacidad. El proceso de etiquetado de datos varía según la aplicación. Para obtener información sobre cómo etiquetar datos para cada aplicación de Adobe admitida, consulte el documento sobre [aplicaciones de Experience Cloud](./experience-cloud-apps.md).

### Determinar los tipos de datos de identidad que se enviarán al Privacy Service {#identity}

Para que el Privacy Service procese una solicitud de privacidad de un cliente, se debe proporcionar al menos un valor de identidad único para ese cliente en la propia solicitud. Un valor de identidad único es cualquier información que pueda utilizarse para identificar a una persona individual y sus datos personales almacenados dentro de su [!DNL Experience Cloud] almacenes de datos. El Privacy Service utiliza esta información de identidad para localizar y procesar los datos personales del cliente según la naturaleza de la solicitud (acceso, eliminación o exclusión).

Según la variable [!DNL Experience Cloud] Para las aplicaciones que utiliza su sistema CRM, variará el tipo y el número de valores de identidad que debe proporcionar a cada cliente. Algunas aplicaciones utilizan sus propios valores de ID de cliente internos (como los ID de Adobe Target), mientras que otras soluciones dependen de los identificadores globales de la Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastrean la actividad de los clientes en todas las [!DNL Experience Cloud] aplicaciones. Además, la información personal genérica, como una dirección de correo electrónico o un número de teléfono, también puede servir como datos de identidad válidos.

Lea el documento el [datos de identidad para solicitudes de privacidad](./identity-data.md) para obtener información más detallada sobre los tipos de información de identidad que se aceptan para el Privacy Service. El documento también proporciona instrucciones sobre cómo aplicar tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada de sus clientes a medida que interactúan con su sitio web y enviar esos datos al Privacy Service en solicitudes de API.

### Empezar a realizar solicitudes de privacidad {#requests}

Una vez que haya determinado las necesidades de privacidad de su empresa y haya decidido qué valores de identidad enviar a Privacy Service, puede empezar a realizar solicitudes de privacidad. Utilice Privacy Service para enviar solicitudes de privacidad a través de la API o la interfaz de usuario.

>[!IMPORTANT]
>
>Las secciones siguientes proporcionan vínculos a documentación que explica cómo realizar solicitudes de privacidad genéricas en la API o la IU. Sin embargo, según la variable [!DNL Experience Cloud] Para las aplicaciones que está utilizando, los campos que debe enviar en la carga útil de la solicitud pueden ser diferentes de los ejemplos mostrados en estas guías.
>
>A medida que siga las guías de la API o la IU, consulte el documento sobre [Aplicaciones de Privacy Service y Experience Cloud](./experience-cloud-apps.md) para obtener más documentación sobre cómo dar formato a las solicitudes de privacidad de su [!DNL Experience Cloud] aplicaciones.
>
>También es importante tener en cuenta que las solicitudes de privacidad se procesan asincrónicamente en todas las aplicaciones de Experience Cloud. Una vez que el Privacy Service recibe una solicitud, cada solicitud puede tardar entre minutos y semanas en completarse. La cantidad de tiempo que se tarda en completar cada solicitud es específica de la aplicación con la que está trabajando y de la cantidad de datos que deben procesarse.

#### Uso de la API {#api}

Para aproximarse programáticamente al cumplimiento de la normativa de privacidad de su [!DNL Experience Cloud] aplicaciones, puede utilizar llamadas de API RESTful a [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) extremos para crear y administrar trabajos de privacidad. Para ver los pasos detallados sobre cómo utilizar la API, consulte la [Guía de API de Privacy Service](api/overview.md).

#### Uso de la IU {#ui}

>[!NOTE]
>
>Actualmente, la IU de Privacy Service solo admite solicitudes de acceso y eliminación. Todas las solicitudes de exclusión deben realizarse a través de la API en su lugar.

Puede crear y supervisar trabajos de privacidad mediante una interfaz gráfica con la interfaz de usuario de Privacy Service. La interfaz de usuario de incluye una **[!UICONTROL Informe de estado]** widget que proporciona una representación visual del estado de todas las solicitudes activas y puede crear solicitudes con el complemento integrado **[!UICONTROL Generador de solicitudes]** o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario de, consulte [Guía del usuario del Privacy Service](ui/overview.md).

### Supervisión de trabajos de privacidad {#monitor}

Una vez que haya realizado trabajos de privacidad, tiene varias opciones para monitorizar su estado y resultados:

| Método de monitorización | Descripción |
| --- | --- |
| IU de Privacy Service | Puede ver una representación visual del estado de todas las solicitudes activas con el panel de monitorización de la IU de Privacy Service. Consulte la [Guía del usuario del Privacy Service](ui/overview.md) para obtener más información. |
| API de Privacy Service | Puede monitorizar mediante programación el estado de los trabajos de privacidad mediante los puntos finales de búsqueda proporcionados por la API de Privacy Service. Consulte la [Guía de API de Privacy Service](./api/overview.md) para ver los pasos detallados sobre cómo utilizar la API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] utilice Eventos de Adobe I/O enviados a un webhook configurado para facilitar una automatización eficiente de las solicitudes de trabajo. Reducen o eliminan la necesidad de sondear la API de Privacy Service para comprobar si un trabajo se ha completado o si se ha alcanzado un determinado hito dentro de un flujo de trabajo. Consulte el tutorial sobre [suscripción a eventos de privacidad](./privacy-events.md) para obtener más información. |

## Pasos siguientes

Este documento proporciona información general de alto nivel sobre Privacy Service y los pasos principales necesarios para comenzar a utilizar las funcionalidades del servicio. Consulte la documentación relacionada con la información general para obtener información más detallada sobre los distintos aspectos de trabajar con Privacy Service.
