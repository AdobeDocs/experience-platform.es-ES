---
keywords: extensión de reenvío de eventos;twitter;extensión de reenvío de eventos de twitter
title: Extensión de reenvío de eventos de Twitter
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite introducir eventos en Twitter para los requisitos de su empresa.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 374c140a5db678adfa2e038b69478ad8c7f8dc95
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# Extensión de reenvío de eventos de [!DNL Twitter]

[[!DNL Twitter]](https://twitter.com/i/flow/login) es un servicio de redes sociales y medios sociales en línea, en el que los usuarios publican e interactúan con mensajes de 280 caracteres conocidos como tweets. Los usuarios pueden interactuar con Twitter usando un navegador, software de front-end móvil o mediante programación a través de sus [API](https://developer.twitter.com/en/docs/twitter-api)

La extensión de la API de conversiones web [!DNL Twitter] [reenvío de eventos](../../../ui/event-forwarding/overview.md) permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Twitter]. Este documento describe los casos de uso de la extensión, cómo instalarla y cómo integrar sus capacidades en las [reglas](../../../ui/managing-resources/rules.md) de reenvío de eventos.

[!DNL Twitter] requiere [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) para la autenticación con la API [!DNL Twitter] [!DNL Web Conversions].

## Casos de uso

Esta extensión debe usarse si desea usar datos de Edge Network en [!DNL Twitter] para aprovechar las capacidades de segmentación y análisis de clientes.

Por ejemplo, considere un equipo de marketing en una organización. El equipo captura los datos de eventos de interacción de usuarios de su sitio web como datos de eventos de su sitio web y los carga en [!DNL Twitter] mediante esta extensión de reenvío de eventos.

