---
title: Conexión de lista de clientes de pinterest
description: Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 83e2c014e62509fee2843505d7975cde368665ef
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] conexión

## Información general {#overview}

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

>[!IMPORTANT]
>
>El equipo de Pinterest creó este destino. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en https://help.pinterest.com/en/contact.

## Requisitos previos {#prerequisites}

* El usuario tendría que autenticarse con una cuenta de Pinterest que tenga acceso a la cuenta del anunciante a la que desee agregar una audiencia. Encontrará detalles sobre cómo compartir las cuentas de anunciante [aquí](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). En concreto, el usuario necesitaría los niveles de acceso de &quot;audiencia&quot;.
* Encontrará detalles sobre los formatos de identidad de la lista de clientes [aquí](https://help.pinterest.com/en/business/article/audience-targeting).

## Identidades admitidas {#supported-identities}

El destino [!DNL Pinterest Customer List] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, asigne las identidades deseadas al campo de destino *pinterest_audience*. Las identidades se distinguen y resuelven tras la ingesta de datos en Pinterest.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Asigne el área de nombres de identidad de origen *GAID* al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y resuelven tras la ingesta de datos en Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Asigne el área de nombres de identidad de origen *IDFA* al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y resuelven tras la ingesta de datos en Pinterest. |
| EMAIL | Direcciones de correo electrónico (texto no cifrado o con hash con el algoritmo SHA256) | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. <br>: asigne el área de nombres de identidad de origen *Email* o *Email_LC_SHA256* al campo de identidad de destino *pinterest_audience*. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de lista de clientes de Pinterest. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Pinterest Customer List], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### #1 de casos de uso

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

## Conectar con destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Al [configurar](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta de publicidad]**: tu ID de anunciante de Pinterest.

### Actualizar credenciales de autenticación {#refresh-authentication-credentials}

Los tokens de pinterest caducan cada 30 días. Una vez caducado el token, las exportaciones de datos al destino dejan de funcionar. Para evitar esta situación, vuelva a autenticarse realizando los siguientes pasos:

1. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Cuentas]**
2. (Opcional) Utilice los filtros disponibles en la página para mostrar solo las cuentas de Pinterest.
   ![Filtrar para mostrar solo cuentas de Pinterest](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Seleccione la cuenta que desea actualizar, seleccione los puntos suspensivos y seleccione **[!UICONTROL Editar detalles]**.
   ![Seleccionar el control Editar detalles](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. En la ventana modal, seleccione **[!UICONTROL Volver a conectar OAuth]** y vuelva a autenticarse con sus credenciales de Pinterest.
   ![Ventana modal con la opción Reconectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Las credenciales de autenticación se actualizan y su hora de caducidad se restablece a 30 días.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Consulte la [página del Centro de ayuda de Pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obtener más información.

+++ Ver registro de cambios


| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Noviembre de 2023 | Actualización de funcionalidad y documentación | El destino de Pinterest en Real-Time CDP ahora utiliza la API del anunciante v5. |

{style="table-layout:auto"}


+++
