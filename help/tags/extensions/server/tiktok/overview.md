---
title: Integración de la extensión de API de eventos web de Adobe TikTok
description: Esta API de eventos web de Adobe Experience Platform le permite compartir interacciones de sitios web directamente con TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 3%

---

# [!DNL TikTok] información general sobre la extensión API web events

El [!DNL TikTok] La API de eventos es un [API del servidor de red perimetral](/help/server-api/overview.md) que le permite compartir información con [!DNL TikTok] directamente sobre las acciones de los usuarios en sus sitios web. Puede aprovechar las reglas del reenvío de eventos para enviar datos desde [!DNL Adobe Experience Platform Edge Network] hasta [!DNL TikTok] mediante el uso de [!DNL TikTok] Extensión de la API de eventos web.

## [!DNL TikTok] requisitos previos {#prerequisites}

Para configurar la variable [!DNL TikTok] API de eventos web para utilizar [!DNL TikTok] API de eventos, debe generar un [!DNL TikTok] código de píxel y token de acceso.

Debe tener un válido [!DNL TikTok] para una cuenta empresarial con el fin de crear una [!DNL TikTok] píxel con la configuración de socio. Vaya a la [[!DNL TikTok] para la página de registro empresarial](https://www.tiktok.com/business/en-US/solutions/business-account) para registrarse y crear una cuenta si aún no la tiene.

Debe haber iniciado sesión en su cuenta empresarial para configurar [!DNL TikTok] Píxel con configuración de socio. Para realizar esto, siga los pasos a continuación:

1. Vaya a **[!UICONTROL Assets]** y seleccione **[!UICONTROL Evento]**.
2. En Eventos web, seleccione **[!UICONTROL Administrar]**.
3. Seleccionar **[!UICONTROL Configuración de eventos web]**.
4. Seleccionar **[!UICONTROL Configuración de socio]** como método de conexión.

Consulte la [Introducción a Pixel](https://ads.tiktok.com/help/article/get-started-pixel) para obtener más información sobre cómo configurar el [!DNL TikTok] píxel.

Puede generar un token de acceso una vez que el píxel se haya creado correctamente. Para ello, vaya al píxel y seleccione la opción **[!UICONTROL Configuración]** pestaña. En la API de eventos, seleccione **[!UICONTROL Generar token de acceso]**.

Consulte la [[!DNL TikTok] guía de introducción](https://business-api.tiktok.com/portal/docs?id=1739584855420929) para obtener más información sobre cómo configurar el código de píxel y el token de acceso.

## Instalación y configuración de [!DNL TikTok] extensión de API de eventos web {#install}

Para instalar la extensión, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , seleccione la pestaña **[!UICONTROL Extensión de API de eventos web de TikTok]** y luego seleccione **[!UICONTROL Instalar]**.

![El catálogo de extensiones que muestra [!DNL TikTok] instalación de resalte de tarjeta de extensión.](../../../images/extensions/server/tiktok/install-extension.png)

En la pantalla siguiente, introduzca los siguientes valores de configuración que generó anteriormente desde [!DNL TikTok] Administrador de anuncios:

* **[!UICONTROL Código de píxel]**
* **[!UICONTROL Token de acceso]**

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![[!DNL TikTok] pantalla de configuración para [!DNL TikTok] extensión de API de eventos web.](../../../images/extensions/server/tiktok/configure.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinen cuándo y cómo se enviarán los eventos a [!DNL TikTok].

Crear un nuevo [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL Extensión de API de eventos web de TikTok]**. Para enviar eventos de Edge Network a [!DNL TikTok], configure el **[!UICONTROL Tipo de acción]** hasta **[!UICONTROL Enviar evento de API de eventos web de TikTok].**

![El [!UICONTROL Enviar evento de API de eventos web de TikTok] tipo de acción que se está seleccionando para una [!DNL TikTok] en la IU de recopilación de datos.](../../../images/extensions/server/tiktok/select-action.png)

Después de la selección, aparecen controles adicionales para configurar aún más el evento, como se describe a continuación. Una vez finalizado, seleccione **[!UICONTROL Conservar cambios]** para guardar la regla.

**[!UICONTROL Eventos y parámetros web]**

Los eventos y parámetros web contienen información general sobre el evento. Los eventos estándar son compatibles en [!DNL TikTok] Las herramientas de integración de y se pueden utilizar para la creación de informes de, la optimización para conversiones y la creación de audiencias.

| Entrada | Descripción |
| --- | --- |
| Nombre del evento | Nombre del evento. Son acciones con nombres predefinidos creados por [!DNL TikTok] y es un campo obligatorio. Consulte la [[!DNL TikTok] API de marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) para obtener más información sobre los eventos admitidos. |
| Hora del evento | Fecha-hora como cadena en ISO 8601 o en `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. Este campo es obligatorio. |
| ID de evento | ID único generado por los anunciantes para indicar cada evento. Este es un campo opcional y se utiliza para la deduplicación. |

{style="table-layout:auto"}

![El [!DNL Web Events and Parameters] sección que muestra la entrada de datos de ejemplo en los campos.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Parámetros de contexto de usuario]**

Los parámetros de contexto del usuario contienen información del cliente que se utiliza para hacer coincidir los eventos de visitantes web con [!DNL TikTok] usuarios. La inclusión de varios tipos de datos coincidentes permite aumentar la precisión de los modelos de segmentación y optimización.

| Entrada | Descripción |
| --- | --- |
| Dirección IP | Dirección IP pública del explorador sin hash. Se admite direcciones IPv4 e IPv6. Se reconocen tanto las formas completas como las comprimidas de las direcciones IPv6. |
| Agente de usuario | El agente de usuario sin hash del dispositivo del usuario. |
| Correo electrónico | Dirección de correo electrónico del contacto asociado con el evento de conversión. |
| Teléfono | El número de teléfono debe estar en formato E164 [+][código de país][código de área][local phone number] antes del hash. |
| ID de cookie | Si utiliza el SDK de píxeles, guardará automáticamente un identificador único en la `_ttp` si las cookies están habilitadas. El `_ttp` Este valor se puede extraer y utilizar para este campo. |
| ID externo | Cualquier identificador único, como ID de usuario, ID de cookie externas, etc., debe tener un cifrado hash con SHA256. |
| ID de clic TikTok | El `ttclid` que se añade a la dirección URL de la página de aterrizaje cada vez que se selecciona un anuncio en [!DNL TikTok]. |
| URL de página | La dirección URL de la página en el momento del evento. |
| URL de referente de página | La URL del referente de la página. |

{style="table-layout:auto"}

![El [!DNL User Context Parameters] sección que muestra la entrada de datos de ejemplo en los campos.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Parámetros de propiedades]**

Utilice los parámetros de propiedades para configurar propiedades compatibles adicionales.

| Entrada | Descripción |
| --- | --- |
| Precio | Coste de un solo artículo. |
| Cantidad | El número de artículos que se compran en el evento. Debe ser un número positivo mayor que 0. |
| Tipo de contenido | Un valor de `product` o `product_group` debe asignarse a la propiedad de objeto content_type, según cómo configure la fuente de datos al configurar el catálogo de productos. |
| ID de contenido | Un identificador único del elemento de producto. |
| Categoría de contenido | Categoría de la página o producto. |
| Nombre del contenido | Nombre de la página o producto. |
| Moneda | La moneda de los artículos que se compran en el evento. Esto se expresa en ISO-4217. |
| Valor | El precio total del pedido. Este valor es igual al precio * cantidad. |
| Descripción | Una descripción del elemento o la página. |
| Consulta | Cadena de texto que se utilizó para buscar un producto. |
| Estado | El estado de un pedido, artículo o servicio. Por ejemplo, &quot;enviado&quot;. |

{style="table-layout:auto"}

![El [!DNL Properties Parameters] sección que muestra la entrada de datos de ejemplo en los campos.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Deduplicación de eventos {#deduplication}

[!DNL TikTok] píxel deberá configurarse para la anulación de duplicación si utiliza ambos [!DNL TikTok] el SDK de píxeles y [!DNL TikTok] extensión de API de eventos web para enviar los mismos eventos a [!DNL TikTok].

La deduplicación no es necesaria si se envían distintos tipos de eventos desde el cliente y el servidor sin ninguna superposición. Para garantizar que los informes no se vean afectados negativamente, debe asegurarse de que cualquier evento individual que comparta la variable [!DNL TikTok] el SDK de píxeles y [!DNL TikTok] La extensión de la API de eventos web está deduplicada.

Al enviar eventos compartidos, asegúrese de que cada evento incluya un ID de píxel, un ID de evento y un nombre. Se combinarán los eventos duplicados que llegan en un plazo de cinco minutos uno del otro. Si el campo de datos estaba ausente del primer evento, se combina con el evento posterior. Se eliminará cualquier evento duplicado recibido en un plazo de 48 horas.

Consulte la [!DNL TikTok] documentación sobre [Deduplicación de eventos](https://ads.tiktok.com/help/article/event-deduplication) para obtener más información sobre este proceso.

## Pasos siguientes

En esta guía se explica cómo enviar datos de eventos del lado del servidor a [!DNL TikTok] uso del [!DNL TikTok] extensión de API de eventos web. Para obtener más información sobre las funcionalidades de reenvío de eventos en [!DNL Adobe Experience Platform], consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).
