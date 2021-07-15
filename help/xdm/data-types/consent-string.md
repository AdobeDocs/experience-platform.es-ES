---
solution: Experience Platform
title: Tipo de datos de cadena de consentimiento
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de la cadena de consentimiento.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# [!UICONTROL Tipo de datos de ] cadena de consentimiento

[!UICONTROL La ] cadena de consentimiento es un tipo de datos XDM estándar que describe un valor de cadena que representa el consentimiento de un cliente. Incluye información contextual, como el estándar para la cadena de consentimiento (por ejemplo, el [Marco de transparencia y consentimiento IAB (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStandard` | Cadena | El estándar para la cadena de consentimiento. Esto ayuda a determinar el formato de la cadena de consentimiento establecida por los servicios de administración de consentimiento. |
| `consentStandardVersion` | Cadena | Versión del estándar de consentimiento, utilizado para definir con precisión el formato de la cadena de consentimiento según lo establecido por los servicios de administración de consentimiento. |
| `consentStringValue` | Cadena | La cadena de consentimiento completa proporcionada por el servicio de administración de consentimiento. `consentStandard` y  `consentStandardVersion` ayuda a definir cómo analizar esta cadena. |
| `containsPersonalData` | Booleano | Cuando este campo es true, significa que esta cadena de consentimiento debe procesarse para la aplicación del consentimiento. |
| `gdprApplies` | Booleano | Cuando este campo es verdadero, significa que el consentimiento viene con datos personales. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
