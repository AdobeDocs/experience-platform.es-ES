---
keywords: conexión de linkedin;conexión de linkedin;destinos de linkedin;linkedin;
title: Conexión de audiencias coincidentes de Linkedin
description: Active perfiles para sus campañas de LinkedIn para la segmentación, personalización y supresión de audiencias, en función de los correos electrónicos con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] conexión

## Información general {#overview}

Activar perfiles para su [!DNL LinkedIn] campañas de segmentación, personalización y supresión de audiencias, basadas en correos electrónicos con hash e ID móviles.

![Destino linkedIn en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo usar el [!DNL LinkedIn Matched Audiences] Destino, este es un caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

Una empresa de software organiza una conferencia y desea mantenerse en contacto con los participantes y mostrarles ofertas personalizadas basadas en su estado de asistencia a la conferencia. La empresa puede introducir direcciones de correo electrónico o ID de dispositivos móviles desde su propio equipo [!DNL CRM] en Adobe Experience Platform. A continuación, puede crear audiencias a partir de sus propios datos sin conexión y enviarlas a [!DNL LinkedIn] plataforma social, optimizando su gasto en publicidad.

## Identidades admitidas {#supported-identities}

[!DNL LinkedIn Matched Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | ID de publicidad de Google | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice las áreas de nombres adecuadas para los correos electrónicos de texto sin formato y con hash, respectivamente. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe todas las audiencias que puede exportar a este destino.

Todos los destinos admiten la activación de audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

Además, este destino también admite la activación de las audiencias que se describen en la tabla siguiente.

| Tipo de audiencia | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias introducidas en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono y otros) utilizados en [!DNL LinkedIn Matched Audiences] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos de cuenta de linkedIn {#LinkedIn-account-prerequisites}

Antes de usar el [!UICONTROL Audiencia coincidente de linkedIn] destino, asegúrese de que su [!DNL LinkedIn Campaign Manager] La cuenta tiene el [!DNL Creative Manager] nivel de permiso o superior.

Para obtener información sobre cómo editar su [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Agregar, editar y quitar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL LinkedIn Matched Audiences] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o ID de dispositivos móviles.

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes.

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico en borrar en Experience Platform, y tener [!DNL Platform] hash en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [introducción a la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) y el [información general sobre ingesta de streaming](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios iniciales y finales de la cadena de correo electrónico. Por ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al crear valores hash de las cadenas de correo electrónico, asegúrese de usar la cadena en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúscula
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No salar la cuerda.

>[!NOTE]
>
>Los datos de áreas de nombres sin hash se cifran automáticamente en hash mediante [!DNL Platform] tras la activación.
> Los datos de origen de los atributos no se cifran automáticamente.
> 
> Durante el [Asignación de identidad](../../ui/activate-segment-streaming-destinations.md#mapping) paso, cuando el campo de origen contenga atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación.
> 
> El **[!UICONTROL Aplicar transformación]** Esta opción solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir áreas de nombres.

![Transformación de asignación de identidad](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

El siguiente vídeo también muestra los pasos para configurar una [!DNL LinkedIn Matched Audiences] Destino y activación de audiencias.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde que se grabó este vídeo. Para obtener la información más actualizada, consulte la [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticar en el destino {#authenticate}

1. Busque el [!DNL LinkedIn Matched Audiences] en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccionar **[!UICONTROL Conectar con destino]**.
   ![Autenticar en LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Introduzca sus credenciales de LinkedIn y seleccione **Iniciar sesión**.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID de cuenta"
>abstract="El ID de cuenta de LinkedIn Campaign Manager. Puede encontrar este ID en su cuenta de LinkedIn Campaign Manager."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL LinkedIn Campaign Manager Account ID]. Puede encontrar este ID en su [!DNL LinkedIn Campaign Manager] cuenta.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Una activación correcta significa que un [!DNL LinkedIn] la audiencia personalizada se crearía mediante programación en [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). La pertenencia a audiencias se añadiría y eliminaría a medida que los usuarios se calificaran o descalificaran para las audiencias activadas.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL LinkedIn Matched Audiences] admite rellenos de audiencia históricos. Todas las cualificaciones de audiencia históricas se envían a [!DNL LinkedIn] al activar las audiencias en el destino.
