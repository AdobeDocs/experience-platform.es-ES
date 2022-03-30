---
title: Cuentas relacionadas en Real-Time CDP B2B Edition
type: Documentation
description: Información general y más información sobre la función de cuentas relacionadas en Experience Platform CDP B2B en tiempo real.
source-git-commit: 09fd6c30461a4229411ce67426fdcb247661f7cb
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 6%

---

# Cuentas relacionadas en Real-Time CDP B2B Edition

## Información general {#overview}

A menudo, las empresas B2B tienen la información de sus clientes almacenada en múltiples sistemas, cada uno de los cuales incluye solamente datos parciales o incluso contradictorios para la misma entidad comercial del mundo real. Esto crea un enorme desafío de llegar a una visión precisa de sus clientes, reduciendo así la eficiencia y eficacia de sus esfuerzos de ventas y marketing B2B.

| ID | Nombre | Sitio web | de la industria | Estado | Phone | Tiene una oportunidad abierta con la cantidad > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Servicio de consultoría Acme | `http://www.acme.com/consulting` | Consultoría de tecnología | NY | (212) 471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

Con cuentas relacionadas, [!DNL Real-time CDP B2B] ahora muestra una lista de cuentas similares a la cuenta que está explorando.

![Pantalla que muestra cuentas relacionadas en la interfaz de usuario del Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Utilice esta función para ver perfiles de cuenta relacionados para un perfil de cuenta en la interfaz de usuario del Experience Platform y, a continuación, incluir las cuentas relacionadas en las definiciones de segmentos para ampliar su alcance o aplicar criterios más amplios en sus segmentos.

## Funcionamiento {#how-it-works}

Los trabajos de aprendizaje automático de ejecución diaria utilizan un algoritmo jerárquico para agrupar perfiles de cuenta similares en grupos basados en tres factores:

* Vínculo de cuenta principal
* Dominio web
* Nombre de la cuenta

Después de un trabajo de procesamiento correcto, cada miembro del grupo de perfiles de cuenta se etiqueta con la lista Cuentas relacionadas. Puede ver la lista en la **Cuentas relacionadas** de la página Perfil de cuenta y utilice las cuentas relacionadas en las definiciones de segmentos.

Consulte la documentación para obtener más información sobre la variable [trabajos de cuentas relacionadas con el enriquecimiento de perfiles](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Cómo ver cuentas relacionadas {#how-to-view}

Puede ver las cuentas relacionadas de una cuenta que está explorando en la interfaz de usuario del Experience Platform.

Consulte la documentación para obtener más información sobre la variable [cómo encontrar cuentas relacionadas en la interfaz de usuario](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Uso de cuentas relacionadas {#how-to-use}

Puede utilizar cuentas y cuentas relacionadas en la segmentación. La decisión de utilizar cuentas relacionadas en las definiciones de segmentos depende del caso de uso de marketing. Por ejemplo, puede utilizar cuentas relacionadas para campañas de publicidad o marketing por correo electrónico en las que acepte una precisión menor a cambio de un alcance más amplio.

Consulte una [ejemplo de segmentación](/help/rtcdp/segmentation/b2b.md#related-account) que utiliza cuentas relacionadas.