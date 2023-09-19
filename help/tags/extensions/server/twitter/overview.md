---
keywords: extensión de reenvío de eventos;twitter;extensión de reenvío de eventos de twitter
title: extensión de reenvío de eventos de twitter
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite introducir eventos en el Twitter para sus necesidades comerciales.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 3%

---

# Extensión de reenvío de eventos de [!DNL Twitter]

[[!DNL Twitter]](https://twitter.com/i/flow/login) es un servicio de redes sociales y redes sociales en línea, en el que los usuarios publican e interactúan con mensajes de 280 caracteres conocidos como tweets. Los usuarios pueden interactuar con el Twitter mediante un explorador, software de front-end móvil o mediante programación a través de su [API](https://developer.twitter.com/en/docs/twitter-api)

El [!DNL Twitter] API de conversiones web [reenvío de eventos](../../../ui/event-forwarding/overview.md) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Twitter]. Este documento describe los casos de uso de la extensión, cómo instalarla y cómo integrar sus funcionalidades en el reenvío de eventos [reglas](../../../ui/managing-resources/rules.md).

[!DNL Twitter] requiere [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) para la autenticación con [!DNL Twitter] [!DNL Web Conversions] API.

## Casos de uso

Debe usar esta extensión si desea usar datos de la red perimetral en [!DNL Twitter] para aprovechar sus capacidades de segmentación y análisis de clientes.

Por ejemplo, considere un equipo de marketing en una organización. El equipo de captura los datos de eventos de interacción de usuarios de su sitio web como datos de eventos de su sitio web y los carga en [!DNL Twitter] uso de esta extensión de reenvío de eventos.

