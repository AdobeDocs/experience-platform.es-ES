---
keywords: Experience Platform;inicio;temas populares;aplicación de políticas;aplicación automática;aplicación basada en API;gobernanza de datos
solution: Experience Platform
title: Resumen de aplicación de políticas
description: Descubra cómo se aplican las políticas de uso de datos en Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Introducción a la aplicación de políticas

Una vez que se hayan aplicado [etiquetas de uso de datos](../labels/overview.md) y se hayan definido [políticas de uso de datos](../policies/overview.md), puede aplicar esas políticas para evitar operaciones de datos que constituyan violaciones de políticas.

>[!NOTE]
>
>Este documento se centra en la aplicación de las políticas de uso de datos. Para obtener información sobre las directivas de control de acceso, consulte la guía sobre [control de acceso basado en atributos](../../access-control/abac/overview.md).

Existen dos métodos para aplicar directivas en Adobe Experience Platform: aplicación automática y aplicación basada en API.

## Aplicación automática

Experience Platform aprovecha el linaje de datos, la clasificación de datos y las capacidades de administración de políticas para evaluar y detectar automáticamente las violaciones de políticas. Consulte la descripción general de [aplicación automática de directivas](./auto-enforcement.md) para obtener más información.

## Aplicación basada en API

La API [!DNL Policy Service] proporciona puntos finales que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se produce alguna infracción de directiva. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la directiva de gobernanza de datos.

Consulte el tutorial sobre [aplicación basada en API](./api-enforcement.md) para ver los pasos sobre cómo evaluar las directivas mediante la API.
