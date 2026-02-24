---
title: Algolia
description: Utilice este conector para activar audiencias en Algolia para la personalización y el uso en búsquedas y recomendaciones. A continuación, puede utilizar el conector de origen del perfil de usuario de Algolia para importar los perfiles en Real-Time CDP y crear audiencias enriquecidas.
exl-id: 116a051a-1b47-4789-826e-c8f0fee60def
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 4%

---

# [!DNL Algolia] conexión

## Información general {#overview}

>[!IMPORTANT]
>
>El conector de destino [!DNL Algolia] y la página de documentación son creados y mantenidos por el equipo de Algolia Integration Services. Para consultas o solicitudes de actualización, comuníquese con ellos en [adobe-algolia-solutions@algolia.com](mailto:adobe-algolia-solutions@algolia.com).

Utilice la conexión de destino [!DNL Algolia] para enviar audiencias de Adobe Experience Platform a Algolia y realizar búsquedas y recomendaciones personalizadas. Para poder usar el conector de destino [!DNL Algolia], primero debe configurar el conector de origen [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md). Durante el tutorial de configuración del conector de origen, creará la identidad del token de usuario de Algolia. Esta identidad es necesaria para la asignación al configurar el conector de destino.

Este tutorial proporciona los pasos para crear una conexión de destino y un flujo de datos de [!DNL Algolia] mediante la interfaz de usuario de Adobe Experience Platform.

![Catálogo de destino con destino Algolia.](../../assets/catalog/personalization/algolia/catalog.png)

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Algolia], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Coherencia de Personalization {#personalization-consistency}

Utilice este conector de destino para ofrecer una personalización coherente en todo el sitio desde la página de inicio hasta la búsqueda.

Por ejemplo, como experto en marketing, es posible que desee crear audiencias enriquecidas en Adobe Experience Platform a partir de varias fuentes de datos de usuario, como Algolia. Puede usar el conector de destino [!DNL Algolia] para compartir audiencias para estrategias de segmentación, lo que provocará un aumento en la personalización y conversión de campañas.

Para implementar este caso de uso, debe usar los conectores de origen [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) y de destino [!DNL Algolia].

Para empezar, debe importar los perfiles de usuario de [!DNL Algolia] existentes en Adobe Experience Platform Real-Time CDP y otras fuentes para empezar a crear audiencias enriquecidas con el conector de origen. Los especialistas en marketing crearían audiencias utilizando los datos de perfil que se pueden enviar a Algolia para la personalización de recomendaciones y búsquedas.

A continuación, utilice el conector de origen [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) correspondiente para introducir y aumentar los perfiles de cliente de nuevo en Real-Time CDP.

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>* Para conectarse al destino, necesita los permisos de control de acceso **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [6&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

## Identidades admitidas {#supported-identities}

[!DNL Algolia] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces).

| Identidad de destino | Descripción | Consideraciones |
|---------|---------|----------|
| userId | [!DNL Algolia] token de usuario | Seleccione esta identidad de destino para asignar la identidad de origen `AlgoliaUserToken` a `userToken` en la plataforma [!DNL Algolia]. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|---------|----------|
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
| Tipo de exportación | **[!DNL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Algolia]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage and Activate Dataset Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Application ID]**: el id. de aplicación [!DNL Algolia] es un identificador único asignado a su cuenta de [!DNL Algolia].
* **[!UICONTROL API Key]**: la clave de API [!DNL Algolia] es una credencial que se usa para autenticar y autorizar solicitudes de API para los servicios de búsqueda e indexación de [!DNL Algolia].

Para obtener más información sobre estas credenciales, consulte la [!DNL Algolia] [documentación de autenticación](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

![Nueva cuenta](../../assets/catalog/personalization/algolia/connection.png)

### Rellenar detalles de destino

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: breve explicación del propósito del destino.
* **[!UICONTROL Region]**: las opciones son **US** o **EU**. Seleccione la región donde se almacenan los datos del cliente.


![Detalles de la cuenta](../../assets/catalog/personalization/algolia/account.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar identidades, necesita el permiso Ver gráfico de identidad [control de acceso](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/home#permissions).

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#mapping-attributes-identities}

Durante [!UICONTROL Mapping step], debe asignar la identidad de origen AlgoliaUserToken a la identidad de destino userId.

![Asignación completa](../../assets/catalog/personalization/algolia/mapping-complete.png)

## Validar exportación de datos {#exported-data}

Para comprobar si las audiencias se han exportado correctamente a los perfiles de usuario, compruebe el panel [!DNL Algolia], navegue hasta **[!UICONTROL Advanced Personalization]** y haga clic en **[!UICONTROL User Inspector]**. Busque un perfil de usuario asociado a la audiencia de Adobe Experience Platform exportada y búsquelo en el Inspector de usuario. Verá el ID de audiencia en la sección del segmento.

![Inspector de usuario de Algolia](../../assets/catalog/personalization/algolia/verify-segment-user-profile.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Consulte la siguiente documentación de [!DNL Algolia] para obtener más información:

* [¿Qué es Personalization avanzado?](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/)
* [Perfiles de usuario](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/concepts/user-profiles/)
* [Usuarios de segmentos con contextos de regla](https://www.algolia.com/doc/guides/personalization/advanced-personalization/implement/guides/segment-users-with-rule-contexts/#assign-a-segment-context-at-query-time)

## Próximos pasos {#next-steps}

Al seguir este tutorial, ha creado correctamente un flujo de datos para exportar audiencias de Experience Platform a su aplicación [!DNL Algolia]. Para obtener más información acerca de la plataforma [!DNL Algolia], consulte la [documentación de Algolia](https://www.algolia.com/doc/).
