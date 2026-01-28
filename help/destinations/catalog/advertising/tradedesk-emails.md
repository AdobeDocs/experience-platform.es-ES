---
title: La conexión de Trade Desk con CRM
description: Active los perfiles en su cuenta de Trade Desk para la segmentación y supresión de audiencias en función de los datos de CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# La conexión [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Hay dos destinos de CRM de The Trade Desk en el [catálogo de destinos](/help/destinations/catalog/overview.md).
>
>* Si obtiene datos en la UE, use el destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Si obtiene datos en las regiones APAC o NAMER, utilice el destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>El equipo *[!DNL Trade Desk]* crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese con su representante de [!DNL Trade Desk].

## Información general {#overview}

Descubra cómo puede activar perfiles en su cuenta de [!DNL Trade Desk] para la segmentación y supresión de audiencias en función de los datos de CRM.

Este conector envía datos a [!DNL The Trade Desk] para la activación de datos de origen. [!DNL The Trade Desk] almacena sus correos electrónicos y números de teléfono sin procesar (sin hash).

>[!TIP]
>
>Utilice el destino [!DNL The Trade Desk - CRM] para enviar datos de CRM (como correos electrónicos y números de teléfono) y otros identificadores de datos de origen, como cookies e ID de dispositivo. Puede seguir usando el [destino de Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) en el catálogo de Experience Platform para las cookies y las asignaciones de ID de dispositivo.

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Antes de activar audiencias en Trade Desk, debe ponerse en contacto con el administrador de cuentas de [!DNL Trade Desk] para habilitar la función. Si está enviando correos electrónicos, números de teléfono y UID2/EUID, debe compartir el acuerdo firmado de UID2/EUID con [!DNL The Trade Desk].

## Requisitos de coincidencia de ID {#id-matching-requirements}

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes. Lea la [descripción general del área de nombres de identidad](/help/identity-service/features/namespaces.md) para obtener más información.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

Adobe Experience Platform admite direcciones de correo electrónico y números de teléfono sin hash y con hash. Siga las instrucciones de la sección Requisitos de coincidencia de ID y utilice los espacios de nombres adecuados para las direcciones de correo electrónico de texto sin formato y con hash, respectivamente.

| Identidad de destino | Descripción |
|---|---|
| Correo electrónico | Direcciones de correo electrónico (texto no cifrado) |
| Email_LC_SHA256 | Las direcciones de correo electrónico deben tener un cifrado hash con SHA256 y estar en minúsculas. No podrá cambiar esta configuración más adelante. |
| Teléfono (E.164) | Números de teléfono que deben normalizarse en formato E.164. El formato E.164 incluye un signo más (+), un código de llamada de país internacional, un código de área local y un número de teléfono. Por ejemplo: (+)(código de país)(código de área)(número de teléfono). Este identificador no está disponible para Trade Desk - First-Party Data (EU). |
| Teléfono (SHA256_E.164) | Números de teléfono que ya se han normalizado al formato E.164 y luego se han cifrado mediante hash mediante SHA-256, con el hash resultante codificado en Base64. Este identificador no está disponible para Trade Desk - First-Party Data (EU). |
| TDID | ID de cookie en Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple ID para anunciantes |
| UID2 | El valor UID2 sin procesar |
| UID2Token | El token de UID2 cifrado, también conocido como token de publicidad. |
| EUID | El valor de ID de la Unión Europea sin procesar |
| EUIDToken | El token de EUID cifrado, también conocido como token de publicidad. |
| RampID | El RampID de 49 o 70 caracteres (anteriormente conocido como IdentityLink o IDL). Debe ser un RampID de LiveRamp asignado específicamente para Trade Desk. |
| netID | El netID del usuario como una cadena de 70 caracteres codificada en Base64. Este ID solo es compatible en Europa. |
| FirstID | First-id del usuario, una cookie de origen que suelen configurar los editores en Francia. Este ID solo es compatible en Europa. |

{style="table-layout:auto"}

## Requisitos de hash de correo electrónico {#email-hashing}

