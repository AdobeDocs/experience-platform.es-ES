---
keywords: Conexión de facebook;conexión de facebook;destinos de facebook;facebook;instagram;mensajero;mensajería de facebook
title: Conexión facebook
description: Active perfiles para sus campañas de Facebook para segmentación de audiencia, personalización y supresión en función de correos electrónicos con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 1%

---

# [!DNL Facebook] connection

## Información general {#overview}

Active perfiles para sus campañas [!DNL Facebook] para segmentación de audiencia, personalización y supresión en función de correos electrónicos con hash.

Puede usar este destino para la segmentación de audiencia en toda la familia [!DNL Facebook’s] de aplicaciones compatibles con [!DNL Custom Audiences], incluidas [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de colocación de [!DNL Facebook Ads Manager].

![Destino de facebook en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL Facebook], estos son dos casos de uso de muestra que los clientes de Adobe Experience Platform pueden resolver mediante esta función.

### Caso de uso número 1

Un comerciante en línea quiere llegar a los clientes existentes a través de plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El comerciante en línea puede ingerir direcciones de correo electrónico desde su propio CRM a Adobe Experience Platform, crear segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a la plataforma social [!DNL Facebook], lo que optimiza su gasto en publicidad.

### Caso de uso n.º 2

Una aerolínea tiene diferentes niveles de clientes (bronce, plata y oro) y desea proporcionar a cada uno de los niveles ofertas personalizadas a través de plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la empresa. Los únicos identificadores que la empresa tiene sobre estos clientes son los ID de pertenencia y las direcciones de correo electrónico.

Para dirigirlos a través de los medios sociales, pueden incorporar los datos de clientes de su CRM a Adobe Experience Platform, utilizando las direcciones de correo electrónico como identificadores.

A continuación, pueden utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de cliente, para crear nuevos segmentos de audiencia a los que pueden dirigirse mediante el destino [!DNL Facebook] .

## Identidades compatibles {#supported-identities}

[!DNL Facebook Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione la identidad objetivo GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Siga las instrucciones de la sección [ID match requirements](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para números de teléfono sin formato y con hash, respectivamente. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [ID match requirements](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para las direcciones de correo electrónico con texto sin formato y con hash, respectivamente. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Tipo de exportación {#export-type}

**Exportación de segmentos** : exporta todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Facebook.

## Requisitos previos de cuenta de facebook {#facebook-account-prerequisites}

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su cuenta de usuario [!DNL Facebook] debe tener el permiso **[!DNL Manage campaigns]** habilitado para la cuenta de anuncio que planea usar.
* La cuenta empresarial de **Adobe Experience Cloud** debe agregarse como socio publicitario en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador empresarial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas**. El permiso es necesario para la integración [!DNL Adobe Experience Platform].
* Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Facebook] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o números de teléfono.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

## Requisitos de hash de número telefónico {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Facebook]:

* **Ingesta de números** de teléfono sin procesar: puede introducir números de teléfono sin procesar en el  [!DNL E.164] formato  [!DNL Platform]. Se colocan automáticamente en hash al activarse. Si elige esta opción, asegúrese de introducir siempre sus números de teléfono sin procesar en el espacio de nombres `Phone_E.164`.
* **Ingesta de números** de teléfono con hash: puede prehash sus números de teléfono antes de ingerirlos a  [!DNL Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en el espacio de nombres `Phone_SHA256`.

>[!NOTE]
>
>Los números de teléfono introducidos en el espacio de nombres `Phone` no se pueden activar en [!DNL Facebook].


## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash sobre las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico claramente en el Experience Platform, y tener [!DNL Platform] hash sobre ellas cuando se activen.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) y la [información general sobre la ingesta de flujo](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios al principio y al final de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al hash de las cadenas de correo electrónico, asegúrese de usar un hash para la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No sal la cadena.

>[!NOTE]
>
>Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.
> Los datos de origen de atributos no se colocan automáticamente en hash. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación.
> La opción **[!UICONTROL Aplicar transformación]** solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir espacios de nombres.

![Transformación de asignación de identidad](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de utilizar el espacio de nombres `Extern_ID` para enviar datos a [!DNL Facebook], asegúrese de sincronizar sus propios identificadores con [!DNL Facebook Pixel]. Consulte la [documentación oficial de Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obtener información detallada.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

El siguiente vídeo también muestra los pasos para configurar un destino [!DNL Facebook] y activar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde la grabación de este vídeo. Para obtener la información más actualizada, consulte el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su  [!DNL Facebook Ad Account ID]. Puede encontrar este ID en su cuenta [!DNL Facebook Ads Manager]. Al introducir este ID, anteponga siempre `act_`.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

En el paso **[!UICONTROL Segment schedule]**, debe proporcionar el [!UICONTROL Origin of audience] al enviar segmentos a [!DNL Facebook Custom Audiences].

![Origen de audiencia de facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Facebook Custom Audience] {#example-facebook}

A continuación se muestra un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Facebook Custom Audience].

Selección de campos de origen:

* Seleccione el espacio de nombres `Email` como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente sobre la ingesta de datos a [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de correo electrónico](#email-hashing-requirements).
* Seleccione el espacio de nombres `PHONE_E.164` como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] realizará un hash de los números de teléfono para cumplir con los  [!DNL Facebook] requisitos.
* Seleccione el espacio de nombres `Phone_SHA256` como identidad de origen si ha hash los números de teléfono sobre la ingesta de datos en [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de números de teléfono](#phone-number-hashing-requirements).
* Seleccione el espacio de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el espacio de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el espacio de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el espacio de nombres `Phone_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `PHONE_E.164` o `Phone_SHA256`.
* Seleccione los espacios de nombres `IDFA` o `GAID` como identidad de destino cuando los espacios de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el espacio de nombres `Extern_ID` como identidad de destino cuando el espacio de nombres de origen sea personalizado.

>[!IMPORTANT]
>
>Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.
> 
>Los datos de origen de atributos no se colocan automáticamente en hash. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación.

![Asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Datos exportados {#exported-data}

Para [!DNL Facebook], una activación correcta significa que se crearía una audiencia personalizada [!DNL Facebook] mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a segmentos en la audiencia se agregaría y eliminaría ya que los usuarios están cualificados o no cumplen los requisitos para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite los rellenos históricos de audiencias. Todas las cualificaciones históricas de segmentos se envían a [!DNL Facebook] al activar los segmentos en el destino.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecta {#bad-request}

Al activar segmentos en [!DNL Facebook], puede recibir el siguiente error:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Este error se produce cuando los clientes utilizan cuentas recién creadas y los permisos [!DNL Facebook] aún no están activos.

Si recibe el mensaje de error `400 Bad Request` después de seguir los pasos en [Requisitos previos de cuenta de Facebook](#facebook-account-prerequisites), permita que entren en vigor unos días para que los permisos de [!DNL Facebook] entren en vigor.