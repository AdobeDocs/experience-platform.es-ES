---
title: Conexión Google Customer Match + Display & Video 360
description: Con el conector de destino Google Customer Match + Display & Video 360, puede utilizar los datos en línea y sin conexión de Experience Platform para llegar a sus clientes y volver a interactuar con ellos en las propiedades de Google y en las que opera, como Search, Shopping, Gmail y YouTube.
badgeBeta: label="Beta" type="Informative"
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 1%

---

# [!DNL Google Customer Match + Display & Video 360] conexión

Utilice este destino para activar su PII de origen [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) listas directamente a [!DNL Google Display & Video 360] propiedades como [!DNL Search], [!DNL YouTube], [!DNL Gmail], y el [!DNL Google Display Network].

Algunos terceros integrados en Google, como Adobe Real-Time CDP, pueden utilizar el [!DNL Google Audience Partner API] para crear [!DNL Customer Match] audiencias directamente en el de los clientes [!DNL Display & Video 360] cuenta.

Con la capacidad recién introducida de poder utilizar [!DNL Customer Matched] audiencias entre [!DNL Display & Video 360]Ahora puede dirigirse a audiencias de una lista ampliada de fuentes de inventario.

>[!IMPORTANT]
>
>Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con el representante del Adobe.

![Coincidencia de clientes de Google + destino DV360 en la interfaz de usuario de Adobe Experience Platform.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Aviso importante sobre los cambios en los destinos de Google relacionados con los requisitos de consentimiento actualizados en la Unión Europea

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Coincidencia de clientes](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), y el [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) con el fin de respaldar los requisitos de conformidad y relacionados con el consentimiento definidos en el [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) en la Unión Europea ([Política de consentimiento del usuario de UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según DMA en la Unión Europea.
><br/>
>Clientes que han adquirido Adobe Privacy &amp; Security Shield y que han configurado un [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos, no es necesario realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar [definición del segmento](../../../segmentation/home.md#segment-definitions) funciones dentro de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos con el fin de seguir utilizando los destinos de Google de Real-Time CDP existentes sin interrupción.

## Cuándo utilizar este destino

Hay varias integraciones con Google disponibles en el catálogo de destinos y puede resultar difícil comprender cuándo utilizar cada uno de los destinos de Google disponibles. Lea la información de la siguiente tabla para ver los diferentes casos de uso:

| [Coincidencia de clientes de Google](/help/destinations/catalog/advertising/google-customer-match.md) | [Google Display &amp; Video 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (este conector) |
|---------|----------|---------|
| Exporte sus audiencias basadas en PII y póngase en contacto con ellas en el inventario disponible en [!DNL Google Customer Match]. | Llegar a las audiencias basadas en cookies en todo el inventario disponible mediante [!DNL Google Display & Video 360], en propiedades de Google como YouTube y [!DNL Search], y más allá. | Creación de audiencias basadas en PII en [!DNL Google Customer Match] y póngase en contacto con ellos en el inventario disponible en [!DNL Google Display & Video 360], solo en propiedades que Google posee y gestiona. |

## Casos de uso {#use-cases}

Para comprender mejor cómo y cuándo utilizar este destino, aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

### Caso de uso #1

Una marca de ropa deportiva quiere llegar a los clientes existentes mediante [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM al Experience Platform y crear audiencias a partir de sus propios datos sin conexión. A continuación, puede enviar estas audiencias a [!DNL Google Customer Match + Display & Video 360] destino que se utilizará en [!DNL Google Display & Video 360] propiedades como [!DNL Search], [!DNL YouTube], [!DNL Gmail], y el [!DNL Google Display Network].

### Caso de uso #2

Una destacada compañía tecnológica ha lanzado un nuevo teléfono. Para promocionar este nuevo modelo de teléfono, buscan concienciar sobre las nuevas funciones y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico desde su base de datos de CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Las audiencias se crean en función de los clientes que poseen modelos de teléfono más antiguos. A continuación, las audiencias se envían a [!DNL Google Customer Match], para que la compañía pueda dirigirse a clientes actuales, clientes que sean propietarios de modelos de teléfono más antiguos y clientes similares en [!DNL Google Display & Video 360] propiedades como [!DNL Search], [!DNL YouTube], [!DNL Gmail], y el [!DNL Google Display Network].

## Identidades admitidas {#supported-identities}

[!DNL Google Customer Match] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| phone_sha256_e.164 | Números de teléfono en formato E164, con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Siga las instrucciones de la [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice las áreas de nombres adecuadas para números de teléfono con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para las direcciones de correo electrónico con hash y texto sin formato, respectivamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |

{style="table-layout:auto"}

<!-- not supported in beta

|GAID|Google Advertising ID|Select this target identity when your source identity is a GAID namespace.|
|IDFA|Apple ID for Advertisers|Select this target identity when your source identity is an IDFA namespace.|
|user_id|Custom user IDs|Select this target identity when your source identity is a custom namespace.| 

-->

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono y otros) utilizados en [!DNL Google Customer Match] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] requisitos previos de cuenta {#google-account-prerequisites}

Antes de configurar un [!DNL Google Customer Match] destino en Experience Platform, asegúrese de leer y cumplir la directiva de Google para utilizar [!DNL Customer Match], se describe en la [Documentación de asistencia de Google](https://support.google.com/google-ads/answer/6299717).

A continuación, asegúrese de que su [!DNL Google] La cuenta de está configurada para una [!DNL Standard] o un nivel de permiso superior. Consulte la [Documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.

### Lista de permitidos {#allowlist}

Antes de crear el [!DNL Google Customer Match] destino en Experience Platform, asegúrese de que su [!DNL Google Ads] La cuenta cumple con la [[!DNL Google Customer Match] directiva](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Google incluida en la lista de permitidos automáticamente a los clientes con cuentas compatibles.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Google] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL Google Customer Match] debe estar desactivado con llave *con hash* identificadores, como direcciones de correo electrónico con hash o números de teléfono.

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes.

### Requisitos de hash de número de teléfono {#phone-number-hashing-requirements}

Existen dos métodos para activar números de teléfono en [!DNL Google Customer Match]:

* **Ingesta de números de teléfono sin procesar**: puede introducir números de teléfono sin procesar en el [!DNL E.164] formatear en [!DNL Platform]y se les aplica automáticamente un cifrado hash tras la activación. Si elige esta opción, asegúrese de introducir siempre los números de teléfono sin procesar en la `Phone_E.164` namespace.
* **Ingesta de números de teléfono con hash**: puede precifrar los números de teléfono antes de ingerirlos en [!DNL Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en la `PHONE_SHA256_E.164` namespace.

>[!NOTE]
>
>Números de teléfono introducidos en `Phone` El área de nombres no se puede activar en [!DNL Google Customer Match + DV360] destino.

### Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico en borrar en Experience Platform, y tener [!DNL Platform] hash en la activación.

Para obtener más información sobre los requisitos de hash de Google y otras restricciones en la activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] con número de teléfono](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] con ID de dispositivos móviles](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [introducción a la ingesta por lotes](../../../ingestion/batch-ingestion/overview.md) y el [información general sobre ingesta de streaming](../../../ingestion/streaming-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google descritos en los vínculos anteriores.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: proporcione un nombre para esta conexión de destino
* **[!UICONTROL Descripción]**: proporcione una descripción para esta conexión de destino
* **[!UICONTROL ID de cuenta]**: su [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). El formato del ID es xxx-xxx-xxxx. Si utiliza el complemento [!DNL Google Ads Manager Account (My Client Center)], no use su ID de cuenta de responsable. Utilice el [ID de cliente de Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en) en su lugar.
* **[!UICONTROL Tipo de cuenta]**: su tipo de cuenta de Google. Seleccione una opción, en función del tipo de cuenta publicitaria con Google:
   * **[!UICONTROL Socio de vídeo de visualización]**
   * **[!UICONTROL Anunciante de vídeo de visualización]**

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades* a los destinos, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](../../assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Ejemplo de asignación: activación de datos de audiencia en [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Este es un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Google Customer Match + Display & Video 360].

Selección de campos de origen:

* Seleccione el `Email` área de nombres como identidad de origen si las direcciones de correo electrónico que utiliza no tienen un hash.
* Seleccione el `Email_LC_SHA256` área de nombres como identidad de origen si ha creado un hash de las direcciones de correo electrónico del cliente al ingerir datos en [!DNL Platform], según [!DNL Google Customer Match] [requisitos de hash de correo electrónico](#hashing-requirements).
* Seleccione el `PHONE_E.164` área de nombres como identidad de origen si los datos constan de números de teléfono sin hash. [!DNL Platform] hará un hash de los números de teléfono para cumplir con [!DNL Google Customer Match] requisitos.
* Seleccione el `Phone_SHA256_E.164` área de nombres como identidad de origen si ha creado un hash de los números de teléfono al ingerir datos en [!DNL Platform], según [!DNL Facebook] [requisitos hash de número de teléfono](#phone-number-hashing-requirements).

Selección de campos de destino:

* Seleccione el `Email_LC_SHA256` área de nombres como identidad de destino cuando las áreas de nombres de origen son `Email` o `Email_LC_SHA256`.
* Seleccione el `Phone_SHA256_E.164` área de nombres como identidad de destino cuando las áreas de nombres de origen son `PHONE_E.164` o `Phone_SHA256_E.164`.

![La asignación de identidad entre los campos de origen y destino se muestra en el paso Asignación del flujo de trabajo de activación.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

Los datos de áreas de nombres sin hash se cifran automáticamente en hash mediante [!DNL Platform] tras la activación.

Los datos de origen de los atributos no se cifran automáticamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación.

![Aplique el control de transformación resaltado en el paso Asignación del flujo de trabajo de activación.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Compruebe que la activación de la audiencia se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambie a **[!UICONTROL Google Ads]** cuenta. Las audiencias activadas se muestran en su cuenta de Google como listas de clientes. Según el tamaño de la audiencia, algunas audiencias no se rellenan a menos que haya más de 1000 usuarios activos para servir. Encontrará más información en la [Documentación de Google Audience Partner](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Tenga en cuenta que debe solicitar a Google acceso a la documentación del vínculo.

## Gobernanza de datos

Algunos destinos de Experience Platform tienen ciertas reglas y obligaciones para los datos enviados a, o recibidos de, la plataforma de destino. Usted es responsable de comprender las limitaciones y obligaciones de sus datos y de cómo los utiliza en Adobe Experience Platform y en la plataforma de destino. Adobe Experience Platform proporciona herramientas de control de datos para ayudarle a administrar algunas de estas obligaciones de uso de datos. [Más información](../../../data-governance/labels/overview.md) acerca de las herramientas y políticas de gobernanza de datos.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen con la [requisitos previos](#google-account-prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta está incluida en la lista de permitidos y configurada para [!DNL Standard] o un nivel de permiso superior. Consulte la [Documentación de Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obtener más información.
