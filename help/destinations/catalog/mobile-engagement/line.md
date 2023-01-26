---
keywords: móvil;destinos de participación móvil;LINE;destino de participación móvil LINE
title: Conexión LINE
description: El destino LINE le permite añadir perfiles al segmento de plataforma y ofrecer experiencias personalizadas a los usuarios conectados.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# [!DNL LINE] connection

## Información general {#overview}

[[!DNL LINE]](https://line.me/en/) es una popular plataforma de comunicación que conecta personas, servicios e información y que ha pasado de ser una aplicación de chat a ser un centro de actividades de entretenimiento, sociales y diarias.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL LINE] API de mensajería](https://developers.line.biz/en/reference/messaging-api/). Puede activar perfiles de los segmentos del Experience Platform como conexiones dentro de [!DNL LINE] para sus necesidades empresariales.

[!DNL LINE] utiliza los tokens del portador como mecanismo de autenticación para comunicarse con el [!DNL LINE] API de mensajería. Instrucciones para autenticarse en su [!DNL LINE] más abajo, dentro de [Autenticar en destino](#authenticate) para obtener más información.

## Casos de uso {#use-cases}

Como especialista en marketing, puede dirigirse a usuarios en un destino de participación móvil, con segmentos incorporados [!DNL Adobe Experience Platform]. Además, puede ofrecerles experiencias personalizadas en función de los atributos de sus [!DNL Adobe Experience Platform] perfiles, en cuanto los segmentos y perfiles se actualicen en [!DNL Adobe Experience Platform].

## Requisitos previos {#prerequisites}

### [!DNL LINE] requisitos previos {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos en [!DNL LINE], para exportar datos de Platform a su [!DNL LINE] cuenta:

#### Debe tener un [!DNL LINE] account {#prerequisites-account}

Debe registrarse y crear un [!DNL LINE] cuenta, si todavía no tiene una. Para crear una cuenta:

1. Vaya a la [!DNL LINE] [inicio de sesión en la cuenta](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) página
2. Select **[!UICONTROL Crear una cuenta]**.

#### Recopile el [!DNL LINE channel access token (long-lived)] de la variable [!DNL LINE] consola de desarrollador {#gather-credentials}

Para permitir que Platform acceda [!DNL LINE] recursos, necesitará la variable *[!DNL Channel access token (long-lived)]* de la [!DNL LINE] *API de mensajería* canal.

1. Inicie sesión con su [!DNL LINE] a [[!DNL LINE] Developer Console](https://developers.line.biz/console).
1. A continuación, acceda al *[!DNL Providers]* y, a continuación, seleccione la *[!DNL Provider]* de interés y, finalmente, seleccione el *API de mensajería* para acceder a su configuración. Si accede a la consola del desarrollador por primera vez, siga la [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para completar los pasos necesarios para crear un proveedor.
1. Finalmente, vaya a la ***[!DNL Channel access token]*** y copie la ***[!DNL Channel access token (long-lived)]*** valor requerido en [Autenticar en destino](#authenticate) paso a paso.

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Su [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulte la [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para obtener instrucciones sobre la creación de un canal o la adición de un canal al [!DNL LINE] a través de [!DNL LINE] consola de desarrolladores.

## Identidades compatibles {#supported-identities}

[!DNL LINE] admite la actualización y exportación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| ID para anunciantes (IFA) | Seleccione la identidad de destino ID para anunciantes (IFA) cuando las identidades de origen sean IFA *(Apple ID para anunciantes)* o Áreas de nombres de GAID *(Google Advertising ID). |
| ID de usuario de LINE | Seleccione la identidad de destino UserID cuando las identidades de origen sean ID de usuario LINE. |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable [!DNL LINE] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL LINE]. También puede localizarlo en la sección **[!UICONTROL Participación móvil]** categoría.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo autenticarse.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Complete los campos obligatorios a continuación.
* **[!UICONTROL Token portador]**: Su [!DNL LINE Channel access token (long-lived)] de la variable [!DNL LINE] consola para desarrolladores. Consulte la [recopilar credenciales](#gather-credentials) para obtener más información.

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Platform que muestra los detalles del destino.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Tipo de audiencia]**: Select **[!UICONTROL ID para anunciantes (IFA)]** si las identidades que desea exportar son del tipo *ID para anunciantes (IFA)*. Select **[!UICONTROL ID de usuario de LINE]** si las identidades que desea exportar son del tipo *ID de usuario de LINE*. Consulte la [Identidades compatibles](#supported-identities) para obtener más información sobre los tipos de identidad.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
>
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Asignación de atributos e identidades {#map}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL LINE] destino, debe pasar por el paso de asignación de campos. La asignación consiste en la creación de un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a la variable [!DNL LINE] campos de destino, siga estos pasos:

Según la identidad de origen, se deben asignar los siguientes espacios de nombres de identidad de destino: | Identidad de Target | Campo de origen | Campo Target | | — | — | — | | ID para anunciantes (IFA) | `IDFA` o `GAID` | `LineId` | | ID de usuario de LINE | `UserID` | `LineId` |

Si las identidades objetivo son *ID de usuario de LINE* necesitará lo siguiente:
![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de Target al usar los ID de usuario de LINE para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Si la identidad objetivo es *ID para anunciantes (IFA)* necesitará lo siguiente:
![Captura de pantalla de la interfaz de usuario de la plataforma que muestra la asignación de Target al usar ID para anunciantes (IFA) para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validación de la exportación de datos {#exported-data}

Cuando la exportación de datos se realiza correctamente desde el Experience Platform, la variable [!DNL LINE] destination crea una nueva audiencia en [!DNL LINE] utilizando el nombre de segmento seleccionado.

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. En [!DNL LINE], inicie sesión en el [Consola de administrador](https://manager.line.biz/).

1. A continuación, vaya a **[!UICONTROL Controles de datos]** > **[!UICONTROL Audiencias]** y compruebe el nombre que coincide con el segmento seleccionado dentro de la variable **[!UICONTROL Nombre de la audiencia]** para abrir el Navegador.

1. El volumen actualizado coincidiría con el recuento dentro del segmento.

1. La variable *Tipo* mención de columna **[!UICONTROL UserID]** si las identidades exportadas son del tipo *UserID*. Del Mismo Modo, El *Tipo* mención de columna **[!UICONTROL ID de publicidad móvil]** si las identidades exportadas son del tipo *IDFA*.

Un ejemplo de configuración dentro de [!DNL LINE] se muestra a continuación:
![Captura de pantalla de la interfaz de usuario de LINE que muestra el volumen de audiencia.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
