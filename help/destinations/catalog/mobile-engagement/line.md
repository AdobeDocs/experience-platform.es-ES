---
keywords: móvil;destinos de participación móvil;LINE;destino de participación móvil de LINE
title: Conexión LINE
description: El destino LINE le permite añadir perfiles a la audiencia de Platform y ofrecer experiencias personalizadas a los usuarios conectados.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 2%

---

# [!DNL LINE] conexión

## Información general {#overview}

[[!DNL LINE]](https://line.me/en/) es una plataforma de comunicación popular que conecta personas, servicios e información y que ha pasado de ser una aplicación de chat a ser un concentrador de actividades de entretenimiento, sociales y cotidianas.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha [[!DNL LINE] la API de mensajería](https://developers.line.biz/en/reference/messaging-api/). Puede activar perfiles de sus audiencias de Experience Platform como conexiones en [!DNL LINE] para sus necesidades comerciales.

[!DNL LINE] usa tokens de portador como mecanismo de autenticación para comunicarse con la API de mensajería [!DNL LINE]. Las instrucciones para autenticarse en su instancia de [!DNL LINE] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

Como especialista en marketing, puede segmentar usuarios en un destino de participación móvil con audiencias creadas en [!DNL Adobe Experience Platform]. Además, puede enviarles experiencias personalizadas basadas en los atributos de sus perfiles [!DNL Adobe Experience Platform] en cuanto las audiencias y los perfiles se actualicen en [!DNL Adobe Experience Platform].

## Requisitos previos {#prerequisites}

### [!DNL LINE] requisitos previos {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos de [!DNL LINE] para exportar datos de Platform a su cuenta de [!DNL LINE]:

#### Necesita tener una cuenta de [!DNL LINE] {#prerequisites-account}

Debe registrarse y crear una cuenta de [!DNL LINE], si todavía no la tiene. Para crear una cuenta de:

1. Vaya a la página [!DNL LINE] [inicio de sesión en la cuenta](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F)
2. Seleccione **[!UICONTROL Crear una cuenta]**.

#### Reunir [!DNL LINE channel access token (long-lived)] de la consola para desarrolladores de [!DNL LINE] {#gather-credentials}

Para permitir que Platform acceda a los recursos de [!DNL LINE], necesitará *[!DNL Channel access token (long-lived)]* del canal [!DNL LINE] *API de mensajería* deseado.

1. Inicie sesión con su cuenta de [!DNL LINE] en [[!DNL LINE] Developer Console](https://developers.line.biz/console).
1. A continuación, accede a la lista *[!DNL Providers]*, selecciona *[!DNL Provider]* de interés y, finalmente, selecciona el canal *API de mensajería* para acceder a su configuración. Si accede a la consola de desarrolladores por primera vez, siga la [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para completar los pasos necesarios para crear un proveedor.
1. Por último, vaya a la sección ***[!DNL Channel access token]*** y copie el valor ***[!DNL Channel access token (long-lived)]*** necesario en el paso [Autenticar en destino](#authenticate).

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Su [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulte la [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para obtener instrucciones sobre cómo crear un canal o agregar uno a su cuenta de [!DNL LINE] existente a través de la consola de desarrolladores de [!DNL LINE].

## Identidades admitidas {#supported-identities}

[!DNL LINE] admite la actualización y exportación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| ID para anunciantes (IFA) | Seleccione la identidad de destino de ID para anunciantes (IFA) cuando las identidades de origen sean áreas de nombres IFA *(Apple ID para anunciantes)* o GAID *(Google Advertising ID). |
| ID de usuario de LINE | Seleccione la identidad de destino UserID cuando las identidades de origen sean ID de usuario de LINE. |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL LINE]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL LINE]. También puede encontrarlo en la categoría **[!UICONTROL Participación móvil]**.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de IU de Platform que muestra cómo autenticarse.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Rellene los campos obligatorios siguientes.
* **[!UICONTROL Token de portador]**: Su [!DNL LINE Channel access token (long-lived)] de la consola para desarrolladores de [!DNL LINE]. Consulte la sección [recopilar credenciales](#gather-credentials).

Si los detalles proporcionados son válidos, la interfaz de usuario mostrará el estado **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de IU de Platform que muestra los detalles del destino.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Tipo de audiencia]**: seleccione **[!UICONTROL ID para anunciantes(IFA)]** si las identidades que desea exportar son del tipo *ID para anunciantes(IFA)*. Seleccione **[!UICONTROL ID de usuario de LINE]** si las identidades que desea exportar son del tipo *ID de usuario de LINE*. Consulte la sección [Identidades admitidas](#supported-identities) para obtener más información sobre los tipos de identidad.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL LINE], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a los campos de destino [!DNL LINE], siga estos pasos:

Según la identidad de origen, se deben asignar las siguientes áreas de nombres de identidad de destino:
| Identidad de destino | Campo de Source | Campo de destino |
| — | — | — |
| ID para anunciantes (IFA) | `IDFA` o `GAID` | `LineId` |
| ID de usuario de LINE | `UserID` | `LineId` |

Si sus identidades de destino son *ID de usuario de LINE*, necesitará lo siguiente:
![Ejemplo de captura de pantalla de IU de Platform que muestra la asignación de destino al usar ID de usuario de LINE para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Si su identidad de destino es *ID para anunciantes (IFA)*, necesitará lo siguiente:
![Ejemplo de captura de pantalla de IU de Platform que muestra la asignación de Target al usar ID para anunciantes (IFA) para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validar exportación de datos {#exported-data}

Una vez que la exportación de datos del Experience Platform se ha realizado correctamente, el destino [!DNL LINE] crea una nueva audiencia dentro de [!DNL LINE] con el nombre de audiencia seleccionado.

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. En [!DNL LINE], inicie sesión en [Manager console](https://manager.line.biz/).

1. A continuación, vaya a **[!UICONTROL Controles de datos]** > **[!UICONTROL Audiencias]** y compruebe que el nombre coincida con la audiencia seleccionada en la columna **[!UICONTROL Nombre de audiencia]**.

1. El volumen actualizado coincidiría con el recuento dentro del segmento.

1. La columna *Tipo* mencionará **[!UICONTROL ID de usuario]** si las identidades que exportó son del tipo *ID de usuario*. De manera similar, la columna *Type* mencionará **[!UICONTROL ID de anuncio móvil]** si las identidades que exportó son del tipo *IDFA*.

A continuación se muestra un ejemplo de configuración en [!DNL LINE]:
![Captura de pantalla de la interfaz de usuario LINE que muestra el volumen de audiencia.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
