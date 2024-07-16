---
title: Integración de la extensión de API de eventos web de Adobe TikTok
description: Esta API de eventos web de Adobe Experience Platform le permite compartir interacciones de sitios web directamente con TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# Información general sobre la extensión API de eventos web [!DNL TikTok]

La API de eventos [!DNL TikTok] es una interfaz segura [API de Edge Network Server](/help/server-api/overview.md) que le permite compartir información con [!DNL TikTok] directamente sobre las acciones del usuario en sus sitios web. Puede aprovechar las reglas de reenvío de eventos para enviar datos de [!DNL Adobe Experience Platform Edge Network] a [!DNL TikTok] mediante la extensión de API de eventos web [!DNL TikTok].

## [!DNL TikTok] requisitos previos {#prerequisites}

Para configurar la API de eventos web [!DNL TikTok] para que use la API de eventos [!DNL TikTok], debe generar un código de píxeles [!DNL TikTok] y un token de acceso.

Debe tener un [!DNL TikTok] válido para la cuenta empresarial a fin de crear un píxel de [!DNL TikTok] mediante la configuración del socio. Vaya a la página de registro [[!DNL TikTok] para empresas](https://www.tiktok.com/business/en-US/solutions/business-account) para registrarse y crear una cuenta si todavía no la tiene.

Debe iniciar sesión en su cuenta empresarial para configurar [!DNL TikTok] píxeles mediante la configuración de socio. Para realizar esto, siga los pasos a continuación:

1. Vaya a la pestaña **[!UICONTROL Assets]** y seleccione **[!UICONTROL Evento]**.
2. En Eventos web, seleccione **[!UICONTROL Administrar]**.
3. Seleccione **[!UICONTROL Configurar eventos web]**.
4. Seleccione **[!UICONTROL Configuración de socio]** como método de conexión.

Consulte la guía de [Introducción a Pixel](https://ads.tiktok.com/help/article/get-started-pixel) para obtener más información sobre cómo configurar el píxel [!DNL TikTok].

Puede generar un token de acceso una vez que el píxel se haya creado correctamente. Para ello, vaya al píxel y seleccione la pestaña **[!UICONTROL Configuración]**. En la API de eventos, seleccione **[!UICONTROL Generar token de acceso]**.

Consulte la [[!DNL TikTok] guía de introducción](https://business-api.tiktok.com/portal/docs?id=1739584855420929) para obtener más información sobre cómo configurar el código de píxel y el token de acceso.

## Instale y configure la extensión de la API de eventos web [!DNL TikTok] {#install}

Para instalar la extensión, seleccione **[!UICONTROL Extensions]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione la extensión de la API **[!UICONTROL TikTok Web Events]** y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Catálogo de extensiones que muestra la tarjeta de extensión [!DNL TikTok] que resalta la instalación.](../../../images/extensions/server/tiktok/install-extension.png)

En la siguiente pantalla, escriba los siguientes valores de configuración que generó anteriormente desde el Administrador de anuncios de [!DNL TikTok]:

* **[!UICONTROL Código en píxeles]**
* **[!UICONTROL Token de acceso]**

Cuando termine, seleccione **[!UICONTROL Guardar]**.

Pantalla de configuración de ![[!DNL TikTok] para la extensión de API de eventos web [!DNL TikTok].](../../../images/extensions/server/tiktok/configure.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinan cuándo y cómo se enviarán los eventos a [!DNL TikTok].

Cree una nueva [regla](../../../ui/managing-resources/rules.md) en su propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Extensión de la API de eventos web de TikTok]**. Para enviar eventos de Edge Network a [!DNL TikTok], establezca **[!UICONTROL Tipo de acción]** en **[!UICONTROL Enviar evento de API de eventos web de TikTok].**

![Se está seleccionando el tipo de acción [!UICONTROL Enviar evento de API de eventos web de TikTok] para una regla [!DNL TikTok] en la IU de recopilación de datos.](../../../images/extensions/server/tiktok/select-action.png)

Después de la selección, aparecen controles adicionales para configurar aún más el evento, como se describe a continuación. Una vez finalizado, seleccione **[!UICONTROL Conservar cambios]** para guardar la regla.

**[!UICONTROL Eventos web y parámetros]**

Los eventos y parámetros web contienen información general sobre el evento. Los eventos estándar son compatibles con las herramientas de integración de [!DNL TikTok] y se pueden usar para generar informes, optimizar conversiones y crear audiencias.

| Entrada | Descripción |
| --- | --- |
| Nombre del evento | Nombre del evento. Son acciones con nombres predefinidos creados por [!DNL TikTok] y es un campo obligatorio. Consulte la documentación de la [[!DNL TikTok] API de marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) para obtener más información sobre los eventos admitidos. |
| Hora del evento | Fecha-hora como cadena en formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Este campo es obligatorio. |
| ID de evento | ID único generado por los anunciantes para indicar cada evento. Este es un campo opcional y se utiliza para la deduplicación. |

{style="table-layout:auto"}

![La sección [!DNL Web Events and Parameters] muestra datos de ejemplo introducidos en los campos.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Parámetros de contexto de usuario]**

Los parámetros de contexto de usuario contienen información de cliente que se usa para hacer coincidir eventos de visitantes web con [!DNL TikTok] usuarios. La inclusión de varios tipos de datos coincidentes permite aumentar la precisión de los modelos de segmentación y optimización.

| Entrada | Descripción |
| --- | --- |
| Dirección IP | Dirección IP pública del explorador sin hash. Se admite direcciones IPv4 e IPv6. Se reconocen tanto las formas completas como las comprimidas de las direcciones IPv6. |
| Agente de usuario | El agente de usuario sin hash del dispositivo del usuario. |
| Correo electrónico | Dirección de correo electrónico del contacto asociado con el evento de conversión. |
| Teléfono | El número de teléfono debe tener el formato E164 [+][código de país][código de área][local phone number] antes del hash. |
| ID de cookies | Si utiliza el SDK de píxeles guardará automáticamente un identificador único en la cookie `_ttp`, en caso de que las cookies estén habilitadas. El valor `_ttp` se puede extraer y utilizar para este campo. |
| ID externo | Cualquier identificador único, como ID de usuario, ID de cookie externas, etc., debe tener un cifrado hash con SHA256. |
| ID de clic TikTok | El `ttclid` que se agrega a la dirección URL de la página de aterrizaje cada vez que se selecciona un anuncio en [!DNL TikTok]. |
| URL de página | La dirección URL de la página en el momento del evento. |
| URL de referente de página | La URL del referente de la página. |

{style="table-layout:auto"}

![La sección [!DNL User Context Parameters] muestra datos de ejemplo introducidos en los campos.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Parámetros de propiedades]**

Utilice los parámetros de propiedades para configurar propiedades compatibles adicionales.

| Entrada | Descripción |
| --- | --- |
| Precio | Coste de un solo artículo. |
| Cantidad | El número de artículos que se compran en el evento. Debe ser un número positivo mayor que 0. |
| Tipo de contenido | Se debe asignar un valor de `product` o `product_group` a la propiedad del objeto content_type, según cómo configure la fuente de datos al configurar el catálogo de productos. |
| ID de contenido | Un identificador único del elemento de producto. |
| Categoría de contenido | Categoría de la página o producto. |
| Nombre del contenido | Nombre de la página o producto. |
| Moneda | La moneda de los artículos que se compran en el evento. Esto se expresa en ISO-4217. |
| Valor | El precio total del pedido. Este valor es igual al precio * cantidad. |
| Descripción | Una descripción del elemento o la página. |
| Consulta | Cadena de texto que se utilizó para buscar un producto. |
| Estado | El estado de un pedido, artículo o servicio. Por ejemplo, &quot;enviado&quot;. |

{style="table-layout:auto"}

![La sección [!DNL Properties Parameters] muestra datos de ejemplo introducidos en los campos.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Deduplicación de eventos {#deduplication}

Se deberán configurar [!DNL TikTok] píxeles para la anulación de duplicación si utiliza el SDK de [!DNL TikTok] píxeles y la extensión de API de eventos web [!DNL TikTok] para enviar los mismos eventos a [!DNL TikTok].

La deduplicación no es necesaria si se envían distintos tipos de eventos desde el cliente y el servidor sin ninguna superposición. Para asegurarse de que los informes no se vean afectados negativamente, debe asegurarse de deduplicar cualquier evento único compartido por el SDK de píxeles [!DNL TikTok] y la extensión de API de eventos web [!DNL TikTok].

Al enviar eventos compartidos, asegúrese de que cada evento incluya un ID de píxel, un ID de evento y un nombre. Se combinarán los eventos duplicados que llegan en un plazo de cinco minutos uno del otro. Si el campo de datos estaba ausente del primer evento, se combina con el evento posterior. Se eliminará cualquier evento duplicado recibido en un plazo de 48 horas.

Consulte la documentación de [!DNL TikTok] sobre [Anulación de duplicación de eventos](https://ads.tiktok.com/help/article/event-deduplication) para obtener más información sobre este proceso.

## Pasos siguientes

En esta guía se explica cómo enviar datos de eventos del lado del servidor a [!DNL TikTok] mediante la extensión de API de eventos web [!DNL TikTok]. Para obtener más información sobre las capacidades de reenvío de eventos en [!DNL Adobe Experience Platform], consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
