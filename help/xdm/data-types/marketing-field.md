---
solution: Experience Platform
title: Tipo de datos de campo de preferencia de marketing genérico
description: Este documento proporciona información general sobre el tipo de datos XDM del campo de preferencias de marketing genéricas.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# [!UICONTROL Campo de preferencia de marketing genérico] tipo de datos

[!UICONTROL Campo de preferencia de marketing genérico] es un tipo de datos XDM estándar que describe la selección de un cliente para una preferencia de marketing determinada.

>[!NOTE]
>
>Este tipo de datos está diseñado para utilizarse para personalizar la estructura de los esquemas de consentimiento de la organización mediante el uso de [[!UICONTROL Consentimientos y preferencias] grupo de campos](../field-groups/profile/consents.md) como punto de referencia.
>
>Si necesita una `subscriptions` para un campo específico de preferencias de marketing, debe usar la variable [campo de marketing con tipo de datos de suscripciones](./marketing-field-subscriptions.md) en su lugar.

![](../images/data-types/marketing-field.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `reason` | Cadena | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |
| `time` | DateTime | Marca de fecha y hora ISO 8601 del momento en que se cambió la preferencia de marketing, si corresponde. |
| `val` | Cadena | La opción de preferencia proporcionada por el cliente para este caso de uso de marketing. Consulte la siguiente tabla para ver los valores y definiciones aceptados. |

{style=&quot;table-layout:auto&quot;}

La siguiente tabla describe los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí (opción de inclusión) | El cliente ha elegido la preferencia. En otras palabras, **do** el consentimiento para el uso de sus datos, tal como indica la preferencia en cuestión. |
| `n` | No (exclusión) | El cliente se ha excluido de la preferencia. En otras palabras, **no** el consentimiento para el uso de sus datos, tal como indica la preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un valor de preferencia final. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación en dos pasos. Por ejemplo, si un cliente decide recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccionen un vínculo en un correo electrónico para verificar que han proporcionado la dirección de correo electrónico correcta, en cuyo momento el consentimiento se actualizaría a `y`.<br><br>Si esta preferencia no utiliza un proceso de verificación de dos conjuntos, la variable `p` en su lugar, se puede utilizar para indicar que el cliente aún no ha respondido al mensaje de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web, antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no ha excluido explícitamente la solicitud (es decir, se asume el consentimiento). |
| `u` | Desconocido | Se desconoce la información de preferencias del cliente. |
| `dy` | Predeterminado de Sí (opción de inclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una opción de inclusión (&quot;Sí&quot;) de forma predeterminada. En otras palabras, se asume el consentimiento hasta que el cliente indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su empresa producen cambios en los valores predeterminados de algunos o de todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `dn` | Valor predeterminado de no (exclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como un valor de exclusión (&quot;No&quot;) de forma predeterminada. En otras palabras, se supone que el cliente ha denegado el consentimiento hasta que indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su empresa producen cambios en los valores predeterminados de algunos o de todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `LI` | Interés legítimo | El interés legítimo de las empresas en recopilar y procesar estos datos con el fin especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones jurídicas de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos con el fin especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recopilación de datos con el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
