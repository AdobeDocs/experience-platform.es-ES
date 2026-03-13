---
keywords: publicidad; microsoft ads; coincidencia de clientes;
title: Conexión de Microsoft Ads Customer Match
description: Utilice el destino de coincidencia de clientes de Microsoft Ads para hacer coincidir clientes por dirección de correo electrónico y volver a interactuar con ellos en toda la red de Advertising de Microsoft, incluidos los anuncios de búsqueda y audiencia.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 4d405ffb-f600-463b-a215-44e806b6d139
source-git-commit: 82f412676c89d7d14116be9328ab7fa438e10fc0
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 3%

---

# [!DNL Microsoft Ads Customer Match] conexión {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>Este conector de destino está actualmente en disponibilidad limitada. Para obtener acceso, póngase en contacto con su representante de Adobe.

## Información general {#overview}

Use el destino [!DNL Microsoft Ads Customer Match] para buscar clientes por dirección de correo electrónico y volver a interactuar con ellos en [!DNL Microsoft Advertising Network], incluidos los anuncios de búsqueda y audiencia. Vincule su cuenta de [!DNL Microsoft Advertising] a Real-Time CDP para automatizar la creación y administración de listas de coincidencia de clientes directamente desde Experience Platform.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL Microsoft Ads Customer Match], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

### Caso de uso #1

Una marca de comercio electrónico desea llegar a los clientes existentes a través de [!DNL Microsoft Search] y [!DNL Microsoft Audience Network] para personalizar las ofertas en función de sus compras anteriores y del historial de exploración. La marca puede ingerir direcciones de correo electrónico de su propio CRM en Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Microsoft Ads Customer Match] para que se utilicen en la búsqueda y en los anuncios de audiencia, lo que optimiza el gasto en publicidad.

### Caso de uso #2

Una empresa de tecnología lanzó un nuevo producto. Para promocionar este nuevo producto, buscan concienciar a los clientes que anteriormente compraron productos relacionados. Cargan direcciones de correo electrónico desde su base de datos de CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Las audiencias se crean en función de los clientes que poseen productos relacionados. Estas audiencias se envían a [!DNL Microsoft Ads Customer Match], de modo que la empresa pueda dirigirse a los clientes actuales y similares de [!DNL Microsoft Advertising Network].

## Identidades admitidas {#supported-identities}

[!DNL Microsoft Ads Customer Match] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| `email` | Direcciones de correo electrónico de texto sin formato | La conexión [!DNL Microsoft Ads Customer Match] solo admite direcciones de correo electrónico de texto sin formato. Experience Platform almacena automáticamente en hash las direcciones de correo electrónico durante la exportación para que coincidan con los requisitos de Microsoft. |

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
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Recopilaciones de datos estructurados almacenados en el lago de datos de Adobe Experience Platform. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores (direcciones de correo electrónico) utilizados en el destino [!DNL Microsoft Ads Customer Match]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para enviar datos de audiencia a [!DNL Microsoft Ads], necesita tener una cuenta activa de [!DNL Microsoft Advertising]. Para obtener más información sobre cómo crear una cuenta, visita la [documentación de Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/53090/0).

### Aceptar los términos y condiciones de coincidencia del cliente {#accept-customer-match-terms}

Antes de activar audiencias a través de este destino, primero debe crear manualmente una lista de coincidencia de clientes en su cuenta de [!DNL Microsoft Advertising]. Esta creación manual inicial es necesaria para aceptar los términos y condiciones de coincidencia del cliente, lo que permite crear automáticamente audiencias enviadas desde Experience Platform. Si no se completa este paso, pueden producirse errores al activar las audiencias.

