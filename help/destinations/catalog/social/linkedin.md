---
keywords: conexión linkedin;conexión linkedin;destinos linkedin;linkedin;
title: Conexión de audiencias coincidentes de Linkedin
description: Active perfiles para sus campañas de LinkedIn para segmentación, personalización y supresión de audiencias, en función de correos electrónicos con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] connection

## Información general {#overview}

Activar perfiles para [!DNL LinkedIn] campañas para segmentación, personalización y supresión de audiencias, basadas en correos electrónicos con hash e ID móviles.

![Destino de linkedIn en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo usar la variable [!DNL LinkedIn Matched Audiences] destino, este es un caso de uso que los clientes de Adobe Experience Platform pueden resolver utilizando esta función.

Una empresa de software organiza una conferencia y quiere mantenerse en contacto con los participantes, y mostrarles ofertas personalizadas basadas en su estado de asistencia a la conferencia. La empresa puede ingerir direcciones de correo electrónico o ID de dispositivos móviles por su cuenta [!DNL CRM] en Adobe Experience Platform. A continuación, pueden generar segmentos a partir de sus propios datos sin conexión y enviarlos al [!DNL LinkedIn] plataforma social, optimizando su gasto publicitario.

## Identidades compatibles {#supported-identities}

[!DNL LinkedIn Matched Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para el texto sin formato y los correos electrónicos con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |

{style="table-layout:auto"}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono y otros) utilizados en la variable [!DNL LinkedIn Matched Audiences] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos de cuenta de linkedIn {#LinkedIn-account-prerequisites}

Antes de usar la variable [!UICONTROL Audiencia coincidente de linkedIn] destino, asegúrese de que su [!DNL LinkedIn Campaign Manager] La cuenta tiene el [!DNL Creative Manager] nivel de permiso o superior.

Para aprender a editar su [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Agregar, editar y eliminar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL LinkedIn Matched Audiences] se puede desactivar *hash* identificadores, como direcciones de correo electrónico o ID de dispositivos móviles.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform o utilizar las direcciones de correo electrónico claramente en Experience Platform, y [!DNL Platform] Hágalos en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta de lotes](/help/ingestion/batch-ingestion/overview.md) y [información general sobre la ingesta de transmisión](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios al principio y al final de la cadena de correo electrónico. Por ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al hash de las cadenas de correo electrónico, asegúrese de usar un hash para la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No sal la cadena.

>[!NOTE]
>
>Los datos de las áreas de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarse.
> Los datos de origen de atributos no se colocan automáticamente en hash.
> 
> Durante el [Asignación de identidades](../../ui/activate-segment-streaming-destinations.md#mapping) cuando el campo de origen contenga atributos sin hash, marque la casilla **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos.
> 
> La variable **[!UICONTROL Aplicar transformación]** solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir espacios de nombres.

![Transformación de asignación de identidad](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

El siguiente vídeo muestra también los pasos para configurar un [!DNL LinkedIn Matched Audiences] dirigir y activar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde la grabación de este vídeo. Para obtener la información más actualizada, consulte la [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticar en destino {#authenticate}

1. Busque la [!DNL LinkedIn Matched Audiences] destino en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Select **[!UICONTROL Conectarse al destino]**.
   ![Autenticar en LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Introduzca sus credenciales de LinkedIn y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID de cuenta"
>abstract="El ID de cuenta de LinkedIn Campaign Manager. Puede encontrar este ID en su cuenta de LinkedIn Campaign Manager."

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su [!DNL LinkedIn Campaign Manager Account ID]. Puede encontrar este ID en su [!DNL LinkedIn Campaign Manager] cuenta.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Una activación correcta significa que [!DNL LinkedIn] la audiencia personalizada se crearía mediante programación en [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). La pertenencia a segmentos en la audiencia se agregaría y eliminaría ya que los usuarios están cualificados o no cumplen los requisitos para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL LinkedIn Matched Audiences] admite los rellenos históricos de audiencia. Todas las cualificaciones históricas de segmentos se envían a [!DNL LinkedIn] al activar los segmentos en el destino.
