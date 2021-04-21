---
solution: Experience Platform
title: Tipo de datos de campo de preferencia de marketing genérico
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM del campo de preferencias de marketing genéricas.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# [!UICONTROL Generic Marketing Preference Field] tipo de datos

[!UICONTROL Generic Marketing Preference Field] es un tipo de datos XDM estándar que describe la selección de un cliente para una preferencia de marketing determinada.

>[!NOTE]
>
>Este tipo de datos está diseñado para utilizarse para personalizar la estructura de los esquemas de consentimiento de su organización utilizando la [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mezcla](../mixins/profile/consents.md) como punto de referencia.
>
>Si necesita un `subscriptions` mapa para un campo de preferencias de marketing determinado, debe utilizar el campo [marketing con el tipo de datos de suscripciones](./marketing-field-subscriptions.md) en su lugar.

![](../images/data-types/marketing-field.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `reason` | Cadena | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |
| `time` | DateTime | Marca de fecha y hora ISO 8601 del momento en que se cambió la preferencia de marketing, si corresponde. |
| `val` | Cadena | La opción de preferencia proporcionada por el cliente para este caso de uso de marketing. Consulte la siguiente tabla para ver los valores y definiciones aceptados. |

La siguiente tabla describe los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí | El cliente ha elegido la preferencia. En otras palabras, **do** consienten en el uso de sus datos como se indica en la preferencia en cuestión. |
| `n` | No | El cliente se ha excluido de la preferencia. En otras palabras, **no** aceptan el uso de sus datos como se indica en la preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un valor de preferencia final. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación en dos pasos. Por ejemplo, si un cliente decide recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccione un vínculo en un correo electrónico para verificar que ha proporcionado la dirección de correo electrónico correcta, momento en el que el consentimiento se actualiza a `y`.<br><br>Si esta preferencia no utiliza un proceso de verificación de dos conjuntos, se puede utilizar la  `p` opción para indicar que el cliente aún no ha respondido a la solicitud de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no ha excluido explícitamente la solicitud (es decir, se asume el consentimiento). |
| `u` | Unknown | Se desconoce la información de preferencias del cliente. |
| `LI` | Interés legítimo | El interés legítimo de las empresas en recopilar y procesar estos datos con el fin especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones jurídicas de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos con el fin especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recopilación de datos con el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
