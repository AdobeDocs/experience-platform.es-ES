---
solution: Experience Platform
title: Tipo de datos de cadena de consentimiento
description: Este documento proporciona información general sobre el tipo de datos XDM de cadena de consentimiento.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---

# [!UICONTROL Cadena de consentimiento] tipo de datos

[!UICONTROL Cadena de consentimiento] es un tipo de datos XDM estándar que describe un valor de cadena que representa el consentimiento de un cliente. Incluye información contextual como el estándar para la cadena de consentimiento (por ejemplo, la variable [Marco de transparencia y consentimiento (TCF) de IAB 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStandard` | Cadena | El estándar para la cadena de consentimiento. Esto ayuda a determinar el formato de la cadena de consentimiento según lo establecido por los servicios de administración de consentimiento. |
| `consentStandardVersion` | Cadena | La versión del estándar de consentimiento, utilizado para definir con precisión el formato de la cadena de consentimiento según lo establecido por los servicios de gestión de consentimiento. |
| `consentStringValue` | Cadena | La cadena de consentimiento completa proporcionada por el servicio de administración de consentimiento. `consentStandard` y `consentStandardVersion` ayuda a definir cómo analizar esta cadena. |
| `containsPersonalData` | Booleano | Cuando este campo es true, significa que esta cadena de consentimiento debe procesarse para la aplicación del consentimiento. |
| `gdprApplies` | Booleano | Cuando este campo es true, significa que el consentimiento incluye datos personales. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
