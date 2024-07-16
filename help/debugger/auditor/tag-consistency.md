---
title: Referencia de prueba de coherencia de etiquetas
description: Descubra cómo Auditor comprueba la coherencia de las etiquetas en Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 38%

---

# Referencia de prueba de coherencia de etiquetas

Esta referencia proporciona más información sobre cómo funciona auditor en las pruebas de Adobe Experience Platform Debugger para mantener la coherencia de las etiquetas.

>[!NOTE]
>
>Para obtener más información sobre las pruebas de auditor en Platform Debugger, consulte [descripción general de la función de auditor](./overview.md).

Las pruebas de coherencia de etiquetas buscan incoherencias en todas las páginas digitalizadas. Son valores o configuraciones que deben ser iguales en todas las páginas del sitio para garantizar una recopilación de datos precisa.

| Prueba | Grosor | Criterios | Recomendación |
| --- | --- | --- | --- |
| Adobe Analytics: versión de código coherente | 5 | Se ha encontrado más de una versión del código de Analytics. | Reemplazar todas las instancias de Analytics con la versión actual.<br><br>[Más información](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |

{style="table-layout:auto"}
