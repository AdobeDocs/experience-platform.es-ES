---
title: Conexión de Google Ads
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas publicar anuncios de pago por clic en búsquedas basadas en texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles en la aplicación.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# [!DNL Google Ads] conexión

## Información general {#overview}

[!DNL Google Ads], anteriormente conocido como [!DNL Google AdWords], es un servicio de publicidad en línea que permite a las empresas publicar publicidad de pago por clic en búsquedas basadas en texto, visualizaciones gráficas, [!DNL YouTube] vídeos y visualizaciones móviles en la aplicación.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ads] destinos:

* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* [!DNL Experience Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ads] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de Experience Cloud ID en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar la sincronización de ID. Si ya había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

## Identidades admitidas {#supported-identities}

[!DNL Google Ads] admite la activación de las identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| UUID DE AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que Audience Manager asocia a cada dispositivo con el que interactúa. | Google usa [UUID de AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para segmentar usuarios en California y el ID de cookie de Google para todos los demás usuarios. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] usa este identificador para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para Advertising. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de Microsoft Advertising. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

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
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

### Cuenta [!DNL Google Ads] existente

>[!IMPORTANT]
>
> [!DNL Google] ha desaprobado nuevas integraciones de cookies [!DNL Google Ads] con proveedores externos. Para realizar los pasos de lista de permitidos de la siguiente sección, debe tener una integración existente con [!DNL Google Ads]. Como resultado, el método recomendado para usar [!DNL Google Ads] es configurar una integración de [!DNL Google Customer Match]. Para obtener más información sobre cómo crear una integración de [!DNL Google Customer Match], lea el tutorial sobre cómo crear una conexión de [[!DNL Google Customer Match]](./google-customer-match.md).

### Lista de permitidos {#allow-listing}

>[!NOTE]
>
>La inclusión en la lista de permitidos es obligatoria antes de configurar su primer destino de [!DNL Google Ads] en Experience Platform. Asegúrese de que el proceso de inclusión en la lista de permitidos descrito a continuación haya sido completado por [!DNL Google] antes de crear un destino.
>La excepción a esta regla es para clientes de [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html). Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

Antes de crear el destino [!DNL Google Ads] en Experience Platform, debe ponerse en contacto con [!DNL Google] para que Adobe se incluya en la lista de proveedores de datos permitidos y para que se agregue su cuenta a la lista de permitidos. Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* Tipo de cuenta: **AdWords**
* **ID de Google AdWords**: Este es su ID con [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Tipo de cuenta]**: AdWords es la única opción disponible.
* **[!UICONTROL Id. de cuenta]**: Rellene el id. de cuenta con [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados

Para comprobar si los datos se han exportado correctamente al destino [!DNL Google Ads], compruebe su cuenta de [!DNL Google Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen los [requisitos previos](#prerequisites) o cuando los clientes intentan configurar el destino sin una cuenta de [!DNL Google Ads] existente.

[!DNL Google] ha desaprobado nuevas integraciones de cookies [!DNL Google Ads] con proveedores externos. Para realizar los pasos de [lista de permitidos](#allow-listing), debe tener una integración existente con [!DNL Google Ads].

El método recomendado para usar [!DNL Google Ads] es configurar una integración de [[!DNL Google Customer Match]](google-customer-match.md).
