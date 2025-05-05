---
title: Conexión de Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP es un destino integrado para Adobe Real-time Customer Data Platform que le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 2%

---

# Conexión de Adobe Advertising Cloud DSP

## Información general {#overview}

El destino de Adobe Advertising Cloud DSP DSP [!DNL Demand-Side Platform] () le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas con los que tiene acceso. Para obtener más información acerca de la integración de Real-Time CDP DSP con las audiencias, consulte [Acerca de la activación de audiencias autenticadas a partir de fuentes de audiencia](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>DSP Esta página ha sido creada por el equipo de. Para cualquier consulta o solicitud de actualización, comuníquese directamente con la atención al cliente de Advertising Cloud al `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Advertising Cloud DSP, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso de publicidad de marca

Un minorista en línea quiere volver a dirigirse a sus clientes de alto valor a través de una campaña de visualización sin utilizar cookies para la segmentación. El minorista comparte una audiencia compuesta por los ID de correo electrónico con hash de sus clientes de alto valor, desde su cuenta de Adobe Real-time Customer Data Platform (Real-Time CDP DSP) a su cuenta de. DSP DSP a continuación, convierte los ID de correo electrónico con hash a [!DNL RampIDs] autenticados mediante una asociación entre y LiveRamp. El(la) [!DNL RampIDs] resultante se puede utilizar en una campaña de visualización para dirigirse a la audiencia.

### Caso de uso de agencia

DSP Una agencia de medios con una cuenta de está ejecutando una campaña de retargeting en nombre de su cliente, una marca líder en la industria de la hospitalidad. La marca quiere volver a dirigirse a todos sus clientes en el último año con una nueva oferta promocional. La marca hospeda toda la información de los invitados en [!DNL Real-Time CDP]. DSP La marca puede compartir una audiencia compuesta por los ID de correo electrónico con hash de sus invitados desde su cuenta de [!DNL Real-Time CDP] a la cuenta de la agencia de medios para redireccionar a los invitados a través de una campaña de medios.

## Requisitos previos {#prerequisites}

* DSP Configuración de nivel de cuenta y nivel de campaña para habilitar el uso compartido de audiencias con [!DNL LiveRamp RampID], lo cual traducirá los datos del cliente a [!DNL RampIDs] para crear segmentos direccionables. DSP El equipo de la cuenta de realizará esta configuración. DSP [!DNL RampID] está disponible a través de una asociación entre el usuario y el usuario [!DNL LiveRamp], y no necesita su propia suscripción a [!DNL LiveRamp] para utilizarlo.
* El ID de organización de Experience Cloud de la cuenta de Experience Platform. Puede encontrar su ID en la página de perfil de usuario [!DNL Real-Time CDP].
* DSP Un [[!DNL Real-Time CDP] origen en el ](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para recibir audiencias para la activación de la campaña. DSP El equipo de cuenta de su Experience Cloud creará el origen utilizando su ID de organización de la cuenta de usuario.
* DSP DSP La clave de origen de la cuenta o anunciante de la cuenta de, que se genera cuando se crea un origen de [[!DNL Real-Time CDP] en el espacio de trabajo de ](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP Su equipo de cuenta de la cuenta compartirá esta clave con usted. Lo usará dentro de Experience Platform para crear una conexión de destino al destino de Advertising Cloud DSP, como se [explica más abajo](#authenticate).
* Datos del cliente que consisten en correos electrónicos o correos electrónicos con hash.

## Identidades admitidas {#supported-identities}

El destino de Adobe Advertising Cloud DSP admite la activación de las identidades que se describen en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Experience Platform admite direcciones de correo electrónico de texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que el Experience Platform aplique automáticamente hash a los datos durante la activación. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la siguiente tabla para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de Advertising Cloud DSP. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarte al destino, necesitas el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de [Ver destinos]** y **[!UICONTROL Administrar destinos]** para el Experience Platform. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino, siga las instrucciones para [crear una conexión de destino](/help/destinations/ui/connect-destination.md) mediante la interfaz de usuario del Experience Platform. En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para conectarse al destino, proporcione el siguiente parámetro en la sección [!UICONTROL Tipo de conexión] y, a continuación, seleccione **[!UICONTROL Conectarse al destino]**.:

* **[!UICONTROL Clave de cuenta o anunciante]**: Esta [!UICONTROL clave de Source DSP] se genera cuando se crea un origen de [[!DNL Real-Time CDP] en la interfaz de usuario de la](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP El equipo de cuenta de la cuenta compartirá esta clave con usted una vez que cree el origen.

![Campo de tipo de conexión](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

![Campos de detalle de destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validar exportación de datos {#exported-data}

Para comprobar que la audiencia de datos se compartió con Advertising Cloud, haga lo siguiente:

* El flujo de datos en su destino [!DNL Real-Time CDP] se ha completado correctamente.

* DSP En la práctica, la audiencia está disponible cuando crea o edita una audiencia de [!UICONTROL Audiencias] > [!UICONTROL Todas las audiencias] o desde la sección [!UICONTROL Segmentación de audiencias] de la configuración de ubicación. La audiencia debe estar visible en la ficha [!UICONTROL Segmentos de Adobe] en la carpeta [!UICONTROL Real-Time CDP].

![Audiencias de Real-Time CDP DSP en la configuración de audiencias de la](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
