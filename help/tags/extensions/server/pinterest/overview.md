---
keywords: extensión de reenvío de eventos;pinterest;extensión de reenvío de eventos de pinterest
title: Extensión de reenvío de eventos de pinterest
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite ingerir eventos en Pinterest para sus necesidades comerciales.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] extensión de reenvío de eventos

[!DNL Pinterest] es un motor de descubrimiento visual para encontrar ideas como recetas, decoración doméstica, inspiración de estilo, etc. Hay miles de millones de pines en [!DNL Pinterest], que también se pueden compartir con otros usuarios en [!DNL Pinterest]. Puede recopilar los eventos de interacción del usuario y aprovechar [!DNL Pinterest Analytics] para comprender el comportamiento del usuario y ejecutar anuncios segmentados.

La variable [[!DNL Pinterest] Conversiones](https://developers.pinterest.com/docs/conversions/conversion-management/) API [reenvío de eventos](../../../ui/event-forwarding/overview.md) permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Pinterest]. Este documento cubre los casos de uso de la extensión, cómo instalarla y cómo integrar sus capacidades en el reenvío de eventos [reglas](../../../ui/managing-resources/rules.md).

Los tokens de acceso de las conversiones son el método de autenticación utilizado por [!DNL Pinterest] al interactuar con la variable [!DNL Pinterest] API.

## Casos de uso

Esta extensión debe usarse si desea utilizar datos de la red perimetral en [!DNL Pinterest] para aprovechar las capacidades de análisis de clientes.

Por ejemplo, supongamos que tenemos un equipo de marketing en una organización. El equipo captura los datos de eventos de interacción de los usuarios desde su sitio web y los carga en [!DNL Pinterest] uso de esta extensión de reenvío de eventos.

Los equipos de marketing y análisis pueden aprovechar [!DNL Pinterest] Funciones de Analytics para comprender las interacciones y el comportamiento clave del usuario, lo que le permite comprender mejor a los usuarios y segmentarlos para campañas de publicidad segmentada.

Para obtener más información sobre casos de uso específicos de [!DNL Pinterest], consulte [[!DNL Pinterest] casos de uso](https://business.pinterest.com/en/success-stories) documentación.

## [!DNL Pinterest] requisitos previos {#prerequisites}

Debe tener una [!DNL Pinterest] [cuenta empresarial](https://help.pinterest.com/en/business/article/get-a-business-account) para utilizar esta extensión. Vaya a la [[!DNL Pinterest] página de registro](https://www.pinterest.com/business/create/) para registrar y crear una cuenta si todavía no la tiene.

También necesitará un [!DNL Pinterest] cuenta de desarrollador, que deberá estar asociada a su [!DNL Pinterest] cuenta empresarial. Para asociar la cuenta de desarrollador con la cuenta de empresa, consulte [[!DNL Pinterest ] cuenta de desarrollador](https://developers.pinterest.com/account-setup/).

### Recopilar los detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Pinterest], se requieren las siguientes entradas:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Ads Account Id | Su [!DNL Pinterest] Id De Cuenta De Publicidad. Consulte la [[!DNL Pinterest] documentación](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) para obtener más información. | 123456789012 |
| Token de acceso de conversión | Su [!DNL Pinterest] Token de acceso de conversión. Consulte la [[!DNL Pinterest] API de conversiones](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento de orientación. <br> **Solo tendrá que hacerlo una vez, ya que este token no caduca.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Instale y configure el [!DNL Pinterest] Extensión {#install}

Para instalar la extensión, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editarla en su lugar.

En el panel de navegación izquierdo, seleccione **[!UICONTROL Extensiones]**. Select **[!UICONTROL Instalar]** en la tarjeta para la variable [!DNL Pinterest] en el **[!UICONTROL Catálogo]** pestaña .

![El catálogo que muestra las variables [!DNL Pinterest] extensión con [!UICONTROL Instalar] resaltado.](../../../images/extensions/server/pinterest/install.png)

### Configurar la extensión de [!DNL Pinterest]

>[!IMPORTANT]
>
>Según las necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de comenzar para determinar qué entidades debe configurar para su caso de uso.

En el panel de navegación izquierdo, seleccione **[!UICONTROL Extensiones]**. Select **[!UICONTROL Configurar]** en la tarjeta para la variable [!DNL Pinterest] en el [!UICONTROL Installed]**.

![[!DNL Pinterest] en la [!UICONTROL Instalar] pestaña con [!UICONTROL Configurar] resaltado.](../../../images/extensions/server/pinterest/configure.png)

En la siguiente pantalla, introduzca el [!UICONTROL Ads Account Id] y [!UICONTROL Token de acceso de conversión] que ha recopilado anteriormente en la [detalles de configuración](#configuration-details) para obtener más información. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**.

![La variable [!DNL Pinterest] [!UICONTROL Configurar] resaltado de la pantalla [!UICONTROL Ads Account Id] y [!UICONTROL Token de acceso de conversión] campos de entrada.](../../../images/extensions/server/pinterest/input.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinen cuándo y cómo se enviarán los eventos a [!DNL Pinterest].

Cree una nueva [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Pinterest]**. Para enviar eventos de Adobe Experience Edge Network a [!DNL Pinterest], establezca la variable **[!UICONTROL Tipo de acción]** a **[!UICONTROL Enviar evento].**

![La variable [!DNL Pinterest] [!UICONTROL Enviar evento] creación de reglas.](../../../images/extensions/server/pinterest/rule.png)

Tras la selección, aparecen controles adicionales para configurar el evento. Debe asignar la variable [!DNL Pinterest] propiedades de evento a los elementos de datos que ha creado anteriormente.

### [!UICONTROL Datos de Evento]

Se necesitarán los siguientes datos de evento para crear la nueva regla:

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- | 
| [!UICONTROL Nombre del evento] | Tipo de evento de usuario. Sin embargo, puede ser cualquier tipo de evento para aprovechar [!DNL Pinterest Analytics] se recomienda utilizar [[!DNL Pinterest] códigos de evento](https://help.pinterest.com/en/business/article/add-event-codes) | * cierre de compra <br> * add_to_cart <br> * page_visit <br> * signup <br> * [Evento definido por el usuario] |
| [!UICONTROL Fuente de la acción] | Origen que indica dónde se produjo el evento de conversión. | * app_android <br> * app_ios <br> * web <br> * sin conexión |
| [!UICONTROL Hora del evento] | Esto hace referencia a la hora del evento. El formato de tiempo predeterminado utilizado es UNIX, en formato `<seconds>.<miliseconds>` según la zona horaria local. Para obtener más información, consulte [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 segundos y 500 milisegundos después de epoch o lunes, 1 de junio de 2015, a las 7:50:55 PM GMT. |
| [!UICONTROL ID de evento] | Una cadena de ID única que identifica este evento y que puede utilizarse para la deduplicación de eventos introducidos mediante la API de conversión y el seguimiento de Pinterest. Sin esto, es probable que los datos del evento se cuenten dos veces y que informen de la inflación de la métrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propiedades del evento] | Un objeto JSON que contiene propiedades personalizadas del evento. Seleccione esta opción para proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de valor clave. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![La variable [!DNL Pinterest] [!UICONTROL Datos de evento] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/event-data.png)

Se pueden configurar las siguientes propiedades de evento:

| Nombre del campo | Descripción |
| --- | --- |
| URL de origen de evento | URL del evento de conversión web. |
| ID del almacén de aplicaciones | El ID de la aplicación de la tienda de aplicaciones. |
| Nombre de aplicación | Nombre de la aplicación  |
| Versión de aplicación | Versión de la aplicación. |
| Marca de dispositivo | Marca del dispositivo que utiliza el usuario. |
| Operador de telefonía móvil | Operador de telefonía móvil del usuario para su dispositivo. |
| Modelo de dispositivo | Modelo del dispositivo del usuario. |
| Device Type | Tipo de dispositivo que utiliza el usuario. |
| Versión del SO | Versión del sistema operativo del dispositivo. |
| Idioma del usuario | Código de idioma ISO-639-1 de dos caracteres que indica el idioma del usuario. |

### [!UICONTROL Datos de usuario]

Los siguientes datos de usuario se pueden introducir mediante campos no obligatorios:

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- | 
| [!UICONTROL Correo electrónico] | Dirección de correo electrónico del usuario o hash SHA256 del correo electrónico de la dirección del usuario. | ebd543592...f2b7e1 |
| [!UICONTROL ID de publicidad móvil] | Hashes Sha256 de los &quot;ID de publicidad de Google&quot; (GAID) o &quot;Identificador de Apple para anunciantes&quot; (IDFA) del usuario | ebd543592...f2b7e1 |
| [!UICONTROL Dirección IP del cliente] | La dirección IP del usuario, que puede estar en formato IPv4 o IPv6. Se utiliza para la coincidencia. | 192.168.0.1 |
| [!UICONTROL Agente de usuario del cliente] | La cadena del agente de usuario del explorador web del usuario. | Mozilla/5.0 (plataforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Datos de información del cliente] | Un objeto JSON que contiene otra información del cliente. Seleccione esta opción para proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de valor clave. | { &quot;ph&quot;: &quot;122333445&quot; } |

![La variable [!DNL Pinterest] [!UICONTROL Datos de usuario] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/user-data.png)

Las propiedades de información del cliente que se pueden configurar son:

| Nombre del campo | Descripción |
| --- | --- |
| Phone | Número de contacto del usuario. Solo se aceptan dígitos, que deben introducirse con código de país, código de área y número. |
| Sexo | El género se puede introducir como &quot;f&quot; para la mujer, &quot;m&quot; para el hombre o &quot;n&quot; para el no binario. |
| Fecha de nacimiento | Fecha de nacimiento, introducida como año, mes y día. |
| Apellidos | Apellido del usuario. |
| Nombre | Nombre del usuario. |
| Ciudad | Ciudad de residencia del usuario. Esto se utiliza principalmente con fines de facturación. |
| Estado | Estado del usuario, que se proporciona como código de dos letras en minúsculas. |
| Código postal | Código postal del usuario, que se utiliza principalmente con fines de facturación. |
| País | Código de país ISO-3166 de dos caracteres que indican el país del usuario. |
| ID externo | ID único del anunciante que identifica a un usuario en su espacio. Por ejemplo, id de usuario, id de fidelidad, etc. |
| ID de clic | Identificador único almacenado en la cookie _epik en su dominio o parámetro de consulta &amp;epik= en la dirección URL. |

>[!IMPORTANT]
>
>Antes de enviar los datos a [!DNL Pinterest] extremo de API, la extensión hash y normalizará los valores de los campos siguientes: Correo electrónico, número de teléfono, nombre, apellidos, sexo, fecha de nacimiento, ciudad, estado, código postal, país e ID externa. La extensión no hash el valor de estos campos si ya existe una cadena SHA256.

### [!UICONTROL Datos personalizados]

Se pueden introducir los siguientes datos personalizados para la regla:

| Nombre del campo | Descripción |
| --- | --- |
| Moneda | El código de divisa ISO-4217. Si no se proporciona, [!DNL Pinterest] pasará de forma predeterminada a la moneda del anunciante que se estableció durante la creación de la cuenta. |
| Valor | Valor total del evento. Se acepta como cadena en la solicitud. Esto se analizará en un dígito doble. |
| Cadena de búsqueda | La cadena de búsqueda relacionada con el evento de conversión de usuario. |
| ID de pedido | El ID de pedido. Envío `order_id` ayuda de [!DNL Pinterest] deduplique eventos cuando sea necesario. |
| Número de productos | Número total de productos del evento. Por ejemplo, el número total de artículos comprados en un evento de cierre de compra. |
| ID de contenido | Lista (matriz) de ID de productos. |
| Contenido | Una lista (matriz) de objetos que contienen información sobre productos, como precio y cantidad. |

![La variable [!DNL Pinterest] [!UICONTROL Datos personalizados] resaltado en la acción de regla.](../../../images/extensions/server/pinterest/custom-data.png)

## Validar datos en [!DNL Pinterest]

Una vez creada y ejecutada la regla de reenvío de eventos, valide si el evento enviado al [!DNL Pinterest] La API se muestra según lo esperado en la [!DNL Pinterest] IU.

Si la recopilación de eventos y [!DNL Experience Platform] si la integración se ha realizado correctamente, verá eventos dentro de [!DNL Pinterest] IU.

![La variable [!DNL Pinterest] administrador de eventos](../../../images/extensions/server/pinterest/event-history.png)

Puede explorar más en profundidad y ver el [!DNL Pinterest] distribución de datos de evento.

![La variable [!DNL Pinterest] distribución de datos](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Pasos siguientes

Esta guía explica cómo instalar y configurar la variable [!DNL Pinterest] extensión de reenvío de eventos en la interfaz de usuario de . Para obtener más información, consulte la documentación oficial:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Información general de la API de conversiones](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
