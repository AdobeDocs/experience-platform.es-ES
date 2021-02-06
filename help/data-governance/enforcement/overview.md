---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;Aplicación basada en API;control de datos
solution: Experience Platform
title: Información general sobre la aplicación de políticas
topic: guide
description: Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos de Adobe Experience Platform y se han definido las políticas de uso de datos para las acciones de mercadotecnia en relación con dichas etiquetas, las capacidades de administración de datos le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan violaciones de políticas. Existen dos métodos de aplicación de políticas proporcionados por las funciones de administración de datos en la plataforma, aplicación basada en API y aplicación automática.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Información general sobre la aplicación de políticas

Una vez que se han aplicado las etiquetas de uso de datos a los conjuntos de datos y se han definido las políticas de uso de datos para las acciones de marketing en relación con dichas etiquetas, las capacidades de administración de datos de Adobe Experience Platform le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan infracciones de políticas.

Existen dos métodos de cumplimiento de políticas proporcionados por las características [!DNL Data Governance] en [!DNL Platform]: Aplicación basada en API y aplicación automática.

## Aplicación basada en API

La API [!DNL Policy Service] proporciona extremos que le permiten probar acciones de mercadotecnia con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para verificar si se producen violaciones de políticas. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos.

Consulte el tutorial en [Aplicación basada en API](./api-enforcement.md) para ver los pasos para evaluar las políticas mediante la API.

## Aplicación automática

El Experience Platform aprovecha las capacidades de administración de políticas, clasificación de datos y linaje de datos para evaluar automáticamente las infracciones de políticas y superarlas. Consulte la información general sobre [aplicación automática de políticas](./auto-enforcement.md) para obtener más información.