---
keywords: móvil;destinos de participación móvil;LINE;destino de participación móvil de LINE
title: Conexión LINE
description: El destino LINE le permite añadir perfiles a la audiencia de Platform y ofrecer experiencias personalizadas a los usuarios conectados.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# [!DNL LINE] conexión

## Información general {#overview}

[[!DNL LINE]](https://line.me/en/) es una popular plataforma de comunicación que conecta personas, servicios e información y que ha crecido desde una aplicación de chat hasta un centro para actividades de entretenimiento, sociales y diarias.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL LINE] API de mensajería](https://developers.line.biz/en/reference/messaging-api/). Puede activar perfiles de las audiencias de Experience Platform como conexiones dentro de [!DNL LINE] para sus necesidades empresariales.

[!DNL LINE] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL LINE] API de mensajería. Instrucciones para autenticarse en su [!DNL LINE] están más abajo, dentro de [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

Como especialista en marketing, puede segmentar usuarios en un destino de participación móvil, con audiencias integradas [!DNL Adobe Experience Platform]. Además, puede ofrecerles experiencias personalizadas en función de los atributos de sus [!DNL Adobe Experience Platform] perfiles, en cuanto las audiencias y los perfiles se actualicen en [!DNL Adobe Experience Platform].

## Requisitos previos {#prerequisites}

### [!DNL LINE] requisitos previos {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos [!DNL LINE], para exportar datos de Platform a su [!DNL LINE] cuenta:

#### Necesita tener un [!DNL LINE] account {#prerequisites-account}

Debe registrarse y crear un [!DNL LINE] cuenta, si aún no dispone de una. Para crear una cuenta de:

1. Vaya a [!DNL LINE] [inicio de sesión de cuenta](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) página
2. Seleccionar **[!UICONTROL Crear una cuenta]**.

#### Reúna los [!DNL LINE channel access token (long-lived)] desde el [!DNL LINE] consola para desarrolladores {#gather-credentials}

Para permitir que Platform acceda a [!DNL LINE] recursos, necesitará el complemento *[!DNL Channel access token (long-lived)]* desde el deseado [!DNL LINE] *API de mensajería* canal.

1. Inicie sesión con su [!DNL LINE] cuenta para el [[!DNL LINE] Consola para desarrolladores](https://developers.line.biz/console).
1. A continuación, acceda a *[!DNL Providers]* , luego seleccione la *[!DNL Provider]* de interés y, finalmente, seleccione la *API de mensajería* para acceder a su configuración. Si accede a la consola de desarrollador por primera vez, siga las [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para completar los pasos necesarios para crear un proveedor.
1. Finalmente, vaya a ***[!DNL Channel access token]*** y copie la sección ***[!DNL Channel access token (long-lived)]*** valor requerido en [Autenticar en el destino](#authenticate) paso.

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Su [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulte la [[!DNL LINE] documentación](https://developers.line.biz/en/docs/messaging-api/getting-started/) para obtener instrucciones sobre cómo crear un canal o añadir un canal a su [!DNL LINE] cuenta a través de [!DNL LINE] consola de desarrolladores.

## Identidades admitidas {#supported-identities}

[!DNL LINE] admite la actualización y exportación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| ID para anunciantes (IFA) | Seleccione la identidad de destino ID para anunciantes (IFA) cuando las identidades de origen sean IFA *(Apple ID para anunciantes)* o GAID *(Google Advertising ID). |
| ID de usuario de LINE | Seleccione la identidad de destino UserID cuando las identidades de origen sean ID de usuario de LINE. |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en [!DNL LINE] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL LINE]. También puede encontrarlo en la sección **[!UICONTROL Participación móvil]** categoría.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**.
![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Rellene los campos obligatorios siguientes.
* **[!UICONTROL Token de portador]**: su [!DNL LINE Channel access token (long-lived)] desde el [!DNL LINE] consola de desarrollador. Consulte la [recopilar credenciales](#gather-credentials) sección.

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Tipo de audiencia]**: Seleccionar **[!UICONTROL ID para anunciantes (IFA)]** si las identidades que desea exportar son del tipo *ID para anunciantes (IFA)*. Seleccionar **[!UICONTROL ID de usuario de LINE]** si las identidades que desea exportar son del tipo *ID de usuario de LINE*. Consulte la [Identidades admitidas](#supported-identities) para obtener más información sobre los tipos de identidad.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
>
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL LINE] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a [!DNL LINE] campos de destino, siga estos pasos:

Según la identidad de origen, se deben asignar las siguientes áreas de nombres de identidad de destino: | Identidad de destino | Campo de origen | Campo de destino | | — | — | — | | ID para anunciantes (IFA) | `IDFA` o `GAID` | `LineId` | | ID de usuario de LINE | `UserID` | `LineId` |

Si las identidades de destino son *ID de usuario de LINE* necesitará lo siguiente:
![Captura de pantalla de la IU de Platform que muestra la asignación de destino al utilizar ID de usuario de LINE para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Si la identidad de destinatario es *ID para anunciantes (IFA)* necesitará lo siguiente:
![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de Target al utilizar ID para anunciantes (IFA) para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validar exportación de datos {#exported-data}

Una vez que la exportación de datos de Experience Platform se haya realizado correctamente, la variable [!DNL LINE] destino crea una nueva audiencia dentro de [!DNL LINE] utilizando el nombre de audiencia seleccionado.

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Entrada [!DNL LINE], inicie sesión en [Consola de responsable](https://manager.line.biz/).

1. A continuación, vaya a **[!UICONTROL Controles de datos]** > **[!UICONTROL Audiencias]** y compruebe que el nombre coincida con la audiencia seleccionada en la **[!UICONTROL Nombre de audiencia]** columna.

1. El volumen actualizado coincidiría con el recuento dentro del segmento.

1. El *Tipo* La columna mencionará **[!UICONTROL UserID]** si las identidades exportadas son del tipo *UserID*. Del Mismo Modo, La *Tipo* La columna mencionará **[!UICONTROL ID de anuncio móvil]** si las identidades exportadas son del tipo *IDFA*.

Un ejemplo de configuración en [!DNL LINE] se muestra a continuación:
![Captura de pantalla de la IU de LINE que muestra el volumen de audiencia.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
