---
title: Extensión de API de conversión de Nexdoor
description: Aprenda a utilizar la extensión de API de conversión de NextDoor para enviar eventos de conversión y rastrear el rendimiento de sus campañas publicitarias.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# Extensión de API de conversión [!DNL Nextdoor] - Guía del usuario

## Información general

[!DNL Nextdoor] es un servicio de redes sociales para barrios que conecta a las personas con sus comunidades locales. Es una plataforma donde los vecinos pueden comunicarse, compartir información, estar al día de los eventos locales y las noticias, y comprar y vender artículos con otros en su área.

Use la [[!DNL Nextdoor] extensión de API de conversión](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) para enviar eventos de conversión directamente a la API de conversión [!DNL Nextdoor's]. Esta extensión le ayuda a realizar un seguimiento y medir el rendimiento de sus campañas publicitarias [!DNL Nextdoor] mediante el envío de datos de conversión del lado del servidor.

Esta guía muestra cómo instalar, configurar y usar la extensión de API de conversión [!DNL Nextdoor] en las [reglas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) del reenvío de eventos.

## Requisitos previos {#prerequisites}

Necesita una cuenta válida de [!DNL Nextdoor] Ads Manager para usar esta extensión. Si todavía no tienes una, ve a la [[!DNL Nextdoor Ads] página de registro](https://ads.nextdoor.com/v2/signup) para registrarte y crear tu cuenta.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar Experience Platform a [!DNL Nextdoor], necesitará la siguiente información:

| Credencial | Descripción | Notas de seguridad |
| --- | --- | --- |
| ID de Data Source | Su identificador de origen de datos único de [!DNL Nextdoor], el cual puede encontrar en su cuenta de [!DNL Nextdoor Ads Manager] si accede a la página Assets > Píxeles y genera un Píxel adyacente. | Es seguro compartir esto dentro de su organización. |
| Token de acceso | Su token de acceso de autenticación de API para una comunicación segura. Puede generar este token iniciando sesión en su cuenta de [!DNL Nextdoor Ads Manager] y accediendo a la configuración de la API. | Mantenga este token seguro, ya que proporciona acceso a su cuenta. |

## Instalar y configurar la extensión [!DNL Nextdoor] {#install}

Para instalar la extensión, seleccione **[!UICONTROL Extensions]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catalog]**, seleccione **[!UICONTROL Nextdoor Conversion API Extension]** y luego seleccione **[!UICONTROL Install]**.

![Catálogo de extensiones que muestra la tarjeta de extensión [!DNL Nextdoor] que resalta la instalación.](../../../images/extensions/server/nextdoor/install-extension.png)

En la siguiente pantalla, escriba los valores de configuración que generó a partir de su [!DNL Nextdoor Ads Manager]:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

Cuando termine, seleccione **[!UICONTROL Save]**.

Pantalla de configuración de ![[!DNL Nextdoor] para la extensión de API de conversión de [!DNL Nextdoor].](../../../images/extensions/server/nextdoor/configure.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, puede crear reglas de reenvío de eventos que determinan cuándo y cómo se envían los eventos a [!DNL Nextdoor].

Cree una nueva [regla](../../../ui/managing-resources/rules.md) en su propiedad de reenvío de eventos. En **[!UICONTROL Actions]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Nextdoor Conversion API Extension]**. Para enviar eventos de Edge Network a [!DNL Nextdoor], establezca **[!UICONTROL Action Type]** en **[!UICONTROL Report Web Conversions]**.

![Se está seleccionando el tipo de acción [!UICONTROL Report Web Conversions] para una regla [!DNL Nextdoor] en la IU de recopilación de datos.](../../../images/extensions/server/nextdoor/select-action.png)

Después de realizar esta selección, aparecen controles adicionales que le permiten configurar el evento más a fondo, como se describe a continuación. Una vez finalizado, seleccione **[!UICONTROL Keep Changes]** para guardar la regla.

**Parámetros de cuerpo principal**

Estos parámetros principales definen el evento de conversión:

| Parámetro | Descripción | Tipo de datos | Requerido | Opciones/formato | Ejemplo |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Especifica el tipo de evento de conversión que se rastrea. | Cadena (menú desplegable) | Requerido | <ul><li>Comprar</li><li>Posible cliente</li><li>Registrarse</li><li>Añadir al carro</li><li>Iniciar cierre de compra</li><li>Vista de página</li><li>Buscar</li><li>Ver contenido</li><li>Añadir a la lista de deseos</li><li>Suscribirse</li><li>Personalizado</li></li>Conversión 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Identificador único para evitar la creación de informes de eventos duplicados. Esto se generará automáticamente si está en blanco. | Cadena | Opcional | Identificador de cadena único | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Marca de tiempo de cuando se produjo el evento de conversión. Si se deja en blanco, el valor predeterminado es el tiempo actual. | Número entero | Opcional | Marca de tiempo Unix en segundos | `1703980800` (30 de diciembre de 2023) |
| [!UICONTROL Action Source] | Canal o plataforma donde se produjo la conversión. | Cadena (menú desplegable) | Requerido | <ul><li>sitio web</li><li>correo electrónico</li><li>aplicación</li><li>phone_call</li><li>charlar</li><li>physical_store</li><li>system_generated</li><li>otro</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Anule el ID de la fuente de datos global para eventos específicos. Se heredará de la configuración si se deja en blanco. | Cadena | Opcional | Cadena alfanumérica | `12345` |
| [!UICONTROL Action Source URL] | Dirección URL específica donde se produjo la conversión. | Cadena | Opcional | Dirección URL completa, incluido el protocolo | https://example.com/checkout/success |

**Parámetros de privacidad y cumplimiento**

Utilice estos parámetros para garantizar el cumplimiento de la privacidad:

| Parámetro | Descripción | Tipo de datos | Requerido | Valores/Formato | Ejemplo |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Indicador para restringir el uso de datos para el cumplimiento de la privacidad. | Número entero | Opcional | <ul><li>0 = Sin restricciones</li><li>1 = Restringir</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Restricciones de procesamiento de datos específicas del país. | Número entero | Opcional | 1 = EE. UU. (pueden admitirse otros códigos) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Restricciones específicas del estado para usuarios estadounidenses. | Número entero | Opcional | 1000 = CA, 1001 = CO, etc. | `1000` |
| [!UICONTROL Test Event] | Marca el evento como una prueba para desarrollo o depuración. | Cadena | Opcional | Cualquier cadena no vacía | `test` |

**Parámetros de información del cliente**

>[!IMPORTANT]
>
>Debe proporcionar al menos un parámetro de información del cliente para la atribución de eventos y la coincidencia adecuadas.

| Parámetro | Descripción | Tipo de datos | Requerido | Formato | Ejemplo |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | Dirección de correo electrónico del cliente para coincidencia de identidad. | Cadena | Se requiere al menos un campo de cliente | Texto sin formato o hash SHA-256 | `user@example.com` |
| [!UICONTROL Phone Number] | Número de teléfono del cliente para coincidencia de identidad. | Cadena | Se requiere al menos un campo de cliente | Formato E.164 (con hash SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Nombre del cliente para mejorar la coincidencia. | Cadena | Se requiere al menos un campo de cliente | Texto sin formato o hash SHA-256 | `John` |
| [!UICONTROL Last Name] | Apellidos del cliente para una mayor coincidencia. | Cadena | Se requiere al menos un campo de cliente | Texto sin formato o hash SHA-256 | `Smith` |
| [!UICONTROL Date of Birth] | Fecha de nacimiento del cliente para la coincidencia demográfica. | Cadena | Opcional | AAAAMMDD (con hash SHA-256) | `19900115` |
| [!UICONTROL Gender] | Sexo del cliente para la segmentación demográfica. | Cadena | Opcional | M/F/O (con hash SHA-256) | `M` |
| [!UICONTROL External ID] | Su identificador interno del cliente. | Cadena | Opcional | Cualquier cadena única | `customer_12345` |
| [!UICONTROL Street Address] | Dirección de la calle del cliente. | Cadena | Opcional | Hash SHA-256 | `123 Main Street` (con hash) |
| [!UICONTROL City] | La ciudad del cliente. | Cadena | Opcional | Hash SHA-256 | `San Francisco` (con hash) |
| [!UICONTROL State] | Estado o provincia del cliente. | Cadena | Opcional | Código de dos letras (con hash SHA-256) | `CA` (con hash) |
| [!UICONTROL Zip Code] | Código postal del cliente. | Cadena | Opcional | Primeros 5 dígitos EE. UU. (con hash SHA-256) | `94102` (con hash) |
| [!UICONTROL Country] | País del cliente. | Cadena | Opcional | ISO-3166-1 alpha-2 (con hash SHA-256) | `US` (con hash) |
| [!UICONTROL Click ID] | Identificador de clic contiguo para la atribución. | Cadena | Opcional | Capturado desde el parámetro de URL `ndclid` | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | Dirección IP del dispositivo del usuario. | Cadena | Opcional | Dirección IPv4 o IPv6 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | Cadena del agente de usuario del explorador. | Cadena | Opcional | Cadena de agente de usuario del explorador sin procesar | `Mozilla/5.0 (Windows...)` |

**Parámetros personalizados**

Estos parámetros proporcionan un contexto adicional sobre el evento de conversión:

| Parámetro | Descripción | Tipo de datos | Requerido | Formato | Ejemplo |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Valor total de la transacción de compra. | Cadena | **REQUERIDO para eventos de compra** | ISO 4217 Divisa + Importe (sin espacios) | `USD123.45` |
| [!UICONTROL Order ID] | Transacción única o identificador de pedido. | Cadena | Opcional | Cualquier cadena única | `order_12345` |
| [!UICONTROL Delivery Category] | Método de entrega de productos/servicios. | Cadena | Opcional | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Información detallada sobre los productos comprados. | Cadena (matriz JSON) | Opcional | Matriz JSON de objetos de producto | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Parámetros de aplicación móvil**

Debe incluir estos parámetros cuando `Action Source = 'APP'`:

| Parámetro | Descripción | Tipo de datos | Requerido | Formato | Ejemplo |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Identificador de la aplicación móvil. | Cadena | **NECESARIO para los eventos de la aplicación** | <ul><li>ID del paquete (iOS)</li><li>Nombre del paquete (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | Estado de consentimiento de transparencia de seguimiento de aplicaciones de iOS. | Cadena | **NECESARIO para los eventos de la aplicación** | Cadena booleana | `true` |
| [!UICONTROL Platform] | Sistema operativo móvil. | Cadena | **NECESARIO para los eventos de la aplicación** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Versión de la aplicación móvil. | Cadena | **NECESARIO para los eventos de la aplicación** | Cadena de versión definida por la aplicación | `2.0.0-beta` |

## Tipos de eventos {#event-types}

Los siguientes tipos de eventos son compatibles con diferentes escenarios de conversión:

| Nombre del evento | Tipo de evento | Descripción | Caso de uso | Campos obligatorios | Notas |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Estándar | Transacción de compra completada. | Conversiones de comercio electrónico | <ul><li>Nombre del evento</li><li>Valor del pedido</li><li>Información del cliente</li></ul> | Lo más importante para la optimización de ROAS |
| [!UICONTROL Lead] | Estándar | Generación de clientes potenciales o consulta. | Envíos de formularios, solicitudes de contacto | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Conversión de alto valor para B2B |
| [!UICONTROL Sign Up] | Estándar | Registro de usuario o creación de cuenta. | Suscripción a la newsletter, registro de cuenta | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Seguimiento de conversiones principales de funnel |
| [!UICONTROL Add to Cart] | Estándar | Producto añadido al carro de compras. | Seguimiento de funnel de comercio electrónico | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Señal de participación de Mid-funnel |
| [!UICONTROL Initiate Checkout] | Estándar | Proceso de extracción iniciado. | Seguimiento de intención de compra | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Indicador de intención de compra fuerte |
| [!UICONTROL Page View] | Estándar | Página importante visitada. | Participación de contenido, páginas de aterrizaje | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Se utiliza solo para páginas de alto valor |
| [!UICONTROL Search] | Estándar | Búsqueda realizada en el sitio. | Descubrimiento de productos/contenido | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Indica la participación activa del usuario |
| [!UICONTROL View Content] | Estándar | Contenido o producto visualizado. | Vistas de página de productos, participación en contenido | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Útil para audiencias de remarketing |
| [!UICONTROL Add to Wishlist] | Estándar | Producto añadido a la lista de deseos | Intenciones de compra futuras | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Indica un fuerte interés por el producto |
| [!UICONTROL Subscribe] | Estándar | Suscripción al servicio/newsletter. | Ingresos recurrentes, participación | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Indicador de valor de duración alto |
| [!UICONTROL Custom Conversion 1 - 10] | Personalizado | Evento de conversión específico de la empresa. | Defina su propio tipo de conversión | <ul><li>Nombre del evento</li><li>Información del cliente</li></ul> | Personalizar para acciones empresariales únicas |

## Integración de elementos de datos {#data-element}

Todos los campos admiten elementos de datos del reenvío de eventos de Adobe. Seleccione el icono de elemento de datos ![elementos de datos](../../../images/extensions/server/nextdoor/data-element-icon.png) junto a cualquier campo para:

* **Seleccionar elementos de datos existentes**: seleccione entre elementos de datos que ya se hayan creado.
* **Agregar nuevos elementos de datos**: cree y defina nuevos elementos de datos según sea necesario.
* **Aplicar valores dinámicos**: Rellene campos con contenido dinámico originado en el sitio web.

## Prácticas recomendadas {#best-practices}

Siga estas prácticas recomendadas para garantizar un seguimiento de conversión preciso, mejorar la calidad de los datos y cumplir con las normas de privacidad. Estas recomendaciones le ayudarán a maximizar la eficacia de su integración de la API de conversión de [!DNL Nextdoor] y a optimizar el rendimiento de su publicidad.

### Calidad de los datos y cumplimiento de privacidad

La administración adecuada de los datos es esencial para maximizar la precisión de atribución de conversión y, al mismo tiempo, mantener la privacidad del usuario y el cumplimiento normativo. Estas prácticas ayudan a garantizar que los datos de sus clientes tengan el formato correcto, se procesen de forma segura y se gestionen de acuerdo con las normas de privacidad.

* **Use un formato de datos coherente**: dé formato a correos electrónicos, números de teléfono y otros datos de forma coherente:

   * **Normalización de correo electrónico**: convierta correos electrónicos a minúsculas, recorte espacios en blanco y elimine puntos de [!DNL Gmail] direcciones.
   * **Normalización de números de teléfono**: use el formato E.164 (+1234567890) para la compatibilidad internacional.
   * **Normalización de direcciones**: estandariza las abreviaturas de las calles (St., Ave., Rd.) y elimina los espacios adicionales.
   * **Formato de nombre**: convierta los nombres a minúsculas, elimine espacios adicionales y controle los caracteres especiales de forma coherente.

* **Datos confidenciales con hash**: considere la posibilidad de cifrar con hash datos confidenciales de clientes antes de enviarlos. Normalice siempre los datos antes del hash para garantizar valores hash coherentes:

   * Utilice el hash SHA-256 para números de teléfono, direcciones y otras PII.
   * La extensión envía automáticamente hash a los correos electrónicos de texto sin formato; puede enviar cualquiera de los dos formatos.
   * Utilice datos hash de forma coherente en todas las implementaciones de seguimiento.
      * **Ejemplo**: Normalice &quot;John@Example.COM&quot; → &quot;john@example.com&quot; antes del hashing.

* **Proporcionar información completa**: incluya toda la información del cliente posible para que haya una mejor coincidencia:

   * Incluya varios identificadores (correo electrónico + teléfono o correo electrónico + nombre + dirección) cuando estén disponibles.
   * Utilice ID de cliente externos para vincular eventos de conversión a los datos de CRM.
   * Proporcionar datos demográficos (edad, sexo) cuando estén disponibles y cumplan con las leyes de privacidad.

* **Administración de consentimiento**: Asegúrese de que cuenta con el consentimiento adecuado para la recopilación de datos:

   * Implemente los mecanismos de consentimiento adecuados antes de recopilar datos de clientes.
   * Respetar las preferencias de exclusión de usuarios y las solicitudes de eliminación de datos.
   * Utilice los parámetros de Uso de datos restringido para los usuarios que han optado por la exclusión.
   * **Recursos**:
      * [Guía de cumplimiento del RGPD](https://gdpr.eu/compliance/)
      * [Requisitos de privacidad de la CCPA](https://oag.ca.gov/privacy/ccpa)

* **Minimización de datos**: Envíe solamente los datos necesarios para el seguimiento de conversiones:

   * Recopile y envíe únicamente datos que sean esenciales para la atribución y la optimización.
   * Revise y audite periódicamente los campos de datos que está enviando.
   * Elimine la información innecesaria del cliente para reducir el riesgo de privacidad.

* **Usar marcas de hora precisas**: Asegúrese de que las marcas de hora de evento sean precisas para la atribución adecuada.
   * Utilice la hora real en la que se produjo la conversión, no cuando procesó los datos.
   * Asegúrese de que las marcas de tiempo estén en formato Unix epoch (segundos desde el 1 de enero de 1970).
   * Tenga en cuenta las diferencias de zona horaria en los cálculos de marca de hora.

### Deduplicación de eventos

Evite los eventos de conversión duplicados para garantizar una medición precisa de la campaña y evitar métricas de rendimiento infladas. Implemente la deduplicación adecuada para que cada conversión se cuente solo una vez, lo que proporciona datos fiables para sus decisiones de optimización.

* **Proporcione ID de evento únicos**: Use siempre ID de evento únicos para evitar conversiones duplicadas.
* **Use un nombre coherente**: Aplique un nombre de evento coherente en toda la implementación.

### Limitación de velocidad

La API de conversión [!DNL Nextdoor] está sujeta a la limitación de velocidad. El límite actual de tarifa es de **100 solicitudes/minuto** por anunciante. Si supera el límite de velocidad, la API devolverá un código de error de `HTTP 429 Too Many Requests`.

## Conclusión {#conclusion}

La extensión de la API de conversión de [!DNL Nextdoor] proporciona una forma eficaz de realizar el seguimiento de conversiones y medir la eficacia de las campañas publicitarias de [!DNL Nextdoor]. Si sigue esta guía e implementa las prácticas recomendadas, puede garantizar un seguimiento de conversión preciso y optimizar el rendimiento de la publicidad.

Para obtener la información más actualizada y los recursos adicionales, visite [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Próximos pasos {#next-steps}

Esta guía muestra cómo enviar datos de evento del lado del servidor a [!DNL Nextdoor] mediante la extensión de API de conversión [!DNL Nextdoor]. Para obtener más información acerca de las funcionalidades de reenvío de eventos en [!DNL Adobe Experience Platform], consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
