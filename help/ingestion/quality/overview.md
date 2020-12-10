---
keywords: Experience Platform;home;popular topics;Data quality;quality;Quality;Supported validation;Validation;supported validation;
solution: Experience Platform
title: Calidad de la ingestión de datos
topic: overview
description: El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y por flujo continuo en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---


# Calidad de datos en Adobe Experience Platform

Adobe Experience Platform ofrece garantías bien definidas de integridad, precisión y coherencia para cualquier dato cargado mediante una ingesta por lotes o por flujo continuo. El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingestión por lotes y por flujo continuo en [!DNL Experience Platform].

## Comprobaciones admitidas

|   | Ingesta de lotes | Transmisión de datos por secuencias |
| ------ | --------------- | ------------------- |
| Comprobación del tipo de datos | Sí | Sí |
| Comprobación de enumeración | Sí | Sí |
| Comprobación del rango (mín., máx.) | Sí | Sí |
| Comprobación de campo obligatoria | Sí | Sí |
| Comprobación de patrón | No | Sí |
| Comprobación de formato | No | Sí |

## Comportamientos de validación admitidos

Tanto la ingestión por lotes como la transmisión por flujo continuo impiden que los datos fallidos se desplacen hacia abajo al mover datos incorrectos para su recuperación y análisis en [!DNL Data Lake]. La ingestión de datos proporciona las siguientes validaciones para la ingestión por lotes y por flujo continuo.

### Ingesta por lotes

Se realizan las siguientes validaciones para la ingestión por lotes:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema **no esté** vacío y contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| `createdUser` | Garantiza que el usuario que ingesta el lote pueda ingestar el lote. |

### Transmisión por flujo continuo

Se realizan las siguientes validaciones para la transmisión por secuencias de ingesta:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema **no esté** vacío y contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| JSON | Garantiza que el JSON sea válido. |
| Organización IMS | Garantiza que la organización de IMS que aparece en la lista sea una organización válida. |
| Nombre del origen | Garantiza que se especifique el nombre del origen de datos. |
| Conjunto de datos | Garantiza que el conjunto de datos se especifique, habilite y no se elimine. |
| Header | Garantiza que el encabezado se especifique y sea válido. |

Encontrará más información sobre cómo [!DNL Platform] monitorear y validar los datos en la documentación [de flujos de datos de](./monitor-data-ingestion.md)monitoreo.
