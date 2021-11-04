---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;aplicación basada en API;control de datos
solution: Experience Platform
title: Información general sobre la aplicación de políticas
topic-legacy: guide
description: Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos de Adobe Experience Platform y se han definido políticas de uso de datos para acciones de marketing contra esas etiquetas, las funcionalidades de control de datos le permiten aplicar esas políticas e impedir operaciones de datos que constituyan infracciones de políticas. Las funciones de control de datos de Platform proporcionan dos métodos de aplicación de políticas, aplicación basada en API y aplicación automática.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Información general sobre la aplicación de políticas

Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos y se han definido políticas de uso de datos para acciones de marketing contra esas etiquetas, las funcionalidades de control de datos de Adobe Experience Platform le permiten aplicar esas políticas y evitar operaciones de datos que constituyan infracciones de políticas.

Las funciones de control de datos proporcionan dos métodos de aplicación de políticas en [!DNL Platform]: Aplicación basada en API y aplicación automática.

## Aplicación basada en API

La variable [!DNL Policy Service] La API proporciona extremos que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna violación de la política. En función de la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente la política de uso de datos.

Consulte el tutorial en [Aplicación basada en API](./api-enforcement.md) para ver los pasos sobre cómo evaluar las políticas mediante la API.

## Aplicación automática

El Experience Platform aprovecha las capacidades de administración de políticas, clasificación de datos y linaje de datos para evaluar automáticamente las infracciones de políticas y mostrarlas. Consulte la descripción general sobre [aplicación automática de directivas](./auto-enforcement.md) para obtener más información.
