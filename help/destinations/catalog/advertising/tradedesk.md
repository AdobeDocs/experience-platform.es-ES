---
keywords: publicidad; mostrador comercial; mostrador comercial de publicidad
title: La conexión con la Oficina de Comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en fuentes de inventario de pantallas, vídeos y móviles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 2%

---

# [!DNL The Trade Desk] conexión

## Información general {#overview}

Utilice este conector de destino para enviar datos de perfil a [!DNL The Trade Desk]. Este conector envía datos al extremo de origen [!DNL The Trade Desk]. La integración entre Adobe Experience Platform y [!DNL The Trade Desk] no permite exportar datos al extremo de terceros [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en pantallas, vídeos y fuentes de inventario móviles.

Para enviar datos de perfil a [!DNL The Trade Desk], primero debe conectarse al destino, tal como se describe en las secciones siguientes de esta página.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar audiencias creadas a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales de retargeting o dirigidas a audiencias.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

A continuación se muestran las identidades admitidas por el destino [!DNL The Trade Desk]. Estas identidades se pueden usar para activar audiencias en [!DNL The Trade Desk].

Todas las identidades de la tabla siguiente están preconfiguradas y asignadas automáticamente durante la activación. No es necesario configurar manualmente estas asignaciones en el flujo de trabajo de activación.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Se activa cuando hay una GAID en el perfil. |
| IDFA | Apple ID para anunciantes | Se activa cuando hay un IDFA en el perfil. |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lea el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| [!DNL Tradedesk] | [!DNL TDID] en la plataforma [!DNL The Trade Desk] | Se activa cuando un perfil tiene un ECID y existe una asignación ECID-to-Trade Desk ID en Experience Platform. |

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

Los requisitos previos dependen de los tipos de identidad que planee utilizar para la activación de audiencia:

**Solo para la activación del identificador móvil**, no hay requisitos previos. Siempre que recopile y administre ID (GAID o IDFA) para sus clientes, puede empezar a activar audiencias en [!DNL The Trade Desk].

**Para el direccionamiento basado en cookies en[!DNL The Trade Desk]**, asegúrese de que se ha establecido una asignación entre ECID y [!DNL Trade Desk ID]. Complete los pasos siguientes para hacerlo:

1. **Habilitar la funcionalidad de sincronización de ID**: Si esta es la primera vez que configura la activación de [!DNL The Trade Desk ID] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) en el servicio de Experience Cloud ID anteriormente (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar la sincronización de ID.
   * Si ya configuró [!DNL The Trade Desk] integraciones en Audience Manager, las sincronizaciones de ID existentes se transferirán automáticamente a Experience Platform.

2. **Instrumente sus páginas web**: Implemente código en sus páginas web para crear asignaciones entre [!DNL The Trade Desk ID] y Adobe ECID. Esto permite a Experience Platform asociar los ID de la oficina de comercio con los perfiles de sus clientes.

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
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso [Programación de audiencias](../../ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente sus audiencias a su ID correspondiente o nombre descriptivo en la plataforma de destino.

Al asignar audiencias, Adobe recomienda utilizar el nombre de audiencia de Experience Platform o una forma más corta de él para facilitar el uso. Sin embargo, el ID de audiencia o el nombre en su destino no tienen que coincidir con el de su cuenta de Experience Platform. El destino reflejará cualquier valor que inserte en el campo de asignación.

### Asignaciones preconfiguradas {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Conjuntos de asignaciones preconfigurados"
>abstract="Hemos preconfigurado estos cuatro conjuntos de asignaciones para usted. Al activar los datos en Trade Desk, los perfiles cualificados para las audiencias activadas no necesariamente tienen que tener las cuatro identidades presentes en los perfiles, ya que este destino funciona con cualquiera de las identidades de destino mostradas aquí. <br> Para el direccionamiento basado en cookies y en función del ID de Trade Desk, necesita un ECID presente en el perfil y una asignación de sincronización de ID entre el ID de Trade Desk y el ECID."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Más información sobre las asignaciones preconfiguradas"

Las siguientes asignaciones de identidad están **preconfiguradas y rellenadas automáticamente** para usted en el flujo de trabajo de activación de audiencia:

* GAID (Google Advertising ID)
* IDFA (Apple ID para anunciantes)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Captura de pantalla que muestra las asignaciones obligatorias](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

Estas asignaciones están atenuadas y son de solo lectura. No es necesario configurar nada en este paso. Seleccione **[!UICONTROL Next]** para continuar.

Experience Platform comprueba automáticamente todos los perfiles pertenecientes a audiencias asignadas en el flujo de trabajo de activación para todos los tipos de identidad admitidos y, a continuación, activa el perfil utilizando cualquier identidad que esté presente.

### Requisitos de identidad por tipo de activación

**Activación de ID móvil (GAID/IDFA):** Los perfiles con GAID o IDFA son suficientes para la activación. No se requieren identidades ni requisitos previos adicionales.

**Direccionamiento basado en cookies ([!DNL Trade Desk ID]):** Requiere lo siguiente:

* ECID presente en el perfil
* Asignación de sincronización de ID entre [!DNL Trade Desk ID] y ECID (configurado como se describe en la sección [requisitos previos](#prerequisites))

**Comportamiento de varios identificadores:** Si un perfil contiene varias identidades admitidas, cada identidad se activará por separado para [!DNL The Trade Desk]. Esto garantiza el máximo alcance y flexibilidad en la activación de audiencias.

### Ejemplos de activación

* **Perfiles de ID móviles:** Los perfiles con GAID o IDFA se activan mediante sus respectivos ID publicitarios. Si un perfil contiene GAID e IDFA, cada ID se activará por separado.
* **Perfil basado en cookies:** Se activará un perfil con ECID y una asignación [!DNL Trade Desk ID] correspondiente mediante el identificador de Trade Desk para el direccionamiento basado en cookies.
* **Perfil solo de ECID:** Un perfil con solo ECID y sin asignación de [!DNL Trade Desk ID] **no se exportará**. El ECID solo no es suficiente para la activación.

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL The Trade Desk], compruebe su cuenta de [!DNL The Trade Desk]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
