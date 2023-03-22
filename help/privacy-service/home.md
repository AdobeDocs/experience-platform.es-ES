---
keywords: Experience Platform;inicio;temas populares;RGPD;rgpd;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Información general del Privacy Service
description: Privacy Service le permite facilitar el cumplimiento automatizado de las normas legales de privacidad en sus operaciones de datos de Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: e09f0598e1d8dc007d0fdfcf13da11d5cad94c54
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 5%

---

# Información general del [!DNL Privacy Service]

>[!IMPORTANT]
>
>Se han mejorado los permisos de Adobe Experience Platform Privacy Service para aumentar su nivel de granularidad. Estos cambios permiten a los administradores de la organización conceder acceso a más usuarios con la función y el nivel de permiso deseados. Los usuarios de cuentas técnicas deben actualizar sus permisos de Privacy Service, ya que esta actualización inminente constituye un cambio radical para ellos. La aplicación de este cambio de permisos tendrá lugar en **28 de marzo de 2023**.
>
>Las cuentas técnicas están disponibles para los clientes empresariales y se crean mediante la consola de desarrolladores de Adobe. La Adobe ID de un titular de cuenta técnica finaliza en `@techacct.adobe.com`. Si no está seguro de si es titular de una cuenta técnica, póngase en contacto con el administrador de su organización.

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan.

Adobe Experience Platform [!DNL Privacy Service] se desarrolló en respuesta a un cambio fundamental en la forma en que se requiere que las empresas gestionen los datos personales de sus clientes. El objetivo central de [!DNL Privacy Service] es automatizar el cumplimiento de las normas de privacidad de datos que, cuando se violan, pueden resultar en importantes multas y interrumpir las operaciones de datos para su empresa.

