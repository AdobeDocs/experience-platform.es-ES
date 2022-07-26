---
title: Clase de proveedor
description: Este documento proporciona una descripción general de la clase Provider en el Modelo de datos de experiencia (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL Proveedor] class

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Proveedor] captura el conjunto mínimo de propiedades que definen una entidad comercial del proveedor (como un proveedor de atención médica o un proveedor de seguros).

![Estructura de la clase](../images/classes/provider.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nombre de la persona]](../data-types/person-name.md) | El nombre del proveedor. |
| `_id` | [!UICONTROL Cadena] | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `providerId` | [!UICONTROL Cadena] | Identificador único del proveedor. |

{style=&quot;table-layout:auto&quot;}

La clase se puede ampliar con el [[!UICONTROL Proveedor de atención médica] grupo de campos](../field-groups/provider/healthcare-provider.md) para describir más detalles sobre un proveedor de atención médica.
