---
title: Reddit Audiencia personalizada
description: Reddit Ads conecta a las marcas con personas que están explorando activamente sus pasiones y problemas en tiempo real. Mediante el emparejamiento de conversaciones de alta intención impulsadas por la comunidad con formatos de publicidad flexibles y una segmentación sólida, Reddit Ads ayuda a los anunciantes a llegar a audiencias comprometidas, impulsar los resultados de rendimiento y aprender directamente de las comunidades que dan forma a la cultura en línea. Esta guía es para anunciantes y equipos de medios que utilizan Adobe Experience Platform para enviar audiencias a Reddit Ads. Abarca lo que necesita para conectar sus cuentas, asignar identidades y activar audiencias.
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: c7c74ba9b5c6a66f92dc6a5403d4f2c5614c0049
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 3%

---


# [!DNL Reddit Custom Audience] conexión {#reddit-custom-audience-connection}

## Información general {#overview}

[!DNL Reddit Ads] conecta marcas con personas que están explorando activamente sus pasiones y problemas en tiempo real. Al combinar conversaciones de alta intención impulsadas por la comunidad con formatos de anuncios flexibles y una segmentación sólida, [!DNL Reddit Ads] ayuda a los anunciantes a llegar a audiencias comprometidas, impulsar los resultados de rendimiento y aprender directamente de las comunidades que dan forma a la cultura en línea.

Esta guía es para anunciantes y equipos multimedia que usan [!DNL Adobe Experience Platform] para enviar audiencias a [!DNL Reddit Ads]. Abarca lo que necesita para conectar sus cuentas, asignar identidades y activar audiencias.

>[!IMPORTANT]
>
>El equipo [!DNL Reddit] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en <adsapi-partner-support@reddit.com>.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Reddit Custom Audience], aquí hay ejemplos de casos de uso que los clientes de [!DNL Adobe Experience Platform] pueden resolver mediante este destino.

### Redireccionamiento de clientes existentes con ofertas personalizadas {#use-case-1}

Un retailer en línea quiere llegar a los clientes existentes a través de plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. Retailer en línea puede ingerir direcciones de correo electrónico e ID de dispositivo (IDFA y GAID) desde su propio CRM a [!DNL Adobe Experience Platform], crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Reddit Ads], optimizando así su gasto en publicidad.

## Requisitos previos {#prerequisites}

Antes de configurar este destino, asegúrese de cumplir los siguientes requisitos previos:

* Una cuenta de [!DNL Reddit Ads] con permiso para usar audiencias personalizadas y listas de clientes.
* Permiso para autorizar la conexión. Debe ser un usuario que puede iniciar sesión en [!DNL Reddit] y aprobar el acceso para [!DNL Experience Platform] a fin de administrar las audiencias en nombre de la cuenta publicitaria.
* Su ID de cuenta de publicidad [!DNL Reddit]: el identificador de la cuenta de publicidad en la que se crean las audiencias. Puede encontrar su ID de cuenta de publicidad en [Cuentas](https://ads.reddit.com/accounts). Por ejemplo: `a2_1b2c34d`.

## Identidades admitidas {#supported-identities}

[!DNL Reddit Custom Audience] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
| --- | --- | --- |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | [!DNL Adobe Experience Platform] admite direcciones de correo electrónico con hash SHA256 y texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] coloque automáticamente los datos en la activación. |
| criada | Google Advertising ID o Apple ID para anunciantes, ambos con el algoritmo SHA256 | Asigne GAID o IDFA a **maid**. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] coloque automáticamente los datos en la activación. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
| --- | --- | --- |
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [!DNL Experience Platform] [servicio de segmentación](../../../segmentation/home.md). |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través del servicio de segmentación. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
| --- | --- | --- | --- |
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Reddit Custom Audience]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

![La pantalla de autenticación de destino Reddit Custom Audience muestra los campos necesarios para la conexión.](../../assets/catalog/advertising/redditcustomaudience/configure_new_destination_fields.png)

Se le redirigirá para que inicie sesión con [!DNL Reddit]. Después de revisar los permisos solicitados, seleccione **[!UICONTROL Allow]** para que [!DNL Experience Platform] pueda crear audiencias y actualizar la membresía en nombre de su cuenta de publicidad.

![Pantalla de permisos de Reddit OAuth.](../../assets/catalog/advertising/redditcustomaudience/reddit_oauth.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Pantalla de detalles de destino de Audiencia personalizada de Reddit.](../../assets/catalog/advertising/redditcustomaudience/reddit_account_details.png)

* **[!UICONTROL Name]**: nombre por el cual reconoce este destino.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino.
* **[!UICONTROL Ad Account ID]**: Su ID de cuenta de publicidad de [!DNL Reddit].

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Las siguientes áreas de nombres de identidad de destino deben asignarse según el caso de uso:

| Campo de origen | Campo de destino | Notas |
| --- | --- | --- |
| Correo electrónico (texto sin formato o con hash) | email_lc_sha256 | El campo de origen puede tener un cifrado hash o deshash. [!DNL Reddit] solo acepta valores con hash. Habilite **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] envíe el correo electrónico con hash. |
| MAID (texto sin formato o con hash) | criada | El campo de origen puede tener un cifrado hash o deshash. [!DNL Reddit] solo acepta valores con hash. Habilite **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] utilice valores hash antes de enviar. |

Debe asignar al menos una de las identidades.

![Pantalla de asignación de identidad que muestra los campos de origen y destino configurados para la audiencia personalizada de Reddit.](../../assets/catalog/advertising/redditcustomaudience/mapping.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Después de activar las audiencias, podrá verlas en su cuenta de [!DNL Reddit] Ads Manager.

Las audiencias recién creadas en [!DNL Reddit] aparecen en estado pendiente. Una vez que se ejecute el flujo de datos y se exporten los perfiles, [!DNL Reddit] coincidirá con los perfiles de [!DNL Reddit] usuarios. Una vez procesados los datos, el estado de la audiencia cambia a **[!UICONTROL Valid]**. El tamaño de la audiencia debe alcanzar [1,000 usuarios o más](https://ads-api.reddit.com/docs/v3/manage-customer-lists) para ser considerado válido. Las audiencias que no alcanzan el tamaño requerido se muestran como **[!UICONTROL Invalid]**.

![Administrador de Reddit Ads que muestra una audiencia exportada y su estado.](../../assets/catalog/advertising/redditcustomaudience/see_audience_in_reddit.png)

El siguiente es un ejemplo de la carga útil enviada a [!DNL Reddit]:

```json
{
  "data": {
    "action_type": "ADD",
    "column_order": [
      "EMAIL_SHA256",
      "MAID_SHA256"
    ],
    "user_data": [
      [
        "d7ef2e7b2a3663c25284a3d6d13b1ca727fc8c659474b81afe0cec997a4737d2",
        "510870d7b3e47a28a2b2f3aef27a4c81aab0b2eefda27dea50bc4c991d9e5435"
      ]
    ]
  }
}
```

Consulte la [documentación de la API de Reddit](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) para obtener más información.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Consulte la [documentación de la API de Reddit](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) para obtener más información sobre cómo funciona el extremo de audiencias personalizado.
