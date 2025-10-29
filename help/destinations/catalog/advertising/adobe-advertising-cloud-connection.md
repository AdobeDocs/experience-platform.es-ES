---
title: Conexión de Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP es un destino integrado para Adobe Real-Time Customer Data Platform que le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Conexión de Adobe Advertising Cloud DSP

## Información general {#overview}

El destino de Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas con DSP. Para obtener más información sobre la integración de Real-Time CDP con DSP, consulte [Acerca de la activación de audiencias autenticadas a partir de fuentes de audiencia](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Esta página ha sido creada por el equipo de DSP. Para cualquier consulta o solicitud de actualización, comuníquese directamente con la atención al cliente de Advertising Cloud al `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para comprender mejor cómo y cuándo debe utilizar el destino de Advertising Cloud DSP, los clientes de Adobe Experience Platform pueden usar este destino en algunos casos de uso.

### Caso de uso de publicidad de marca

Un retailer en línea quiere volver a dirigirse a sus clientes de alto valor a través de una campaña de visualización sin utilizar cookies para la segmentación. Retailer comparte una audiencia compuesta por los ID de correo electrónico con hash de sus clientes de alto valor, desde su cuenta de Adobe Real-Time Customer Data Platform (Real-Time CDP) a su cuenta de DSP. A continuación, DSP convierte los ID de correo electrónico con hash a [!DNL RampIDs] autenticados mediante una asociación entre DSP y LiveRamp. El(la) [!DNL RampIDs] resultante se puede utilizar en una campaña de visualización para dirigirse a la audiencia.

### Caso de uso de agencia

Una agencia de medios con una cuenta de DSP está ejecutando una campaña de resegmentación en nombre de su cliente, una marca líder en la industria de la hospitalidad. La marca quiere volver a dirigirse a todos sus clientes en el último año con una nueva oferta promocional. La marca hospeda toda la información de los invitados en [!DNL Real-Time CDP]. La marca puede compartir una audiencia compuesta por los ID de correo electrónico con hash de sus invitados desde su cuenta de [!DNL Real-Time CDP] a la cuenta de DSP de la agencia de medios para redireccionar a los invitados a través de una campaña de medios.

## Requisitos previos {#prerequisites}

* Configuración de nivel de cuenta y nivel de campaña de DSP para habilitar el uso compartido de audiencias con [!DNL LiveRamp RampID], lo cual traducirá los datos del cliente a [!DNL RampIDs] para crear segmentos direccionables. El equipo de la cuenta de DSP realizará esta configuración. [!DNL RampID] está disponible a través de una asociación entre DSP y [!DNL LiveRamp], y no necesita su propia pertenencia a [!DNL LiveRamp] para utilizarlo.
* El ID de organización de Experience Cloud de la cuenta de Experience Platform. Puede encontrar su ID en la página de perfil de usuario [!DNL Real-Time CDP].
* Un origen de [[!DNL Real-Time CDP] en DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para recibir audiencias para la activación de la campaña. El equipo de cuenta de DSP creará la fuente de datos con el ID de organización de Experience Cloud.
* Clave de origen de la cuenta o anunciante de DSP, que se genera cuando se crea un origen de [[!DNL Real-Time CDP] en DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de la cuenta de DSP compartirá esta clave con usted. Lo usará en Experience Platform para crear una conexión de destino al destino de DSP de Advertising Cloud, como se explica a continuación [1&rbrace;.](#authenticate)
* Datos del cliente que consisten en correos electrónicos o correos electrónicos con hash.

## Identidades admitidas {#supported-identities}

El destino de Adobe Advertising Cloud DSP admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Experience Platform admite direcciones de correo electrónico de texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que Experience Platform agregue automáticamente los datos al activarlos. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la siguiente tabla para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de DSP de Advertising Cloud. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL View Destinations]** y el **[!UICONTROL Manage Destinations]** [permiso de control de acceso](/help/access-control/home.md#permissions) para Experience Platform. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino, siga las instrucciones para [crear una conexión de destino](/help/destinations/ui/connect-destination.md) mediante la interfaz de usuario de Experience Platform. En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para conectarse al destino, proporcione el siguiente parámetro en la sección [!UICONTROL Connection type] y, a continuación, seleccione **[!UICONTROL Connect to destination]**.:

* **[!UICONTROL Account or Advertiser Key]**: este [!UICONTROL Source Key] se genera cuando se crea un [[!DNL Real-Time CDP] origen en la interfaz de usuario de DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de la cuenta de DSP compartirá esta clave con usted después de crear el origen.

![Campo de tipo de conexión](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.

![Campos de detalle de destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validar exportación de datos {#exported-data}

Para verificar que la audiencia de datos se compartió con Advertising Cloud, compruebe lo siguiente:

* El flujo de datos en su destino [!DNL Real-Time CDP] se ha completado correctamente.

* En DSP, la audiencia está disponible cuando crea o edita una audiencia de [!UICONTROL Audiences] > [!UICONTROL All Audiences] o desde la sección [!UICONTROL Audience Targeting] de la configuración de ubicación. La audiencia debe ser visible en la ficha [!UICONTROL Adobe Segments] bajo la carpeta [!UICONTROL Real-Time CDP].

![Audiencias de Real-Time CDP en la configuración de audiencias de DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