### Configuración de cuenta {#account-configuration}

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL Customer ID]: su [!DNL Microsoft Ads] ID de cliente (CID), en formato entero. Consulte la [documentación de Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obtener instrucciones sobre cómo encontrar su ID de cliente.
* [!UICONTROL Customer Account ID]: su ID de cuenta de cliente [!DNL Microsoft Ads]. Consulte la [documentación de Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obtener instrucciones sobre cómo encontrar su ID de cuenta de cliente.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Rellenar detalles de destino {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Customer ID"
>abstract="Su ID de cliente de Microsoft Advertising, también conocido como ID de cuenta de responsable. Este es el identificador de nivel superior de Microsoft Advertising que puede tener varias cuentas de anunciante (ID de cuenta de cliente)."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Búsqueda del ID de cliente"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="ID de cuenta de cliente"
>abstract="Su ID de cuenta de cliente de Microsoft Advertising, también conocido como ID de cuenta del anunciante. Esto identifica una cuenta de anunciante específica en su ID de cliente."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Búsqueda del ID de cuenta de cliente"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="Duración de abono"
>abstract="El número de días que un usuario permanece en la lista de coincidencia de clientes. Los valores aceptados están entre 1 y 390 días."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="Disponibilidad de lista de coincidencia de clientes"
>abstract="Seleccione si la lista de coincidencia de clientes está disponible para una sola cuenta de anunciante o para todas las cuentas de la cuenta de responsable. Seleccione ID de cliente para que la lista esté disponible en todas las cuentas de anunciante con su ID de cliente. Seleccione ID de cuenta de cliente para restringir la lista al ID de cuenta de cliente específico."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Obtenga más información sobre cómo compartir listas de audiencias en Microsoft Advertising"

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Customer ID]**: Su [!DNL Microsoft Ads] ID de cliente (CID). Consulte la [documentación de Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obtener instrucciones sobre cómo encontrar su ID de cliente.
* **[!UICONTROL Customer Account ID]**: Su ID de cuenta de cliente [!DNL Microsoft Ads]. Consulte la [documentación de Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obtener instrucciones sobre cómo encontrar su ID de cuenta de cliente.
* **[!UICONTROL Membership Duration]**: número de días que un usuario permanece en la lista de coincidencia de clientes. Los valores aceptados están entre 1 y 390 días.
* **[!UICONTROL Customer Match List Availability]**: seleccione la disponibilidad de la lista de coincidencia de clientes. En [!DNL Microsoft Advertising], un ID de cliente puede tener varios ID de cuenta de cliente (cuentas de anunciante). Seleccione **[!UICONTROL Customer ID (all advertising accounts)]** para que la lista esté disponible en todas las cuentas de anunciante bajo su ID de cliente o **[!UICONTROL Customer Account ID (single advertising account)]** para restringir la lista al ID de cuenta de cliente específico que proporcionó anteriormente. Consulte la [documentación de Microsoft Advertising](https://help.ads.microsoft.com/apex/index/3/en/56727) para obtener más información.

![Imagen de la interfaz de usuario de la plataforma que muestra los campos de detalles de destino del destino de Customer Match de Microsoft Ads.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades* a destinos, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignación {#mapping}

En el paso **[!UICONTROL Mapping]**, debe asignar la identidad de correo electrónico de los perfiles de origen a la identidad de destino en [!DNL Microsoft Ads Customer Match].

* **Campo de Source**: seleccione `IdentityMap: Email` como campo de origen para asignar identidades de correo electrónico a partir de los perfiles. También puede seleccionar un atributo XDM como `personalEmail.address` como campo de origen.
* **Campo de destino**: seleccione `Identity: email` como campo de destino.

>[!IMPORTANT]
>
>Debe utilizar campos de origen sin hash (texto sin formato). No utilice identidades de origen prehash como `Emails (SHA256, lowercased)`. Experience Platform almacena automáticamente en hash las direcciones de correo electrónico durante la exportación para que coincidan con los requisitos de Microsoft.

![Imagen de la interfaz de usuario que muestra el paso de asignación con el correo electrónico de IdentityMap asignado al correo electrónico de Identity.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL Microsoft Ads Customer Match], compruebe su cuenta de [!DNL Microsoft Advertising]. Si la activación se realizó correctamente, las audiencias se rellenan en su cuenta como listas de coincidencia de clientes.

## Recursos adicionales {#additional-resources}

Consulte el [Centro de ayuda de Microsoft Advertising](https://help.ads.microsoft.com/) para obtener más información.
