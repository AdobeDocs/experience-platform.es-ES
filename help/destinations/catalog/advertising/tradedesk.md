---
keywords: publicidad; mostrador comercial; mostrador comercial de publicidad
title: La conexión con la Oficina de Comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en pantallas, vídeos y fuentes de inventario móviles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---

# [!DNL The Trade Desk] conexión

## Información general {#overview}

[!DNL The Trade Desk] El destino le ayuda a enviar datos de perfil a [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en pantallas, vídeos y fuentes de inventario móviles.

Para enviar datos de perfil a [!DNL Trade Desk], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar audiencias creadas a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales de retargeting o segmentación de audiencia.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| ID de la oficina de comercio | ID del anunciante en la plataforma de Trade Desk |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si quiere crear su primer destino con [!DNL The Trade Desk] y no han habilitado el [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el Servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si había configurado anteriormente [!DNL The Trade Desk] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL Trade Desk] [!UICONTROL ID de cuenta].
* **[!UICONTROL Ubicación del servidor]**: pregunte a su [!DNL Trade Desk] representa qué servidor regional debe utilizar. Estos son los servidores regionales disponibles entre los que puede elegir:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Este de Norteamérica]**
   * **[!UICONTROL Oeste de Norteamérica]**
   * **[!UICONTROL América Latina]**

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el [Programación de audiencia](../../ui/activate-segment-streaming-destinations.md#scheduling) , debe asignar manualmente las audiencias a su ID correspondiente o nombre descriptivo en la plataforma de destino.

Al asignar segmentos, le recomendamos que utilice el nombre de audiencia de Platform o una forma más corta de él, para facilitar el uso. Sin embargo, el ID de audiencia o el nombre en el destino no tienen por qué coincidir con el de su cuenta de Platform. El destino reflejará cualquier valor que inserte en el campo de asignación.

Si utiliza varias asignaciones de dispositivos (ID de cookie, [!DNL IDFA], [!DNL GAID]), asegúrese de utilizar el mismo valor de asignación para las tres asignaciones. [!DNL The Trade Desk] Los agregará todos en un solo segmento, con un desglose por dispositivo.

![ID de asignación de segmentos](../../assets/common/segment-mapping-id.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente a [!DNL The Trade Desk] destino, compruebe su [!DNL Trade Desk] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
