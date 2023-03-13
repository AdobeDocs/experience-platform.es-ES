---
keywords: Google ads;anuncios de google;google adwords;Google AdWords;Google Adwords
title: Conexión de Google Ads
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas publicar anuncios de pago por clic en búsquedas basadas en texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles en la aplicación.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 7d32499bec8d7248472ae60b07893dbb5496d984
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 2%

---

# [!DNL Google Ads] conexión

## Información general {#overview}

[!DNL Google Ads], anteriormente conocido como [!DNL Google AdWords], es un servicio de publicidad en línea que permite a las empresas pagar por clic en publicidad en búsquedas basadas en texto, pantallas gráficas, [!DNL YouTube] vídeos y visualizaciones móviles en la aplicación.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos de [!DNL Google Ads] destinos:

* Las audiencias activadas se crean mediante programación en [!DNL Google] plataforma.
* [!DNL Platform] actualmente no incluye una métrica de medición para validar que la activación se haya realizado correctamente. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si quiere crear su primer destino con [!DNL Google Ads] y no han habilitado el [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el Servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Platform.

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| AAM UUID DE USUARIO | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Google utiliza [AAM UUID DE USUARIO](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=es) para dirigirse a los usuarios de California y el ID de cookie de Google para todos los demás usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de publicidad de Microsoft. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

### Existente [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] ha obsoleto nuevo [!DNL Google Ads] integraciones de cookies con proveedores externos. Para realizar los pasos de lista de permitidos de la siguiente sección, debe tener una integración existente con [!DNL Google Ads]. Como resultado, el enfoque recomendado para utilizar [!DNL Google Ads] está configurando un [!DNL Google Customer Match] integración. Para obtener más información sobre la creación de un [!DNL Google Customer Match] integración, lea el tutorial sobre la creación de un [[!DNL Google Customer Match]](./google-customer-match.md) conexión.

### Lista de permitidos {#allow-listing}

>[!NOTE]
>
>La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ads] en Platform. Asegúrese de que ha completado el proceso de inclusión en la lista de permitidos descrito a continuación [!DNL Google] antes de crear un destino.
>La excepción a esta regla es para [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) clientes. Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

Antes de crear el [!DNL Google Ads] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se añada a la lista de permitidos. Contacto [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente del Adobe con Google. ID de cliente: 89690775.
* Tipo de cuenta: **AdWord**
* **ID de Google AdWords**: Este es su ID con [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Tipo de cuenta]**: AdWords es la única opción disponible.
* **[!UICONTROL ID de cuenta]**: Rellene el ID de cuenta con [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados

Para comprobar si los datos se han exportado correctamente a [!DNL Google Ads] destino, compruebe su [!DNL Google Ads] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen con las [requisitos previos](#prerequisites) o cuando los clientes intentan configurar el destino sin un [!DNL Google Ads] cuenta.

[!DNL Google] ha obsoleto nuevo [!DNL Google Ads] integraciones de cookies con proveedores externos. Para realizar la [lista de permitidos](#allow-listing) pasos, debe tener una integración existente con [!DNL Google Ads].

El método recomendado para utilizar [!DNL Google Ads] está configurando un [[!DNL Google Customer Match]](google-customer-match.md) integración.
