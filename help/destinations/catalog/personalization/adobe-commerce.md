---
title: (Beta) Conector de destino de Adobe Commerce
description: Descubra cómo los comerciantes de Adobe Commerce y Real-Time CDP pueden personalizar la experiencia de compra al ofrecer contenido y promociones de sitio altamente relevantes, personalizados para los segmentos de clientes creados y administrados dentro de Real-Time CDP.
source-git-commit: 0a6100f2aa98f5c40f2492dcfab79a991eded94b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# (Beta) Conexión de Adobe Commerce {#adobe-commerce}

## Información general {#overview}

>[!IMPORTANT]
> 
>La variable **[!UICONTROL Adobe Commerce]** El conector está en versión beta y solo está disponible para un número determinado de clientes.

La variable [!DNL Adobe Commerce] el conector de destino le permite seleccionar uno o varios segmentos de Real-Time CDP para activarlos en su [!DNL Adobe Commerce] para ofrecer una experiencia personalizada dinámica para sus compradores. Within [!DNL Adobe Commerce], puede seleccionar los segmentos de Real-Time CDP para personalizar las ofertas únicas del carro de compras, como &quot;comprar 2 obtener 1 gratis&quot;. También puede mostrar banners a pantalla completa y modificar los precios de los productos mediante ofertas promocionales, todas ellas personalizadas para segmentos de Adobe Real-Time CDP.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Requisitos previos {#prerequisites}

Esta extensión está disponible en el catálogo de destinos para clientes beta seleccionados que hayan comprado Real-Time CDP Prime o Ultimate y Adobe Commerce.

Los clientes de la versión beta deben tener acceso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Consola de desarrollador de Adobe](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud versión 2.4.3 o superior](https://business.adobe.com/products/magento/magento-commerce.html)

En Experience Platform, cree lo siguiente:

- [Esquema](../../../xdm/schema/composition.md). El esquema que cree representa los datos que planea introducir desde Adobe Commerce. [Más información](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) acerca de cómo crear un esquema que contenga grupos de campos específicos de comercio.
- [Conjunto de datos](../../../catalog/datasets/user-guide.md#create). Un conjunto de datos es una construcción de almacenamiento y administración para una recopilación de datos. Debe crear este conjunto de datos a partir del esquema creado anteriormente.
- [Datastream](../../../edge/datastreams/overview.md#create). ID que permite el flujo de datos de Adobe Experience Platform a otros productos DX de Adobe. Este ID debe estar asociado a un sitio web específico de la instancia de Adobe Commerce específica. Cuando cree este conjunto de datos, especifique el esquema XDM que ha creado anteriormente.

Después de completar los requisitos previos, conéctese a la [!DNL Commerce] destino.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a la [!DNL Adobe Commerce] destino:

1. En el [Interfaz de plataforma](https://experience.adobe.com/platform/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
1. Select **[!UICONTROL Personalización]**.
1. Seleccione el destino de Adobe Commerce para resaltarlo y, a continuación, seleccione **[!UICONTROL Configuración]**.
1. Siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

- **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
- **[!UICONTROL Descripción]**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
- **[!UICONTROL Alias de integración]**: Este valor se envía al SDK web del Experience Platform como nombre de objeto JSON.
- **[!UICONTROL ID de almacén de datos]**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/datastreams/overview.md) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Active segmentos en el [!DNL Commerce] destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en la variable [!DNL Commerce] destino.

## Pasos siguientes en [!DNL Adobe Commerce]

Ahora que ha configurado la variable [!DNL Commerce] destino dentro de Experience Platform, debe configurar la variable [!DNL Commerce Admin] para importar los segmentos de Real-Time CDP que ha creado. Consulte la [[!DNL Commerce] documentación](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html) para obtener más información.

## Validar la activación de audiencias en Commerce {#exported-data}

Después de activar los segmentos de Real-Time CDP en el [!DNL Adobe Commerce] verá esos segmentos disponibles en la [!DNL Admin] al crear una regla de precio del carro de compras:

![Administrador de Adobe Commerce](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](/help/data-governance/home.md).
