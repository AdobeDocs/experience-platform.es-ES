---
title: Conexión de Adobe Advertising DSP
description: Obtenga información sobre cómo compartir audiencias de origen autenticadas y no autenticadas con Adobe Advertising Cloud Demand-Side Platform (DSP) mediante varios tipos de identidad.
feature: Destinations
source-git-commit: 5513e95637c1016caeb6abe699e1807cc234ed40
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 2%

---


# Conexión de Adobe Advertising DSP

## Información general {#overview}

El destino Adobe Advertising Cloud Demand-Side Platform (DSP) permite a los usuarios compartir audiencias de origen autenticadas y no autenticadas con una cuenta de DSP o con un anunciante específico dentro de una cuenta.

Este destino permite a los clientes compartir audiencias de origen con cualquiera o todos estos ID:

* ID de correo electrónico con hash, que se convierte en [!DNL LiveRamp RampID] o [!DNL Unified ID 2.0] (UID2.0) para la segmentación en DSP

* Cookies de terceros de Experience Cloud ID (ECID) y Adobe Advertising

* ID de publicidad móvil (MAID):

   * [!DNL Google] Advertising ID (GAID) para [!DNL Android] dispositivos

   * Identificadores para anunciantes (IDFA) para [!DNL Apple iOS] dispositivos

Esta conexión reemplaza la [conexión heredada de Adobe Advertising Cloud DSP](adobe-advertising-cloud-connection-legacy.md), que solo admite direcciones de correo electrónico con hash.

