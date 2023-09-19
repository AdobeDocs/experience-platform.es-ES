---
keywords: extensión de reenvío de eventos;braze;extensión de reenvío de eventos braze
title: Extensión de reenvío de eventos de Braze
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de red perimetral a Brazo.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 5%

---

# Extensión de reenvío de eventos de [!DNL Braze Track Events API]

[[!DNL Braze]](https://www.braze.com) es una plataforma de participación del cliente que potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real. Uso de [!DNL Braze], puede hacer lo siguiente:

- Ofrezca datos (como mensajes de marketing) a los usuarios segmentados en función de sus preferencias de idioma, ubicación, preferencias, etc. para aumentar las tasas de conversión y lograr objetivos comerciales clave.
- Envíe a los clientes mensajes personalizados en varios canales, incluidos correo electrónico, notificaciones push y mensajes en la aplicación, en el momento adecuado y en sus idiomas preferidos.
- Oriente a usuarios específicos para campañas promocionales y de marketing a fin de aumentar el número de clientes repetidos.
- Estudiar el comportamiento y los patrones de los usuarios para dirigirse a audiencias específicas con mensajes personalizados, lo que podría ayudar a aumentar los ingresos.

El [!DNL Braze Track Events API] [reenvío de eventos](../../../ui/event-forwarding/overview.md) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor que utilizan el [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Este documento describe los casos de uso de la extensión, cómo instalarla en las bibliotecas de reenvío de eventos y cómo utilizar sus funcionalidades en un reenvío de eventos [regla](../../../ui/managing-resources/rules.md).

## Casos de uso

Debe usar esta extensión si desea usar datos de la red perimetral en [!DNL Braze] para aprovechar sus capacidades de segmentación y análisis de clientes.

Por ejemplo, considere una organización minorista que tenga presencia multicanal (sitio web y móvil) y que capture entradas transaccionales o conversacionales como datos de evento de su sitio web y plataformas móviles. Uso de varios [etiqueta](../../../home.md) , estos datos se envían a Edge Network en tiempo real. A partir de aquí, el [!DNL Braze] la extensión de reenvío de eventos envía automáticamente los eventos relevantes a [!DNL Braze] del lado del servidor.

Una vez enviados los datos, los equipos de análisis de la organización pueden aprovecharlos [!DNL Braze's] Funcionalidades para procesar los conjuntos de datos y derivar perspectivas comerciales para generar gráficos, tableros u otras visualizaciones para informar a las partes interesadas empresariales. Consulte la [[!DNL Braze] clientes](https://www.braze.com/customers) para obtener más información sobre los distintos casos de uso de la plataforma.

## [!DNL Braze] requisitos previos y protecciones {#prerequisites}

Debe tener un [!DNL Braze] para utilizar sus tecnologías. Si no tiene una cuenta de, vaya al [Página de introducción](https://www.braze.com/get-started/) el [!DNL Braze] para conectarse a [!DNL Braze Sales] e inicie el proceso de creación de cuentas.

### Protecciones de API

La extensión de utiliza dos de [!DNL Braze]Las API de y sus límites se describen a continuación:

| API | Límites de velocidad |
| --- | --- |
| [!DNL User Track] | 50.000 peticiones por minuto. <br>Consulte la [[!DNL User Track] Documentación de API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obtener más información. |
| [!DNL User Identify] | 20.000 peticiones por minuto. <br>Consulte la [[!DNL User Identify] Documentación de API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obtener más información. |

>[!NOTE]
>
> Consulte la guía de [[!DNL Braze] Límites de API](https://www.braze.com/docs/api/api_limits/) para más detalles sobre los límites que imponen.

### Puntos de datos facturables

Envío de atributos personalizados adicionales a [!DNL Braze] puede aumentar sus [!DNL Braze] consumo de puntos de datos. Consulte con su [!DNL Braze] administrador de cuentas antes de enviar atributos personalizados adicionales. Consulte la [!DNL Braze] documentación sobre [puntos de datos facturables](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) para obtener más información.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar la red perimetral a [!DNL Braze], se requieren las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| [!DNL Braze] Instancia | El extremo REST asociado con [!DNL Braze] cuenta. Consulte la [!DNL Braze] documentación sobre [instances](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) para obtener orientación. | `https://rest.iad-03.braze.com` |
| Clave de API | El [!DNL Braze] Clave de API asociada con [!DNL Braze] cuenta. <br/>Consulte la [!DNL Braze] documentación sobre la [Clave de API de REST](https://www.braze.com/docs/api/basics/#rest-api-key) para obtener orientación. | `YOUR-BRAZE-REST-API-KEY` |

### Crear un secreto

Crear un nuevo [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y establezca el valor en su [[!DNL Braze] Clave de API](#configuration-details). Se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

## Instalación y configuración de [!DNL Braze] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** pestaña, seleccione **[!UICONTROL Instalar]** en la tarjeta de [!DNL Braze] extensión.

![[!DNL Braze]Instalar la extensión.](../../../images/extensions/server/braze/install-extension.png)

En la pantalla siguiente, introduzca lo siguiente [valores de configuración](#configuration-details) que recopiló anteriormente de [!DNL Braze]:

- **[!UICONTROL URL de extremo de resto de Bear]**: Puede introducir el valor de su [!DNL Braze] URL de extremo REST como texto sin formato en la entrada proporcionada.
- **[!UICONTROL Clave de API]**: seleccione la [elemento de datos secreto](#create-a-secret) que creó anteriormente, que contiene su [!DNL Braze] Clave de API.

Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![El [!DNL Braze] página de configuración de la extensión.](../../../images/extensions/server/braze/configure-extension.png)

## Crear un [!DNL Send Event] regla {#tracking-rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione **[!UICONTROL Soldar]** extensión y seleccione **[!UICONTROL Enviar evento]** para el tipo de acción.

![Añada una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, estos también deben ser largos, aleatorios y estar bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugeridos](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Borrar ID de usuario] | Identificador de usuario de Bear. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a usuarios con dimensiones diferentes a las del ID de usuario principal. <br><br> El objeto de alias de usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con diferentes etiquetas, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe rellenar las etiquetas [!UICONTROL ID de usuario externo] o el campo [!UICONTROL Identificador De Usuario De Braze] o el campo [!UICONTROL Alias de usuario] sección.

**[!UICONTROL Datos de Evento]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Nombre del evento &#x200B;] | Nombre del evento. | Sí |
| [!UICONTROL Hora del evento] | Fecha-hora como cadena en ISO 8601 o en `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sí |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad con una aplicación específica de su grupo de aplicaciones. Designa con qué aplicación del grupo de aplicaciones está interactuando. Obtenga más información acerca de [Tipos de identificadores API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propiedades del evento] | Objeto JSON que contiene propiedades personalizadas del evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> El **[!UICONTROL Evento Send de Braze]** la acción solo requiere un **[!UICONTROL Nombre del evento]** y **[!UICONTROL Hora del evento]** que se van a especificar, pero se debe incluir la mayor información posible en el campo propiedades personalizadas. Para obtener más información sobre [!DNL Braze] objeto de evento, consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos del usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que creen o actualicen un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] | |
| [!UICONTROL Apellidos] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Correo electrónico] | |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otro), &quot;N&quot; (no aplicable), &quot;P&quot; (prefiero no decir). |
| [!UICONTROL Ciudad] | |
| [!UICONTROL País] | País como cadena en [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como cadena en [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Fecha de nacimiento] | Cadena en formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria de [Base de datos de zona horaria IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, &quot;América/Nueva_York&quot; o &quot;Hora del Este (EE. UU. y Canadá)&quot;). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), likes (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, identificador de Twitter), followers_count (entero), friends_count (entero), statuses_count(entero). |

{style="table-layout:auto"}

## Crear un [!DNL Send Purchase Event] regla {#purchase-rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione **[!UICONTROL Soldar]** extensión y seleccione **[!UICONTROL Enviar evento de compra]** para el tipo de acción.

![Añada una configuración de acción de tipo Acción de compra en bloque de la regla de reenvío de eventos.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, estos también deben ser largos, aleatorios y estar bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugeridos](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Borrar ID de usuario] | Identificador de usuario de Bear. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a usuarios con dimensiones diferentes a las del ID de usuario principal. <br><br> El objeto de alias de usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con diferentes etiquetas, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe completar las [!UICONTROL ID de usuario externo] , el [!UICONTROL Identificador De Usuario De Braze] o el campo [!UICONTROL Alias de usuario] sección.

**[!UICONTROL Datos de compra]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL ID del producto &#x200B;] | Identificador de la compra. (por ejemplo, Nombre de producto o Categoría de producto) | Sí |
| [!UICONTROL Hora de compra] | Fecha-hora como cadena en ISO 8601 o en `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sí |
| [!UICONTROL Moneda &#x200B;] | Moneda como cadena en [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) Formato de código de moneda alfabético. | Sí |
| [!UICONTROL Precio &#x200B;] | Precio. | Sí |
| [!UICONTROL Cantidad &#x200B;] | Si no se proporciona, el valor predeterminado será 1. El valor máximo debe ser inferior a 100. | |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad con una aplicación específica de su grupo de aplicaciones. Designa con qué aplicación del grupo de aplicaciones está interactuando. Obtenga más información acerca de [Tipos de identificadores API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propiedades de compra] | Un objeto JSON que contiene propiedades personalizadas de la compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> El **[!UICONTROL Evento Send de Braze]** la acción solo requiere un **[!UICONTROL Nombre del evento]** y **[!UICONTROL Hora del evento]** no especificado, pero debe incluir la mayor cantidad de información posible en el campo propiedades personalizadas. Para obtener más información sobre [!DNL Braze] objeto de evento, consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos del usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que creen o actualicen un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] | |
| [!UICONTROL Apellidos] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Correo electrónico] | |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otro), &quot;N&quot; (no aplicable), &quot;P&quot; (prefiero no decir). |
| [!UICONTROL Ciudad] | |
| [!UICONTROL País] | País como cadena en [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como cadena en [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Fecha de nacimiento] | Cadena en formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria de [Base de datos de zona horaria IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, &quot;América/Nueva_York&quot; o &quot;Hora del Este (EE. UU. y Canadá)&quot;). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), likes (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, identificador de Twitter), followers_count (entero), friends_count (entero), statuses_count(entero). |

{style="table-layout:auto"}

## Validación de datos dentro de [!DNL Braze] {#validate}

Si la colección de eventos y [!DNL Adobe Experience Platform] integración se han realizado correctamente, verá eventos dentro de la variable [!DNL Braze] consolar cuando [ver perfiles de usuario](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Concretamente, los nuevos datos de evento se envían a [!DNL Braze] se refleja en la variable [!DNL Purchases] de la sección de un usuario en particular [ficha información general](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Braze] uso del reenvío de eventos. Para obtener más información sobre las aplicaciones de flujo descendente para los datos de evento enviados a [!DNL Braze], consulte la [documentación oficial](https://www.braze.com/docs).

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).
