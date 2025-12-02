---
title: Restablecer ID de combinación
description: Acción obsoleta que permite separar eventos invocados en la misma página.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Restablecer ID de combinación

>[!IMPORTANT]
>
>Esta acción está obsoleta. En su lugar, [recopile la configuración de clics](../configure/data-collection.md#collect-internal-link-clicks) en vínculos internos.

El tipo de acción **[!UICONTROL Reset merge ID]** le permite separar eventos invocados en la misma página. Suele utilizarse en escenarios de vínculos internos en los que podría tener varias cargas útiles que desee enviar a Adobe. Esta acción le permite restablecer el ID de combinación de un evento para que no se considere parte del mismo evento después de llegar a Edge Network.

Si desea controlar cómo se separan o combinan varios eventos en la misma página, utilice la opción [Recopilar clics en vínculos internos](../configure/data-collection.md#collect-internal-link-clicks) al configurar la extensión de etiqueta.
