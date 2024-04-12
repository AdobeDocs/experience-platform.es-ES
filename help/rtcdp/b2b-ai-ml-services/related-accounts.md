---
title: Cuentas relacionadas en Real-Time CDP B2B Edition
type: Documentation
description: Información general y más información sobre las funciones de cuentas relacionadas en Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# Cuentas relacionadas en Real-Time CDP B2B Edition

## Información general {#overview}

Las empresas B2B a menudo almacenan la información de sus clientes en varios sistemas, cada uno de los cuales incluye solo datos parciales o incluso en conflicto para la misma entidad comercial del mundo real. Esto crea un desafío masivo de llegar a una vista precisa de sus clientes, reduciendo así la eficiencia y eficacia de sus esfuerzos de marketing y ventas B2B.

| ID | Nombre | Sitio web | de la industria | Estado | Teléfono | Tiene una oportunidad abierta con un importe > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408) 536-6000 |   |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Servicio de consultoría de Acme | `http://www.acme.com/consulting` | Asesoría tecnológica | NY | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

Con cuentas relacionadas, [!DNL Real-Time CDP B2B] ahora muestra una lista de cuentas similares a la cuenta que está explorando.

![Pantalla que muestra las cuentas relacionadas en la IU de Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Utilice esta función para ver los perfiles de cuenta relacionados de un perfil de cuenta en la interfaz de usuario de Experience Platform y, a continuación, incluya las cuentas relacionadas en las definiciones de segmentos para ampliar su alcance o aplicar criterios más amplios a las audiencias.

## Habilitar el servicio de cuentas relacionadas {#enable}

Para habilitar el servicio, seleccione **[!UICONTROL Perfiles]** en la barra lateral seguida de **[!UICONTROL Configuración]**.

![IU del Experience Platform que resalta perfiles y configuraciones.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Seleccione la opción junto a [!UICONTROL Habilitar cuentas relacionadas] para habilitar el servicio y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Pantalla de configuración de la cuenta que resalta la opción y guarda.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Funcionamiento {#how-it-works}

Los trabajos de aprendizaje automático de ejecución diaria utilizan un algoritmo jerárquico para agrupar perfiles de cuenta similares en grupos en función de tres factores:

* Vínculo de cuenta principal
* Dominio web
* Nombre de la cuenta

Después de un trabajo de procesamiento correcto, cada miembro del grupo de perfiles de cuenta se etiqueta con la lista Cuentas relacionadas. Puede ver la lista en la **Cuentas relacionadas** de la página Perfil de Cuenta y utilice las cuentas relacionadas en las definiciones de segmentos.

Consulte la documentación para obtener más información sobre [trabajos de cuentas relacionadas con profile enrichment](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Visualización de cuentas relacionadas {#how-to-view}

Puede ver las cuentas relacionadas de una cuenta que esté explorando en la interfaz de usuario de Experience Platform.

Consulte la documentación para obtener más información sobre [Cómo encontrar cuentas relacionadas en la interfaz de usuario de](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Uso de cuentas relacionadas {#how-to-use}

Puede utilizar cuentas de y cuentas relacionadas en la segmentación. La decisión de usar cuentas relacionadas en las definiciones de segmentos depende de su caso de uso de marketing. Por ejemplo, puede utilizar cuentas relacionadas para campañas de marketing por correo electrónico o publicidad donde puede aceptar una precisión menor a cambio de un alcance más amplio.

Consulte un [ejemplo de segmentación](/help/rtcdp/segmentation/b2b.md#related-accounts) que utiliza cuentas relacionadas.
