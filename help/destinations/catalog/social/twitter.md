---
title: Conexión de Audiencias personalizadas de twitter
description: Oriente a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences] conexión

## Información general {#overview}

Dirija su actividad a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Antes de configurar su [!DNL Twitter Custom Audiences] destino, asegúrese de revisar los siguientes requisitos previos de Twitter que debe cumplir.

1. Su [!DNL Twitter Ads] La cuenta debe ser apta para la publicidad. Nuevo [!DNL Twitter Ads] Las cuentas de no son aptas para la publicidad en las 2 primeras semanas después de su creación.
2. Su cuenta de usuario de Twitter para la que autorizó el acceso en [!DNL Twitter Audience Manager] debe tener el *[!DNL Partner Audience Manager]* permiso habilitado.

## Identidades admitidas {#supported-identities}

[!DNL Twitter Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| device_id | ID de IDFA/AdID/Android | Google Advertising ID (GAID) y Apple ID para anunciantes (IDFA) son compatibles con Adobe Experience Platform. Asigne estas áreas de nombres o atributos desde su esquema de origen según corresponda en la [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino. |
| email | Direcciones de correo electrónico del usuario | Asigne sus direcciones de correo electrónico de texto sin formato y sus direcciones de correo electrónico con hash SHA256 a este campo. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. Si escribe hash las direcciones de correo electrónico de los clientes antes de cargarlas en Adobe Experience Platform, tenga en cuenta que estas identidades deben tener un cifrado hash con SHA256, sin formato. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores utilizados en el destino de Audiencias personalizadas de Twitter. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Twitter Custom Audiences] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### #1 de casos de uso

Oriente a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform como [!DNL List Custom Audiences] en Twitter.

## Conectar con destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

1. Busque el [!DNL Twitter Custom Audiences] en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccionar **[!UICONTROL Conectar con destino]**.
   ![Autenticar en LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Introduzca sus credenciales de Twitter y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID de cuenta"
>abstract="Su ID de cuenta de Twitter Ads. Se puede encontrar en la configuración de Twitter Ads."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL Twitter Ads] ID de cuenta. Esto se puede encontrar en su [!DNL Twitter Ads] configuración.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Al asignar segmentos de audiencia a Twitter, asegúrese de cumplir los siguientes requisitos de nomenclatura de segmentos:

1. Proporcione nombres de asignación de segmentos legibles por un humano. Se recomienda utilizar el mismo nombre que utilizó para los segmentos del Experience Platform.
2. No utilice caracteres especiales (+ &amp; , % : ; @ / = ? $) en los nombres de asignación de segmentos y segmentos. Si el nombre del segmento del Experience Platform contiene estos caracteres, elimínelos antes de asignar el segmento a un destino de Twitter.

Más información sobre [!DNL List Custom Audiences] en Twitter se puede encontrar en la [Documentación de twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