>[!IMPORTANT]
>
>Esta página fue creada por el equipo de Adobe Advertising [!DNL DSP]. Para cualquier consulta o solicitud de actualización, comuníquese directamente con la atención al cliente de Advertising Cloud al `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Este destino permite a los anunciantes llegar a su audiencia a través de los navegadores con cookies y sin cookies.

Los anunciantes tienen la opción de compartir segmentos con identificadores de origen autenticados (como [!DNL RampID] y [!DNL UID2.0]) o como ID no autenticados (como cookies y MAID).

## Requisitos previos {#prerequisites}

* Para [!DNL RampID activation], [!DNL DSP] la configuración de nivel de cuenta y de nivel de campaña para habilitar el uso compartido de audiencias con [!DNL LiveRamp RampID], lo que traduce los datos de clientes a [!DNL RampIDs] para crear segmentos segmentables. El equipo de cuenta de Adobe realizará esta configuración. [!DNL RampID] está disponible a través de una asociación entre [!DNL DSP] y [!DNL LiveRamp], y no necesita su propia pertenencia a [!DNL LiveRamp] para utilizarlo.

* ID de audiencias:

   * Para [!DNL RampID] y [!DNL UID2.0], los perfiles deben contener ID de correo electrónico con hash.

   * Para las cookies, configure un proceso de sincronización de cookies con [!DNL Web SDK] flujos de datos o [!DNL Experience Cloud ID Service]. Consulte [Configurar la sincronización de ID para compartir cookies](#cookie-sync) a continuación.

   * Para perfiles con MAID:

      * Para cada GAID, incluya el valor `GAID` en una columna IdentityMap.

      * Para cada IDFA, incluya el valor `IDFA` en una columna IdentityMap.

* El ID de organización de Experience Cloud de la cuenta de Experience Platform. Puede encontrar su ID en la página de perfil de usuario de Adobe Real-Time Customer Data Platform (Real-Time CDP).

* Un origen de [Real-Time CDP en DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para recibir audiencias para la activación de la campaña. El equipo de cuenta de Adobe creará el origen con el ID de organización de Experience Cloud.

* Clave de origen de la cuenta o anunciante [!DNL DSP], que se genera cuando se crea un origen de [Real-Time CDP en [!DNL DSP]](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de cuenta de [!DNL DSP] compartirá esta clave con usted. Lo utilizará en Experience Platform para crear una conexión de destino al destino de DSP de Advertising Cloud, como se explica a continuación.

### Configurar la sincronización de ID para compartir cookies {#cookie-sync}

La sincronización de ID es un requisito previo para compartir cookies de terceros. Configure un proceso de sincronización de cookies con [!DNL Web SDK] flujos de datos o con [!DNL Experience Cloud ID Service]. Para obtener más contexto sobre la administración de identidades para cookies de terceros, consulte [destinos de Advertising que dependen de integraciones de cookies de terceros](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Habilitar sincronización de ID de terceros con[!DNL Web SDK]**

Si usa [!DNL Experience Platform Web SDK], habilite la sincronización de ID de terceros en el flujo de datos configurando la opción [!UICONTROL Third Party ID Sync] en la configuración avanzada. Para obtener instrucciones, consulte [Configurar opciones avanzadas](/help/datastreams/configure.md#advanced-options) en la documentación de flujos de datos.

**Habilitar sincronización de ID de terceros con[!DNL Experience Cloud ID Service]**

Si usa etiquetas de [!DNL Experience Platform] con [!DNL Experience Cloud ID Service], configure la sincronización de ID de terceros con la [extensión del servicio de Experience Cloud ID](/help/tags/extensions/client/id-service/overview.md). Esto permite que la cookie de Adobe Advertising coincidente para el ECID determinado esté disponible al activar la audiencia desde Real-Time CDP.

## Identidades admitidas {#supported-identities}

El destino de Adobe Advertising Cloud DSP admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | Direcciones de correo electrónico con el algoritmo SHA256 | Experience Platform admite direcciones de correo electrónico de texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que Experience Platform agregue automáticamente los datos al activarlos. |
| `ECID` | Cookie de origen para Experience Cloud | Necesario para crear segmentos basados en cookies. |
| `Everesttech cookie` | Cookie de terceros para Adobe Advertising | Necesario para crear segmentos basados en cookies. |
| `GAID` | [!DNL Android] ID de dispositivo | Necesario para segmentar [!DNL Android] dispositivos. |
| `IDFA` | [!DNL iOS] ID de dispositivo | Necesario para segmentar [!DNL iOS] dispositivos. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como Adobe Journey Optimizer, </li><li> y más. </li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
| -------------------- | --------- | ----------- | --------- |
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Recopilaciones de datos estructurados almacenados en el lago de datos de Adobe Experience Platform. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la siguiente tabla para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| ---- | ---- | ----- |
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores elegidos. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL View Destinations]** y el **[!UICONTROL Manage Destinations]** [permiso de control de acceso](/help/access-control/home.md#permissions) para Experience Platform. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino, siga las instrucciones para [crear una conexión de destino](/help/destinations/ui/connect-destination.md) mediante la interfaz de usuario de Experience Platform. En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las subsecciones siguientes.

### Autenticarse en el destino {#authenticate}

Para conectarse al destino, proporcione el siguiente parámetro en la sección [!UICONTROL Connection type] y, a continuación, seleccione **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Account or Advertiser Key]**: este(a) [!UICONTROL Source Key] se genera(a) cuando se crea un [origen de Real-Time CDP en la interfaz de usuario de DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). El equipo de cuenta de Adobe compartirá esta clave con usted después de crear el origen.

![Captura de pantalla de la sección Tipo de conexión que muestra el campo Cuenta o Clave del anunciante.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.

![Captura de pantalla de los campos de detalle de destino que muestran las entradas Nombre y Descripción.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar identidades, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Puede elegir los ID que desea enviar a Adobe Advertising DSP. De forma predeterminada, los identificadores de cookie se seleccionan para el anunciante. También puede elegir agregar [!UICONTROL Hashed Email], [!UICONTROL IDFA] y [!UICONTROL GAID].

Para obtener instrucciones, vea [Asignar atributos e identidades](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

![Captura de pantalla de la sección de asignación de identidad que muestra identificadores de cookies, correo electrónico con hash, opciones IDFA y GAID.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

## Validar exportación de datos {#exported-data}

Para verificar que los datos de audiencia se compartieron con Advertising Cloud, compruebe lo siguiente:

* El flujo de datos en su destino [!DNL Real-Time CDP] se ha completado correctamente.

* En DSP, la audiencia está disponible cuando crea o edita una audiencia de **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** o desde la sección **[!UICONTROL Audience Targeting]** de la configuración de ubicación. La audiencia debe ser visible en la ficha [!UICONTROL Adobe Segments] bajo la carpeta [!UICONTROL Real-Time CDP].

![Audiencias de Real-Time CDP en la configuración de audiencias de DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