Los equipos de marketing y análisis pueden aprovechar [!DNL Twitter's] capacidades para realizar análisis adicionales y dirigirse a estos usuarios para campañas publicitarias dirigidas.

Para obtener más información sobre casos de uso específicos de [!DNL Twitter], consulte la [[!DNL Twitter] casos de uso](https://developer.twitter.com/en/use-cases/build-for-businesses) documentación.

## [!DNL Twitter] requisitos previos y protecciones {#prerequisites}

Debe tener un válido [!DNL Twitter] para utilizar esta extensión. Vaya a la [[!DNL Twitter] página de registro](https://help.twitter.com/en/using-twitter/create-twitter-account) para registrarse y crear una cuenta si aún no la tiene.

Debe configurar su cuenta como [!DNL Twitter] cuenta de desarrollador de. Para obtener información sobre cómo registrarse como desarrollador, consulte la [[!DNL Twitter] cuenta de desarrollador](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Protecciones de API {#guardrails}

El [!DNL Twitter] La API de conversiones web tiene un límite de velocidad de 60 000 solicitudes por intervalo de 15 minutos, en el que cada solicitud permite 500 eventos.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar al Experience Platform a [!DNL Twitter], se requieren las siguientes entradas:

| Tipo de clave | Descripción |
| --- | --- |
| Clave de consumidor | Clave de API de la aplicación para acceder a [!DNL Twitter] API. Consulte la [!DNL Twitter] documentación sobre [claves y secretos de api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obtener orientación. | |
| Secreto del consumidor | El Secreto de la API permite que su aplicación acceda al [!DNL Twitter] API. Consulte la [!DNL Twitter] documentación sobre [claves y secretos de api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obtener orientación. |
| Secreto de token | El secreto de token que no caduca de su aplicación, que se utiliza para autenticarse en el [!DNL Twitter] API mediante OAuth. Consulte la [!DNL Twitter] documentación sobre [obtención de tokens de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obtener orientación. |
| Token de acceso | El token de acceso de su aplicación, que no caduca y que se utiliza para la autenticación en [!DNL Twitter] API mediante OAuth. Consulte la [!DNL Twitter] documentación sobre [obtención de tokens de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obtener orientación. |
| ID de píxel | El [!DNL Twitter] Píxel es una etiqueta de sitio web que se implementa en el sitio web para rastrear acciones o conversiones del sitio. Consulte la [!DNL Twitter] documentación sobre [seguimiento de conversión para sitios web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) para obtener orientación. |

## Instalación y configuración de [!DNL Twitter] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** pestaña, seleccione **[!UICONTROL Instalar]** en la tarjeta de [!DNL Twitter] extensión.

![Catálogo que muestra [!DNL Twitter] instalación de resalte de extensión.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Según sus necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de empezar para determinar qué entidades debe configurar para su caso de uso.

En la pantalla siguiente, introduzca lo siguiente [valores de configuración](#configuration-details) que recopiló anteriormente de [!DNL Twitter]:

* **[!UICONTROL ID de píxel]**
* **[!UICONTROL Clave de consumidor]**
* **[!UICONTROL Secreto del consumidor]**
* **[!UICONTROL Token]**
* **[!UICONTROL Secreto de token]**

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![[!DNL Twitter] pantalla de configuración para [!DNL Twitter] extensión.](../../../images/extensions/server/twitter/configure.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinen cuándo y cómo se enviarán los eventos a [!DNL Twitter].

Crear un nuevo [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL Twitter]**. Para enviar eventos de Edge Network a [!DNL Twitter], configure el **[!UICONTROL Tipo de acción]** hasta **[!UICONTROL Enviar conversión web].**

Después de la selección, aparecen controles adicionales para configurar aún más el evento. Debe asignar el [!DNL Twitter] propiedades de evento a los elementos de datos creados anteriormente. Para obtener más información, consulte la [[!DNL Twitter] API de conversiones web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![El [!DNL Twitter] crear una regla de evento de conversión.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identificación de usuario]**

| Nombre del campo | Descripción | Ejemplo | Requerido |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID de clic] | [!DNL Twitter] Haga clic en ID tal como se analiza desde la URL de pulsación. | 26l6412g5p4iyj65a2oic2ayg2 | Obligatorio si no se añade ningún otro identificador. |
| [!UICONTROL Correo electrónico] | Una dirección de correo electrónico con hash SHA256. El texto debe escribirse en minúsculas y los espacios iniciales o finales deben eliminarse antes del hash. | eventforwarding@example.com | Obligatorio si no se añade ningún otro identificador. |
| [!UICONTROL Phone] | El teléfono sirve como identificador para coincidir con el evento de conversión. El número de teléfono debe estar en formato E164 [+][código de país][código de área][local phone number] antes del hash. | +911234567875 | Obligatorio si no se añade ningún otro identificador. |

**[!UICONTROL Datos de conversión]**

| Nombre del campo | Descripción | Ejemplo | Requerido |
| --- | --- | --- | --- |
| [!UICONTROL Tiempo de conversión] | Fecha-hora como cadena en ISO 8601 o en aaaa-MM-dd&#39;T&#39;HH:mm:formato ss:SSSZ. | 18-02-2022:14:00,603Z | Sí |
| [!UICONTROL ID de evento] | El ID en base 36 de un evento específico. Este ID debe coincidir con un evento preconfigurado contenido en su [!DNL Twitter] cuenta de publicidad. Esto se conoce como ID del evento correspondiente en el Administrador de eventos. | o87ne o tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sí |
| [!UICONTROL Número de elementos] | El número de artículos que se compran en el evento. Debe ser un número positivo mayor que 0. | 4 | No |
| [!UICONTROL Moneda] | La moneda de los artículos que se compran en el evento. Esto se expresa en ISO-4217 y, si no se proporciona, el valor predeterminado es USD. | USD | No |
| [!UICONTROL Valor] | El valor del precio de los artículos que se compran en el evento. | 100.00 | No |
| [!UICONTROL ID de conversión] | Identificador de un evento de conversión que se puede utilizar para la deduplicación entre conversiones de API de conversión y píxeles web en la misma etiqueta de evento. | 23294827 | No |
| [!UICONTROL Descripción] | Una descripción con cualquier información adicional sobre las conversiones. | Probar conversión | No |

## Validación de datos dentro de [!DNL Twitter]

Una vez creada y ejecutada la regla de reenvío de eventos, valide si el evento que se envió a [!DNL Twitter] API se muestra según lo esperado en la [!DNL Twitter] IU.

Si la colección de eventos y [!DNL Experience Platform] integración se han realizado correctamente, verá eventos dentro de la variable [!DNL Twitter] [!UICONTROL Administrador de eventos].

![El [!DNL Twitter] administrador de eventos](../../../images/extensions/server/twitter/event-manager.png)

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Twitter] uso del reenvío de eventos. Para obtener más información sobre estas tecnologías subyacentes, consulte la documentación oficial:

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversión web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token de acceso de usuario](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [ID de píxel y seguimiento de conversión](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
