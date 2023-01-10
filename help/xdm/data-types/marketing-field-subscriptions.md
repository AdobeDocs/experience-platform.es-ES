---
solution: Experience Platform
title: Campo de preferencia de marketing genérico con tipo de datos de suscripciones
description: Este documento proporciona información general sobre el campo de preferencia de marketing genérico con el tipo de datos XDM de suscripciones.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# [!UICONTROL Campo de preferencia de marketing genérico con suscripciones] tipo de datos

[!UICONTROL Campo de preferencia de marketing genérico con suscripciones] es un tipo de datos XDM estándar que describe la selección de un cliente para una preferencia de marketing determinada.

>[!NOTE]
>
>Este tipo de datos está diseñado para utilizarse para personalizar la estructura de los esquemas de consentimiento de la organización mediante el uso de [[!UICONTROL Consentimientos y preferencias] grupo de campos](../field-groups/profile/consents.md) como punto de referencia.
>
>Si no necesita un `subscriptions` para un campo específico de preferencias de marketing, puede usar la variable [tipo de datos básico de campo de marketing](./marketing-field.md) en su lugar.

![](../images/data-types/marketing-field-subscriptions.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `reason` | Cadena | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |
| `subscriptions` | Mapa | Mapa de las preferencias de marketing de los clientes para suscripciones específicas. Consulte la sección sobre [suscripciones](#subscriptions) para obtener más información. |
| `time` | DateTime | Marca de fecha y hora ISO 8601 del momento en que se cambió la preferencia de marketing, si corresponde. |
| `val` | Cadena | La opción de preferencia proporcionada por el cliente para este caso de uso de marketing. Consulte la [sección siguiente](#val) para valores y definiciones aceptados. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

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

## `subscriptions` {#subscriptions}

Algunas empresas permiten a los clientes aceptar distintas suscripciones asociadas a un canal de marketing determinado. Por ejemplo, una empresa bancaria puede permitir que los clientes se suscriban a las alertas telefónicas para cuentas extraviadas o que reciban llamadas de ventas para ofertas de programas de fidelidad.

El siguiente JSON representa un campo de marketing de ejemplo para un canal de marketing de llamada telefónica que contiene un `subscriptions` mapa. Cada clave de la variable `subscriptions` representa una suscripción individual para el canal de marketing. A su vez, cada suscripción contiene un valor de inclusión (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La variable [valor de consentimiento](#val) para la suscripción. |
| `type` | El tipo de suscripción. Puede ser cualquier cadena descriptiva, siempre que tenga 15 caracteres o menos. |
| `topics` | Matriz de cadenas que representan las áreas de interés a las que se suscribió un cliente y que pueden utilizarse para enviarle contenido relevante. |
| `subscribers` | Campo opcional de tipo asignación que representa un conjunto de identificadores (como direcciones de correo electrónico o números de teléfono) que se han suscrito a una suscripción determinada. Cada clave de este objeto representa el identificador en cuestión y contiene dos subpropiedades: <ul><li>`time`: Marca de tiempo ISO 8601 del momento de la suscripción de la identidad, si procede.</li><li>`source`: Origen del suscriptor. Puede ser cualquier cadena descriptiva, siempre que tenga 15 caracteres o menos.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Recursos adicionales

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
