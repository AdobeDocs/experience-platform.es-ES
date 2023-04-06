---
keywords: extensión de reenvío de eventos;brase;extensión de reenvío de eventos de brasil
title: Extensión de reenvío de eventos de Braze
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de Adobe Experience Edge Network a Braze.
source-git-commit: 88e589eb17c249a8bdc82fe7a041a5581a60c7e6
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 4%

---


# [!DNL Braze Track Events API] extensión de reenvío de eventos

[[!DNL Braze]](https://www.braze.com) es una plataforma de participación del cliente que potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real. Uso [!DNL Braze], puede hacer lo siguiente:

- Entregue datos (como mensajes de marketing) a los usuarios objetivo en función de sus preferencias de idioma, preferencias de ubicación, etc., para aumentar las tasas de conversión y lograr los objetivos clave del negocio.
- Envíe mensajes personalizados a los clientes a través de varios canales, incluidos correos electrónicos, notificaciones push y mensajes en la aplicación, en el momento adecuado y en los idiomas que prefieran.
- Diríjase a usuarios específicos para campañas de marketing y promocionales a fin de aumentar el número de clientes que repiten.
- Estudie el comportamiento y los patrones del usuario para dirigirse a audiencias específicas con mensajes personalizados, lo que podría ayudar a aumentar los ingresos.

La variable [!DNL Braze Track Events API] [reenvío de eventos](../../../ui/event-forwarding/overview.md) permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor utilizando la variable [[!DNL Braze User Identify]](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify) y [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Este documento cubre los casos de uso de la extensión, cómo instalarla en las bibliotecas de reenvío de eventos y cómo utilizar sus capacidades en un reenvío de eventos [regla](../../../ui/managing-resources/rules.md).

## Casos de uso

Esta extensión debe usarse si desea utilizar datos de la red perimetral en [!DNL Braze] para aprovechar las capacidades de orientación y análisis de clientes.

Por ejemplo, considere una organización de venta minorista que tiene una presencia multicanal (sitio web y móvil) y que captura las entradas transaccionales o conversacionales como datos de eventos de su sitio web y plataformas móviles. Uso de varias [etiqueta](../../../home.md) , estos datos se envían a la red perimetral en tiempo real. Desde aquí, la variable [!DNL Braze] la extensión de reenvío de eventos envía automáticamente los eventos relevantes a [!DNL Braze] del lado del servidor.

Una vez enviados los datos, los equipos de análisis de la organización pueden aprovechar [!DNL Braze's] funciones para procesar los conjuntos de datos y derivar perspectivas empresariales para generar gráficos, tableros u otras visualizaciones que informen a las partes interesadas del negocio. Consulte la [[!DNL Braze] clientes](https://www.braze.com/customers) para obtener más información sobre los distintos casos de uso de la plataforma.

## [!DNL Braze] requisitos previos y protecciones {#prerequisites}

Debe tener un [!DNL Braze] para utilizar sus tecnologías. Si no tiene una cuenta, vaya a la [Página Introducción](https://www.braze.com/get-started/) en [!DNL Braze] para conectarse a [!DNL Braze Sales] e inicie el proceso de creación de cuentas.

### Protecciones de API

La extensión utiliza dos de [!DNL Braze]Las API de y sus límites se describen a continuación:

| API | Límites de tasa |
| --- | --- |
| [!DNL User Track] | 50.000 solicitudes por minuto. <br>Consulte la [[!DNL User Track] Documentación de API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obtener más información. |
| [!DNL User Identify] | 20.000 solicitudes por minuto. <br>Consulte la [[!DNL User Identify] Documentación de API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obtener más información. |

>[!NOTE]
>
> Consulte la guía de [[!DNL Braze] Límites de API](https://www.braze.com/docs/api/api_limits/) para obtener más información sobre los límites que imponen.

### Puntos de datos facturables

Envío de atributos personalizados adicionales a [!DNL Braze] puede aumentar su [!DNL Braze] consumo de puntos de datos. Consulte con su [!DNL Braze] administrador de cuentas antes de enviar atributos personalizados adicionales. Consulte la [!DNL Braze] documentación sobre [puntos de datos facturables](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) para obtener más información.

### Recopilar los detalles de configuración necesarios {#configuration-details}

Para conectar la red perimetral a [!DNL Braze], se requieren las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| [!DNL Braze] Instancia | El extremo REST asociado con la variable [!DNL Braze] cuenta. Consulte la [!DNL Braze] documentación sobre [instancias](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) para obtener más información. | `https://rest.iad-03.braze.com` |
| Clave de API | La variable [!DNL Braze] Clave de API asociada a la variable [!DNL Braze] cuenta. <br/>Consulte la [!DNL Braze] documentación sobre [Clave de API de REST](https://www.braze.com/docs/api/basics/#rest-api-key) para obtener más información. | `YOUR-BRAZE-REST-API-KEY` |

### Crear un secreto

Cree una nueva [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y establezca el valor en su [[!DNL Braze] Clave de API](#configuration-details). Se utilizará para autenticar la conexión con su cuenta mientras se mantiene el valor seguro.

## Instale y configure el [!DNL Braze] Extensión {#install}

Para instalar la extensión, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editarla en su lugar.

Select **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , seleccione **[!UICONTROL Instalar]** en la tarjeta para la variable [!DNL Braze] extensión.

![Instale el [!DNL Braze] extensión.](../../../images/extensions/server/braze/install-extension.png)

En la siguiente pantalla, introduzca lo siguiente [valores de configuración](#configuration-details) que ha recopilado anteriormente de [!DNL Braze]:

- **[!UICONTROL URL del extremo del resto de Brazo]**: Puede introducir el valor de su [!DNL Braze] reposar URL de extremo como texto sin formato en la entrada proporcionada.
- **[!UICONTROL Clave de API]**: Seleccione el [elemento de datos secreto](#create-a-secret) que creó anteriormente, que contiene su [!DNL Braze] Clave de API.

Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![La variable [!DNL Braze] página de configuración de la extensión.](../../../images/extensions/server/braze/configure-extension.png)

## Cree un [!DNL Send Event] regla {#tracking-rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones para la regla, seleccione la **[!UICONTROL Brazo]** extensión y, a continuación, seleccione **[!UICONTROL Enviar evento]** para el tipo de acción.

![Agregue una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, también deben ser largos, aleatorios y bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuario de Brazo] | Identificador de usuario de Braze. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a los usuarios en diferentes dimensiones que su ID de usuario principal. <br><br> El objeto alias del usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con etiquetas diferentes, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe rellenar cualquiera de las opciones siguientes: [!UICONTROL ID de usuario externo] o [!UICONTROL Identificador de usuario de Braze] o [!UICONTROL Alias de usuario] para obtener más información.

**[!UICONTROL Datos de Evento]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Nombre del evento &#x200B;] | Nombre del evento. | Sí |
| [!UICONTROL Hora del evento ] | Fecha-hora como cadena en ISO 8601 o en `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sí |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad a una aplicación específica de su grupo de aplicaciones. Designa la aplicación dentro del grupo de aplicaciones con la que está interactuando. Obtenga más información sobre [Tipos de identificadores de API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; de propiedades de evento] | Un objeto JSON que contiene propiedades personalizadas del evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La variable **[!UICONTROL Evento de envío en brasil]** la acción solo requiere un **[!UICONTROL Nombre del evento]** y **[!UICONTROL Hora del evento]** para que se especifique, pero debe incluir la mayor cantidad de información posible en el campo de propiedades personalizadas. Para obtener más información sobre [!DNL Braze] objeto de evento, consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que vayan a crear o actualizar un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] |  |
| [!UICONTROL Apellidos] |  |
| [!UICONTROL Phone] |  |
| [!UICONTROL Correo electrónico] |  |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otros), &quot;N&quot; (no aplicable), &quot;P&quot; (preferir no decir). |
| [!UICONTROL Ciudad] |  |
| [!UICONTROL País] | País como cadena en [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como cadena en [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Fecha de nacimiento] | Cadena con el formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria desde [Base de datos de zona horaria IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, ’América/Nueva York’ o ’Hora del Este (EE.UU. y Canadá)’). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), me gusta (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, control de Twitter), seguidores_count (entero), friends_count (entero), statuses_count(integer). |

{style="table-layout:auto"}

## Cree un [!DNL Send Purchase Event] regla {#purchase-rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones para la regla, seleccione la **[!UICONTROL Brazo]** extensión y, a continuación, seleccione **[!UICONTROL Enviar evento de compra]** para el tipo de acción.

![Agregue una configuración de acción de tipo de acción de compra de Braze reenvío de eventos de regla.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificación de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL ID de usuario externo] | UUID o GUID largos, aleatorios y bien distribuidos. Si elige un método diferente para asignar un nombre a los ID de usuario, también deben ser largos, aleatorios y bien distribuidos. Más información sobre [convención de nomenclatura de ID de usuario sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuario de Brazo] | Identificador de usuario de Braze. |
| [!UICONTROL Alias de usuario] | Un alias sirve como identificador de usuario único alternativo. Utilice alias para identificar a los usuarios en diferentes dimensiones que su ID de usuario principal. <br><br> El objeto alias del usuario consta de dos partes: un alias_name para el propio identificador y un alias_label que indica el tipo de alias. Los usuarios pueden tener varios alias con etiquetas diferentes, pero solo un alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular el evento a un usuario, debe completar la [!UICONTROL ID de usuario externo] , el campo [!UICONTROL Identificador de usuario de Braze] o [!UICONTROL Alias de usuario] para obtener más información.

**[!UICONTROL Datos de compra]**

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL ID del producto &#x200B;] | Identificador de la compra. (p. ej., Nombre del producto o Categoría del producto) | Sí |
| [!UICONTROL Hora de compra ] | Fecha-hora como cadena en ISO 8601 o en `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sí |
| [!UICONTROL Moneda &#x200B;] | Moneda como cadena en [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) Formato Código de moneda alfabético. | Sí |
| [!UICONTROL Precio &#x200B;] | Precio. | Sí |
| [!UICONTROL Cantidad &#x200B;] | Si no se proporciona, el valor predeterminado será 1. El valor máximo debe ser inferior a 100. |  |
| [!UICONTROL Identificador de aplicación] | El identificador de la aplicación o <strong>app_id</strong> es un parámetro que asocia la actividad a una aplicación específica de su grupo de aplicaciones. Designa la aplicación dentro del grupo de aplicaciones con la que está interactuando. Obtenga más información sobre [Tipos de identificadores de API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; Propiedades de compra] | Un objeto JSON que contiene propiedades personalizadas de la compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La variable **[!UICONTROL Evento de envío en brasil]** la acción solo requiere un **[!UICONTROL Nombre del evento]** y **[!UICONTROL Hora del evento]** para que se especifique, pero debe incluir la mayor cantidad de información posible en el campo de propiedades personalizadas. Para obtener más información sobre [!DNL Braze] objeto de evento, consulte la [documentación oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuario]**

Los atributos de usuario pueden ser un objeto JSON que contenga campos que vayan a crear o actualizar un atributo con el nombre y el valor proporcionados en el perfil de usuario especificado. Se admiten las siguientes propiedades:

| Atributo de usuario | Descripción |
| --- | --- |
| [!UICONTROL Nombre] |  |
| [!UICONTROL Apellidos] |  |
| [!UICONTROL Phone] |  |
| [!UICONTROL Correo electrónico] |  |
| [!UICONTROL Sexo] | Una de las siguientes cadenas: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (otros), &quot;N&quot; (no aplicable), &quot;P&quot; (preferir no decir). |
| [!UICONTROL Ciudad] |  |
| [!UICONTROL País] | País como cadena en [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como cadena en [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Fecha de nacimiento] | Cadena con el formato &quot;AAAA-MM-DD&quot; (por ejemplo, 1980-12-21). |
| [!UICONTROL Zona horaria] | Nombre de zona horaria desde [Base de datos de zona horaria IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por ejemplo, ’América/Nueva York’ o ’Hora del Este (EE.UU. y Canadá)’). |
| [!UICONTROL Facebook] | Hash que contiene cualquiera de id (cadena), me gusta (matriz de cadenas), num_friends (entero). |
| [!UICONTROL Twitter] | Hash que contiene cualquiera de id (entero), screen_name (cadena, control de Twitter), seguidores_count (entero), friends_count (entero), statuses_count(integer). |

{style="table-layout:auto"}

## Validar datos en [!DNL Braze] {#validate}

Si la recopilación de eventos y [!DNL Adobe Experience Platform] si la integración se ha realizado correctamente, verá eventos dentro de [!DNL Braze] consola cuando [visualización de perfiles de usuario](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Específicamente, los nuevos datos de evento enviados a [!DNL Braze] se refleja en la variable [!DNL Purchases] de la sección de un usuario en particular [ficha Información general](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Pasos siguientes

Esta guía explica cómo enviar eventos de conversión a [!DNL Braze] uso del reenvío de eventos. Para obtener más información sobre las aplicaciones descendentes para los datos de evento enviados a [!DNL Braze], consulte [documentación oficial](https://www.braze.com/docs).

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [información general sobre el reenvío de eventos](../../../ui/event-forwarding/overview.md).
