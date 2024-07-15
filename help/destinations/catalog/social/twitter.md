---
title: Conexión de Audiencias personalizadas de twitter
description: Oriente a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: ba9b59a24079b61a0f5d6076f3acfd83fc8f4092
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences] conexión

## Información general {#overview}

Oriente a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Antes de configurar el destino [!DNL Twitter Custom Audiences], asegúrese de revisar los siguientes requisitos previos de Twitter que debe cumplir.

1. Su cuenta de [!DNL Twitter Ads] debe cumplir los requisitos para la publicidad. Las nuevas cuentas de [!DNL Twitter Ads] no son elegibles para la publicidad en las primeras 2 semanas después de crearse.
2. La cuenta de usuario de Twitter para la que autorizó el acceso en [!DNL Twitter Audience Manager] debe tener habilitado el permiso *[!DNL Partner Audience Manager]*.

## Identidades admitidas {#supported-identities}

[!DNL Twitter Custom Audiences] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) y Apple ID para anunciantes (IDFA) son compatibles con Adobe Experience Platform. Asigne estas áreas de nombres o atributos desde el esquema de origen según corresponda en el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino. |
| email | Direcciones de correo electrónico del usuario | Asigne sus direcciones de correo electrónico de texto sin formato y sus direcciones de correo electrónico con hash SHA256 a este campo. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] aplique automáticamente el hash a los datos durante la activación. Si escribe hash las direcciones de correo electrónico de los clientes antes de cargarlas en Adobe Experience Platform, tenga en cuenta que estas identidades deben tener un cifrado hash con SHA256, sin formato. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores utilizados en el destino Twitter de audiencias personalizadas. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Twitter Custom Audiences], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### #1 de casos de uso

Oriente a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform como [!DNL List Custom Audiences] en Twitter.

## Conectar con destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

1. Busque el destino [!DNL Twitter Custom Audiences] en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccione **[!UICONTROL Conectar con destino]**.
   ![Autenticar con LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Escriba sus credenciales de Twitter y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID de cuenta"
>abstract="Su ID de cuenta de Twitter Ads. Se puede encontrar en la configuración de Twitter Ads."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su ID de cuenta [!DNL Twitter Ads]. Se encuentra en la configuración de [!DNL Twitter Ads].

>[!IMPORTANT]
>
>No utilice caracteres especiales (+ &amp; , % : ; @ / = ? $ \n) en los nombres de asignación de audiencia, descripción y audiencia. Si el nombre de la audiencia del Experience Platform contiene estos caracteres, elimínelos antes de asignar la audiencia a un destino de Twitter.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones de asignación {#mapping-considerations}

Al asignar audiencias al Twitter, proporcione nombres de asignación de audiencias legibles por humanos. Se recomienda utilizar el mismo nombre que utilizó para los segmentos del Experience Platform.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Encontrará más información sobre [!DNL List Custom Audiences] en el Twitter en la [documentación del Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
