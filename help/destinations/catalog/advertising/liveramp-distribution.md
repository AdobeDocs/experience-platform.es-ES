---
title: 'LiveRamp: conexión de distribución'
description: Aprenda a utilizar el conector LiveRamp - Distribution para activar audiencias previamente integradas en LiveRamp a otros destinos publicitarios.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 40%

---


# [!DNL LiveRamp - Distribution] conexión {#liveramp-onboarding}

El [!DNL LiveRamp - Distribution] La conexión de le permite activar audiencias de Experience Platform a premium publishers en medios móviles, web, de visualización y de TV conectados.

>[!IMPORTANT]
>
>LiveRamp crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con LiveRamp [aquí](mailto:example@email.com).

## Destinos admitidos {#supported-destinations}

[!DNL LiveRamp - Distribution] actualmente admite la activación de audiencias en las siguientes plataformas:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL LiveRamp - Distribution] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

El equipo de marketing de un minorista de ropa deportiva utilizó el [LiveRamp: incorporación](liveramp-onboarding.md) para enviar audiencias desde Experience Platform a su cuenta de LiveRamp.

A través de [!DNL LiveRamp - Distribution] conexión ahora pueden almacenar en déclencheur la activación de las audiencias integradas en los destinos mencionados en la parte superior de esta página, para que puedan dirigirse a los usuarios en dispositivos móviles, web abierta, sociales y [!DNL CTV] plataformas.

## Incorporar audiencias a LiveRamp {#onboarding}

Antes de activar audiencias a través de [!DNL LiveRamp - Distribution] conexión, utilice el [LiveRamp: incorporación](liveramp-onboarding.md) para exportar las audiencias de Experience Platform a LiveRamp.