[!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. con [!DNL Privacy Service], puede enviar solicitudes para acceder a los datos personales de los clientes y eliminarlos de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

>[!IMPORTANT]
>
>Privacy Service solo está diseñado para el interesado y las solicitudes de derechos del consumidor. No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos. El Adobe tiene la obligación jurídica de cumplirlos a su debido tiempo. Por lo tanto, no se permite la prueba de carga en el Privacy Service, ya que se trata de un entorno de solo producción y crea un atraso innecesario en las solicitudes de privacidad válidas.
>
>Ahora existe un límite de carga diaria estricto para ayudar a evitar el uso indebido del servicio. Los usuarios a los que se descubra que abusan del sistema tendrán deshabilitado su acceso al servicio. Posteriormente se celebrará una reunión con ellos para abordar sus actividades y examinar el uso aceptable de los Privacy Service.

## Introducción a [!DNL Privacy Service] {#getting-started}

Con el fin de [!DNL Privacy Service], es necesario tomar varias decisiones clave en términos de los requisitos de privacidad de su organización, los tipos de datos de identidad que recopila de sus clientes y la mejor manera de interconectar su sistema CRM con el servicio.

Estas decisiones pueden resumirse en las siguientes preguntas:

1. **¿Qué información recopilo de mis clientes?**
   * Para sacar el máximo partido a [!DNL Privacy Service], debe comprender detalladamente los tipos de datos que recopila de sus clientes y cuál de ellos está sujeto a las normas de privacidad. Consulte la sección sobre [determinación de los requisitos de privacidad](#requirements) para obtener más información.
1. **¿He etiquetado correctamente mis datos?**
   * Los datos deben etiquetarse correctamente para que el servicio pueda determinar a qué campos acceder o eliminar durante los trabajos de privacidad. Consulte la sección sobre [etiquetado de datos](#label) para obtener más información.
1. **¿Sé a qué ID enviar? [!DNL Privacy Service]?**
   * Al enviar solicitudes de privacidad, se deben proporcionar ID de cliente individuales específicos de aplicaciones de Adobe específicas. Consulte las secciones de [proporcionar datos de identidad](#identity)  y [realizar solicitudes de privacidad](#requests) para obtener más información.
1. **¿Cómo realizo el seguimiento de mis trabajos de privacidad?**
   * Una vez que haya realizado solicitudes de privacidad, hay varias opciones para rastrear su estado y resultados. Consulte la sección sobre [monitorización de trabajos de privacidad](#monitor) para obtener más información.

En las secciones que figuran a continuación se proporcionan orientaciones generales sobre estas importantes etapas previas y también se proporcionan enlaces para otras [!DNL Privacy Service] documentación para obtener más información.

### Determine los requisitos de privacidad de su organización {#requirements}

Según la naturaleza de su negocio y las jurisdicciones bajo las que actúa, sus operaciones de datos pueden estar sujetas a regulaciones legales de privacidad. Estas regulaciones, a menudo, otorgan a sus clientes el derecho de solicitar acceso a los datos que se recopilan de ellos, así como de solicitar la eliminación de esos datos almacenados. Estas solicitudes de datos personales de los clientes se denominan &quot;solicitudes de privacidad&quot; en toda la documentación.

Para obtener más información sobre las diferentes regulaciones legales de privacidad que [!DNL Privacy Service] gestiona las solicitudes de, incluidos los términos clave y las respuestas a las preguntas más frecuentes, consulte [documentación de las normas de privacidad](./regulations/overview.md).

Si sus operaciones de datos caen dentro del ámbito de aplicación de cualquiera de las regulaciones admitidas, revise su documentación para obtener información importante, como los derechos de privacidad específicos que conceden a sus clientes y las ventanas de cumplimiento de normas para cumplir con las solicitudes de privacidad. Esta información debe tenerse en cuenta a la hora de determinar cómo se integra [!DNL Privacy Service] en su sistema CRM y cómo los clientes deben interactuar con su sitio web para realizar solicitudes de privacidad.

Además de los reglamentos legales, cualquier norma organizativa o industrial aplicable a su organización también debe ser considerada al tomar estas decisiones.

### Etiquetado de datos para solicitudes de privacidad {#label}

Según el [!DNL Experience Cloud] las aplicaciones que utilice, debe etiquetar los campos de datos específicos a los que se debe acceder o eliminar en respuesta a las solicitudes de privacidad. El proceso de etiquetado de datos varía según la aplicación. Para obtener información sobre cómo etiquetar datos para cada aplicación de Adobe admitida, consulte el documento en [aplicaciones Experience Cloud](./experience-cloud-apps.md).

### Determinar los tipos de datos de identidad a los que enviar [!DNL Privacy Service] {#identity}

Para [!DNL Privacy Service] para procesar una solicitud de privacidad de un cliente, en la propia solicitud debe proporcionarse al menos un valor de identidad único para ese cliente. Un valor de identidad único es cualquier información que puede utilizarse para identificar a una persona individual y sus datos personales almacenados dentro de su [!DNL Experience Cloud] almacenes de datos. [!DNL Privacy Service] utiliza esta información de identidad para localizar y procesar los datos personales del cliente según la naturaleza de la solicitud (acceso, eliminación o exclusión).

Según el [!DNL Experience Cloud] aplicaciones que utiliza su sistema CRM, el tipo y el número de valores de identidad que debe proporcionar para cada cliente variarán. Algunas aplicaciones utilizan sus propios valores de ID de cliente internos (como Adobe Target ID), mientras que otras soluciones dependen de los identificadores globales de Adobe [!DNL Experience Cloud Identity Service] (ECID) que realizan un seguimiento de la actividad de los clientes en todas las [!DNL Experience Cloud] aplicaciones. Además, la información personal genérica, como una dirección de correo electrónico o un número de teléfono, también puede servir como datos de identidad válidos.

El documento de [datos de identidad para solicitudes de privacidad](./identity-data.md) proporciona información más detallada sobre los tipos de información de identidad que se aceptan para [!DNL Privacy Service]. El documento también proporciona instrucciones sobre cómo aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada de los clientes a medida que interactúan con el sitio web y enviar esos datos a [!DNL Privacy Service] en solicitudes de API.

### Comenzar a realizar solicitudes de privacidad {#requests}

Una vez que haya determinado las necesidades de privacidad de su empresa y haya decidido a qué valores de identidad se enviarán [!DNL Privacy Service], puede empezar a realizar solicitudes de privacidad. [!DNL Privacy Service] le permite enviar solicitudes de privacidad a través de la API o la interfaz de usuario.

>[!IMPORTANT]
>
>Las secciones siguientes proporcionan vínculos a documentación que explica cómo realizar solicitudes de privacidad genéricas en la API o la interfaz de usuario. Sin embargo, según la variable [!DNL Experience Cloud] aplicaciones que utilice, los campos que debe enviar en la carga útil de la solicitud pueden diferir de los ejemplos mostrados en estas guías.
>
>A medida que siga junto con las guías de la API o la interfaz de usuario, consulte el documento sobre [aplicaciones de Privacy Service y Experience Cloud](./experience-cloud-apps.md) para obtener más documentación sobre cómo dar formato a las solicitudes de privacidad de su [!DNL Experience Cloud] aplicación(s).
>
>También es importante tener en cuenta que las solicitudes de privacidad se procesan asincrónicamente en las aplicaciones de Experience Cloud. Una vez que el Privacy Service recibe una solicitud, cada aplicación puede tardar entre minutos y semanas en completarse. La cantidad de tiempo que se tarda en completar cada solicitud es específica para la aplicación con la que esté trabajando y la cantidad de datos que se deben procesar.

#### Uso de la API

La variable [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) proporciona varios puntos de conexión para crear y administrar trabajos de privacidad mediante llamadas a la API RESTful, lo que le permite abordar mediante programación el cumplimiento de la normativa de privacidad para su [!DNL Experience Cloud] aplicaciones. Para ver los pasos detallados sobre cómo utilizar la API, consulte la [Guía de API del Privacy Service](api/overview.md).

#### Uso de la interfaz de usuario

>[!NOTE]
>
>La variable [!DNL Privacy Service] Actualmente, la interfaz de usuario solo admite solicitudes de acceso y eliminación. Todas las solicitudes de exclusión deben realizarse a través de la API .

La variable [!DNL Privacy Service] La interfaz de usuario le permite crear y supervisar trabajos de privacidad mediante una interfaz gráfica. La interfaz de usuario incluye un **[!UICONTROL Informe de estado]** que proporciona una representación visual del estado de todas las solicitudes activas y le permite crear nuevas solicitudes mediante el complemento **[!UICONTROL Creador de solicitudes]** o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario, consulte la [Guía del usuario del Privacy Service](ui/overview.md).

### Supervisar trabajos de privacidad {#monitor}

Una vez que haya realizado trabajos de privacidad, tiene varias opciones para monitorizar su estado y sus resultados:

| Método de monitorización | Descripción |
| --- | --- |
| [!DNL Privacy Service] IU | La variable [!DNL Privacy Service] La interfaz de usuario proporciona un panel de monitorización que le permite ver una representación visual del estado de todas las solicitudes activas. Consulte la [Guía del usuario del Privacy Service](ui/overview.md) para obtener más información. |
| [!DNL Privacy Service] API | Puede monitorizar mediante programación el estado de los trabajos de privacidad mediante los extremos de búsqueda proporcionados por la variable [!DNL Privacy Service] API. Consulte la [Guía de API del Privacy Service](./api/overview.md) para ver los pasos detallados sobre cómo utilizar la API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveche los eventos de Adobe I/O enviados a un enlace web configurado para facilitar la automatización eficiente de las solicitudes de trabajo. Reducen o eliminan la necesidad de sondear el [!DNL Privacy Service] para comprobar si un trabajo se ha completado o si se ha alcanzado un hito determinado dentro de un flujo de trabajo. Consulte el tutorial en [suscripción a eventos de privacidad](./privacy-events.md) para obtener más información. |

## Pasos siguientes

Este documento ofrece una visión general de alto nivel de [!DNL Privacy Service] y los pasos principales necesarios para empezar a utilizar las capacidades del servicio. Consulte la documentación vinculada a lo largo de la descripción general para obtener información más detallada sobre los distintos aspectos del trabajo con [!DNL Privacy Service].
