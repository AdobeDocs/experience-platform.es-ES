---
keywords: coincidencia de clientes de google;coincidencia de clientes de Google;coincidencia de clientes de Google
title: Conexión Google Customer Match
description: Google Customer Match le permite utilizar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades que Google posee y gestiona, como Search, Shopping, Gmail y YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: b189f1b0fe29ebefb3cba9c4f820022a772ce297
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---

# [!DNL Google Customer Match] connection

## Información general {#overview}

[Coincidencia de clientes de Google](https://support.google.com/google-ads/answer/6379332?hl=en) permite utilizar los datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades que posee y gestiona Google, como: [!DNL Search], [!DNL Shopping], [!DNL Gmail]y [!DNL YouTube].

![Destino de coincidencia del cliente de Google en la interfaz de usuario de Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo usar la variable [!DNL Google Customer Match] destino, estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver mediante esta función.

### Caso de uso número 1

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM al Experience Platform y generar segmentos a partir de sus propios datos sin conexión. A continuación, pueden enviar estos segmentos a [!DNL Google Customer Match] para su uso en [!DNL Search] y [!DNL Shopping], optimizando su gasto en publicidad.

### Caso de uso n.º 2

Una destacada compañía tecnológica lanzó un nuevo teléfono. Para promocionar este nuevo modelo de teléfono, buscan sensibilizar sobre las nuevas funciones y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico de su base de datos CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Los segmentos se crean en función de los clientes que poseen modelos de teléfono más antiguos. A continuación, los segmentos se envían a [!DNL Google Customer Match], de modo que la empresa pueda dirigirse a los clientes actuales, a los clientes que poseen modelos de teléfono antiguos y a clientes similares en [!DNL YouTube].

## Control de datos para [!DNL Google Customer Match] destinos {#data-governance}

Algunos destinos en Experience Platform tienen ciertas reglas y obligaciones para los datos enviados a la plataforma de destino o recibidos de ella. Usted es el responsable de comprender las limitaciones y obligaciones de sus datos y cómo utiliza esos datos en Adobe Experience Platform y en la plataforma de destino. Adobe Experience Platform proporciona herramientas de control de datos para ayudarle a administrar algunas de esas obligaciones de uso de datos. [Más información](../../../data-governance/labels/overview.md) acerca de las herramientas y políticas de control de datos.

## Identidades compatibles {#supported-identities}

[!DNL Google Customer Match] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256_e.164 | Números de teléfono en formato E164, con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para los números de teléfono sin formato y con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para el texto sin formato y las direcciones de correo electrónico con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| user_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono y otros) utilizados en la variable [!DNL Google Customer Match] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] requisitos previos de la cuenta {#google-account-prerequisites}

Antes de configurar un [!DNL Google Customer Match] destino en Experience Platform, asegúrese de leer y cumplir la directiva de Google para usar [!DNL Customer Match], descritos en la sección [Documentación de asistencia de Google](https://support.google.com/google-ads/answer/6299717).

A continuación, asegúrese de que su [!DNL Google] la cuenta está configurada para un [!DNL Standard] o nivel de permiso superior. Consulte la [Documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.

### Lista de permitidos {#allowlist}

Antes de crear la variable [!DNL Google Customer Match] destino en Experience Platform, asegúrese de que su [!DNL Google Ads] la cuenta cumple con el [Política de coincidencias de clientes de Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Google permite automáticamente a los clientes con cuentas compatibles aparecer en la lista.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Google] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Google Customer Match] se puede desactivar *hash* identificadores, como direcciones de correo electrónico o números de teléfono.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

### Requisitos de hash de número telefónico {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Google Customer Match]:

* **Ingesta de números de teléfono sin procesar**: puede ingerir números de teléfono sin procesar en la [!DNL E.164] formatear en [!DNL Platform]y se colocan automáticamente en hash al activarlos. Si elige esta opción, asegúrese de introducir siempre sus números de teléfono sin procesar en la `Phone_E.164` espacio de nombres.
* **Ingesta de números de teléfono con hash**: puede prehash sus números de teléfono antes de ingerirlos a [!DNL Platform]. Si elige esta opción, asegúrese de ingerir siempre sus números de teléfono con hash en la variable `PHONE_SHA256_E.164` espacio de nombres.

>[!NOTE]
>
>Números de teléfono introducidos en la variable `Phone` el espacio de nombres no se puede activar en [!DNL Google Customer Match].

### Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform o utilizar las direcciones de correo electrónico claramente en Experience Platform, y [!DNL Platform] Hágalos en la activación.

Para obtener más información sobre los requisitos hash de Google y otras restricciones en la activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Customer Match con número de teléfono](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Coincidencia de cliente con ID de dispositivos móviles](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta de lotes](../../../ingestion/batch-ingestion/overview.md) y [información general sobre la ingesta de transmisión](../../../ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google descritos en los vínculos anteriores.

### Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de usar la variable `User_ID` espacio de nombres para enviar datos a Google, asegúrese de sincronizar sus propios identificadores mediante [!DNL gTag]. Consulte la [Documentación oficial de Google](https://support.google.com/google-ads/answer/9199250) para obtener información detallada.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: proporcionar un nombre para esta conexión de destino
* **[!UICONTROL Descripción]**: proporcionar una descripción para esta conexión de destino
* **[!UICONTROL ID de cuenta]**: your [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). El formato del ID es xxx-xxx-xxxx. Si está utilizando la variable [!DNL Google Ads Manager Account (My Client Center)], no use su ID de cuenta de administrador. Utilice la variable [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en) en su lugar.

>[!IMPORTANT]
>
> * La variable **[!UICONTROL Combinación con PII]** la acción de marketing está seleccionada de forma predeterminada para la variable [!DNL Google Customer Match] destino y no se pueden eliminar.


### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

En el **[!UICONTROL Programación de segmentos]** paso, debe proporcionar la variable [!UICONTROL ID de la aplicación] al enviar [!DNL IDFA] o [!DNL GAID] segmentos a [!DNL Google Customer Match].

![ID de aplicación de Google Customer Match](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obtener más información sobre cómo encontrar la variable [!DNL App ID], consulte [Documentación oficial de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Google Customer Match] {#example-gcm}

Este es un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Google Customer Match].

Selección de campos de origen:

* Seleccione el `Email` área de nombres como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el `Email_LC_SHA256` área de nombres como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente en la ingesta de datos en [!DNL Platform], según [!DNL Google Customer Match] [requisitos de hash de correo electrónico](#hashing-requirements).
* Seleccione el `PHONE_E.164` área de nombres como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] hash de los números de teléfono con los que cumplir [!DNL Google Customer Match] requisitos.
* Seleccione el `Phone_SHA256_E.164` área de nombres como identidad de origen si ha hash los números de teléfono en la ingesta de datos en [!DNL Platform], según [!DNL Facebook] [requisitos de hash de número telefónico](#phone-number-hashing-requirements).
* Seleccione el `IDFA` área de nombres como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el `GAID` área de nombres como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el `Custom` área de nombres como identidad de origen si sus datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el `Email_LC_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `Email` o `Email_LC_SHA256`.
* Seleccione el `Phone_SHA256_E.164` área de nombres como identidad de destino cuando las áreas de nombres de origen son `PHONE_E.164` o `Phone_SHA256_E.164`.
* Seleccione el `IDFA` o `GAID` áreas de nombres como identidad de destino cuando las áreas de nombres de origen son `IDFA` o `GAID`.
* Seleccione el `User_ID` como identidad de destino cuando el espacio de nombres de origen es personalizado.

![Asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Los datos de las áreas de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarse.

Los datos de origen de atributos no se colocan automáticamente en hash. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos.

![Transformación de asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambie a su **[!UICONTROL Publicidades de Google]** cuenta. Los segmentos activados se muestran en su cuenta de Google como listas de clientes. Tenga en cuenta que, según el tamaño del segmento, algunas audiencias no se rellenan a menos que haya más de 100 usuarios activos a los que atender.

Al asignar un segmento a ambas [!DNL IDFA] y [!DNL GAID] ID móviles, [!DNL Google Customer Match] crea un segmento independiente para cada asignación de ID. Su [!DNL Google Ads] La cuenta muestra dos segmentos diferentes, uno para la variable [!DNL IDFA]y una para la variable [!DNL GAID] asignación.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecta {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen con las [requisitos previos](#google-account-prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta esté incluida en la lista de permitidos y configurada para un [!DNL Standard] o nivel de permiso superior. Consulte la [Documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.

## Recursos adicionales {#additional-resources}

* [Integración de Customer Match de Google: tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

