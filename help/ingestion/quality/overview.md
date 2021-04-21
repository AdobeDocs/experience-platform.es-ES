---
keywords: Experience Platform;inicio;temas populares;calidad de datos;calidad;calidad;validación admitida;validación;validación admitida;
solution: Experience Platform
title: Calidad de los datos
topic-legacy: overview
description: El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y flujos en Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---

# Calidad de los datos en Adobe Experience Platform

Adobe Experience Platform ofrece garantías bien definidas de integridad, precisión y coherencia para cualquier dato cargado mediante ingesta por lotes o por transmisión. El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y flujos en [!DNL Experience Platform].

## Comprobaciones admitidas

|   | Ingesta de lotes | Ingesta de flujo continuo |
| ------ | --------------- | ------------------- |
| Comprobación de tipo de datos | Sí | Sí |
| Comprobación de enumeración | Sí | Sí |
| Comprobación de rango (mín., máx.) | Sí | Sí |
| Comprobación de campo requerida | Sí | Sí |
| Comprobación de motivo | No | Sí |
| Comprobación de formato | No | Sí |

## Comportamientos de validación admitidos

Tanto la ingesta por lotes como la de flujo continuo impiden que los datos fallidos se desplacen hacia abajo al mover datos incorrectos para su recuperación y análisis en [!DNL Data Lake]. El consumo de datos proporciona las siguientes validaciones para la ingesta por lotes y de flujo continuo.

### Ingesta por lotes

Las siguientes validaciones se realizan para la ingesta por lotes:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y que contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| `createdUser` | Garantiza que el usuario que ha introducido el lote pueda ingerirlo. |

### Ingesta de la transmisión

Las siguientes validaciones se realizan para la ingesta de flujo continuo:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y que contenga una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| JSON | Garantiza que el JSON sea válido. |
| Organización IMS | Garantiza que la organización de IMS que aparece en la lista sea válida. |
| Nombre de origen | Garantiza que se especifique el nombre del origen de datos. |
| Conjunto de datos | Garantiza que el conjunto de datos se especifique, se habilite y no se elimine. |
| Encabezado | Garantiza que el encabezado se especifique y sea válido. |

Encontrará más información sobre cómo [!DNL Platform] supervisa y valida los datos en la [documentación de monitorización de flujos de datos](./monitor-data-ingestion.md).
