---
keywords: conexión de facebook;conexión de facebook;destinos de facebook;facebook;instagram;messenger;facebook messenger
title: Conexión de Facebook
description: Active perfiles para sus campañas de Facebook para la segmentación, personalización y supresión de público en función de los correos electrónicos con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 6%

---

# [!DNL Facebook] conexión

## Información general {#overview}

Active perfiles para sus campañas [!DNL Facebook] de segmentación, personalización y supresión de audiencias en función de los correos electrónicos con hash.

Puede usar este destino para segmentar audiencias en [!DNL Facebook's] familia de aplicaciones compatibles con [!DNL Custom Audiences], entre ellas [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de ubicación de [!DNL Facebook Ads Manager].

![Destino de Facebook en la interfaz de usuario de Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL Facebook], aquí hay dos casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

### Caso de uso #1

Un retailer en línea quiere llegar a los clientes existentes a través de plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. Retailer en línea puede ingerir direcciones de correo electrónico desde su propio CRM a Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a la plataforma social [!DNL Facebook], lo que optimiza el gasto en publicidad.

### Caso de uso #2

Una aerolínea tiene diferentes niveles de clientes (Bronce, Plata y Oro) y desea proporcionar a cada uno de los niveles ofertas personalizadas a través de plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la compañía. Los únicos identificadores que la compañía tiene sobre estos clientes son ID de miembros y direcciones de correo electrónico.

Para dirigirlos a todos los medios sociales, pueden incorporar los datos de clientes de su CRM a Adobe Experience Platform, utilizando las direcciones de correo electrónico como identificadores.

A continuación, puede utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de clientes, para crear nuevas audiencias a las que dirigirse a través del destino [!DNL Facebook].

## Identidades admitidas {#supported-identities}

[!DNL Facebook Custom Audiences] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para números de teléfono con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para direcciones de correo electrónico de texto sin formato y con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Facebook. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos de cuenta de Facebook {#facebook-account-prerequisites}

Antes de enviar las audiencias a [!DNL Facebook], asegúrese de cumplir con los siguientes requisitos:

* La cuenta de usuario [!DNL Facebook] debe tener acceso completo a [!DNL Facebook Business Account], que posee la cuenta de publicidad que está utilizando.
* La cuenta de usuario [!DNL Facebook] debe tener habilitado el permiso **[!DNL Manage campaigns]** para la cuenta de publicidad que planea usar.
* La cuenta empresarial **Adobe Experience Cloud** debe agregarse como socio de publicidad en [!DNL Facebook Ad Account]. Usar `business ID=206617933627973`. Consulte [Agregar socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.

  >[!IMPORTANT]
  >
  > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas**. Se requiere el permiso para la integración de [!DNL Adobe Experience Platform].

* Lea y firme los términos de servicio de [!DNL Facebook Custom Audiences]. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`, donde `accountID` es su [!DNL Facebook Ad Account ID]. Asegúrese de que la sección `business_id=206617933627973` esté presente en la dirección URL al firmar los Términos de servicio.

  >[!IMPORTANT]
  >
  >Al firmar los Términos de servicio de [!DNL Facebook Custom Audiences], asegúrese de usar la misma cuenta de usuario que utilizó para autenticarse en la API de Facebook.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Facebook] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias activadas en [!DNL Facebook] pueden tener claves de *identificadores hash*, como direcciones de correo electrónico o números de teléfono.

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes.

## Requisitos de hash de número de teléfono {#phone-number-hashing-requirements}

Hay dos métodos para activar números de teléfono en [!DNL Facebook]:

* **Ingesta de números de teléfono sin procesar**: puede ingerir números de teléfono sin procesar con el formato [!DNL E.164] en [!DNL Experience Platform]. Se colocan automáticamente en el hash tras la activación. Si elige esta opción, asegúrese de introducir siempre los números de teléfono sin procesar en el área de nombres `Phone_E.164`.
* **Ingesta de números de teléfono con hash**: puede prehash sus números de teléfono antes de ingerirlos en [!DNL Experience Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en el área de nombres `Phone_SHA256`.

>[!NOTE]
>
>Los números de teléfono introducidos en el área de nombres `Phone` no se pueden activar en [!DNL Facebook].

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede usar las direcciones de correo electrónico en borrar en Experience Platform y hacer que [!DNL Experience Platform] las hash en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [descripción general de la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) y la [descripción general de la ingesta por transmisión](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recortar todos los espacios iniciales y finales de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al crear valores hash de las cadenas de correo electrónico, asegúrese de usar la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No salar la cuerda.

>[!NOTE]
>
>[!DNL Experience Platform] crea automáticamente un hash de los datos de las áreas de nombres sin hash tras la activación.
> Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación.
> La opción **[!UICONTROL Aplicar transformación]** solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir áreas de nombres.

![Aplicar control de transformación resaltado en el paso de asignación.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de poder usar el área de nombres `Extern_ID` para enviar datos a [!DNL Facebook], asegúrese de sincronizar sus propios identificadores con [!DNL Facebook Pixel]. Consulte la [documentación oficial de Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obtener información detallada.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

El siguiente vídeo también muestra los pasos para configurar un destino [!DNL Facebook] y activar audiencias.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario de Experience Platform se actualiza con frecuencia y puede haber cambiado desde que se grabó este vídeo. Para obtener la información más actualizada, consulte el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticarse en el destino {#authenticate}

1. Busque el destino de Facebook en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccione **[!UICONTROL Conectar con destino]**.
   ![Paso Autenticar en Facebook mostrado en el flujo de trabajo de activación.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Escribe tus credenciales de Facebook y selecciona **Iniciar sesión**.

### Actualizar credenciales de autenticación {#refresh-authentication-credentials}

Los tokens de autenticación de Facebook caducan cada 60 días. Una vez caducado el token, las exportaciones de datos al destino dejan de funcionar.

Puede supervisar las fechas de caducidad de los tokens desde la columna **[!UICONTROL Fecha de caducidad de la cuenta]** en las pestañas **[!UICONTROL Cuentas]** o **[!UICONTROL Examinar]**.

![Columna de fecha de caducidad del token de la cuenta de Facebook en la pestaña Examinar](../../assets/catalog/social/facebook/account-expiration-browse.png)

![Columna de fecha de caducidad del token de la cuenta de Facebook en la ficha Cuentas](../../assets/catalog/social/facebook/account-expiration-accounts.png)

Para evitar que la caducidad del token interrumpa los flujos de datos de activación, vuelva a autenticarse realizando los siguientes pasos:

1. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Cuentas]**
2. (Opcional) Utilice los filtros disponibles en la página para mostrar solo las cuentas de Facebook.
   ![Filtrar para mostrar solo cuentas de Facebook](/help/destinations/assets/catalog/social/facebook/refresh-oauth-filters.png)
3. Seleccione la cuenta que desea actualizar, seleccione los puntos suspensivos y seleccione **[!UICONTROL Editar detalles]**.
   ![Seleccionar el control Editar detalles](/help/destinations/assets/catalog/social/facebook/refresh-oauth-edit-details.png)
4. En la ventana modal, seleccione **[!UICONTROL Volver a conectar OAuth]** y vuelva a autenticarse con sus credenciales de Facebook.
   ![Ventana modal con la opción Reconectar OAuth](/help/destinations/assets/catalog/social/facebook/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Las credenciales de autenticación se actualizan y su hora de caducidad se restablece a 60 días.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID de cuenta"
>abstract="Su ID de cuenta de Facebook Ad. Puede encontrar este ID en su cuenta de Facebook Ads Manager. Al introducir este ID, utilice siempre como prefijo `act_`."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Id. de cuenta]**: Su [!DNL Facebook Ad Account ID]. Puede encontrar este identificador en su cuenta de [!DNL Facebook Ads Manager]. Al introducir este ID, utilice siempre como prefijo `act_`.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origen de la audiencia"
>abstract="Elija cómo se recopilaron originalmente los datos del cliente en el público. Los datos se muestran en Facebook cuando un usuario sea el objetivo del segmento"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Origen de la audiencia"
>abstract="Los anunciantes recopilaron datos directamente de los clientes."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origen de la audiencia"
>abstract="Los anunciantes recopilaron datos directamente de sus socios."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origen de la audiencia"
>abstract="Los anunciantes recopilaron datos directamente de sus clientes y socios."

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso **[!UICONTROL Programación de segmentos]**, debe proporcionar [!UICONTROL Origen de la audiencia] al enviar audiencias a [!DNL Facebook Custom Audiences].

![Menú desplegable Origen de la audiencia mostrado en el paso de activación de Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Ejemplo de asignación: activar datos de audiencia en [!DNL Facebook Custom Audience] {#example-facebook}

A continuación se muestra un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Facebook Custom Audience].

Selección de campos de origen:

* Seleccione el área de nombres `Email` como identidad de origen si las direcciones de correo electrónico que está utilizando no tienen hash.
* Seleccione el área de nombres `Email_LC_SHA256` como identidad de origen si ha creado un hash de las direcciones de correo electrónico de los clientes al ingerir datos en [!DNL Experience Platform], de acuerdo con [!DNL Facebook] [los requisitos de hash de correo electrónico](#email-hashing-requirements).
* Seleccione el área de nombres `PHONE_E.164` como identidad de origen si los datos constan de números de teléfono sin hash. [!DNL Experience Platform] hará un hash de los números de teléfono para cumplir con los requisitos de [!DNL Facebook].
* Seleccione el área de nombres `Phone_SHA256` como identidad de origen si ha creado valores hash de números de teléfono en la ingesta de datos en [!DNL Experience Platform], de acuerdo con [!DNL Facebook] [los requisitos de hash de números de teléfono](#phone-number-hashing-requirements).
* Seleccione el área de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el área de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el área de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el área de nombres `Email_LC_SHA256` como identidad de destino cuando las áreas de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el área de nombres `Phone_SHA256` como identidad de destino cuando las áreas de nombres de origen sean `PHONE_E.164` o `Phone_SHA256`.
* Seleccione las áreas de nombres `IDFA` o `GAID` como identidad de destino cuando las áreas de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el área de nombres `Extern_ID` como identidad de destino cuando el área de nombres de origen sea personalizada.

>[!IMPORTANT]
>
>[!DNL Experience Platform] crea automáticamente un hash de los datos de las áreas de nombres sin hash tras la activación.
> 
>Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación.

![Aplicar control de transformación resaltado en el paso de asignación.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Datos exportados {#exported-data}

Para [!DNL Facebook], una activación correcta significa que se crearía una audiencia personalizada de [!DNL Facebook] mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a audiencias se añadiría y eliminaría a medida que los usuarios se calificaran o descalificaran para las audiencias activadas.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite rellenos históricos de audiencias. Todas las clasificaciones de audiencia históricas se envían a [!DNL Facebook] cuando activa las audiencias en el destino.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Este error se produce cuando los clientes utilizan cuentas recién creadas y los permisos de [!DNL Facebook] aún no están activos.

>[!IMPORTANT]
>
>Asegúrese de aceptar [!DNL Facebook Custom Audience Terms of Service] en `business ID 206617933627973`, tal como se muestra en la plantilla URL de la sección [requisitos previos de la cuenta](#facebook-account-prerequisites).

Si recibe el mensaje de error `400 Bad Request` después de seguir los pasos de los [requisitos previos de la cuenta de Facebook](#facebook-account-prerequisites), espere unos días para que los permisos de [!DNL Facebook] entren en vigor.


