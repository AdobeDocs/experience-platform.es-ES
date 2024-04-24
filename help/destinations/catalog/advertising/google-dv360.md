---
title: Conexión de Google Display & Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager es una herramienta utilizada para ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 0db22ba2993012357cf65daaeffb5676193fba23
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] conexión

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Coincidencia de clientes](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), y el [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) con el fin de respaldar los requisitos de conformidad y relacionados con el consentimiento definidos en el [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) en la Unión Europea ([Política de consentimiento del usuario de UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según DMA en la Unión Europea.
><br/>
>Clientes que han adquirido Adobe Privacy &amp; Security Shield y que han configurado un [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos, no es necesario realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar [definición del segmento](../../../segmentation/home.md#segment-definitions) funciones dentro de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos con el fin de seguir utilizando los destinos de Google de Real-Time CDP existentes sin interrupción.

[!DNL Display & Video 360], anteriormente conocido como [!DNL DoubleClick Bid Manager], es una herramienta que se utiliza para ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos de [!DNL Google Display & Video 360] destinos:

* Las audiencias activadas se crean mediante programación en la plataforma de Google.
* La activación de los rellenos de audiencia en [!DNL Google Display & Video 360] está programado que el destino se produzca de 24 a 48 horas después de que una audiencia se asigne por primera vez a una conexión de destino. Esta actualización es en respuesta a la política de Google de esperar 24 horas hasta la ingesta de datos y está pensada para mejorar las tasas de coincidencia entre Real-Time CDP y [!DNL Google Display & Video 360]. Esta es una configuración back-end aplicable solo a este destino y que no está relacionada con ninguna opción de programación configurable por el cliente en la interfaz de usuario.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha activado la opción [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el Servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Platform.

## Identidades admitidas {#supported-identities}

[!DNL Google Display & Video 360] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID DE USUARIO | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Google utiliza [AAM UUID DE USUARIO](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para dirigirse a los usuarios de California y el ID de cookie de Google para todos los demás usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de publicidad de Microsoft. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

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
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Requisitos previos {#prerequisites}

### Lista de permitidos {#allow-listing}

>[!NOTE]
>
>La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Display & Video 360] en Platform. Asegúrese de que ha completado el proceso de inclusión en la lista de permitidos descrito a continuación [!DNL Google] antes de crear un destino.
>La excepción a esta regla es para [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) clientes. Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

Antes de crear el [!DNL Google Display & Video 360] en Platform, debe ponerse en contacto con Google para solicitar que el Adobe se incluya en la lista de proveedores de datos permitidos y que se añada su cuenta a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **Su tipo de cuenta**: uso **[!DNL Invite advertiser]** para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360 o utilice **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas en su cuenta de Display &amp; Video 360.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, en función de su cuenta con Google:
   * Uso `Invite Advertiser` para permitir que las audiencias se compartan únicamente con una marca específica de la cuenta de Display &amp; Video 360.
   * Uso `Invite Partner` para permitir que las audiencias se compartan con todas las marcas en su cuenta de Display &amp; Video 360.
* **[!UICONTROL ID de cuenta]**: Rellene el **[!DNL Invite partner]** o **[!DNL Invite advertiser]** ID de cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.

>[!NOTE]
>
>Al configurar un [!DNL Google Display & Video 360] destino, trabaje con su [!DNL Google Account Manager] o un representante del Adobe para comprender qué tipo de cuenta tiene.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados

Para comprobar si los datos se han exportado correctamente a [!DNL Google Display & Video 360] destino, compruebe su [!DNL Google Display & Video 360] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecto {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen con la [requisitos previos](#prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta esté incluida en la lista de permitidos.