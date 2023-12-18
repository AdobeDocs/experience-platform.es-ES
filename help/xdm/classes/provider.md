---
title: Clase de proveedor
description: Obtenga información acerca de la clase Provider en el modelo de datos de experiencia (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Proveedor] clase

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Proveedor] La clase captura el conjunto mínimo de propiedades que definen una entidad empresarial del proveedor (como un proveedor de atención médica o un proveedor de seguros).

![Estructura de clase](../images/classes/provider.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nombre de persona]](../data-types/person-name.md) | El nombre del proveedor. |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `providerId` | [!UICONTROL Cadena] | Un identificador único del proveedor. |

{style="table-layout:auto"}

La clase se puede ampliar con la variable [[!UICONTROL Proveedor de atención médica] grupo de campos](../field-groups/provider/healthcare-provider.md) para describir más detalles acerca de un proveedor de atención médica.
