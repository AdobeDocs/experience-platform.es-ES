---
keywords: extensión de reenvío de eventos;pinterest;extensión de reenvío de eventos de pinterest
title: Extensión de reenvío de eventos de pinterest
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite introducir eventos en Pinterest para los requisitos de su empresa.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 5%

---

# Extensión de reenvío de eventos de [!DNL Pinterest]

[!DNL Pinterest] es un motor de descubrimiento visual para encontrar ideas como recetas, decoración del hogar, inspiración de estilo, y más. Hay miles de millones de pines en [!DNL Pinterest], que también se puede compartir con otros en [!DNL Pinterest]. Puede recopilar los eventos de interacción del usuario y aprovechar [!DNL Pinterest Analytics] para comprender el comportamiento del usuario y ejecutar anuncios dirigidos.

El [[!DNL Pinterest] Conversiones](https://developers.pinterest.com/docs/conversions/conversion-management/) API [reenvío de eventos](../../../ui/event-forwarding/overview.md) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest]. Este documento describe los casos de uso de la extensión, cómo instalarla y cómo integrar sus funcionalidades en el reenvío de eventos [reglas](../../../ui/managing-resources/rules.md).

Los tokens de acceso a conversiones son el método de autenticación utilizado por [!DNL Pinterest] al interactuar con [!DNL Pinterest] API.

## Casos de uso

Debe usar esta extensión si desea usar datos de la red perimetral en [!DNL Pinterest] para aprovechar las ventajas de las funcionalidades de customer analytics.

Por ejemplo, considere un equipo de marketing en una organización. El equipo de captura los datos del evento de interacción del usuario de su sitio web y los carga en [!DNL Pinterest] uso de esta extensión de reenvío de eventos.

Los equipos de marketing y análisis pueden aprovechar [!DNL Pinterest] Las capacidades de Analytics permiten comprender las interacciones y el comportamiento de los usuarios clave, lo que le permite comprender mejor a los usuarios y dirigirlos a campañas de publicidad segmentadas.

Para obtener más información sobre casos de uso específicos de [!DNL Pinterest], consulte la [[!DNL Pinterest] casos de uso](https://business.pinterest.com/en/success-stories) documentación.

## [!DNL Pinterest] requisitos previos {#prerequisites}

Debe tener un válido [!DNL Pinterest] [cuenta empresarial](https://help.pinterest.com/en/business/article/get-a-business-account) para utilizar esta extensión. Vaya a la [[!DNL Pinterest] página de registro](https://www.pinterest.com/business/create/) para registrarse y crear una cuenta si aún no la tiene.

También necesitará un [!DNL Pinterest] cuenta de desarrollador de, que deberá asociarse con su [!DNL Pinterest] cuenta empresarial. Para asociar su cuenta de desarrollador de con su cuenta empresarial, consulte la [[!DNL Pinterest ] cuenta de desarrollador](https://developers.pinterest.com/account-setup/).

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar al Experience Platform a [!DNL Pinterest], se requieren las siguientes entradas:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de cuenta de anuncios | Su [!DNL Pinterest] ID de cuenta de anuncios. Consulte la [[!DNL Pinterest] documentación](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) para obtener orientación. | 123456789012 |
| Token de acceso de conversión | Su [!DNL Pinterest] Token de acceso de conversión. Consulte la [[!DNL Pinterest] API de conversiones](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento de orientación. <br> **Solo se le pedirá que realice esta acción una vez, ya que este token no caduca.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Instalación y configuración de [!DNL Pinterest] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

En el panel de navegación izquierdo, seleccione **[!UICONTROL Extensiones]**. Seleccionar **[!UICONTROL Instalar]** en la tarjeta de [!DNL Pinterest] extensión en la **[!UICONTROL Catálogo]** pestaña.

![Catálogo que muestra el [!DNL Pinterest] extensión con [!UICONTROL Instalar] resaltado.](../../../images/extensions/server/pinterest/install.png)

### Configurar la extensión de [!DNL Pinterest]

>[!IMPORTANT]
>
>Según sus necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de empezar para determinar qué entidades debe configurar para su caso de uso.

En el panel de navegación izquierdo, seleccione **[!UICONTROL Extensiones]**. Seleccionar **[!UICONTROL Configurar]** en la tarjeta de [!DNL Pinterest] extensión en la [!UICONTROL Instalado]Pestaña **.

![[!DNL Pinterest] extensión que se muestra en la [!UICONTROL Instalar] pestaña con [!UICONTROL Configurar] resaltado.](../../../images/extensions/server/pinterest/configure.png)

En la pantalla siguiente, introduzca la variable [!UICONTROL ID de cuenta de anuncios] y [!UICONTROL Token de acceso de conversión] que recopiló anteriormente en el [detalles de configuración](#configuration-details) sección. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![El [!DNL Pinterest] [!UICONTROL Configurar] pantalla que resalta el [!UICONTROL ID de cuenta de anuncios] y [!UICONTROL Token de acceso de conversión] campos de entrada.](../../../images/extensions/server/pinterest/input.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinen cuándo y cómo se enviarán los eventos a [!DNL Pinterest].

Crear un nuevo [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL Pinterest]**. Para enviar eventos de Edge Network a [!DNL Pinterest], configure el **[!UICONTROL Tipo de acción]** hasta **[!UICONTROL Enviar evento].**

![El [!DNL Pinterest] [!UICONTROL Enviar evento] creación de reglas.](../../../images/extensions/server/pinterest/rule.png)

Después de la selección, aparecen controles adicionales para configurar aún más el evento. Debe asignar el [!DNL Pinterest] propiedades de evento a los elementos de datos creados anteriormente.

### [!UICONTROL Datos de Evento]

Se requerirán los siguientes datos de evento para crear la nueva regla:

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- | 
| [!UICONTROL Nombre del evento] | Tipo del evento de usuario. Sin embargo, este puede ser cualquier tipo de evento para aprovechar [!DNL Pinterest Analytics] se recomienda utilizar [[!DNL Pinterest] códigos de evento](https://help.pinterest.com/en/business/article/add-event-codes) | * cierre de compra <br> * add_to_cart <br> * page_visit <br> * suscripción <br> * [Evento definido por el usuario] |
| [!UICONTROL Origen de acción] | Origen que indica dónde se produjo el evento de conversión. | * app_android <br> * app_ios <br> * web <br> * sin conexión |
| [!UICONTROL Hora del evento] | Hace referencia a la hora del evento. El formato de hora predeterminado utilizado es UNIX, con el formato `<seconds>.<miliseconds>` según la zona horaria local. Para obtener más información, consulte la [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 segundos y 500 milisegundos después de epoch o el lunes, 1 de junio de 2015, a las 7:50:17:00 GMT. |
| [!UICONTROL ID de evento] | Una cadena de ID única que identifica este evento y que puede utilizarse para la desduplicación entre eventos introducidos mediante la API de conversión y el seguimiento de Pinterest. Sin esto, es probable que los datos del evento se contabilicen dos veces e informarán sobre la inflación de las métricas. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propiedades del evento] | Objeto JSON que contiene propiedades personalizadas del evento. Seleccione entre proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de clave-valor. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![El [!DNL Pinterest] [!UICONTROL Datos de evento] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/event-data.png)

Se pueden configurar las siguientes propiedades de evento:

| Nombre del campo | Descripción |
| --- | --- |
| URL de origen de evento | URL del evento de conversión web. |
| ID de tienda de aplicaciones | ID de aplicación de la tienda de aplicaciones. |
| Nombre de aplicación | Nombre de la aplicación  |
| Versión de aplicación | La versión de la aplicación. |
| Marca del dispositivo | Marca del dispositivo que utiliza el usuario. |
| Operador de dispositivo | Operador de telefonía móvil del usuario para su dispositivo. |
| Modelo de dispositivo | Modelo del dispositivo del usuario. |
| Device Type | Tipo de dispositivo que utiliza el usuario. |
| Versión del SO | Versión del sistema operativo del dispositivo. |
| Idioma del usuario | Código de idioma ISO-639-1 de dos caracteres que indica el idioma del usuario. |

### [!UICONTROL Datos de usuario]

Los siguientes datos de usuario se pueden introducir mediante campos no obligatorios:

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- | 
| [!UICONTROL Correo electrónico] | Dirección de correo electrónico del usuario o hash SHA256 del correo electrónico de la dirección del usuario. | ebd543592...f2b7e1 |
| [!UICONTROL ID de publicidad móvil] | Hashes Sha256 de los ID publicitarios de Google (GAID) o el identificador de Apple para anunciantes (IDFA) del usuario | ebd543592...f2b7e1 |
| [!UICONTROL Dirección IP del cliente] | La dirección IP del usuario, que puede estar en formato IPv4 o IPv6. Se utiliza para la coincidencia. | 192.168.0.1 |
| [!UICONTROL Agente de usuario cliente] | Cadena del agente de usuario del explorador web del usuario. | Mozilla/5.0 (plataforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Datos de información del cliente] | Objeto JSON que contiene otra información del cliente. Seleccione entre proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de clave-valor. | { &quot;ph&quot;: &quot;122333445&quot; } |

![El [!DNL Pinterest] [!UICONTROL Datos de usuario] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/user-data.png)

Las propiedades de información del cliente que se pueden configurar son las siguientes:

| Nombre del campo | Descripción |
| --- | --- |
| Phone | Número de contacto del usuario. Solo se aceptan dígitos y deben introducirse con el código de país, el código de área y el número. |
| Sexo | El sexo puede introducirse como &quot;f&quot; para las mujeres, &quot;m&quot; para los hombres o &quot;n&quot; para los no binarios. |
| Fecha de nacimiento | Fecha de nacimiento, indicada como año, mes y día. |
| Apellidos | Apellido del usuario. |
| Nombre | Nombre del usuario. |
| Ciudad | Ciudad de residencia del usuario. Esto se utiliza principalmente con fines de facturación. |
| Estado | El estado del usuario, que se proporciona como código de dos letras en minúsculas. |
| Código postal | Código postal del usuario, que se utiliza principalmente con fines de facturación. |
| País | Código de país ISO-3166 de dos caracteres que indica el país del usuario. |
| ID externo | ID único del anunciante que identifica a un usuario en su espacio. Por ejemplo, ID de usuario, ID de fidelidad, etc. |
| ID de clic | El identificador único almacenado en la cookie _epik de su dominio o en el parámetro de consulta &amp;epik= de la dirección URL. |

>[!IMPORTANT]
>
>Antes de enviar los datos a [!DNL Pinterest] Al final de la API, la extensión hará un hash y normalizará los valores de los siguientes campos: Correo electrónico, Número de teléfono, Nombre, Apellidos, Sexo, Fecha de nacimiento, Ciudad, Estado, Código postal, País e ID externo. La extensión no hará un hash del valor de estos campos si ya hay una cadena SHA256.

### [!UICONTROL Datos personalizados]

Se pueden introducir los siguientes datos personalizados para la regla:

| Nombre del campo | Descripción |
| --- | --- |
| Moneda | El código de divisa en formato ISO-4217. Si no se proporciona, [!DNL Pinterest] tomará de forma predeterminada la moneda del anunciante establecida durante la creación de la cuenta. |
| Valor | Valor total del evento. Se acepta como cadena en la solicitud. Esto se analizará en un dígito doble. |
| Cadena de búsqueda | La cadena de búsqueda relacionada con el evento de conversión del usuario. |
| ID de pedido | ID del pedido. Enviando `order_id` ayudará [!DNL Pinterest] deduplique los eventos cuando sea necesario. |
| Número de productos | Número total de productos del evento. Por ejemplo, el número total de artículos comprados en un evento de cierre de compra. |
| ID de contenido | Lista (matriz) de ID de productos. |
| Contenido | Una lista (matriz) de objetos que contienen información sobre productos, como precio y cantidad. |

![El [!DNL Pinterest] [!UICONTROL Datos personalizados] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/custom-data.png)

## Validación de datos dentro de [!DNL Pinterest]

Una vez creada y ejecutada la regla de reenvío de eventos, valide si el evento que se envió a [!DNL Pinterest] API se muestra según lo esperado en la [!DNL Pinterest] IU.

Si la colección de eventos y [!DNL Experience Platform] integración se han realizado correctamente, verá eventos dentro de la variable [!DNL Pinterest] IU.

![El [!DNL Pinterest] administrador de eventos](../../../images/extensions/server/pinterest/event-history.png)

Puede obtener más detalles y ver el [!DNL Pinterest] distribución de datos de evento.

![El [!DNL Pinterest] distribución de datos](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Pasos siguientes

Esta guía explica cómo instalar y configurar el [!DNL Pinterest] extensión de reenvío de eventos en la interfaz de usuario. Para obtener más información, consulte la documentación oficial:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Resumen de API de conversiones](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
