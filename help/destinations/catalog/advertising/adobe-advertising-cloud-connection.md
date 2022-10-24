---
title: Conexión Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP es un destino integrado para Adobe Real-time Customer Data Platform, que le permite compartir segmentos de origen autenticados con anunciantes y usuarios aprobados para la activación de campañas.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# Conexión Adobe Advertising Cloud DSP

## Información general {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) el destino le permite compartir segmentos de origen autenticados con anunciantes y usuarios aprobados para la activación de campañas con DSP. Para obtener más información sobre la integración de Real-Time CDP con DSP, consulte [Acerca de la activación de segmentos autenticados desde fuentes de audiencia](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Esta página la creó el equipo de DSP. Para cualquier solicitud de consulta o actualización, póngase en contacto con el servicio de asistencia técnica de Advertising Cloud directamente en `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Advertising Cloud DSP, estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso de publicidad de marca

Un minorista en línea quiere redirigir a sus clientes de alto valor a través de una campaña de visualización sin usar cookies para el objetivo. El minorista comparte un segmento que consta de los ID de correo electrónico con hash de sus clientes de alto valor desde su cuenta de Adobe Real-time Customer Data Platform (Real-Time CDP) a su cuenta de DSP. DSP convierte los ID de correo electrónico con hash en autenticados [!DNL RampIDs] mediante una asociación entre DSP y LiveRamp. El resultado [!DNL RampIDs] se puede usar en una campaña de visualización para dirigirse al público.

### Caso de uso de la agencia

Una agencia de medios con una cuenta DSP está ejecutando una campaña de redireccionamiento en nombre de su cliente, una marca de primera categoría en la industria hotelera. La marca quiere redirigirse a todos sus invitados en el último año con una nueva oferta promocional. La marca aloja toda la información de los invitados en [!DNL Real-Time CDP]. La marca puede compartir un segmento que consta de los ID de correo electrónico con hash de sus invitados desde su [!DNL Real-Time CDP] cuenta a la cuenta de DSP de la agencia de medios para redirigirse a los invitados a través de una campaña de medios.

## Requisitos previos {#prerequisites}

* DSP la configuración de nivel de cuenta y nivel de campaña para permitir el uso compartido de segmentos con [!DNL LiveRamp RampID], que traducirá los datos de los clientes a [!DNL RampIDs] para crear segmentos con objetivo. El equipo de su cuenta de DSP realizará esta configuración. [!DNL RampID] está disponible mediante una asociación entre DSP y [!DNL LiveRamp], y no necesita el suyo propio [!DNL LiveRamp] membresía para utilizarla.
* El ID de organización del Experience Cloud para la cuenta del Experience Platform. Puede encontrar su ID en su [!DNL Real-Time CDP] página de perfil de usuario.
* A [[!DNL Real-Time CDP] fuente en DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para recibir segmentos para la activación de campañas. El equipo de su cuenta de DSP creará la fuente con su ID de organización de Experience Cloud.
* La clave de origen de la cuenta de DSP o del anunciante, que se genera cuando se [[!DNL Real-Time CDP] el origen se crea en DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de su cuenta de DSP compartirá esta clave con usted. Lo utilizará en Experience Platform para crear una conexión de destino con el destino de Advertising Cloud DSP, como [se explica a continuación](#authenticate).
* Datos del cliente consistentes en correos electrónicos o correos electrónicos con hash.

## Identidades compatibles {#supported-identities}

El destino de Adobe Advertising Cloud DSP admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Experience Platform admite direcciones de correo electrónico con texto sin formato y con hash SHA 256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para que el Experience Platform hash automáticamente almacene los datos en el hash al activarlos. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la siguiente tabla para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de Advertising Cloud DSP. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Cuando un perfil se actualiza en Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions) para Experience Platform. Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino, siga las instrucciones para [crear una conexión de destino](/help/destinations/ui/connect-destination.md) uso de la interfaz de usuario de Experience Platform. En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para conectarse al destino, proporcione el siguiente parámetro en la variable [!UICONTROL Tipo de conexión] y, a continuación, seleccione **[!UICONTROL Conectarse al destino]**.:

* **[!UICONTROL Cuenta o clave del anunciante]**: Esta [!UICONTROL Clave de origen] se genera cuando una [[!DNL Real-Time CDP] el origen se crea en la interfaz de usuario de DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de su cuenta de DSP compartirá esta clave con usted después de crear la fuente.

![Campo de tipo de conexión](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.

![Campos de detalles de destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Validación de la exportación de datos {#exported-data}

Para verificar que el segmento de datos se compartió con Advertising Cloud, compruebe lo siguiente:

* El flujo de datos de su [!DNL Real-Time CDP] el destino se ha realizado correctamente.

* En DSP, el segmento está disponible al crear o editar una audiencia desde [!UICONTROL Audiencias] > [!UICONTROL Todas las audiencias] o desde dentro de [!UICONTROL Segmentación de audiencia] de la configuración de ubicación. El segmento debe ser visible en la variable [!UICONTROL Segmentos de Adobe] en la pestaña [!UICONTROL Real-Time CDP] carpeta.

![Segmentos de Real-Time CDP en DSP configuración de audiencia](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