Los equipos de marketing y análisis pueden aprovechar las capacidades de [!DNL Twitter's] para realizar análisis adicionales y dirigir a estos usuarios a campañas publicitarias dirigidas.

Para obtener más información sobre casos de uso específicos de [!DNL Twitter], consulte la documentación de [[!DNL Twitter] casos de uso](https://developer.twitter.com/en/use-cases/build-for-businesses).

## [!DNL Twitter] requisitos previos y protecciones {#prerequisites}

Debe tener una cuenta de [!DNL Twitter] válida para utilizar esta extensión. Vaya a la [[!DNL Twitter] página de registro](https://help.twitter.com/en/using-twitter/create-twitter-account) para registrarse y crear una cuenta si todavía no la tiene.

Debe configurar su cuenta como una cuenta de desarrollador de [!DNL Twitter]. Para saber cómo registrarse como desarrollador, consulte la [[!DNL Twitter] cuenta de desarrollador](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Protecciones de API {#guardrails}

La API de conversiones web [!DNL Twitter] tiene un límite de tasa de 60 000 solicitudes por intervalo de 15 minutos, en el que cada solicitud permite 500 eventos.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Twitter], se requieren las siguientes entradas:

| Tipo de clave | Descripción |
| --- | --- |
| Clave de consumidor | Clave de API de la aplicación para acceder a la API [!DNL Twitter]. Consulte la documentación de [!DNL Twitter] sobre [secretos y claves de api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obtener instrucciones. |
| Secreto del consumidor | El Secreto de API permite que su aplicación acceda a la API [!DNL Twitter]. Consulte la documentación de [!DNL Twitter] sobre [secretos y claves de api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obtener instrucciones. |
| Secreto de token | El secreto de token que no caduca de su aplicación, que se usa para autenticarse en la API [!DNL Twitter] a través de OAuth. Consulte la documentación de [!DNL Twitter] sobre [obtención de tokens de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obtener instrucciones. |
| Token de acceso | El token de acceso de su aplicación, que no caduca y que se usa para autenticarse en la API [!DNL Twitter] a través de OAuth. Consulte la documentación de [!DNL Twitter] sobre [obtención de tokens de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obtener instrucciones. |
| ID de píxel | El píxel [!DNL Twitter] es una etiqueta de sitio web que se implementa en el sitio web para rastrear acciones o conversiones del sitio. Consulte la documentación de [!DNL Twitter] sobre el [seguimiento de conversión para sitios web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) para obtener instrucciones. |

## Instalar y configurar la extensión [!DNL Twitter] {#install}

Para instalar la extensión, [cree una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Instalar]** en la tarjeta de la extensión [!DNL Twitter].

![Catálogo que muestra la extensión [!DNL Twitter] que resalta la instalación.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Según sus necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de empezar para determinar qué entidades debe configurar para su caso de uso.

En la siguiente pantalla, escriba los siguientes [valores de configuración](#configuration-details) que recopiló anteriormente de [!DNL Twitter]:

* **[!UICONTROL Id. de píxel]**
* **[!UICONTROL Clave de consumidor]**
* **[!UICONTROL Secreto del consumidor]**
* **[!UICONTROL Token]**
* **[!UICONTROL Secreto de token]**

Cuando termine, seleccione **[!UICONTROL Guardar]**.

Pantalla de configuración de ![[!DNL Twitter] para la extensión [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinan cuándo y cómo se enviarán los eventos a [!DNL Twitter].

Cree una nueva [regla](../../../ui/managing-resources/rules.md) en su propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Twitter]**. Para enviar eventos de Edge Network a [!DNL Twitter], establezca **[!UICONTROL Tipo de acción]** en **[!UICONTROL Enviar conversión web].**

Después de la selección, aparecen controles adicionales para configurar aún más el evento. Debe asignar las propiedades de evento [!DNL Twitter] a los elementos de datos que creó anteriormente. Para obtener más información, consulte la [[!DNL Twitter] API de conversiones web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![El [!DNL Twitter] está creando una regla de evento de conversión.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identificación de usuario]**

| Nombre del campo | Descripción | Ejemplo | Requerido |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Clic ID] | [!DNL Twitter] ID de clic según se analizó en la URL de pulsación. | 26l6412g5p4iyj65a2oic2ayg2 | Obligatorio si no se añade ningún otro identificador. |
| [!UICONTROL Correo electrónico] | Una dirección de correo electrónico con hash SHA256. El texto debe escribirse en minúsculas y los espacios iniciales o finales deben eliminarse antes del hash. | eventforwarding@example.com | Obligatorio si no se añade ningún otro identificador. |
| [!UICONTROL Teléfono] | El teléfono sirve como identificador para coincidir con el evento de conversión. El número de teléfono debe tener el formato E164 [+][código de país][código de área][local phone number] antes del hash. | +911234567875 | Obligatorio si no se añade ningún otro identificador. |

**[!UICONTROL Datos de conversión]**

| Nombre del campo | Descripción | Ejemplo | Requerido |
| --- | --- | --- | --- |
| [!UICONTROL Tiempo de conversión] | Fecha-hora como cadena en formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Sí |
| [!UICONTROL Id. de evento] | El ID en base 36 de un evento específico. Este identificador debe coincidir con un evento preconfigurado contenido en su cuenta publicitaria de [!DNL Twitter]. Esto se conoce como ID del evento correspondiente en el Administrador de eventos. | o87ne o tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sí |
| [!UICONTROL Número de elementos] | El número de artículos que se compran en el evento. Debe ser un número positivo mayor que 0. | 4 | No |
| [!UICONTROL Moneda] | La moneda de los artículos que se compran en el evento. Esto se expresa en ISO-4217 y, si no se proporciona, el valor predeterminado es USD. | USD | No |
| [!UICONTROL Valor] | El valor del precio de los artículos que se compran en el evento. | 100,00 | No |
| [!UICONTROL ID de conversión] | Identificador de un evento de conversión que se puede utilizar para la deduplicación entre conversiones de API de conversión y píxeles web en la misma etiqueta de evento. | 23294827 | No |
| [!UICONTROL Descripción] | Una descripción con cualquier información adicional sobre las conversiones. | Probar conversión | No |

## Validar datos dentro de [!DNL Twitter]

Una vez creada y ejecutada la regla de reenvío de eventos, valide si el evento enviado a la API [!DNL Twitter] se muestra según lo esperado en la interfaz de usuario de [!DNL Twitter].

Si la recopilación de eventos y la integración de [!DNL Experience Platform] se realizaron correctamente, verá eventos dentro del [!DNL Twitter] [!UICONTROL administrador de eventos].

![Administrador de eventos [!DNL Twitter]](../../../images/extensions/server/twitter/event-manager.png)

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Twitter] mediante el reenvío de eventos. Para obtener más información sobre estas tecnologías subyacentes, consulte la documentación oficial:

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversión web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [ID de píxel y seguimiento de conversión](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
