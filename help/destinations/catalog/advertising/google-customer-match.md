---
keywords: coincidencia de clientes de google;coincidencia de clientes de Google;coincidencia de clientes de Google
title: Conexión de Google Customer Match
description: Google Customer Match le permite utilizar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades de Google que usted posee y gestiona, como Search, Shopping, Gmail y YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL Google Customer Match] connection

## Información general {#overview}

[Las ](https://support.google.com/google-ads/answer/6379332?hl=en) coincidencias de clientes de Google le permiten usar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades de Google y en las que opera, como:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail], y  [!DNL YouTube].

![Destino de Google Customer Match en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL Google Customer Match], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver mediante esta función.

### Caso de uso número 1

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM al Experience Platform y generar segmentos a partir de sus propios datos sin conexión. A continuación, pueden enviar estos segmentos a [!DNL Google Customer Match] para usarlos en [!DNL Search] y [!DNL Shopping], lo que optimiza su gasto en publicidad.

### Caso de uso n.º 2

Una destacada compañía tecnológica lanzó un nuevo teléfono. Para promocionar este nuevo modelo de teléfono, buscan sensibilizar sobre las nuevas funciones y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico de su base de datos CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Los segmentos se crean en función de los clientes que poseen modelos de teléfono más antiguos. A continuación, los segmentos se envían a [!DNL Google Customer Match], de modo que la empresa pueda dirigirse a los clientes actuales, a los clientes que son propietarios de modelos de teléfono antiguos y a clientes similares en [!DNL YouTube].

## Control de datos para destinos [!DNL Google Customer Match] {#data-governance}

Algunos destinos en Experience Platform tienen ciertas reglas y obligaciones para los datos enviados a la plataforma de destino o recibidos de ella. Usted es el responsable de comprender las limitaciones y obligaciones de sus datos y cómo utiliza esos datos en Adobe Experience Platform y en la plataforma de destino. Adobe Experience Platform proporciona herramientas de control de datos para ayudarle a administrar algunas de esas obligaciones de uso de datos. [Obtenga ](../../../data-governance/labels/overview.md) más información sobre las herramientas y políticas de control de datos.

## Identidades compatibles {#supported-identities}

[!DNL Google Customer Match] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| phone_sha256_e.164 | Números de teléfono en formato E164, con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Siga las instrucciones de la sección [ID match requirements](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para números de teléfono sin formato y con hash, respectivamente. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [ID match requirements](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para las direcciones de correo electrónico con texto sin formato y con hash, respectivamente. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación. |
| user_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono y otros) utilizados en el  [!DNL Google Customer Match] destino.

## [!DNL Google Customer Match] requisitos previos de la cuenta {#google-account-prerequisites}

Antes de configurar un destino [!DNL Google Customer Match] en el Experience Platform, asegúrese de leer y cumplir la directiva de Google para usar [!DNL Customer Match], que se describe en la [documentación de soporte de Google](https://support.google.com/google-ads/answer/6299717).

A continuación, asegúrese de que su cuenta [!DNL Google] esté configurada para un nivel de acceso [!DNL Standard] o superior. Consulte la [documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.

### Lista de permitidos {#allowlist}

Antes de crear el destino [!DNL Google Customer Match] en el Experience Platform, asegúrese de que su cuenta [!DNL Google Ads] cumple con la [Política de coincidencia del cliente de Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Google permite automáticamente a los clientes con cuentas compatibles aparecer en la lista.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Google] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Google Customer Match] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o números de teléfono.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

## Requisitos de hash de número telefónico {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Google Customer Match]:

* **Ingesta de números** de teléfono sin procesar: puede ingerir números de teléfono sin procesar en el  [!DNL E.164] formato en  [!DNL Platform], y se colocan automáticamente en hash al activarlos. Si elige esta opción, asegúrese de introducir siempre sus números de teléfono sin procesar en el espacio de nombres `Phone_E.164`.
* **Ingesta de números** de teléfono con hash: puede prehash sus números de teléfono antes de ingerirlos a  [!DNL Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en el espacio de nombres `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Los números de teléfono introducidos en el espacio de nombres `Phone` no se pueden activar en [!DNL Google Customer Match].

## Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash sobre las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico claramente en el Experience Platform, y tener [!DNL Platform] hash sobre ellas cuando se activen.

Para obtener más información sobre los requisitos hash de Google y otras restricciones en la activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Customer Match con número de teléfono](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Coincidencia de cliente con ID de dispositivos móviles](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta por lotes](../../../ingestion/batch-ingestion/overview.md) y la [información general sobre la ingesta de flujo](../../../ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google, descritos en los vínculos anteriores.

## Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de utilizar el espacio de nombres `User_ID` para enviar datos a Google, asegúrese de sincronizar sus propios identificadores con [!DNL gTag]. Consulte la [documentación oficial de Google](https://support.google.com/google-ads/answer/9199250) para obtener información detallada.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: proporcionar un nombre para esta conexión de destino
* **[!UICONTROL Descripción]**: proporcionar una descripción para esta conexión de destino
* **[!UICONTROL ID de cuenta]**: su ID de cliente de Google. El formato del ID es xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * La acción de marketing **[!UICONTROL Combinar con PII]** está seleccionada de forma predeterminada para el destino [!DNL Google Customer Match] y no se puede eliminar.


## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

En el paso **[!UICONTROL Programación de segmentos]**, debe proporcionar el [!UICONTROL ID de aplicación] al enviar segmentos [!DNL IDFA] o [!DNL GAID] a [!DNL Google Customer Match].

![ID de aplicación de coincidencia de clientes de Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obtener más información sobre cómo encontrar el [!DNL App ID], consulte la [documentación oficial de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Google Customer Match] {#example-gcm}

Este es un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Google Customer Match].

Selección de campos de origen:

* Seleccione el espacio de nombres `Email` como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente sobre la ingesta de datos a [!DNL Platform], de acuerdo con los [!DNL Google Customer Match] [requisitos de hash de correo electrónico](#hashing-requirements).
* Seleccione el espacio de nombres `PHONE_E.164` como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] realizará un hash de los números de teléfono para cumplir con los  [!DNL Google Customer Match] requisitos.
* Seleccione el espacio de nombres `Phone_SHA256_E.164` como identidad de origen si ha hash los números de teléfono sobre la ingesta de datos en [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de números de teléfono](#phone-number-hashing-requirements).
* Seleccione el espacio de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el espacio de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el espacio de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el espacio de nombres `Phone_SHA256_E.164` como identidad de destino cuando los espacios de nombres de origen sean `PHONE_E.164` o `Phone_SHA256_E.164`.
* Seleccione los espacios de nombres `IDFA` o `GAID` como identidad de destino cuando los espacios de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el espacio de nombres `User_ID` como identidad de destino cuando el espacio de nombres de origen sea personalizado.

![Asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.

Los datos de origen de atributos no se colocan automáticamente en hash. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación.

![Transformación de asignación de identidad](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambie a su cuenta de **[!UICONTROL Google Ads]**. Los segmentos activados se muestran en su cuenta de Google como listas de clientes. Tenga en cuenta que, según el tamaño del segmento, algunas audiencias no se rellenan a menos que haya más de 100 usuarios activos a los que atender.

Al asignar un segmento a [!DNL IDFA] e [!DNL GAID] ID móviles, [!DNL Google Customer Match] crea un segmento independiente para cada asignación de ID. Su cuenta [!DNL Google Ads] muestra dos segmentos diferentes, uno para [!DNL IDFA] y otro para la asignación [!DNL GAID].

## Recursos adicionales {#additional-resources}

* [Integración de la coincidencia de clientes de Google: tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
