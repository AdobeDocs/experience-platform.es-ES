---
title: Conector de destino de Adobe Commerce
description: Descubra cómo los comerciantes de Adobe Commerce y Real-Time CDP pueden personalizar la experiencia de compra ofreciendo promociones y contenido del sitio muy relevantes, personalizados para las audiencias de los clientes creadas y administradas dentro de Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 4%

---

# Conexión de Adobe Commerce {#adobe-commerce}

## Información general {#overview}

El conector de destino [!DNL Adobe Commerce] le permite seleccionar una o más audiencias de Real-Time CDP para activarlas en su cuenta de [!DNL Adobe Commerce] y así ofrecer una experiencia dinámica y personalizada a sus compradores. En [!DNL Adobe Commerce], puede seleccionar esas audiencias de Real-Time CDP para personalizar ofertas únicas en el carro de compras, como &quot;comprar 2 y obtener 1 gratis&quot;. También puede mostrar banners de pantalla completa y modificar los precios de los productos mediante ofertas promocionales, todas ellas personalizadas para las audiencias de Adobe Real-Time CDP.

## Requisitos previos {#prerequisites}

Este conector está disponible en el catálogo de destinos para clientes que han adquirido Real-Time CDP Prime o Ultimate y Adobe Commerce.

Para utilizar esta conexión de destino, asegúrese de que tiene acceso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Con acceso a la consola de desarrollador, puede ver la información de cuenta de servicio y credenciales que se necesita para [completar la configuración](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) de la extensión en Adobe Commerce.
- [Adobe Commerce Cloud versión 2.4.4 o superior](https://business.adobe.com/products/magento/magento-commerce.html)

En Experience Platform, cree lo siguiente:

- [Esquema](../../../xdm/schema/composition.md). El esquema que cree representa los datos que planea introducir desde Adobe Commerce. [Más información](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) sobre cómo crear un esquema que contenga grupos de campos específicos de Commerce.
- [Conjunto de datos](../../../catalog/datasets/user-guide.md#create). Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos. Puede crear este conjunto de datos a partir del esquema que ha creado anteriormente.
- [Flujo de datos](../../../datastreams/overview.md#create). ID que permite que los datos fluyan desde Adobe Experience Platform a otros productos Adobe DX. Este ID debe estar asociado a un sitio web específico dentro de la instancia de Adobe Commerce específica. Cuando cree este flujo de datos, especifique el esquema XDM que ha creado anteriormente.

Una vez cumplidos los requisitos previos, conéctese al destino [!DNL Commerce].

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse al destino [!DNL Adobe Commerce]:

1. En la [interfaz de Experience Platform](https://experience.adobe.com/platform/), vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
1. Seleccione **[!UICONTROL Personalization]**.
1. Seleccione el destino de Adobe Commerce para resaltarlo y luego seleccione **[!UICONTROL Configurar]**.
1. Siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

- **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
- **[!UICONTROL Descripción]**: escribe una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
- **[!UICONTROL Alias de integración]**: Este valor se envía a Experience Platform Web SDK como nombre de objeto JSON.
- **[!UICONTROL ID de secuencia de datos]**: Esto determina qué secuencia de datos de recopilación de datos contiene las audiencias que se incluyen en la respuesta a la página. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Consulte [Configuración de una secuencia de datos](../../../datastreams/overview.md) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en el destino [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea [Activar perfiles y audiencias en destinos de solicitud de perfil](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar audiencias en el destino [!DNL Commerce].

## Pasos siguientes en [!DNL Adobe Commerce]

Ahora que ha configurado el destino [!DNL Commerce] en Experience Platform, debe instalar la extensión [!DNL Audience Activation] en [!DNL Commerce] y configurar [!DNL Commerce Admin] para importar las audiencias de Real-Time CDP que ha creado. Consulte la [[!DNL Commerce] documentación](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) para obtener más información.

## Validar la activación de audiencias en Commerce {#exported-data}

Después de activar las audiencias de Real-Time CDP en su cuenta de [!DNL Adobe Commerce], verá esas audiencias disponibles cuando vaya a la barra lateral de _Administración_ y luego vaya a **[!UICONTROL Clientes]** > **[!UICONTROL Audiencia de Real-Time CDP]**.

![Panel de audiencias de Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