Puede hash las direcciones de correo electrónico antes de introducirlas en Adobe Experience Platform o utilizar direcciones de correo electrónico sin procesar.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, lea la [descripción general de la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Elimine los espacios iniciales y finales.
* Convierta todos los caracteres ASCII a minúsculas.
* En `gmail.com` direcciones de correo electrónico, elimine los siguientes caracteres de la parte de nombre de usuario de la dirección de correo electrónico:

      * El punto (`.`) (código ASCII 46). Por ejemplo, normalice &quot;jane.doe@gmail.com&quot; a &quot;janedoe@gmail.com&quot;.
     * El carácter de signo más (`+`) (código ASCII 43) y todos los caracteres posteriores. Por ejemplo, normalice &quot;janedoe+home@gmail.com&quot; a &quot;janedoe@gmail.com&quot;.
  

## Normalización de números de teléfono y requisitos de hash {#phone-hashing}

Esto es lo que debe saber acerca de cargar números de teléfono:

* Debe normalizar los números de teléfono antes de enviarlos en una solicitud, independientemente de si los envía con hash o sin hash en una solicitud.
* Para cargar datos normalizados, con hash y codificados, debe enviar los números de teléfono como hashes SHA-256 con codificación Base64 de los números de teléfono normalizados.

Tanto si desea cargar números de teléfono sin procesar como con hash, debe normalizarlos.

>[!IMPORTANT]
>
>La normalización antes del hash garantiza que el valor del ID generado siempre sea el mismo y que los datos puedan coincidir con precisión.

Esto es lo que debe saber acerca de los requisitos de normalización de números de teléfono:

* UID2 Operator acepta números de teléfono en formato E.164, que es el formato de número de teléfono internacional que garantiza la exclusividad global.
* Los números de teléfono E.164 pueden tener un máximo de 15 dígitos.
* Los números de teléfono E.164 normalizados utilizan la siguiente sintaxis: `[+][country code][subscriber number including area code]` sin espacios, guiones, paréntesis u otros caracteres especiales. A continuación se muestran algunos ejemplos:

      * EE.UU.: 1 (234) 567-8901 está normalizado a +12345678901.
     * Singapur: 65 1243 5678 está normalizado a +6512345678.
     * Australia: el número de teléfono móvil 0491 570 006 está normalizado para agregar el código de país y soltar el cero a la izquierda: +61491570006.
     * Reino Unido: el número de teléfono móvil 07812 345678 está normalizado para agregar el código de país y soltar el cero a la izquierda: +447812345678.
  
Asegúrese de que el número de teléfono normalizado es UTF-8, no otro sistema de codificación como UTF-16.

Un hash de número de teléfono es un hash SHA-256 cifrado en Base64 de un número de teléfono normalizado. El número de teléfono primero se normaliza, luego se crea un hash con el algoritmo hash SHA-256 y, a continuación, los bytes resultantes del valor hash se codifican con la codificación Base64. Tenga en cuenta que la codificación Base64 se aplica a los bytes del valor hash, no a la representación de cadena con codificación hexadecimal.
En la tabla siguiente se muestra un ejemplo de un número de teléfono de entrada simple y el resultado a medida que se aplica cada paso para llegar a un valor seguro y opaco.

| Tipo | Ejemplo | Comentarios y uso |
|---|---|---|
| Número de teléfono sin procesar | 1 (234) 567-8901 | Este es el punto de partida. |
| Número de teléfono normalizado | +12345678901 | La normalización es siempre el primer paso. |
| Hash SHA-256 del número de teléfono normalizado | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Esta cadena de 64 caracteres es una representación con codificación hexadecimal del SHA-256 de 32 bytes. |
| Codificación Hex a Base64 SHA-256 del número de teléfono normalizado y con hash | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | Esta cadena de 44 caracteres es una representación con codificación Base64 del SHA-256 de 32 bytes. El hash SHA-256 es un valor hexadecimal. Debe utilizar un codificador Base64 que tome un valor hexadecimal como entrada. Utilice esta codificación para los valores phone_hash enviados en el cuerpo de la solicitud. |

>[!IMPORTANT]
>
>Al aplicar la codificación Base64, asegúrese de utilizar una función que tome un valor hexadecimal como entrada. Si utiliza una función que toma texto como entrada, el resultado es una cadena más larga que no es válida a efectos de UID2.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de la oficina de comercio. |
| Frecuencia de exportación | **[!UICONTROL Daily Batch]** | Como el perfil se actualiza en Experience Platform en función de la evaluación de audiencias, el perfil (las identidades) se actualiza una vez al día de forma descendente a la plataforma de destino. Más información sobre [exportaciones por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

### Autenticar en Destino {#authenticate}

[!DNL The Trade Desk] El destino de CRM es una carga de archivo por lotes diaria y no requiere autenticación por parte del usuario.

### Rellene los detalles del destino {#fill-in-details}

Para poder enviar o activar datos de audiencia a un destino, debe configurar una conexión con su propia plataforma de destino. Mientras [configura](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Account Type]**: Elija la opción **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Advertiser ID]**: su [!DNL Trade Desk Advertiser ID], que puede compartir el administrador de cuentas de [!DNL Trade Desk] o encontrarse en [!DNL Advertiser Preferences] en la interfaz de usuario de [!DNL Trade Desk].

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra cómo rellenar los detalles de destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Al conectarse al destino, la configuración de una directiva de control de datos es completamente opcional. Consulte la [descripción general del control de datos](/help/data-governance/policies/overview.md) de Experience Platform para obtener más información.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en un destino.

En la página **[!UICONTROL Scheduling]**, puede configurar la programación y los nombres de archivo para cada audiencia que esté exportando. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

![Captura de pantalla de la IU de Experience Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todas las audiencias activadas en [!DNL The Trade Desk] destino de CRM se establecen automáticamente en una frecuencia diaria y exportación de archivos completa.

![Captura de pantalla de la IU de Experience Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

En la página **[!UICONTROL Mapping]**, debe seleccionar atributos o áreas de nombres de identidad de la columna de origen y asignarlos a la columna de destino.

![Captura de pantalla de la IU de Experience Platform para asignar la activación de audiencia.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

A continuación se muestra un ejemplo de asignación de identidad correcta al activar audiencias en [!DNL The Trade Desk] destino de CRM.

Selección de los campos de origen y destino:

| Campo de origen | Campo de destino |
|---|---|
| Correo electrónico | correo electrónico |
| Email_LC_SHA256 | hashed_email |
| Teléfono (E.164) | phone |
| Teléfono (SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | papa |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| RampID | ralentí |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Validar exportación de datos {#validate}

Para validar que los datos se exportan correctamente desde Experience Platform a [!DNL The Trade Desk], busque las audiencias en la pestaña Adobe 1PD en la biblioteca [!DNL The Trade Desk] &quot;Datos del anunciante e identidad&quot;. Estos son los pasos para encontrar el ID correspondiente en la interfaz de usuario de [!DNL Trade Desk]:

1. Primero, seleccione la ficha **[!UICONTROL Libraries]** y revise la sección **[!UICONTROL Advertiser data and identity]**.
2. Haga clic en **[!UICONTROL Adobe 1PD]** y se enumerarán todas las audiencias activadas para [!DNL The Trade Desk].
3. El nombre del segmento o el ID del segmento de Experience Platform aparecerán como el nombre del segmento en la interfaz de usuario de [!DNL Trade Desk].

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
