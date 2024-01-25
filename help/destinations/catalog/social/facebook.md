---
keywords: conexión de facebook;conexión de facebook;destinos de facebook;facebook;instagram;messenger;facebook messenger
title: Conexión de facebook
description: Active perfiles para sus campañas de Facebook para la segmentación, personalización y supresión de audiencias en función de los correos electrónicos con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 7%

---

# [!DNL Facebook] conexión

## Información general {#overview}

Activar perfiles para su [!DNL Facebook] campañas de segmentación, personalización y supresión de audiencias basadas en correos electrónicos con hash.

Puede utilizar este destino para la segmentación de audiencias en [!DNL Facebook's] familia de aplicaciones compatibles con [!DNL Custom Audiences], incluido [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de colocación de [!DNL Facebook Ads Manager].

![Destino facebook en la interfaz de usuario de Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo usar el [!DNL Facebook] Destino: estos son dos casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

### Caso de uso #1

Un minorista en línea quiere llegar a los clientes existentes a través de plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El minorista en línea puede introducir direcciones de correo electrónico de su propio CRM a Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Facebook] plataforma social, optimizando su gasto en publicidad.

### Caso de uso #2

Una aerolínea tiene diferentes niveles de clientes (Bronce, Plata y Oro) y desea proporcionar a cada uno de los niveles ofertas personalizadas a través de plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la compañía. Los únicos identificadores que la compañía tiene sobre estos clientes son ID de miembros y direcciones de correo electrónico.

Para dirigirlos a todos los medios sociales, pueden incorporar los datos de clientes de su CRM a Adobe Experience Platform, utilizando las direcciones de correo electrónico como identificadores.

A continuación, puede utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de clientes, para crear nuevas audiencias a las que dirigirse a través de [!DNL Facebook] destino.

## Identidades admitidas {#supported-identities}

[!DNL Facebook Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Siga las instrucciones de la [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice las áreas de nombres adecuadas para números de teléfono con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para las direcciones de correo electrónico con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Facebook. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos de cuenta de facebook {#facebook-account-prerequisites}

Antes de enviar las audiencias a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su [!DNL Facebook] La cuenta de usuario de debe tener acceso completo a [!DNL Facebook Business Account] que posee la cuenta publicitaria que está utilizando.
* Su [!DNL Facebook] la cuenta de usuario debe tener el **[!DNL Manage campaigns]** permiso habilitado para la cuenta de Ad que planea usar.
* El **Adobe Experience Cloud** La cuenta comercial de debe añadirse como socio de publicidad en su [!DNL Facebook Ad Account]. Utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
  >[!IMPORTANT]
  >
  > Al configurar los permisos para Adobe Experience Cloud, debe habilitar la variable **Administración de campañas** permiso. Se requiere el permiso para el [!DNL Adobe Experience Platform] integración.
* Lea y firme el [!DNL Facebook Custom Audiences] Condiciones del servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >Al firmar el [!DNL Facebook Custom Audiences] Condiciones del servicio, asegúrese de utilizar la misma cuenta de usuario que utilizó para autenticarse en la API de Facebook.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Facebook] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL Facebook] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes.

## Requisitos de hash de número de teléfono {#phone-number-hashing-requirements}

Existen dos métodos para activar números de teléfono en [!DNL Facebook]:

* **Ingesta de números de teléfono sin procesar**: puede introducir números de teléfono sin procesar en el [!DNL E.164] formatear en [!DNL Platform]. Se colocan automáticamente en el hash tras la activación. Si elige esta opción, asegúrese de introducir siempre los números de teléfono sin procesar en la `Phone_E.164` namespace.
* **Ingesta de números de teléfono con hash**: puede precifrar los números de teléfono antes de ingerirlos en [!DNL Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en la `Phone_SHA256` namespace.

>[!NOTE]
>
>Números de teléfono introducidos en `Phone` el área de nombres no se puede activar en [!DNL Facebook].

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico en borrar en Experience Platform, y tener [!DNL Platform] hash en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [introducción a la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) y el [información general sobre ingesta de streaming](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recortar todos los espacios iniciales y finales de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al crear valores hash de las cadenas de correo electrónico, asegúrese de usar la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No salar la cuerda.

>[!NOTE]
>
>Los datos de áreas de nombres sin hash se cifran automáticamente en hash mediante [!DNL Platform] tras la activación.
> Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación.
> El **[!UICONTROL Aplicar transformación]** Esta opción solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir áreas de nombres.

![Aplique el control de transformación resaltado en el paso de asignación.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de usar el `Extern_ID` área de nombres a la que enviar datos [!DNL Facebook], asegúrese de sincronizar sus propios identificadores mediante [!DNL Facebook Pixel]. Consulte la [Documentación oficial de facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obtener información detallada.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

El siguiente vídeo también muestra los pasos para configurar una [!DNL Facebook] Destino y activación de audiencias.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde que se grabó este vídeo. Para obtener la información más actualizada, consulte la [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticarse en el destino {#authenticate}

1. Busque el destino de Facebook en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccionar **[!UICONTROL Conectar con destino]**.
   ![Paso Autenticar en Facebook mostrado en el flujo de trabajo de activación.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Introduzca sus credenciales de Facebook y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID de cuenta"
>abstract="Su ID de cuenta de Facebook Ad. Puede encontrar este ID en su cuenta de Facebook Ads Manager. Al introducir este ID, utilice siempre como prefijo `act_`."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL Facebook Ad Account ID]. Puede encontrar este ID en su [!DNL Facebook Ads Manager] cuenta. Al introducir este ID, utilice siempre como prefijo `act_`.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origen del público"
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
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el **[!UICONTROL Programación de segmentos]** paso, debe proporcionar el [!UICONTROL Origen de la audiencia] al enviar audiencias a [!DNL Facebook Custom Audiences].

![El origen del menú desplegable de Audiencia se muestra en el paso de activación de Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Facebook Custom Audience] {#example-facebook}

A continuación se muestra un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Facebook Custom Audience].

Selección de campos de origen:

* Seleccione el `Email` área de nombres como identidad de origen si las direcciones de correo electrónico que utiliza no tienen un hash.
* Seleccione el `Email_LC_SHA256` área de nombres como identidad de origen si ha creado un hash de las direcciones de correo electrónico del cliente al ingerir datos en [!DNL Platform], según [!DNL Facebook] [requisitos de hash de correo electrónico](#email-hashing-requirements).
* Seleccione el `PHONE_E.164` área de nombres como identidad de origen si los datos constan de números de teléfono sin hash. [!DNL Platform] hará un hash de los números de teléfono para cumplir con [!DNL Facebook] requisitos.
* Seleccione el `Phone_SHA256` área de nombres como identidad de origen si ha creado un hash de los números de teléfono al ingerir datos en [!DNL Platform], según [!DNL Facebook] [requisitos hash de número de teléfono](#phone-number-hashing-requirements).
* Seleccione el `IDFA` área de nombres como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivos.
* Seleccione el `GAID` área de nombres como identidad de origen si los datos constan de [!DNL Android] ID de dispositivos.
* Seleccione el `Custom` área de nombres como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el `Email_LC_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `Email` o `Email_LC_SHA256`.
* Seleccione el `Phone_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `PHONE_E.164` o `Phone_SHA256`.
* Seleccione el `IDFA` o `GAID` áreas de nombres como identidad de destino cuando las áreas de nombres de origen `IDFA` o `GAID`.
* Seleccione el `Extern_ID` área de nombres como identidad de destino cuando el área de nombres de origen es personalizada.

>[!IMPORTANT]
>
>Los datos de áreas de nombres sin hash se cifran automáticamente en hash mediante [!DNL Platform] tras la activación.
> 
>Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación.

![Aplique el control de transformación resaltado en el paso de asignación.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Datos exportados {#exported-data}

Para [!DNL Facebook], una activación correcta significa que una [!DNL Facebook] la audiencia personalizada se crearía mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a audiencias se añadiría y eliminaría a medida que los usuarios se calificaran o descalificaran para las audiencias activadas.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite rellenos de audiencia históricos. Todas las cualificaciones de audiencia históricas se envían a [!DNL Facebook] al activar las audiencias en el destino.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Este error se produce cuando los clientes utilizan cuentas de nueva creación y la variable [!DNL Facebook] Los permisos de aún no están activos.

Si recibe el `400 Bad Request` mensaje de error después de seguir los pasos indicados en [Requisitos previos de cuenta de facebook](#facebook-account-prerequisites), espere unos días para el [!DNL Facebook] permisos para que entren en vigor.
