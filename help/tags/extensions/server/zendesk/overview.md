---
title: Extensión de reenvío de eventos de Zendesk
description: Extensión de reenvío de eventos de Zendesk para Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: d23f1cc9dd0155aceae78bf938d35463e9c38181
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 4%

---

# [!DNL Zendesk] Información general sobre la extensión API Events

[Zendesk](https://www.zendesk.com) es una solución de servicio al cliente y una herramienta de ventas. El Zendesk [reenvío de eventos](../../../ui/event-forwarding/overview.md) La extensión de aprovecha [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) para enviar eventos desde Adobe Experience Platform Edge Network a Zendesk para un procesamiento posterior. Puede utilizar la extensión para recopilar interacciones de perfil del cliente para utilizarlas en análisis y acciones posteriores.

Este documento explica cómo instalar y configurar la extensión en la interfaz de usuario de.

## Requisitos previos

Debe tener una cuenta de Zendesk para utilizar esta extensión. Puede registrarse para obtener una cuenta de Zendesk en la [Sitio web de Zendesk](https://www.zendesk.com/register/).

También debe recopilar los siguientes detalles para su configuración de Zendesk:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| Subdomain | Durante el proceso de registro, un **subdominio** se crea específicamente para la cuenta de. Consulte la [Documentación de Zendesk](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) para obtener más información. | `xxxxx.zendesk.com` (donde `xxxxx` es el valor proporcionado durante la creación de la cuenta) |
| Token de API | Zendesk utiliza tokens de portador como mecanismo de autenticación para comunicarse con la API de Zendesk. Después de iniciar sesión en el portal de Zendesk, genere un token de API. Consulte la [Documentación de Zendesk](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) para obtener más información. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

Finalmente, debe crear un secreto de reenvío de eventos para el token de API. Establezca el tipo secreto en **[!UICONTROL Token]** y establezca el valor en el token de API que haya recopilado de su configuración de Zendesk. Consulte la documentación sobre [secretos en el reenvío de eventos](../../../ui/event-forwarding/secrets.md) para obtener más información sobre la configuración de secretos.

## Instalar la extensión {#install}

Para instalar la extensión de Zendesk en la interfaz de usuario de, vaya a **Reenvío de eventos** y seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, vaya a **Extensiones** > **Catálogo**. Buscar &quot;[!DNL Zendesk]&quot;, y luego seleccione **[!DNL Install]** en la extensión de Zendesk.

![Botón Instalar para la extensión de Zendesk seleccionada en la interfaz de usuario](../../../images/extensions/server/zendesk/install.png)

## Configuración de la extensión {#configure}

>[!IMPORTANT]
>
>Según sus necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de empezar para determinar qué entidades debe configurar para su caso de uso.

Seleccionar **Extensiones** en el panel de navegación izquierdo. En **Instalado**, seleccione **Configurar** en la extensión de Zendesk.

![Botón Configurar para la extensión de Zendesk seleccionada en la interfaz de usuario](../../../images/extensions/server/zendesk/configure.png)

En **[!UICONTROL Dominio de Zendesk]**, introduzca el valor del subdominio de Zendesk. En **[!UICONTROL Token de Zendesk]**, seleccione el secreto que creó anteriormente que contiene el token de API.

![Opciones de configuración rellenadas en la interfaz de usuario](../../../images/extensions/server/zendesk/input.png)

## Configuración de una regla de reenvío de eventos

Empezar a crear una nueva regla de reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione [!UICONTROL Zendesk] extensión y, a continuación, seleccione la [!UICONTROL Crear evento] tipo de acción.

![Definir regla](../../../images/extensions/server/zendesk/rule.png)

Al establecer la configuración de la acción, se le pedirá que asigne elementos de datos a las distintas propiedades que se enviarán a Zendesk.

![Definir configuración de acción](../../../images/extensions/server/zendesk/action-configurations.png)

Estos elementos de datos deben asignarse como se hace referencia a continuación.

### `event` teclas

`event` es un objeto JSON que representa el evento activado por el usuario. Consulte el documento de Zendesk en la [anatomía de un evento](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) para obtener más información sobre las propiedades capturadas por `event` objeto.

Se puede hacer referencia a las siguientes claves dentro de la variable `event` al asignar elementos de datos:

| `event` key | Tipo | Ruta de plataforma | Descripción | Obligatorio | Límites |
| --- | --- | --- | --- | --- | --- |
| `source` | Cadena | `arc.event.xdm._extconndev.event_source` | La aplicación que envió el evento. | Sí | No use `Zendesk` como un valor, ya que es un nombre de fuente protegido para los eventos estándar de Zendesk. Si intenta usarlo, se producirá un error.<br>La longitud del valor no debe superar los 40 caracteres. |
| `type` | Cadena | `arc.event.xdm._extconndev.event_type` | Un nombre para el tipo de evento. Puede utilizar este campo para denotar diferentes tipos de eventos para un origen determinado. Por ejemplo, puede crear un conjunto de eventos para los inicios de sesión de los usuarios y otro para los carros de compras. | Sí | La longitud del valor no debe superar los 40 caracteres. |
| `description` | Cadena | `arc.event.xdm._extconndev.description` | Una descripción del evento. | No | (N/D) |
| `created_at` | Cadena | `arc.event.xdm.timestamp` | Una marca de tiempo ISO-8601 que refleja la hora en que se creó el evento. | No | (N/D) |
| `properties` | Objeto | `arc.event.xdm._extconndev.EventProperties` | Un objeto JSON personalizado con detalles sobre el evento. | Sí | (N/D) |

{style="table-layout:auto"}

>[!NOTE]
>
>Consulte la [[!DNL Zendesk Events API] documentación](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) para obtener instrucciones adicionales sobre las propiedades de eventos.

### `profile` teclas

`profile` es un objeto JSON que representa al usuario que activó el evento. Consulte el documento de Zendesk en la [anatomía de un perfil](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/) para obtener más información sobre las propiedades capturadas por `profile` objeto.

Se puede hacer referencia a las siguientes claves dentro de la variable `profile` al asignar elementos de datos:

| `profile` key | Tipo | Ruta de plataforma | Descripción | Obligatorio | Límites |
| --- | --- | --- | --- | --- | --- |
| `source` | Cadena | `arc.event.xdm._extconndev.profile_source` | El producto o servicio asociado con el perfil, como `Support`, `CompanyName`, o `Chat`. | Sí | (N/D) |
| `type` | Cadena | `arc.event.xdm._extconndev.profile_type` | Un nombre para el tipo de perfil. Puede utilizar este campo para crear diferentes tipos de perfiles para una fuente determinada. Por ejemplo, puede crear un conjunto de perfiles de compañía para clientes y otro para empleados. | Sí | La longitud del tipo de perfil no debe superar los 40 caracteres. |
| `name` | Cadena | `arc.event.xdm._extconndev.name` | El nombre de la persona del perfil | No | (N/D) |
| `user_id` | Cadena | `arc.event.xdm._extconndev.user_id` | El ID de usuario de la persona en Zendesk. | No | (N/D) |
| `identifiers` | Matriz | `arc.event.xdm._extconndev.identifiers` | Matriz que contiene al menos un identificador. Cada identificador consta de un tipo y un valor. | Sí | Consulte la [Documentación de Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/profiles_api/profiles_api/#identifiers-array) para obtener más información sobre `identifiers` matriz. Todos los campos y valores deben ser únicos. |
| `attributes` | Objeto | `arc.event.xdm._extconndev.attrbutes` | Objeto que contiene propiedades definidas por el usuario sobre la persona. | No | Consulte la [Documentación de Zendesk](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/#attributes) para obtener más información sobre los atributos de perfil. |

{style="table-layout:auto"}

## Validación de datos en Zendesk {#validate}

Si la recopilación de eventos y la integración de Adobe Experience Platform son exitosas, entonces los eventos dentro de la consola de Zendesk deberían aparecer como se muestra a continuación. Esto indica una integración correcta.

Perfiles:

![Página Perfiles de Zendesk](../../../images/extensions/server/zendesk/zendesk-profiles.png)

Eventos:

![Página de eventos de Zendesk](../../../images/extensions/server/zendesk/zendesk-events.png)

## Límites de solicitudes {#limits}

Según el tipo de cuenta, el [!DNL Events API] puede gestionar el siguiente número de solicitudes por minuto:

| [!DNL Account Type] | Solicitudes por minuto |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

Consulte la [Documentación de Zendesk](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) para obtener más información sobre estos límites.

## Errores y solución de problemas {#errors-and-troubleshooting}

Al utilizar o configurar la extensión, la API de eventos de Zendesk podría devolver los errores siguientes:

| Código de error | Descripción | Resolución | Ejemplo |
|---|---|---|---|
| 400 | **Longitud de perfil no válida:** Este error se produce cuando la longitud de un atributo de perfil contiene más de 40 caracteres. | Limite la longitud de los datos de atributos de perfil a un máximo de 40 caracteres. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Ruta no encontrada:** Este error se produce cuando se ha proporcionado un dominio no válido. | Compruebe que un dominio válido se proporciona en el siguiente formato: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Falta la autenticación o no es válida:** Este error se produce cuando el acceso al token no es válido, falta o ha caducado. | Compruebe que el token de acceso es válido y no ha caducado. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Permisos insuficientes:** Este error se produce cuando no se proporcionan los permisos suficientes para acceder al recurso. | Compruebe que se han proporcionado los permisos necesarios. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Demasiadas solicitudes:** Este error se produce cuando se ha superado el límite de registros del objeto de extremo. | Consulte la sección anterior sobre [límites de solicitudes](#limits) para obtener más información sobre los umbrales por límite. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## Pasos siguientes

Este documento explica cómo instalar y configurar la extensión de reenvío de eventos de Zendesk en la interfaz de usuario. Para obtener más información sobre la recopilación de datos de eventos en Zendesk, consulte la documentación oficial:

* [Introducción a los eventos](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [API de eventos de Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/)
* [Acerca de la API de eventos](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomía de un evento](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [API de perfiles de Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/#profile-object)
* [Acerca de la API de perfiles](https://developer.zendesk.com/documentation/ticketing/profiles/about-the-profiles-api/)
* [Anatomía de un perfil](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)