Una vez incorporadas las audiencias a LiveRamp, continúe con el flujo de trabajo de activación desde el [conectar con el destino](#connect) paso.

## Conectar con el destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Configuración de identificador"
>abstract="Seleccione los identificadores admitidos por el destino. Consulte la documentación para obtener la lista completa de identificadores admitidos por cada destino."

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en LiveRamp {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Imagen de la IU de Platform que muestra el archivo screen.l de conexión de destino](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL URL de token]**: su URL de token de LiveRamp.
* **[!UICONTROL ID de organización de LiveRamp]**: ID de organización de su cuenta de LiveRamp.
* **[!UICONTROL Nombre de usuario]**: su nombre de usuario de cuenta de LiveRamp.
* **[!UICONTROL Contraseña]**: la contraseña de su cuenta de LiveRamp.

### Configurar detalles del destino {#destination-details}

Una vez que se haya conectado correctamente a su cuenta de LiveRamp, introduzca la información necesaria para conectarse al destino en el que desea activar las audiencias.

![Imagen de la interfaz de usuario de Platform que muestra los detalles de destino screen.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para la conexión de destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para el destino. Utilice una descripción que le ayude a identificar fácilmente el propósito de este destino.
* **[!UICONTROL Destino]**: utilice el menú desplegable para seleccionar el destino al que desea activar las audiencias. El destino que seleccione aquí afecta directamente a lo que se ve en la [configuración específica del destino](#destination-settings) pantalla.
* **[!UICONTROL Integración]**: seleccione la cuenta de integración que desee utilizar para el destino.
* **[!UICONTROL Identificador]**: Seleccione los identificadores admitidos por el destino. Actualmente, todos los destinos tienen los identificadores admitidos rellenados previamente en el menú desplegable.

## Configuración específica del destino {#destination-settings}

Cada uno de los destinos [compatible](#supported-destinations) por [!DNL LiveRamp - Onboarding] requiere que rellene opciones de configuración específicas.

Consulte las secciones siguientes para obtener instrucciones detalladas sobre cómo configurar cada destino.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="ID del perfil de marca de 4C"
>abstract="Introduzca el ID numérico asociado con su perfil de marca de 4C. Si no tiene este ID, póngase en contacto con su representante de servicios del cliente de 4C."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Acuerdo de términos sobre el destino de los datos del anunciante"
>abstract="Escriba `I AGREE` para confirmar el reconocimiento y la aceptación de los términos de datos del anunciante de Disney."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Leer el acuerdo"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Su dirección de correo electrónico"
>abstract="Introduzca una dirección de correo electrónico vinculada a un individuo. Esta dirección de correo electrónico sirve como firma del acuerdo de términos de datos del anunciante. También se utilizará esta dirección de correo electrónico para ponernos en contacto con usted si fuera necesario."

Para configurar los detalles del destino, rellene los campos siguientes.

![Imagen de la IU de Platform que muestra los campos de datos del cliente para el destino de Disney.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Acuerdo de términos de destino de datos del anunciante]**: escribir en `I AGREE` para confirmar el reconocimiento y el acuerdo de los términos de datos del anunciante de Disney.
* **[!UICONTROL Nombre del cliente]**: introduzca el nombre de su empresa tal como desea que se muestre al socio de destino.
* **[!UICONTROL Correo electrónico]**: introduzca una dirección de correo electrónico vinculada a un individuo. Esta dirección de correo electrónico sirve como firma del acuerdo de términos de datos del anunciante.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Nombre del proveedor de datos"
>abstract="El nombre de su compañía tal y como desea que se muestre a Pandora. El nombre puede incluir un máximo de 40 caracteres en minúsculas y alfanuméricos (p. ej. Mi_Empresa)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="Dirección de correo electrónico del representante de la cuenta"
>abstract="La dirección de correo electrónico del representante de su cuenta de Pandora. Esta dirección se utiliza para enviar actualizaciones de taxonomía. Para introducir varias direcciones, sepárelas con comas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="Correo electrónico Dirección"
>abstract="Esta dirección se utiliza para enviar actualizaciones de taxonomía. Para introducir varias direcciones, sepárelas con comas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nombre de la cuenta"
>abstract="El nombre de su cuenta de Pandora. Póngase en contacto con el representante de su cuenta de Pandora si no está seguro de cuál es su nombre de cuenta. No utilice espacios ni caracteres especiales."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="ID de anunciante de Reddit"
>abstract="Su ID de anunciante de Reddit. Debe comenzar por &quot;t2_&quot; o &quot;a2_&quot;. Póngase en contacto con su representante de Reddit si no conoce su ID de anunciante."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nombre de anunciante de Reddit"
>abstract="Su nombre de anunciante de Reddit. No utilice espacios ni caracteres especiales."

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Dirección de correo electrónico de la cuenta de Roku"
>abstract="Introduzca la dirección de correo electrónico asociada a su cuenta de Roku."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Dirección de correo electrónico del representante de la cuenta de Roku"
>abstract="Introduzca la dirección de correo electrónico del representante de su cuenta de Roku. Esta dirección se utiliza para enviar actualizaciones de taxonomía. Para introducir varias direcciones, sepárelas con comas."

Para configurar los detalles del destino, rellene los campos siguientes.

![Imagen de la IU de Platform que muestra los identificadores admitidos para el destino Roku.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Dirección de correo electrónico de la cuenta Roku]**: Introduzca la dirección de correo electrónico asociada a su cuenta de Roku.
* **[!UICONTROL Dirección de correo electrónico del representante de cuentas Roku]**: introduzca la dirección de correo electrónico del representante de la cuenta de Roku. Para introducir varias direcciones, sepárelas con comas.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Token de cuenta"
>abstract="Identificador alfanumérico que indica a Spotify dónde trasladar los datos y le informa de que está autorizado para usar este flujo de trabajo. Póngase en contacto con el administrador de su cuenta de Spotify para obtener este token."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Dirección de correo electrónico del administrador de cuentas"
>abstract="La dirección de correo electrónico del administrador de cuentas de Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nombre del cliente"
>abstract="El nombre de la cuenta del anunciante, tal como desea que se muestre al socio de destino. Utilice el nombre de su empresa. No utilice espacios ni caracteres especiales."

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, lea la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

El [!DNL LiveRamp - Distribution] activa audiencias que ya se han incorporado a su cuenta de LiveRamp a través de la [LiveRamp: incorporación](liveramp-onboarding.md) conexión.

Para activar correctamente las audiencias, en este paso debe seleccionar **mismas audiencias** que ha incorporado anteriormente a LiveRamp.

>[!IMPORTANT]
>
>Déclencheur La selección de audiencias que no se hayan incorporado anteriormente a LiveRamp no afectará a la incorporación de las nuevas audiencias.

## Datos exportados / Validar exportación de datos {#exported-data}

Para verificar y monitorear la activación de sus audiencias, inicie sesión en su cuenta de LiveRamp y compruebe las métricas de activación.

Si tiene preguntas sobre la activación de audiencia, póngase en contacto con el representante de su cuenta de LiveRamp.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener más información sobre cómo configurar su [!DNL LiveRamp - Onboarding] , consulte la [documentación oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
