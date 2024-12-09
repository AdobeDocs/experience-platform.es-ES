---
title: Tipo de datos de dosis
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de dosificación (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!UICONTROL Dosis] tipo de datos

[!UICONTROL Dosis] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe cómo se tomó o se debe tomar el medicamento. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de dosis](../../images/data-types/healthcare/dosage/dosage.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Instrucciones adicionales] | `additionalInstruction` | Matriz de [[!UICONTROL concepto codificable]](../healthcare/codeable-concept.md) | Instrucciones o advertencias suplementarias para el paciente. |
| [!UICONTROL Según Sea Necesario Para] | `asNeededFor` | Matriz de [[!UICONTROL concepto codificable]](../healthcare/codeable-concept.md) | Describe para qué problema se debe tomar el medicamento según sea necesario. |
| [!UICONTROL Dosis Y Tasa] | `doseAndRate` | Matriz de objetos | La cantidad de medicamento administrado, a administrar o la cantidad típica a administrar. Consulte la [sección siguiente](#dose-and-rate) para obtener más información |
| [!UICONTROL Dosis Máxima Por Administración] | `maxDosePerAdministration` | [[!UICONTROL Cantidad simple]](../healthcare/simple-quantity.md) | El límite superior de medicación por administración. |
| [!UICONTROL Dosis Máxima Por Vida] | `maxDosePerLifetime` | [[!UICONTROL Cantidad simple]](../healthcare/simple-quantity.md) | El límite superior de medicación por vida del paciente. |
| [!UICONTROL Dosis Máxima Por Período] | `maxDosePerPeriod` | Matriz de [[!UICONTROL Ratio]](../healthcare/ratio.md) | El límite superior de medicación por unidad de tiempo. |
| [!UICONTROL Método] | `method` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | La técnica para administrar la medicación. |
| [!UICONTROL Ruta] | `route` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | Cómo debe entrar el fármaco en el cuerpo. |
| [!UICONTROL Sitio del cuerpo] | `site` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | El sitio del cuerpo para administrar el fármaco. |
| [!UICONTROL Tiempo] | `timing` | [[!UICONTROL Tiempo]](../healthcare/timing.md) | Cuándo se debe administrar la medicación. |
| [!UICONTROL Según sea necesario] | `asNeeded` | Booleano | Un indicador para saber si el medicamento debe tomarse según sea necesario. |
| [!UICONTROL Instrucciones para el paciente] | `patientInstruction` | Cadena | Instrucciones en términos que debe entender el paciente o el consumidor. |
| [!UICONTROL Secuencia] | `Integer` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | El orden de las instrucciones de dosificación. |
| [!UICONTROL Texto] | `text` | Cadena | Planifique las instrucciones de dosificación textuales. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de dosis y velocidad](../../images/data-types/healthcare/dosage/dose-and-rate.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Cantidad de dosis] | `doseQuantity` | [[!UICONTROL Cantidad simple]](../healthcare/simple-quantity.md) | La cantidad de medicamento por dosis. |
| [!UICONTROL Intervalo de dosis] | `doseRange` | [[!UICONTROL Intervalo]](../healthcare/range.md) | La cantidad de medicamento por dosis. |
| [!UICONTROL Cantidad de tarifa] | `rateQuantity` | [[!UICONTROL Cantidad simple]](../healthcare/simple-quantity.md) | La cantidad de medicamento por unidad de tiempo. |
| [!UICONTROL Intervalo de tarifa] | `rateRange` | [[!UICONTROL Intervalo]](../healthcare/range.md) | La cantidad de medicamento por unidad de tiempo. |
| [!UICONTROL Proporción de tarifa] | `rateRatio` | [[!UICONTROL Proporción]](../healthcare/ratio.md) | La cantidad de medicamento por unidad de tiempo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | El tipo de dosis o tasa especificada. |
