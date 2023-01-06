---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;aplicación basada en API;control de datos
solution: Experience Platform
title: Información general sobre la aplicación de políticas
description: Descubra cómo se aplican las políticas de uso de datos en Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Información general sobre la aplicación de políticas

Una vez [etiquetas de uso de datos](../labels/overview.md) se han aplicado y [políticas de uso de datos](../policies/overview.md) se han definido, puede aplicar esas políticas para evitar operaciones de datos que constituyan infracciones de políticas.

>[!NOTE]
>
>Este documento se centra en la aplicación de las políticas de uso de datos. Para obtener información sobre las políticas de control de acceso, consulte la guía de [control de acceso basado en atributos](../../access-control/abac/overview.md).

Existen dos métodos para aplicar políticas en Adobe Experience Platform: aplicación automática y aplicación basada en API.

## Aplicación automática

El Experience Platform aprovecha las capacidades de administración de políticas, clasificación de datos y linaje de datos para evaluar automáticamente las infracciones de políticas y mostrarlas. Consulte la descripción general sobre [aplicación automática de directivas](./auto-enforcement.md) para obtener más información.

## Aplicación basada en API

La variable [!DNL Policy Service] La API proporciona extremos que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna violación de la política. En función de la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente la política de control de datos.

Consulte el tutorial en [Aplicación basada en API](./api-enforcement.md) para ver los pasos sobre cómo evaluar las políticas mediante la API.
