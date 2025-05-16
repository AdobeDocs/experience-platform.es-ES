---
keywords: coincidencia de cliente de google;coincidencia de cliente de Google;coincidencia de cliente de Google
title: Conexión de Google Customer Match
description: Customer Match de Google le permite utilizar sus datos con y sin conexión para llegar a sus clientes y volver a interactuar con ellos en las propiedades de Google y en las que opera, como Search, Shopping y Gmail.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: ce205622260f4252d1a7db7c5011366fb2ed4d3c
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 2%

---

# [!DNL Google Customer Match] conexión

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) y la [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para admitir los requisitos relacionados con el cumplimiento y el consentimiento definidos en la [Ley de Mercados Digitales](https://digital-markets-act.ec.europa.eu/index_es) (DMA) de la Unión Europea ([Política de consentimiento del Usuario de la UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según la DMA en la Unión Europea.
><br/>
>Los clientes que hayan adquirido Adobe Privacy &amp; Security Shield y hayan configurado una [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos no tienen que realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar las funciones de [definición de segmento](../../../segmentation/home.md#segment-definitions) de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos y así poder seguir utilizando los destinos de Real-Time CDP Google existentes sin interrupción.

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) le permite usar sus datos con y sin conexión para llegar a sus clientes y volver a interactuar con ellos en las propiedades de Google que posee y opera, como: [!DNL Search], [!DNL Shopping] y [!DNL Gmail].

>[!TIP]
>
>Para llegar a los clientes en el inventario [!DNL YouTube], usa el destino [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), que usa la API de Google Audience Partner.

![Destino de Google Customer Match en la interfaz de usuario de Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL Google Customer Match], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

### Caso de uso #1

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM a Experience Platform y crear audiencias a partir de sus propios datos sin conexión. A continuación, puede enviar estas audiencias a [!DNL Google Customer Match] para que las usen en [!DNL Search] y [!DNL Shopping], con lo que se optimiza el gasto en publicidad.

### Caso de uso #2

>[!TIP]
>
>Para ejecutar este caso de uso en el inventario [!DNL YouTube], use el nuevo destino [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), que usa la API de Google Audience Partner.

Una destacada compañía tecnológica lanzó un nuevo teléfono. Para promocionar este nuevo modelo de teléfono, buscan concienciar sobre las nuevas funciones y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico desde su base de datos de CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Las audiencias se crean en función de los clientes que poseen modelos de teléfono más antiguos. A continuación, las audiencias se envían a [!DNL Google Customer Match] para que la compañía pueda dirigirse a los clientes actuales, los clientes que poseen modelos de teléfono antiguos y los clientes similares de [!DNL YouTube].

## Gobernanza de datos para [!DNL Google Customer Match] destinos {#data-governance}

Algunos destinos de Experience Platform tienen ciertas reglas y obligaciones para los datos enviados a la plataforma de destino o recibidos de ella. Usted es responsable de comprender las limitaciones y obligaciones de sus datos y de cómo los utiliza en Adobe Experience Platform y en la plataforma de destino. Adobe Experience Platform proporciona herramientas de control de datos para ayudarle a administrar algunas de estas obligaciones de uso de datos. [Más información](../../../data-governance/labels/overview.md) acerca de las herramientas y directivas de control de datos.

## Identidades admitidas {#supported-identities}

[!DNL Google Customer Match] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres GAID. |
| `IDFA` | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| `phone_sha256_e.164` | Números de teléfono en formato E164, con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para números de teléfono con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| `email_lc_sha256` | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para direcciones de correo electrónico de texto sin formato y con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| `user_id` | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |
| `address_info_first_name` | Nombre del usuario | Esta identidad de destino debe usarse junto con `address_info_last_name`, `address_info_country_code` y `address_info_postal_code` cuando desee enviar datos de direcciones de correo a su destino. <br><br>Para asegurarse de que Google coincida con la dirección, debe asignar los cuatro campos de dirección (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`) y asegurarse de que ninguno de estos campos contiene datos ausentes en los perfiles exportados. <br> Si algún campo no está asignado o contiene datos que faltan, Google no coincidirá con la dirección. |
| `address_info_last_name` | Apellidos del usuario | Esta identidad de destino debe usarse junto con `address_info_first_name`, `address_info_country_code` y `address_info_postal_code` cuando desee enviar datos de direcciones de correo a su destino. <br><br>Para asegurarse de que Google coincida con la dirección, debe asignar los cuatro campos de dirección (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`) y asegurarse de que ninguno de estos campos contiene datos ausentes en los perfiles exportados. <br> Si algún campo no está asignado o contiene datos que faltan, Google no coincidirá con la dirección. |
| `address_info_country_code` | Código de país de dirección de usuario | Esta identidad de destino debe usarse junto con `address_info_first_name`, `address_info_last_name` y `address_info_postal_code` cuando desee enviar datos de direcciones de correo a su destino. <br><br>Para asegurarse de que Google coincida con la dirección, debe asignar los cuatro campos de dirección (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`) y asegurarse de que ninguno de estos campos contiene datos ausentes en los perfiles exportados. <br> Si algún campo no está asignado o contiene datos que faltan, Google no coincidirá con la dirección. <br><br>Formato aceptado: códigos de país en minúsculas y de 2 letras en formato [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| `address_info_postal_code` | Código postal de la dirección de usuario | Esta identidad de destino debe usarse junto con `address_info_first_name`, `address_info_last_name` y `address_info_country_code` cuando desee enviar datos de direcciones de correo a su destino. <br><br>Para asegurarse de que Google coincida con la dirección, debe asignar los cuatro campos de dirección (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`) y asegurarse de que ninguno de estos campos contiene datos ausentes en los perfiles exportados. <br> Si algún campo no está asignado o contiene datos que faltan, Google no coincidirá con la dirección. |

{style="table-layout:auto"}

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
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono y otros) utilizados en el destino [!DNL Google Customer Match]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] requisitos previos de cuenta {#google-account-prerequisites}

Antes de configurar un destino [!DNL Google Customer Match] en Experience Platform, asegúrese de leer y cumplir la directiva de Google para usar [!DNL Customer Match], descrita en [Documentación de asistencia de Google](https://support.google.com/google-ads/answer/6299717).

A continuación, asegúrese de que su cuenta de [!DNL Google] esté configurada para un nivel de permisos de [!DNL Standard] o superior. Consulte la [documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.

### Lista de permitidos {#allowlist}

Antes de crear el destino [!DNL Google Customer Match] en Experience Platform, asegúrese de que su cuenta de [!DNL Google Ads] cumpla con la [[!DNL Google Customer Match] directiva](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Google incluida en la lista de permitidos automáticamente a los clientes con cuentas compatibles.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Google] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias activadas en [!DNL Google Customer Match] pueden tener claves de *identificadores hash*, como direcciones de correo electrónico o números de teléfono.

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes.

### Requisitos de hash de número de teléfono {#phone-number-hashing-requirements}

Hay dos métodos para activar números de teléfono en [!DNL Google Customer Match]:

* **Ingesta de números de teléfono sin procesar**: puede ingerir números de teléfono sin procesar con el formato [!DNL E.164] en [!DNL Experience Platform] y se aplicarán automáticamente hash a la activación. Si elige esta opción, asegúrese de introducir siempre los números de teléfono sin procesar en el área de nombres `Phone_E.164`.
* **Ingesta de números de teléfono con hash**: puede prehash sus números de teléfono antes de ingerirlos en [!DNL Experience Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en el área de nombres `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Los números de teléfono introducidos en el área de nombres `Phone` no se pueden activar en [!DNL Google Customer Match].

### Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede usar las direcciones de correo electrónico en borrar en Experience Platform y hacer que [!DNL Experience Platform] las hash en la activación.

Para obtener más información sobre los requisitos de hash de Google y otras restricciones en la activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] con número de teléfono](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] con ID de dispositivos móviles](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [descripción general de la ingesta por lotes](../../../ingestion/batch-ingestion/overview.md) y la [descripción general de la ingesta por transmisión](../../../ingestion/streaming-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google descritos en los vínculos anteriores.

### Requisitos de hash de campo de dirección {#address-field-hashing}

Al asignar campos relacionados con direcciones a [!DNL Google Customer Match], Experience Platform **agrega automáticamente valores hash a** de los valores `address_info_first_name` y `address_info_last_name` antes de enviarlos a Google. Este hash automático es necesario para cumplir con los requisitos de seguridad y privacidad de Google.

**no** proporciona valores prehash para `address_info_first_name` o `address_info_last_name`. Si proporciona valores con hash, el proceso de coincidencia fallará.

### Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de poder usar el área de nombres `User_ID` para enviar datos a Google, asegúrese de sincronizar sus propios identificadores con [!DNL gTag]. Consulte la [documentación oficial de Google](https://support.google.com/google-ads/answer/9199250) para obtener información detallada.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Vídeo introductorio {#video-overview}

Vea el siguiente vídeo para obtener una explicación de las ventajas y cómo activar los datos en Customer Match de Google.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: proporcione un nombre para esta conexión de destino
* **[!UICONTROL Descripción]**: proporcione una descripción para esta conexión de destino
* **[!UICONTROL ID de cuenta]**: su [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). El formato del ID es xxx-xxx-xxxx. Si está usando [!DNL Google Ads Manager Account (My Client Center)], no use su identificador de cuenta de responsable. En su lugar, use el [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en).

>[!IMPORTANT]
>
> * La acción de marketing **[!UICONTROL Combinar con PII]** está seleccionada de forma predeterminada para el destino [!DNL Google Customer Match] y no se puede quitar.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades* a destinos, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de [Ver gráfico de identidad]**. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso **[!UICONTROL Programación de segmentos]**, debe proporcionar el [!UICONTROL ID de aplicación] al enviar audiencias [!DNL IDFA] o [!DNL GAID] a [!DNL Google Customer Match].

![Campo de ID de aplicación Customer Match de Google resaltado en el paso de programación del segmento del flujo de trabajo de activación.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obtener más información sobre cómo encontrar [!DNL App ID], consulte la [documentación oficial de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) o pregunte a su representante de Google.

### Ejemplo de asignación: activar datos de audiencia en [!DNL Google Customer Match] {#example-gcm}

Este es un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Google Customer Match].

Selección de campos de origen:

* Seleccione el área de nombres `Email` como identidad de origen si las direcciones de correo electrónico que está utilizando no tienen hash.
* Seleccione el área de nombres `Email_LC_SHA256` como identidad de origen si ha creado un hash de las direcciones de correo electrónico de los clientes al ingerir datos en [!DNL Experience Platform], de acuerdo con [!DNL Google Customer Match] [los requisitos de hash de correo electrónico](#hashing-requirements).
* Seleccione el área de nombres `PHONE_E.164` como identidad de origen si los datos constan de números de teléfono sin hash. [!DNL Experience Platform] hará un hash de los números de teléfono para cumplir con los requisitos de [!DNL Google Customer Match].
* Seleccione el área de nombres `Phone_SHA256_E.164` como identidad de origen si ha creado valores hash de números de teléfono en la ingesta de datos en [!DNL Experience Platform], de acuerdo con [!DNL Facebook] [los requisitos de hash de números de teléfono](#phone-number-hashing-requirements).
* Seleccione el área de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el área de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el área de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el área de nombres `Email_LC_SHA256` como identidad de destino cuando las áreas de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el área de nombres `Phone_SHA256_E.164` como identidad de destino cuando las áreas de nombres de origen sean `PHONE_E.164` o `Phone_SHA256_E.164`.
* Seleccione las áreas de nombres `IDFA` o `GAID` como identidad de destino cuando las áreas de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el área de nombres `User_ID` como identidad de destino cuando el área de nombres de origen sea personalizada.

![Asignación de identidad entre los campos de origen y destino mostrados en el paso Asignación del flujo de trabajo de activación.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

[!DNL Experience Platform] crea automáticamente un hash de los datos de las áreas de nombres sin hash tras la activación.

Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación.

![Aplicar control de transformación resaltado en el paso Asignación del flujo de trabajo de activación.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Supervisar destino {#monitor-destination}

Después de conectarse al destino y establecer un flujo de datos de destino, puede usar la [funcionalidad de supervisión](/help/dataflows/ui/monitor-destinations.md) en Real-Time CDP para obtener información detallada acerca de los registros de perfil activados en el destino en cada ejecución de flujo de datos.

>[!IMPORTANT]
>
>Al asignar las cuatro identidades de destino relacionadas con direcciones (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` y `address_info_postal_code`), se cuentan como identidades individuales independientes para cada perfil en la página de supervisión del flujo de datos.

## Compruebe que la activación de la audiencia se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambia a tu cuenta de **[!UICONTROL Google Ads]**. Las audiencias activadas se muestran en su cuenta de Google como listas de clientes. Según el tamaño de la audiencia, algunas audiencias no se rellenan a menos que haya más de 100 usuarios activos para ofrecer.

Al asignar una audiencia a [!DNL IDFA] y [!DNL GAID] ID móviles, [!DNL Google Customer Match] crea una audiencia independiente para cada asignación de ID. Su cuenta de [!DNL Google Ads] muestra dos segmentos diferentes, uno para [!DNL IDFA] y otro para la asignación de [!DNL GAID].

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen los [requisitos previos](#google-account-prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta esté incluida en la lista de permitidos y configurada para un nivel de permisos de [!DNL Standard] o superior. Consulte la [documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.