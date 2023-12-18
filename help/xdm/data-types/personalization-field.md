---
solution: Experience Platform
title: Tipo de datos del campo Preferencias de personalización genéricas
description: Obtenga información sobre el tipo de datos XDM del campo de preferencia de personalización genérica.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# [!UICONTROL Campo de preferencias de personalización genéricas] tipo de datos

[!UICONTROL Campo de preferencias de personalización genéricas] es un tipo de datos XDM estándar que describe la selección de un cliente para una preferencia de personalización determinada.

>[!NOTE]
>
>Este tipo de datos está diseñado para utilizarse para personalizar la estructura de los esquemas de consentimiento de su organización mediante [[!UICONTROL Consentimientos y preferencias] grupo de campos](../field-groups/profile/consents.md) como línea de base.

![](../images/data-types/personalization-field.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `val` | Cadena | La opción de preferencia proporcionada por el cliente para este caso de uso de personalización. Consulte la tabla siguiente para ver los valores y definiciones aceptados. |

{style="table-layout:auto"}

En la tabla siguiente se describen los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí (adhesión) | El cliente ha elegido esta preferencia. En otras palabras, **hacer** consentimiento para el uso de sus datos según lo indicado por la preferencia en cuestión. |
| `n` | No (exclusión) | El cliente ha optado por no participar en la preferencia. En otras palabras, **no** consentimiento para el uso de sus datos según lo indicado por la preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un valor de preferencia final. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación de dos pasos. Por ejemplo, si un cliente decide recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccionen un vínculo en un correo electrónico para verificar que han proporcionado la dirección de correo electrónico correcta, momento en el que el consentimiento se actualizaría a `y`.<br><br>Si esta preferencia no utiliza un proceso de verificación de dos conjuntos, la variable `p` choice se puede utilizar para indicar que el cliente aún no ha respondido a la solicitud de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web, antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no se ha excluido explícitamente (es decir, se asume el consentimiento). |
| `u` | Desconocido | Se desconoce la información de preferencias del cliente. |
| `dy` | El valor predeterminado es Sí (inclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una opción de inclusión (&quot;Sí&quot;) de forma predeterminada. En otras palabras, se asume el consentimiento hasta que el cliente indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `dn` | Valor predeterminado de No (exclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una exclusión (&quot;No&quot;) de forma predeterminada. En otras palabras, se supone que el cliente ha denegado el consentimiento hasta que indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `LI` | Interés legítimo | El interés comercial legítimo de recopilar y procesar estos datos para el propósito especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones legales de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos para el propósito especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recogida de datos para el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
