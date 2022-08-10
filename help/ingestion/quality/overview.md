---
keywords: Experience Platform;inicio;temas populares;calidad de datos;calidad;calidad;validación admitida;validación;validación admitida;
solution: Experience Platform
title: Calidad de los datos
topic-legacy: overview
description: El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y flujos en Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 7857b9a82dc1b5e12c9f8d757f6967b926124ec4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

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
| Esquema | Garantiza que el esquema sea **not** vacío y contiene una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| `createdUser` | Garantiza que el usuario que ha introducido el lote pueda ingerirlo. |

### Ingesta de la transmisión

Las siguientes validaciones se realizan para la ingesta de flujo continuo:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema sea **not** vacío y contiene una referencia al esquema de unión, como se indica a continuación: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| JSON | Garantiza que el JSON sea válido. |
| Organización IMS | Garantiza que la organización de IMS que aparece en la lista sea válida. |
| Nombre de origen | Garantiza que se especifique el nombre del origen de datos. |
| Conjunto de datos | Garantiza que el conjunto de datos se especifique, se habilite y no se elimine. |
| Encabezado | Garantiza que el encabezado se especifique y sea válido. |

Más información sobre cómo [!DNL Platform] los datos de supervisa y valida se encuentran en la [monitorización de la documentación de flujos de datos](./monitor-data-ingestion.md).

## Validación del valor de identidad

La siguiente tabla describe las reglas existentes que debe seguir para garantizar una validación correcta del valor de identidad.

| Área de nombres | Regla de validación | Comportamiento del sistema cuando se infringe la regla |
| --- | --- | --- |
| ECID | <ul><li>El valor de identidad de un ECID debe tener exactamente 38 caracteres.</li><li>El valor de identidad de un ECID debe constar únicamente de números.</li></ul> | <ul><li>Si el valor de identidad de ECID no es exactamente de 38 caracteres, se omite el registro.</li><li>Si el valor de identidad de ECID contiene caracteres no numéricos, se omite el registro.</li></ul> |
| No ECID | El valor de identidad no puede superar los 1024 caracteres. | Si el valor de identidad supera los 1024 caracteres, se omitirá el registro. |

Para obtener más información, consulte [!DNL Identity Service] proteccionistas, vea la [[!DNL Identity Service] información general sobre las protecciones](../../identity-service/guardrails.md).
