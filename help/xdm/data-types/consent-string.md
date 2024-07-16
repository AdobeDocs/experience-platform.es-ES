---
solution: Experience Platform
title: Tipo de datos de cadena de consentimiento
description: Obtenga información acerca del tipo de datos XDM de cadena de consentimiento.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 13%

---

# [!UICONTROL Tipo de datos de cadena de consentimiento]

[!UICONTROL Cadena de consentimiento] es un tipo de datos XDM estándar que describe un valor de cadena que representa el consentimiento de un cliente. Incluye información contextual como el estándar para la cadena de consentimiento (por ejemplo, el [Marco de transparencia y consentimiento IAB (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStandard` | Cadena | El estándar para la cadena de consentimiento. Esto ayuda a determinar el formato de la cadena de consentimiento según lo establecido por los servicios de gestión de consentimiento. |
| `consentStandardVersion` | Cadena | La versión del estándar de consentimiento, utilizado para definir con precisión el formato de la cadena de consentimiento según lo establecido por los servicios de gestión de consentimiento. |
| `consentStringValue` | Cadena | La cadena de consentimiento completa proporcionada por el servicio de administración de consentimiento. `consentStandard` y `consentStandardVersion` ayudan a definir cómo analizar esta cadena. |
| `containsPersonalData` | Booleano | Cuando este campo es true, significa que esta cadena de consentimiento debe procesarse para la aplicación del consentimiento. |
| `gdprApplies` | Booleano | Cuando este campo es true, significa que el consentimiento incluye datos personales. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
