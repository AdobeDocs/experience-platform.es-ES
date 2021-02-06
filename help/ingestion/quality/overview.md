---
keywords: Experience Platform;inicio;temas populares;Calidad de los datos;Calidad;Validación admitida;Validación;validación admitida;
solution: Experience Platform
title: Calidad de los datos
topic: overview
description: El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y por flujo continuo en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

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

Tanto la ingestión por lotes como la de flujo continuo impiden que los datos fallidos se desplacen hacia abajo al mover datos incorrectos para su recuperación y análisis en [!DNL Data Lake]. La ingestión de datos proporciona las siguientes validaciones para la ingestión por lotes y por flujo continuo.

### Ingesta por lotes

Se realizan las siguientes validaciones para la ingestión por lotes:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| `createdUser` | Garantiza que el usuario que ingesta el lote pueda ingestar el lote. |

### Ingesta de la transmisión

Se realizan las siguientes validaciones para la transmisión por secuencias de ingesta:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| JSON | Garantiza que el JSON sea válido. |
| Organización IMS | Garantiza que la organización de IMS que aparece en la lista sea una organización válida. |
| Nombre del origen | Garantiza que se especifique el nombre del origen de datos. |
| Conjunto de datos | Garantiza que el conjunto de datos se especifique, habilite y no se elimine. |
| Encabezado | Garantiza que el encabezado se especifique y sea válido. |

Encontrará más información sobre cómo [!DNL Platform] monitorea y valida los datos en la [documentación de los flujos de datos de monitoreo](./monitor-data-ingestion.md).
