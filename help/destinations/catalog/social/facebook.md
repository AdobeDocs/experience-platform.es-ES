---
keywords: Conexión de facebook;conexión de facebook;destinos de facebook;facebook;instagram;mensajero;mensajería de facebook
title: Conexión facebook
description: Active perfiles para sus campañas de Facebook para segmentación de audiencia, personalización y supresión en función de correos electrónicos con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 6%

---

# [!DNL Facebook] connection

## Información general {#overview}

Activar perfiles para [!DNL Facebook] campañas para segmentación, personalización y supresión de audiencia basadas en correos electrónicos con hash.

Puede usar este destino para la segmentación de audiencias en [!DNL Facebook’s] familia de aplicaciones compatibles con [!DNL Custom Audiences], incluyendo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de colocación de [!DNL Facebook Ads Manager].

![Destino de facebook en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo usar la variable [!DNL Facebook] destino, estos son dos casos de uso de muestra que los clientes de Adobe Experience Platform pueden resolver mediante esta función.

### Caso de uso número 1

Un comerciante en línea quiere llegar a los clientes existentes a través de plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El comerciante en línea puede ingerir direcciones de correo electrónico desde su propio CRM a Adobe Experience Platform, crear segmentos a partir de sus propios datos sin conexión y enviar estos segmentos al [!DNL Facebook] plataforma social, optimizando su gasto publicitario.

### Caso de uso n.º 2

Una aerolínea tiene diferentes niveles de clientes (bronce, plata y oro) y desea proporcionar a cada uno de los niveles ofertas personalizadas a través de plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la empresa. Los únicos identificadores que la empresa tiene sobre estos clientes son los ID de pertenencia y las direcciones de correo electrónico.

Para dirigirlos a través de los medios sociales, pueden incorporar los datos de clientes de su CRM a Adobe Experience Platform, utilizando las direcciones de correo electrónico como identificadores.

A continuación, pueden utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de cliente, para crear nuevos segmentos de audiencia a los que pueden dirigirse mediante el [!DNL Facebook] destino.

## Identidades compatibles {#supported-identities}

[!DNL Facebook Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione la identidad objetivo GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para los números de teléfono sin formato y con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para el texto sin formato y las direcciones de correo electrónico con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Facebook. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos de cuenta de facebook {#facebook-account-prerequisites}

Antes de poder enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su [!DNL Facebook] la cuenta de usuario debe tener la variable **[!DNL Manage campaigns]** permiso habilitado para la cuenta de anuncio que planea usar.
* La variable **Adobe Experience Cloud** la cuenta comercial debe agregarse como socio de publicidad en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador empresarial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar la variable **Administración de campañas** permiso. El permiso es necesario para la variable [!DNL Adobe Experience Platform] integración.
* Lea y firme el [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >Al firmar el [!DNL Facebook Custom Audiences] Términos del servicio, asegúrese de utilizar la misma cuenta de usuario que utilizó para autenticarse en la API de Facebook.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Facebook] se puede desactivar *hash* identificadores, como direcciones de correo electrónico o números de teléfono.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

## Requisitos de hash de número telefónico {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Facebook]:

* **Ingesta de números de teléfono sin procesar**: puede ingerir números de teléfono sin procesar en la [!DNL E.164] formatear en [!DNL Platform]. Se colocan automáticamente en hash al activarse. Si elige esta opción, asegúrese de introducir siempre sus números de teléfono sin procesar en la `Phone_E.164` espacio de nombres.
* **Ingesta de números de teléfono con hash**: puede prehash sus números de teléfono antes de ingerirlos a [!DNL Platform]. Si elige esta opción, asegúrese de ingerir siempre sus números de teléfono con hash en la variable `Phone_SHA256` espacio de nombres.

>[!NOTE]
>
>Números de teléfono introducidos en la variable `Phone` el espacio de nombres no se puede activar en [!DNL Facebook].

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform o utilizar las direcciones de correo electrónico claramente en Experience Platform, y [!DNL Platform] Hágalos en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta de lotes](/help/ingestion/batch-ingestion/overview.md) y [información general sobre la ingesta de transmisión](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios al principio y al final de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al hash de las cadenas de correo electrónico, asegúrese de usar un hash para la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No sal la cadena.

>[!NOTE]
>
>Los datos de las áreas de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarse.
> Los datos de origen de atributos no se colocan automáticamente en hash. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos.
> La variable **[!UICONTROL Aplicar transformación]** solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir espacios de nombres.

![Transformación de asignación de identidad](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de usar la variable `Extern_ID` espacio de nombres para enviar datos a [!DNL Facebook], asegúrese de sincronizar sus propios identificadores mediante [!DNL Facebook Pixel]. Consulte la [Documentación oficial de facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obtener información detallada.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

El siguiente vídeo muestra también los pasos para configurar un [!DNL Facebook] dirigir y activar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde la grabación de este vídeo. Para obtener la información más actualizada, consulte la [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticar en destino {#authenticate}

1. Busque el destino de Facebook en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Select **[!UICONTROL Conectarse al destino]**.
   ![Autenticar en Facebook](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Introduzca sus credenciales de Facebook y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID de cuenta"
>abstract="Su ID de cuenta de Facebook Ad. Puede encontrar este ID en su cuenta de Facebook Ads Manager. Al introducir este ID, utilice siempre como prefijo `act_`."

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su [!DNL Facebook Ad Account ID]. Puede encontrar este ID en su [!DNL Facebook Ads Manager] cuenta. Al introducir este ID, utilice siempre como prefijo `act_`.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origen de la audiencia"
>abstract="Elija cómo se recopilaron originalmente los datos del cliente en el segmento. Los datos se mostrarán en Facebook cuando un usuario sea el objetivo del segmento"

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
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

En el **[!UICONTROL Programación de segmentos]** paso, debe proporcionar la variable [!UICONTROL Origen de la audiencia] al enviar segmentos a [!DNL Facebook Custom Audiences].

![Origen de audiencia de facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Facebook Custom Audience] {#example-facebook}

A continuación se muestra un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Facebook Custom Audience].

Selección de campos de origen:

* Seleccione el `Email` área de nombres como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el `Email_LC_SHA256` área de nombres como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente en la ingesta de datos en [!DNL Platform], según [!DNL Facebook] [requisitos de hash de correo electrónico](#email-hashing-requirements).
* Seleccione el `PHONE_E.164` área de nombres como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] hash de los números de teléfono con los que cumplir [!DNL Facebook] requisitos.
* Seleccione el `Phone_SHA256` área de nombres como identidad de origen si ha hash los números de teléfono en la ingesta de datos en [!DNL Platform], según [!DNL Facebook] [requisitos de hash de número telefónico](#phone-number-hashing-requirements).
* Seleccione el `IDFA` área de nombres como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el `GAID` área de nombres como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el `Custom` área de nombres como identidad de origen si sus datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el `Email_LC_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `Email` o `Email_LC_SHA256`.
* Seleccione el `Phone_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `PHONE_E.164` o `Phone_SHA256`.
* Seleccione el `IDFA` o `GAID` áreas de nombres como identidad de destino cuando las áreas de nombres de origen son `IDFA` o `GAID`.
* Seleccione el `Extern_ID` como identidad de destino cuando el espacio de nombres de origen es personalizado.

>[!IMPORTANT]
>
>Los datos de las áreas de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarse.
> 
>Los datos de origen de atributos no se colocan automáticamente en hash. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos.

![Asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Datos exportados {#exported-data}

Para [!DNL Facebook], una activación correcta significa que [!DNL Facebook] la audiencia personalizada se crearía mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a segmentos en la audiencia se agregaría y eliminaría ya que los usuarios están cualificados o no cumplen los requisitos para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite los rellenos históricos de audiencia. Todas las cualificaciones históricas de segmentos se envían a [!DNL Facebook] al activar los segmentos en el destino.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecta {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Este error se produce cuando los clientes utilizan cuentas recién creadas y la variable [!DNL Facebook] los permisos de aún no están activos.

Si recibe la variable `400 Bad Request` mensaje de error después de seguir los pasos indicados en [Requisitos previos de cuenta de facebook](#facebook-account-prerequisites), dedique unos días a la [!DNL Facebook] permisos para entrar en vigor.
