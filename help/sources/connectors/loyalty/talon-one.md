---
title: Información general sobre Talon.One Source
description: Obtenga información sobre las fuentes de Talon.One en Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: 6b6a03fb8675ed01dd255f7206b23b05c809f2a6
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>Los orígenes de [!DNL Talon.One] se encuentran en la versión beta. Lea los [términos y condiciones](../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

Con [!DNL Talon.One], puede crear, administrar y optimizar fácilmente campañas de marketing personalizadas adaptadas a sus clientes. Utilice esta potente plataforma para ejecutar descuentos, distribuir cupones, lanzar programas de recomendación, configurar programas de fidelidad y ofrecer incentivos con juegos, todo ello desde un sistema escalable diseñado para ayudarle a atraer y recompensar a su audiencia.

Puede usar los orígenes [!DNL Talon.One] en el catálogo de orígenes de Adobe Experience Platform para introducir datos de fidelidad por lotes y de flujo continuo desde su cuenta de [!DNL Talon.One].

* [Eventos de streaming de Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Conector Source de Talon.One Batch](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Los datos de fidelización hacen referencia a la información del programa de fidelización de los usuarios finales, como los puntos de fidelidad, los puntos de fidelidad gastados, el nivel actual, los cupones concedidos, las referencias y los logros.

## Requisitos previos {#prerequisites}

Proporcione valores para las siguientes credenciales a fin de autenticar y conectar [!DNL Talon.One Batch Source Connector].

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Dominio | La URL única asociada con el entorno de la aplicación [!DNL Talon.One]. Asegúrese de no incluir el protocolo o la ruta al introducir el dominio. | `acmetalonone.us-east4` |
| Clave de API de administración [!DNL Talon.One] | La clave de la API de administración es una credencial que se usa para autenticar y autorizar el acceso a la API de administración de [!DNL Talon.One]. Esto gestiona operaciones como las siguientes: <ul><li>Importación de cupones</li><li>Recuperación de datos de campaña</li><li>Administrar aplicaciones y extremos</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Asignación {#mapping}

Para ayudarle a asignar cada objeto de efecto en función de su valor `effectType` único, puede utilizar la función de preparación de datos `array_to_map`. Esto le permite convertir fácilmente una matriz desordenada de efectos en pares clave-valor que se ajusten a sus necesidades. Consulte el ejemplo siguiente para obtener instrucciones.

También puede utilizar los grupos de campos de lealtad estandarizados que proporciona Adobe para modelar los conceptos del programa de lealtad de forma coherente.

>[!BEGINTABS]

>[!TAB Detalles de fidelización]

Este es un grupo de campos XDM estándar para el perfil individual XDM, que se utiliza para describir el estado de pertenencia de fidelidad de una persona capturando sus atributos de registro, en lugar de los datos de evento. Utilice este grupo de campos en los esquemas de Perfil para capturar:

* **Quién** es el miembro del programa (`loyaltyID`, `program`, `status`, `tier`)
* Sus **saldos actuales y permanentes** (`points`, `lifetimePoints`, `expiredPoints`, etc.)
* Clave **fechas de pertenencia** (`joinDate`, `upgradeDate`, `tierExpiryDate`)

>[!TAB Detalles del evento de fidelización]

El grupo de campos Detalles del evento de fidelización está diseñado para capturar la actividad de fidelidad en el nivel de evento, como los puntos obtenidos o canjeados en una transacción específica. Este grupo de campos incluye campos como `xdm:points`, `xdm:pointsRedeemed`, `xdm:pointsAsOfDate` y `xdm:program`. Utilice este grupo de campos de nivel de evento en los esquemas de Experience Event para capturar:

* **Movimientos por evento** en puntos (obtenidos, canjeados, caducados)
* **Descuentos** impulsados por cupones de fidelidad o recomendaciones
* **ID de programa** e ID de transacción para la reconciliación con el proveedor de fidelidad.

>[!ENDTABS]

| Fuente | Destino |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Próximos pasos

Lea la siguiente documentación para aprender a conectar su cuenta de [!DNL Talon.One] a Experience Platform e ingerir datos de fidelidad por lotes y de flujo continuo.

* [Eventos de streaming de Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Conector Source de Talon.One Batch](../../tutorials/ui/create/loyalty/talon-one-batch.md)
