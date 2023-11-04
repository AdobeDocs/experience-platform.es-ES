---
title: Conexión de Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP es un destino integrado para Adobe Real-time Customer Data Platform que le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---

# Conexión de Adobe Advertising Cloud DSP

## Información general {#overview}

El Adobe Advertising Cloud [!DNL Demand-Side Platform] DSP DSP () el destino le permite compartir audiencias de origen autenticadas con anunciantes y usuarios aprobados para la activación de campañas de con los anunciantes y los usuarios de la campaña de la manera más segura y con más frecuencia. Para obtener más información acerca de la integración de Real-Time CDP DSP con la aplicación, consulte la sección sobre la integración con la aplicación de [Acerca de la activación de audiencias autenticadas a partir de fuentes de audiencia](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>DSP Esta página ha sido creada por el equipo de. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con el servicio de asistencia de Advertising Cloud en `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Advertising Cloud DSP, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso de publicidad de marca

Un minorista en línea quiere volver a dirigirse a sus clientes de alto valor a través de una campaña de visualización sin utilizar cookies para la segmentación. El minorista comparte una audiencia compuesta por los ID de correo electrónico con hash de sus clientes de alto valor, desde su cuenta de Adobe Real-time Customer Data Platform (Real-Time CDP DSP) a su cuenta de. DSP a continuación, convierte los ID de correo electrónico con hash a autenticados [!DNL RampIDs] DSP a través de una asociación entre el grupo de trabajo de la red de y LiveRamp. El resultante [!DNL RampIDs] se puede utilizar en una campaña de visualización para dirigirse a la audiencia.

### Caso de uso de agencia

DSP Una agencia de medios con una cuenta de está ejecutando una campaña de retargeting en nombre de su cliente, una marca líder en la industria de la hospitalidad. La marca quiere volver a dirigirse a todos sus clientes en el último año con una nueva oferta promocional. La marca aloja toda la información de los huéspedes en [!DNL Real-Time CDP]. La marca puede compartir una audiencia compuesta por los ID de correo electrónico con hash de sus invitados desde su [!DNL Real-Time CDP] DSP cuenta a la cuenta de la agencia de medios para redirigirse a los invitados a través de una campaña de medios.

## Requisitos previos {#prerequisites}

* DSP Configuración de nivel de cuenta y nivel de campaña para habilitar el uso compartido de audiencias con [!DNL LiveRamp RampID], que traducirá los datos del cliente a [!DNL RampIDs] para crear segmentos segmentables. DSP El equipo de la cuenta de realizará esta configuración. [!DNL RampID] DSP está disponible a través de una asociación entre y [!DNL LiveRamp], y no necesitas los tuyos propios [!DNL LiveRamp] abono para utilizarlo.
* El ID de organización de Experience Cloud de la cuenta de Experience Platform. Puede encontrar su ID en su [!DNL Real-Time CDP] página de perfil de usuario.
* A [[!DNL Real-Time CDP] DSP origen en la](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para recibir audiencias para la activación de campañas. DSP El equipo de cuenta de su Experience Cloud creará el origen utilizando su ID de organización de la cuenta de usuario.
* DSP La clave de origen de la cuenta o el anunciante de la cuenta de, que se genera cuando se crea un [[!DNL Real-Time CDP] DSP El origen se crea en el](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP Su equipo de cuenta de la cuenta compartirá esta clave con usted. Lo utilizará en Experience Platform para crear una conexión de destino al destino de Advertising Cloud DSP, como [explicado a continuación](#authenticate).
* Datos del cliente que consisten en correos electrónicos o correos electrónicos con hash.

## Identidades admitidas {#supported-identities}

El destino de Adobe Advertising Cloud DSP admite la activación de las identidades que se describen en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Experience Platform admite direcciones de correo electrónico de texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción para que el Experience Platform hash automáticamente los datos en la activación. |

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
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions) para el Experience Platform. Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino, siga las instrucciones a [crear una conexión de destino](/help/destinations/ui/connect-destination.md) uso de la interfaz de usuario del Experience Platform. En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para conectarse al destino, proporcione el siguiente parámetro en la variable [!UICONTROL Tipo de conexión] , y luego seleccione **[!UICONTROL Conectar con destino]**.:

* **[!UICONTROL Cuenta o clave del anunciante]**: esto [!UICONTROL Clave de origen] se genera cuando un [[!DNL Real-Time CDP] DSP El origen de se crea en la interfaz de usuario de](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). DSP El equipo de cuenta de la cuenta compartirá esta clave con usted una vez que cree el origen.

![Campo Tipo de conexión](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

![Campos de detalles de destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validar exportación de datos {#exported-data}

Para comprobar que la audiencia de datos se compartió con Advertising Cloud, haga lo siguiente:

* El flujo de datos en su [!DNL Real-Time CDP] el destino se ha realizado correctamente.

* DSP En la práctica, la audiencia está disponible cuando crea o edita una audiencia desde [!UICONTROL Audiencias] > [!UICONTROL Todas las audiencias] o desde dentro de [!UICONTROL Segmentación de audiencia] de la configuración de ubicación. La audiencia debe ser visible en el [!UICONTROL Segmentos de Adobe] debajo de la pestaña [!UICONTROL Real-Time CDP] carpeta.

![Audiencias de Real-Time CDP DSP en la configuración de audiencia de](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
