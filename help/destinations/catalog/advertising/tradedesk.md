---
keywords: publicidad; mostrador comercial; mostrador comercial de publicidad
title: La conexión con la Oficina de Comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 0954b5f22d609b0b12352de70f6c618cc88757c8
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 6%

---

# [!DNL The Trade Desk] conexión

## Información general {#overview}

>[!IMPORTANT]
>
>* Desde el viernes, 31 de julio de 2025, puede ver dos tarjetas **[!DNL The Trade Desk]** una al lado de la otra en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se cambió el nombre del conector de destino **[!DNL The Trade Desk]** existente a **[!UICONTROL (obsoleto) The Trade Desk]** y ahora tiene disponible una nueva tarjeta con el nombre **[!UICONTROL The Trade Desk]**.
>* Use la nueva conexión **[!UICONTROL The Trade Desk]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL (obsoleto) de la oficina de comercio]**, se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción.
>* Si está creando flujos de datos a través de la [API de Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar sus [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores:
>   * ID de especificación de flujo: `86134ea1-b014-49e8-8bd3-689f4ce70578`
>   * ID de especificación de conexión: `1029798b-a97f-4c21-81b2-e0301471166e`

Utilice este conector de destino para enviar datos de perfil a [!DNL The Trade Desk]. Este conector envía datos al extremo de origen [!DNL The Trade Desk]. La integración entre Adobe Experience Platform y [!DNL The Trade Desk] no permite exportar datos al extremo de terceros [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en pantallas, vídeos y fuentes de inventario móviles.

Para enviar datos de perfil a [!DNL The Trade Desk], primero debe conectarse al destino, tal como se describe en las secciones siguientes de esta página.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar audiencias creadas a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales de retargeting o dirigidas a audiencias.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

A continuación se muestran las identidades admitidas por el destino [!DNL The Trade Desk]. Estas identidades se pueden usar para activar audiencias en [!DNL The Trade Desk].

Todas las identidades de la tabla siguiente son asignaciones obligatorias.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| ECID | Experience Cloud ID | Esta identidad es obligatoria para que la integración funcione correctamente, pero no se utiliza para la activación de audiencias. |
| ID de la oficina de comercio | ID de anunciante en la plataforma [!DNL The Trade Desk] | Utilice esta identidad cuando active audiencias basadas en el ID propietario de Trade Desk. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL The Trade Desk] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/es/docs/id-service/using/id-service-api/methods/idsync) en el servicio de Experience Cloud ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado [!DNL The Trade Desk] integraciones en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso]** de Ver destinos **[!UICONTROL y]** Administrar destinos[&#128279;](/help/access-control/home.md#permissions)5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: [!DNL The Trade Desk] [!UICONTROL ID de cuenta].
* **[!UICONTROL Ubicación del servidor]**: pregunte al representante de [!DNL The Trade Desk] qué servidor regional debe utilizar. A continuación se muestran los servidores regionales disponibles entre los que puede elegir:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL RU/UE]**
   * **[!UICONTROL Costa Este de Estados Unidos]**
   * **[!UICONTROL Costa oeste de EE. UU.]**

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso]** de [Ver gráfico de identidad](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso [Programación de audiencias](../../ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente sus audiencias a su ID correspondiente o nombre descriptivo en la plataforma de destino.

Al asignar audiencias, Adobe recomienda utilizar el nombre de audiencia de Experience Platform o una forma más corta de él para facilitar el uso. Sin embargo, el ID de audiencia o el nombre en su destino no tienen que coincidir con el de su cuenta de Experience Platform. El destino reflejará cualquier valor que inserte en el campo de asignación.

### Asignaciones obligatorias {#mandatory-mappings}

Todas las identidades de destino descritas en la sección [identidades admitidas](#supported-identities) son obligatorias y deben asignarse durante el proceso de activación de audiencia. Esto incluye lo siguiente:

* **GAID** (Google Advertising ID)
* **IDFA** (Apple ID para anunciantes)
* **ECID** (Experience Cloud ID)
* **Identificador de la oficina de comercio**

Si no se asignan todas las identidades requeridas, la activación correcta de la audiencia no se realizará correctamente en [!DNL The Trade Desk]. Cada identidad cumple un propósito específico en la integración y todas son necesarias para que el destino funcione correctamente.

![Captura de pantalla que muestra las asignaciones obligatorias](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL The Trade Desk], compruebe su cuenta de [!DNL The Trade Desk]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
