---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre la aplicación de políticas
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# Información general sobre la aplicación de políticas

Una vez que las etiquetas de uso de datos se han aplicado a los conjuntos de datos de la plataforma y se han definido las políticas de uso de datos para las acciones de mercadotecnia en relación con dichas etiquetas, las capacidades de administración de datos le permiten aplicar dichas directivas y evitar operaciones de datos que constituyan violaciones de políticas.

Existen dos métodos de aplicación de políticas proporcionados por las características de administración de datos en la plataforma: Aplicación **basada en** API y aplicación **automática**.

## Aplicación basada en API

La API de servicio de directivas proporciona extremos que le permiten probar acciones de marketing con conjuntos de datos o combinaciones arbitrarias de etiquetas de uso de datos para comprobar si se producen violaciones de directivas. En función de la respuesta de la API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente el cumplimiento de la política de uso de datos.

Consulte el tutorial sobre la aplicación de [políticas](api-enforcement.md) para ver los pasos para evaluar las políticas mediante la API.

## Aplicación automática

Determinadas aplicaciones que se crean en la parte superior de la plataforma de experiencia (como la plataforma de datos del cliente en tiempo real) proporcionan una aplicación automática de las políticas de uso de datos. Cada aplicación mantiene su propio método de detectar violaciones de políticas y proporcionar pasos para resolver problemas.

Consulte la documentación de la aplicación basada en la plataforma que está utilizando para obtener más información sobre la aplicación automática de políticas de uso de datos. Para obtener información sobre la aplicación automática de políticas en tiempo real, consulte la información general [sobre la gobernanza de datos CDP en tiempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.