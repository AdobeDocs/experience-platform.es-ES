---
title: Clase de pagador
description: Este documento proporciona información general sobre la clase Payer en el Modelo de datos de experiencia (XDM).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---

# [!UICONTROL Pagador] class

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Pagador] captura el conjunto mínimo de propiedades que definen una entidad empresarial pagadora que recopila datos pertenecientes a compañías de seguros (como seguro de enfermedad).

![Estructura de la clase](../images/classes/payer.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | [!UICONTROL Cadena] | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `payerId` | [!UICONTROL Cadena] | Identificador único del ordenante. |
| `payerName` | [!UICONTROL Cadena] | Nombre del ordenante. |

{style=&quot;table-layout:auto&quot;}
