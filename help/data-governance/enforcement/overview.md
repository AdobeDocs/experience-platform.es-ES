---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Información general sobre la aplicación de políticas
topic: enforcement
description: Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos de Adobe Experience Platform y se han definido las políticas de uso de datos para las acciones de mercadotecnia en relación con dichas etiquetas, las capacidades de administración de datos le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan violaciones de políticas. Existen dos métodos de aplicación de políticas proporcionados por las funciones de administración de datos en la plataforma, aplicación basada en API y aplicación automática.
translation-type: tm+mt
source-git-commit: 83f1392ffab3571ebd91325123fbe7095ad59e28
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Información general sobre la aplicación de políticas

Una vez que las etiquetas de uso de datos se han aplicado a los [!DNL Platform] [!DNL Data Governance] conjuntos de datos y se han definido las políticas de uso de datos para las acciones de mercadotecnia en relación con dichas etiquetas, las capacidades le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan violaciones de políticas.

Existen dos métodos de aplicación de las políticas proporcionados por [!DNL Data Governance] las características en [!DNL Platform]: Aplicación basada en API y aplicación automática.

## Aplicación basada en API

La [!DNL Policy Service] API proporciona puntos finales que le permiten probar acciones de mercadotecnia con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se producen violaciones de políticas. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos.

Consulte el tutorial sobre la aplicación de [políticas](api-enforcement.md) para ver los pasos para evaluar las políticas mediante la API.

## Aplicación automática

Algunas aplicaciones que se crean sobre [!DNL Experience Platform] (por ejemplo, [!DNL Real-time Customer Data Platform]) proporcionan una aplicación automática de las políticas de uso de datos. Cada aplicación mantiene su propio método de detectar violaciones de políticas y proporcionar pasos para resolver problemas.

La aplicación automática de políticas en el CDP en tiempo real aprovecha las capacidades de administración de políticas, clasificación de datos y linaje de datos para evaluar y detectar infracciones de políticas. Para obtener más información, consulte la información general [sobre la gobernanza de datos CDP en tiempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) real.