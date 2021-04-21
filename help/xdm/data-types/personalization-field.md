---
solution: Experience Platform
title: Tipo de datos de campo de preferencia de personalización genérica
topic-legacy: overview
description: Este documento proporciona una descripción general del tipo de datos XDM del campo de preferencia de personalización genérica.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# [!UICONTROL Generic Personalization Preference Field] tipo de datos

[!UICONTROL Generic Personalization Preference Field] es un tipo de datos XDM estándar que describe la selección de un cliente para una preferencia de personalización determinada.

>[!NOTE]
>
>Este tipo de datos está diseñado para utilizarse para personalizar la estructura de los esquemas de consentimiento de su organización utilizando la [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mezcla](../mixins/profile/consents.md) como punto de referencia.

![](../images/data-types/personalization-field.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `val` | Cadena | La opción de preferencia proporcionada por el cliente para este caso de uso de personalización. Consulte la siguiente tabla para ver los valores y definiciones aceptados. |

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

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
