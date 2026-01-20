---
keywords: publicidad; mostrador comercial; mostrador comercial de publicidad
title: La conexión con la Oficina de Comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 036d784014e7cdb101f39f63f9d6e8bac01fdc97
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---

# [!DNL The Trade Desk] conexión

## Información general {#overview}


>[!IMPORTANT]
>
> Después de la [actualización interna](../../../release-notes/2025/july-2025.md#destinations) al servicio de destinos a partir de julio de 2025, es posible que observe una **caída en el número de perfiles activados** en sus flujos de datos a [!DNL The Trade Desk].
> Esta caída se debe a la mejora de la visibilidad de la monitorización. Los perfiles sin ECID ahora se cuentan correctamente como perdidos en las métricas de activación. Consulte la sección [asignación obligatoria](#mandatory-mappings) en esta página para obtener información detallada.
>
>**Qué cambió:**
>
>* El servicio de destinos ahora informa correctamente cuando se pierden perfiles sin ECID de la activación.
>* **Importante:** Los perfiles sin ECID nunca llegaron a [!DNL The Trade Desk] ni siquiera antes de esta actualización. La integración siempre ha requerido un ECID. Esta actualización corrige un error que anteriormente impedía que estas caídas fueran visibles en sus métricas.
>
>**Lo que debe hacer:**
>
>* Revise los datos de audiencia para confirmar que los perfiles tienen valores ECID válidos.
>* Monitorice las métricas de activación para verificar los recuentos de perfiles esperados. Los recuentos más bajos reflejan una creación de informes precisa, no un cambio en el comportamiento de destino.

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
| [!DNL GAID] | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| [!DNL IDFA] | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| [!DNL ECID] | Experience Cloud ID | Esta identidad es obligatoria para que la integración funcione correctamente, pero no se utiliza para la activación de audiencias. |
| [!DNL Tradedesk] | [!DNL TDID] en la plataforma [!DNL The Trade Desk] | Utilice esta identidad cuando active audiencias basadas en el ID propietario de Trade Desk. |

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
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Va a exportar todos los miembros de una audiencia al destino. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL The Trade Desk] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) en el servicio de Experience Cloud ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado [!DNL The Trade Desk] integraciones en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Account ID]**: su [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: pregunte al representante de [!DNL The Trade Desk] qué servidor regional debe utilizar. A continuación se muestran los servidores regionales disponibles entre los que puede elegir:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso [Programación de audiencias](../../ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente sus audiencias a su ID correspondiente o nombre descriptivo en la plataforma de destino.

Al asignar audiencias, Adobe recomienda utilizar el nombre de audiencia de Experience Platform o una forma más corta de él para facilitar el uso. Sin embargo, el ID de audiencia o el nombre en su destino no tienen que coincidir con el de su cuenta de Experience Platform. El destino reflejará cualquier valor que inserte en el campo de asignación.

### Asignaciones obligatorias {#mandatory-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Conjuntos de asignaciones preconfigurados"
>abstract="Hemos preconfigurado estos cuatro conjuntos de asignaciones para usted. A medida que activa los datos en Trade Desk, los perfiles cualificados para las audiencias activadas no necesariamente tienen que tener las cuatro identidades presentes en los perfiles, ya que este destino funciona con cualquiera de las identidades de destino mostradas aquí."

Todas las identidades de destino descritas en la sección [identidades admitidas](#supported-identities) deben asignarse en el paso de asignación del flujo de trabajo de activación de audiencia. Esto incluye lo siguiente:

* [!DNL GAID] (Google Advertising ID)
* [!DNL IDFA] (Apple ID para anunciantes)
* [!DNL ECID] (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Captura de pantalla que muestra las asignaciones obligatorias](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

La asignación de todas las identidades de destino garantiza que la activación pueda dividir y enviar correctamente los perfiles mediante cualquier identidad presente. Esto no significa que todas las identidades deban estar presentes en cada perfil.

Para que la exportación a The Trade Desk se realice correctamente, un perfil debe contener:

* [!DNL ECID] y
* al menos uno de: [!DNL GAID], [!DNL IDFA] o [!DNL The Trade Desk ID]

Ejemplos:

* [!DNL ECID] solamente: no exportado
* [!DNL ECID] + [!DNL The Trade Desk ID]: exportado
* [!DNL ECID] + [!DNL IDFA]: exportado
* [!DNL ECID] + [!DNL GAID]: exportado
* [!DNL IDFA] + [!DNL The Trade Desk ID] (no [!DNL ECID]): no exportado

>[!NOTE]
> 
>Después de la actualización de [julio de 2025](/help/release-notes/2025/july-2025.md#destinations) al servicio de destinos, los perfiles que faltan [!DNL ECID] ahora se registran correctamente como perdidos en las métricas de activación. Este siempre ha sido el comportamiento de la integración (los perfiles sin [!DNL ECID] nunca llegaron a [!DNL The Trade Desk]), pero las caídas ahora están correctamente visibles en la monitorización del flujo de datos. Los recuentos de activación más bajos reflejan un sistema de informes preciso, no un cambio en la funcionalidad de destino.

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL The Trade Desk], compruebe su cuenta de [!DNL The Trade Desk]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
