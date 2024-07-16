---
keywords: extensión de reenvío de eventos;braze;extensión de reenvío de eventos braze
title: Extensión de reenvío de eventos de Braze
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de Edge Network a Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# Extensión de reenvío de eventos de [!DNL Braze Track Events API]

[[!DNL Braze]](https://www.braze.com) es una plataforma de participación del cliente que potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real. Con [!DNL Braze], puede hacer lo siguiente:

- Ofrezca datos (como mensajes de marketing) a los usuarios segmentados en función de sus preferencias de idioma, ubicación, preferencias, etc. para aumentar las tasas de conversión y lograr objetivos comerciales clave.
- Envíe a los clientes mensajes personalizados en varios canales, incluidos correo electrónico, notificaciones push y mensajes en la aplicación, en el momento adecuado y en sus idiomas preferidos.
- Oriente a usuarios específicos para campañas promocionales y de marketing a fin de aumentar el número de clientes repetidos.
- Estudiar el comportamiento y los patrones de los usuarios para dirigirse a audiencias específicas con mensajes personalizados, lo que podría ayudar a aumentar los ingresos.

La extensión [!DNL Braze Track Events API] [reenvío de eventos](../../../ui/event-forwarding/overview.md) le permite aprovechar los datos capturados en el Edge Network de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor mediante la API [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track).

Este documento describe los casos de uso de la extensión, cómo instalarla en las bibliotecas de reenvío de eventos y cómo emplear sus capacidades en una [regla](../../../ui/managing-resources/rules.md) de reenvío de eventos.

## Casos de uso

Esta extensión debe usarse si desea usar datos del Edge Network en [!DNL Braze] para aprovechar las capacidades de segmentación y análisis de clientes.

Por ejemplo, considere una organización minorista que tenga presencia multicanal (sitio web y móvil) y que capture entradas transaccionales o conversacionales como datos de evento de su sitio web y plataformas móviles. Con varias reglas [tag](../../../home.md), estos datos se envían al Edge Network en tiempo real. Desde aquí, la extensión de reenvío de eventos [!DNL Braze] envía automáticamente los eventos relevantes a [!DNL Braze] desde el servidor.

Una vez enviados los datos, los equipos de análisis de la organización pueden aprovechar las capacidades de [!DNL Braze's] para procesar los conjuntos de datos y obtener perspectivas comerciales para generar gráficos, tableros u otras visualizaciones para informar a las partes interesadas empresariales. Consulte la página [[!DNL Braze] clientes](https://www.braze.com/customers) para obtener más información sobre los distintos casos de uso de la plataforma.

## [!DNL Braze] requisitos previos y protecciones {#prerequisites}

Debe tener una cuenta de [!DNL Braze] para poder usar sus tecnologías. Si no tiene una cuenta, vaya a la [página de introducción](https://www.braze.com/get-started/) en [!DNL Braze] para conectarse a [!DNL Braze Sales] e iniciar el proceso de creación de cuentas.

### Protecciones de API

La extensión usa dos de las API de [!DNL Braze] y sus límites se describen a continuación:

| API | Límites de velocidad |
| --- | --- |
| [!DNL User Track] | 50.000 peticiones por minuto. <br>Consulte la [[!DNL User Track] documentación de la API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obtener detalles. |
| [!DNL User Identify] | 20.000 peticiones por minuto. <br>Consulte la [[!DNL User Identify] documentación de la API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obtener detalles. |

>[!NOTE]
>
> Consulte la guía de [[!DNL Braze] límites de API](https://www.braze.com/docs/api/api_limits/) para obtener más información sobre los límites que imponen.

### Puntos de datos facturables

Si envía atributos personalizados adicionales a [!DNL Braze], podría aumentar su consumo de puntos de datos [!DNL Braze]. Consulte con su administrador de cuentas de [!DNL Braze] antes de enviar atributos personalizados adicionales. Consulte la documentación de [!DNL Braze] sobre [puntos de datos facturables](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable) para obtener más información.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar el Edge Network a [!DNL Braze], se requieren las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| Instancia de [!DNL Braze] | El extremo REST asociado con la cuenta [!DNL Braze]. Consulte la documentación de [!DNL Braze] en [instancias](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) para obtener instrucciones. | `https://rest.iad-03.braze.com` |
| Clave de API | La clave de API [!DNL Braze] asociada con la cuenta [!DNL Braze]. <br/>Consulte la documentación de [!DNL Braze] sobre la clave de API de [REST](https://www.braze.com/docs/api/basics/#rest-api-key) para obtener instrucciones. | `YOUR-BRAZE-REST-API-KEY` |

### Crear un secreto

Cree un nuevo [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y establezca el valor en su [[!DNL Braze] clave de API](#configuration-details). Se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

## Instalar y configurar la extensión [!DNL Braze] {#install}

Para instalar la extensión, [cree una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Instalar]** en la tarjeta de la extensión [!DNL Braze].

![Instalar la extensión [!DNL Braze].](../../../images/extensions/server/braze/install-extension.png)

En la siguiente pantalla, escriba los siguientes [valores de configuración](#configuration-details) que recopiló anteriormente de [!DNL Braze]:

- **[!UICONTROL URL de extremo REST de Braze]**: puede escribir el valor de su URL de extremo REST [!DNL Braze] como texto sin formato en la entrada proporcionada.
- **[!UICONTROL Clave API]**: Seleccione el [elemento de datos secreto](#create-a-secret) que creó anteriormente, que contiene su clave API [!DNL Braze].

Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![Página de configuración de la extensión [!DNL Braze].](../../../images/extensions/server/braze/configure-extension.png)

## Crear una regla [!DNL Send Event] {#tracking-rule}

Después de instalar la extensión, cree una nueva regla de reenvío de eventos [rule](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione la extensión **[!UICONTROL Braze]** y, a continuación, seleccione **[!UICONTROL Enviar evento]** para el tipo de acción.

![Agregar una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, estos también deben ser largos, aleatorios y estar bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Identificador de usuario de Braze] | Identificador de usuario de Bear. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a usuarios con dimensiones diferentes a las del ID de usuario principal. <br><br>: el objeto de alias de usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con diferentes etiquetas, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe rellenar el campo [!UICONTROL ID de usuario externo], el campo [!UICONTROL Identificador de usuario de Bear] o la sección [!UICONTROL Alias de usuario].

**[!UICONTROL Datos de evento]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Nombre del evento] | Nombre del evento. | Sí |
| [!UICONTROL Hora del evento] | Fecha-hora como cadena en formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sí |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad con una aplicación específica de su grupo de aplicaciones. Designa con qué aplicación del grupo de aplicaciones está interactuando. Más información sobre los [tipos de identificadores de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propiedades de evento] | Objeto JSON que contiene propiedades personalizadas del evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La acción **[!UICONTROL Braze Send Event]** solo requiere que se especifiquen **[!UICONTROL Event Name]** y **[!UICONTROL Event Time]**, pero debe incluir la mayor información posible en el campo de propiedades personalizadas. Para obtener más información sobre el objeto de evento [!DNL Braze], consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que creen o actualicen un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] | |
| [!UICONTROL Apellidos] | |
| [!UICONTROL Teléfono] | |
| [!UICONTROL Correo electrónico] | |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otro), &quot;N&quot; (no aplicable), &quot;P&quot; (prefiero no decir). |
| [!UICONTROL Ciudad] | |
| [!UICONTROL País] | País como cadena en formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Idioma] | Idioma como cadena en formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Fecha de nacimiento] | Cadena en formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria de [base de datos de zona horaria de IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, &#39;América/Nueva_York&#39; o &#39;Hora del Este (EE.UU. y Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), likes (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, identificador de Twitter), followers_count (entero), friends_count (entero), statuses_count(entero). |

{style="table-layout:auto"}

## Crear una regla [!DNL Send Purchase Event] {#purchase-rule}

Después de instalar la extensión, cree una nueva regla de reenvío de eventos [rule](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione la extensión **[!UICONTROL Braze]** y, a continuación, seleccione **[!UICONTROL Enviar evento de compra]** para el tipo de acción.

![Agregar una configuración de acción de reenvío de eventos de tipo Acción de compra en bloque.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, estos también deben ser largos, aleatorios y estar bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Identificador de usuario de Braze] | Identificador de usuario de Bear. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a usuarios con dimensiones diferentes a las del ID de usuario principal. <br><br>: el objeto de alias de usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con diferentes etiquetas, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe completar el campo [!UICONTROL Id. de usuario externo], el campo [!UICONTROL Identificador de usuario independiente] o la sección [!UICONTROL Alias de usuario].

**[!UICONTROL Datos de compra]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL ID de producto] | Identificador de la compra. (por ejemplo, Nombre de producto o Categoría de producto) | Sí |
| [!UICONTROL Hora de compra] | Fecha-hora como cadena en formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sí |
| [!UICONTROL Moneda] | Moneda como cadena en formato de código alfabético de moneda [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217). | Sí |
| [!UICONTROL Precio] | Precio. | Sí |
| [!UICONTROL Cantidad] | Si no se proporciona, el valor predeterminado será 1. El valor máximo debe ser inferior a 100. | |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad con una aplicación específica de su grupo de aplicaciones. Designa con qué aplicación del grupo de aplicaciones está interactuando. Más información sobre los [tipos de identificadores de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propiedades de compra] | Un objeto JSON que contiene propiedades personalizadas de la compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La acción **[!UICONTROL Braze Send Event]** solo requiere que se especifiquen **[!UICONTROL Event Name]** y **[!UICONTROL Event Time]**, pero debe incluir la mayor información posible en el campo de propiedades personalizadas. Para obtener más información sobre el objeto de evento [!DNL Braze], consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que creen o actualicen un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] | |
| [!UICONTROL Apellidos] | |
| [!UICONTROL Teléfono] | |
| [!UICONTROL Correo electrónico] | |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otro), &quot;N&quot; (no aplicable), &quot;P&quot; (prefiero no decir). |
| [!UICONTROL Ciudad] | |
| [!UICONTROL País] | País como cadena en formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Idioma] | Idioma como cadena en formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Fecha de nacimiento] | Cadena en formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria de [base de datos de zona horaria de IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, &#39;América/Nueva_York&#39; o &#39;Hora del Este (EE.UU. y Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), likes (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, identificador de Twitter), followers_count (entero), friends_count (entero), statuses_count(entero). |

{style="table-layout:auto"}

## Validar datos dentro de [!DNL Braze] {#validate}

Si la recopilación de eventos y la integración de [!DNL Adobe Experience Platform] se realizaron correctamente, verá eventos dentro de la consola [!DNL Braze] al [ver perfiles de usuario](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Específicamente, los nuevos datos de evento enviados a [!DNL Braze] se reflejan en la sección [!DNL Purchases] de la [ficha de información general](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab) de un usuario en particular.

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Braze] mediante el reenvío de eventos. Para obtener más información sobre las aplicaciones de flujo descendente para los datos de evento enviados a [!DNL Braze], consulte la [documentación oficial](https://www.braze.com/docs).

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
