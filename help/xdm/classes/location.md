---
title: Clase de ubicación
description: Obtenga información sobre la clase Ubicación en el modelo de datos de experiencia (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# clase [!UICONTROL Location]

En Experience Data Model (XDM), la clase [!UICONTROL Location] captura información de ubicación de eventos en vivo, como una sala de viajes o un coliseo deportivo.

![Estructura de clase de ubicación](../images/classes/location.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Identificador] | `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no es necesario proporcionarle un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| [!UICONTROL Identificador de ubicación] | `locationID` | [!UICONTROL Cadena] | Un identificador único de la ubicación. |
| [!UICONTROL Nombre de ubicación] | `locationName` | [!UICONTROL Cadena] | El nombre de la ubicación. |

La clase se puede ampliar con el grupo de campos [[!UICONTROL Location]](../field-groups/location/healthcare-location.md) para describir más detalles acerca de una ubicación.
