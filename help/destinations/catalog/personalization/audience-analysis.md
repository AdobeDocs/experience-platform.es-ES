---
title: Destino de Audience Analysis
description: Vea las audiencias para las que los clientes cumplen los requisitos en Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilidad limitada" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---

# Destino de Audience Analysis

El destino [!UICONTROL Audience Analysis] le permite enriquecer los datos de audiencia de Adobe Experience Platform en [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es). Puede seleccionar qué audiencias desea incluir en los datos enriquecidos resultantes. Las cualificaciones de audiencia están disponibles como dimensiones en los informes de [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html).

>[!AVAILABILITY]
>
>Este destino se encuentra en una fase de prueba limitada. Si está interesado en utilizar este destino, póngase en contacto con el equipo de cuenta de Adobe.

## Requisitos previos

Se requiere lo siguiente antes de utilizar este destino:

* Debe estar aprovisionado para utilizar el destino de Análisis de audiencia. Si todavía no se le ha proporcionado este destino, póngase en contacto con su equipo de cuenta de Adobe.
* Debe estar aprovisionado para utilizar Customer Journey Analytics.
* Debe tener al menos una audiencia creada en Adobe Experience Platform.

## Identidades admitidas

El análisis de audiencia admite la activación de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md). Normalmente, se utiliza un Experience Cloud ID (ECID).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] ponga en hash automáticamente los datos durante la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] ponga en hash automáticamente los datos durante la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style="table-layout:auto"}

## Audiencias compatibles

Se admiten los siguientes tipos de audiencias al utilizar este destino:

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Análisis de audiencia. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar nuevo destino

>[!IMPORTANT]
> 
>Para crear un destino, necesita los permisos de control de acceso **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [3}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para crear este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Detalles del destino

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: el nombre de destino.
* **[!UICONTROL Description]**: la descripción de destino.
* **[!UICONTROL Datastream ID]**: ID de secuencia de datos que desea enriquecer con audiencias aptas. Puede obtener este identificador en el [administrador de flujos de datos](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]**: alias de la integración.

### Alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: recibir una notificación cuando la tasa de activación omitida supere un umbral.

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

### Política de gobernanza y medidas coercitivas

Esta sección opcional le permite definir las políticas de control de datos y asegurarse de que los datos utilizados sean compatibles cuando las audiencias se envíen y estén activas.

Cuando termine de seleccionar las acciones de marketing deseadas para el destino, seleccione **[!UICONTROL Create]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Una vez creado el destino, puede activar las audiencias que desee para el destino.

1. Si aún no se encuentra en el destino creado, puede volver a localizarlo si navega a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
1. Seleccione **[!UICONTROL Activate audiences]**.
1. Seleccione las audiencias para las que desee analizar las cualificaciones. Cuando termine, seleccione **[!UICONTROL Next]**.
1. Revise la configuración de destino y la configuración de audiencia, y luego seleccione **[!UICONTROL Finish]**.

Para agregar más audiencias que analizar en el futuro, vuelva a la página **[!UICONTROL Activate audiences]**. Las audiencias no se pueden eliminar una vez activadas.
