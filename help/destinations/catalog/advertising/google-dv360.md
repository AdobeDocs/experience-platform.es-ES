---
title: Conexión de Google Display & Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager es una herramienta utilizada para ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 4%

---

# [!DNL Google Display & Video 360] conexión

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) y la [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para admitir los requisitos relacionados con el cumplimiento y el consentimiento definidos en la [Ley de Mercados Digitales](https://digital-markets-act.ec.europa.eu/index_es) (DMA) de la Unión Europea ([Política de consentimiento del Usuario de la UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según la DMA en la Unión Europea.
><br/>
>Los clientes que hayan adquirido Adobe Privacy &amp; Security Shield y hayan configurado una [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos no tienen que realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar las funciones de [definición de segmento](../../../segmentation/home.md#segment-definitions) de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos y así poder seguir utilizando los destinos de Real-Time CDP Google existentes sin interrupción.

[!DNL Display & Video 360], anteriormente conocido como [!DNL DoubleClick Bid Manager], es una herramienta que se usa para ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Display & Video 360] destinos:

* Las audiencias activadas se crean mediante programación en la plataforma de Google.
* Se ha programado la activación de los rellenos de audiencia en el destino [!DNL Google Display & Video 360] de 24 a 48 horas después de que una audiencia se asigne por primera vez a una conexión de destino. Esta actualización es en respuesta a la directiva de Google de esperar 24 horas hasta la ingesta de datos y está pensada para mejorar las tasas de coincidencia entre Real-Time CDP y [!DNL Google Display & Video 360]. Esta es una configuración back-end aplicable solo a este destino y que no está relacionada con ninguna opción de programación configurable por el cliente en la interfaz de usuario.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio Experience Cloud ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar la sincronización de ID. Si ya había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

## Identidades admitidas {#supported-identities}

[!DNL Google Display & Video 360] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID DE AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que Audience Manager asocia a cada dispositivo con el que interactúa. | Google usa [UUID de AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para segmentar usuarios en California y el ID de cookie de Google para todos los demás usuarios. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] usa este identificador para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para Advertising. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de Microsoft Advertising. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

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

## Requisitos previos {#prerequisites}

### Lista de permitidos {#allow-listing}

>[!NOTE]
>
>La inclusión en la lista de permitidos es obligatoria antes de configurar su primer destino de [!DNL Google Display & Video 360] en Experience Platform. Asegúrese de que el proceso de inclusión en la lista de permitidos descrito a continuación haya sido completado por [!DNL Google] antes de crear un destino.
>La excepción a esta regla es para clientes de [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html). Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

Antes de crear el destino [!DNL Google Display & Video 360] en Experience Platform, debe ponerse en contacto con Google para solicitar que Adobe se incluya en la lista de proveedores de datos permitidos y que se agregue su cuenta a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **Tipo de cuenta**: usa **[!DNL Invite advertiser]** para permitir que las audiencias se compartan solo con una marca específica de tu cuenta de Display &amp; Video 360, o usa **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de tu cuenta de Display &amp; Video 360.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Tipo de cuenta]**: selecciona una opción, según tu cuenta con Google:
   * Use `Invite Advertiser` para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360.
   * Use `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **[!UICONTROL ID de cuenta]**: Rellene su **[!DNL Invite partner]** o **[!DNL Invite advertiser]** ID de cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.

>[!NOTE]
>
>Al configurar un destino de [!DNL Google Display & Video 360], colabore con su representante de [!DNL Google Account Manager] o Adobe para saber qué tipo de cuenta tiene.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados

Para comprobar si los datos se han exportado correctamente al destino [!DNL Google Display & Video 360], compruebe su cuenta de [!DNL Google Display & Video 360]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen los [requisitos previos](#prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta esté incluida en la lista de permitidos.