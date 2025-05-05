---
title: Grupo de campos Detalles del cliente potencial del socio (ejemplo)
description: Obtenga información acerca del grupo de campos de esquema (XDM) Detalles del posible cliente (ejemplo) de Partner.
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL Detalles del cliente potencial del socio (ejemplo)] grupo de campos

[!UICONTROL Detalles del cliente potencial del socio (ejemplo)] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). [!UICONTROL Detalles del posible cliente asociado (ejemplo)] proporciona un marco de ejemplo para varios detalles relacionados con el perfil de un cliente potencial. Este marco de trabajo agiliza el proceso de organización y gestión de diversa información relacionada con los posibles clientes.

Este grupo de campos amplía la [clase de perfil de cliente potencial individual](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html?lang=es) en el contexto de un socio.

![Diagrama del grupo de campos [!UICONTROL Detalles del posible cliente asociado (muestra)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | cadena | Rango de edad dentro del hogar. |
| [!UICONTROL accesorios de ropa] | `apparelAccessories` | cadena | Preferencias o participación en ropa/accesorios. |
| [!UICONTROL ciclismo] | `bicycling` | cadena | Interés o participación en actividades de ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | cadena | Indica compromiso con la televisión por cable. |
| [!UICONTROL doméstico] | `domestics` | cadena | Preferencias o participación en actividades domésticas. |
| [!UICONTROL electrónica] | `electronics` | cadena | Interés o participación en dispositivos electrónicos. |
| [!UICONTROL comida y bebida] | `foodAndBeverage` | cadena | Preferencias o participación en alimentos/bebidas. |
| [!UICONTROL calzado] | `footwear` | cadena | Interés o implicación en el calzado. |
| [!UICONTROL healthFoods] | `healthFoods` | cadena | Preferencias o participación en alimentos saludables. |
| [!UICONTROL excursionismo] | `hiking` | cadena | Interés o participación en actividades de senderismo. |
| [!UICONTROL idDeCasa] | `householdId` | cadena | Un identificador único del hogar. |
| [!UICONTROL individualId] | `individualId` | cadena | Un identificador único del individuo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | cadena | La inferencia de ser titular de una tarjeta. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | cadena | La inferencia de ser un titular de una tarjeta premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | cadena | Un indicador del nivel de coincidencia. |
| [!UICONTROL Clasificación del comprador] | `buyerRating` | cadena | Una calificación relacionada con el comportamiento de compra. |
| [!UICONTROL Clasificación del donante] | `donorRating` | cadena | Una clasificación relacionada con el comportamiento del donante. |
| [!UICONTROL Clasificación de la inversión] | `investmentRating` | cadena | Una calificación relacionada con el comportamiento de la inversión. |
| [!UICONTROL Puntuación del respondedor] | `responderRating` | cadena | Una clasificación relacionada con el comportamiento de los que responden. |
| [!UICONTROL VelocidadDeGasto] | `spendingVelocity` | cadena | La velocidad o la tasa de gasto. |
| [!UICONTROL Volumen de gasto] | `spendingVolume` | cadena | La cantidad o el volumen de gasto. |
| [!UICONTROL recordId] | `recordId` | cadena | Un identificador único del registro. |
| [!UICONTROL residenceId] | `residenceId` | cadena | Un identificador único de la residencia. |
| [!UICONTROL navegando] | `sailing` | cadena | Indica el interés o la participación en actividades de vela. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | cadena | Indica las preferencias o la participación en productos de vacaciones. |
| [!UICONTROL esquiando] | `skiing` | cadena | Indica el interés o la participación en actividades de esquí. |
| [!UICONTROL tenis] | `tennis` | cadena | Indica el interés o la participación en actividades de tenis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | cadena | Indica la participación con las compras de TV. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) en el repositorio XDM público.
