---
title: Referencia de prueba de coherencia de etiquetas
description: Descubra cómo la función auditor comprueba la coherencia de etiquetas en Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 38%

---

# Referencia de prueba de coherencia de etiquetas

Esta referencia proporciona más información sobre cómo auditor comprueba la coherencia de las etiquetas en Adobe Experience Platform Debugger.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Experience Platform Debugger, consulte [descripción general de la función de auditor](./overview.md).

Las pruebas de coherencia de etiquetas buscan incoherencias en todas las páginas digitalizadas. Son valores o configuraciones que deben ser iguales en todas las páginas del sitio para garantizar una recopilación de datos precisa.

| Prueba | Grosor | Criterios | Recomendación |
| --- | --- | --- | --- |
| Adobe Analytics: versión de código coherente | 5 | Se ha encontrado más de una versión del código de Analytics. | Reemplazar todas las instancias de Analytics con la versión actual.<br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es) |

{style="table-layout:auto"}
