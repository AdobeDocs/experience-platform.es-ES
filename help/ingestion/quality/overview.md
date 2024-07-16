---
keywords: Experience Platform;inicio;temas populares;Calidad de los datos;Calidad;Validación admitida;Validación admitida;Validación admitida;
solution: Experience Platform
title: Calidad de datos
description: El siguiente documento proporciona un resumen de las comprobaciones y los comportamientos de validación admitidos para la ingesta por lotes y la transmisión en Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Calidad de los datos en Adobe Experience Platform

Adobe Experience Platform ofrece garantías bien definidas de integridad, precisión y coherencia de cualquier dato cargado mediante la ingesta por lotes o de flujo continuo. El siguiente documento proporciona un resumen de las comprobaciones admitidas y los comportamientos de validación para la ingesta por lotes y de flujo continuo en [!DNL Experience Platform].

## Comprobaciones admitidas

|   | Ingesta por lotes | Ingesta por streaming |
| ------ | --------------- | ------------------- |
| Comprobación del tipo de datos | Sí | Sí |
| Comprobación de enumeración | Sí | Sí |
| Comprobación del intervalo (mín., máx.) | Sí | Sí |
| Comprobación de campo obligatoria | Sí | Sí |
| Comprobación del patrón | No | Sí |
| Comprobación de formato | No | Sí |

## Comportamientos de validación admitidos

Tanto la ingesta por lotes como la de flujo continuo evitan que los datos con errores vayan a la fase posterior moviendo los datos incorrectos para su recuperación y análisis en [!DNL Data Lake]. La ingesta de datos proporciona las siguientes validaciones para la ingesta por lotes y streaming.

### Ingesta por lotes

Se realizan las siguientes validaciones para la ingesta por lotes:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y contenga una referencia al esquema de unión, de la siguiente manera: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| `createdUser` | Garantiza que el usuario que ha introducido el lote puede introducir el lote. |

### Ingesta por streaming

Se realizan las siguientes validaciones para la ingesta de transmisión:

| Área de validación | Descripción |
| --------------- | ----------- |
| Esquema | Garantiza que el esquema esté **no** vacío y contenga una referencia al esquema de unión, de la siguiente manera: `"meta:immutableTags": ["union"]` |
| `identityField` | Garantiza que se definan todos los descriptores de identidad válidos. |
| JSON | Garantiza que el JSON sea válido. |
| Organización | Garantiza que la organización de la lista sea una organización válida. |
| Nombre de origen | Garantiza que se especifique el nombre de la fuente de datos. |
| Conjunto de datos | Garantiza que el conjunto de datos esté especificado, habilitado y no se haya eliminado. |
| Encabezado | Garantiza que el encabezado esté especificado y sea válido. |

Encontrará más información sobre cómo [!DNL Platform] supervisa y valida los datos en la [documentación sobre la supervisión de flujos de datos](./monitor-data-ingestion.md).

## Validación del valor de identidad

En la tabla siguiente se describen las reglas existentes que debe seguir para garantizar una validación correcta del valor de identidad.

| Área de nombres | Regla de validación | Comportamiento del sistema cuando se infringe la regla |
| --- | --- | --- |
| ECID | <ul><li>El valor de identidad de un ECID debe ser exactamente de 38 caracteres.</li><li>El valor de identidad de un ECID debe constar solo de números.</li></ul> | <ul><li>Si el valor de identidad de ECID no es exactamente de 38 caracteres, se omite el registro.</li><li>Si el valor de identidad de ECID contiene caracteres no numéricos, se omite el registro.</li></ul> |
| No ECID | El valor de identidad no puede superar los 1024 caracteres. | Si el valor de identidad supera los 1024 caracteres, se omite el registro. |

Para obtener más información sobre [!DNL Identity Service] protecciones, consulte la [[!DNL Identity Service] descripción general de las protecciones](../../identity-service/guardrails.md).
