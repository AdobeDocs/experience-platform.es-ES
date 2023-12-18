---
title: Grupo de campos Detalles del cliente potencial del socio (ejemplo)
description: Obtenga información acerca del grupo de campos de esquema (XDM) Detalles del posible cliente (ejemplo) de Partner.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Detalles del cliente potencial del socio (ejemplo)] grupo de campos

[!UICONTROL Detalles del cliente potencial del socio (ejemplo)] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El [!UICONTROL Detalles del cliente potencial del socio (ejemplo)] proporciona un marco de ejemplo para varios detalles relacionados con el perfil de un cliente potencial. Este marco de trabajo agiliza el proceso de organización y gestión de diversa información relacionada con los posibles clientes.

Este grupo de campos amplía la variable [Clase de perfil de cliente potencial individual](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) en el contexto de un socio.

![Un diagrama de la [!UICONTROL Detalles del cliente potencial del socio (ejemplo)] grupo de campos.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | Rango de edad dentro del hogar. |
| [!UICONTROL ApparelAccessories] | `apparelAccessories` | string | Preferencias o participación en ropa/accesorios. |
| [!UICONTROL ciclismo] | `bicycling` | string | Interés o participación en actividades de ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | string | Indica compromiso con la televisión por cable. |
| [!UICONTROL doméstico] | `domestics` | string | Preferencias o participación en actividades domésticas. |
| [!UICONTROL electrónica] | `electronics` | string | Interés o participación en dispositivos electrónicos. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Preferencias o participación en alimentos/bebidas. |
| [!UICONTROL calzado] | `footwear` | string | Interés o implicación en el calzado. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Preferencias o participación en alimentos saludables. |
| [!UICONTROL senderismo] | `hiking` | string | Interés o participación en actividades de senderismo. |
| [!UICONTROL householdId] | `householdId` | string | Un identificador único del hogar. |
| [!UICONTROL individualId] | `individualId` | string | Un identificador único del individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | La inferencia de ser titular de una tarjeta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | string | La inferencia de ser un titular de una tarjeta premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Un indicador del nivel de coincidencia. |
| [!UICONTROL Clasificación del comprador] | `buyerRating` | string | Una calificación relacionada con el comportamiento de compra. |
| [!UICONTROL Clasificación del donante] | `donorRating` | string | Una clasificación relacionada con el comportamiento del donante. |
| [!UICONTROL InvestmentRating] | `investmentRating` | string | Una calificación relacionada con el comportamiento de la inversión. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Una clasificación relacionada con el comportamiento de los que responden. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | string | La velocidad o la tasa de gasto. |
| [!UICONTROL VolumenGasto] | `spendingVolume` | string | La cantidad o el volumen de gasto. |
| [!UICONTROL recordId] | `recordId` | string | Un identificador único del registro. |
| [!UICONTROL residenceId] | `residenceId` | string | Un identificador único de la residencia. |
| [!UICONTROL navegación a vela] | `sailing` | string | Indica el interés o la participación en actividades de vela. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | string | Indica las preferencias o la participación en productos de vacaciones. |
| [!UICONTROL esquí] | `skiing` | string | Indica el interés o la participación en actividades de esquí. |
| [!UICONTROL tenis] | `tennis` | string | Indica el interés o la participación en actividades de tenis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Indica la participación con las compras de TV. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) en el repositorio XDM público.
