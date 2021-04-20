---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;consentimiento;preferencias;preferencias;privacyOptOut;marketingPreferences;optOutType;baseOfProcessing;consentimiento;consentimiento
title: Tipo de datos de consentimientos y preferencias
description: El tipo de datos Consent for Privacy, Personalization and Marketing Preferences está diseñado para admitir la recopilación de permisos y preferencias de cliente generados por las plataformas de administración de consentimiento (CMP) y otras fuentes a partir de sus operaciones de datos.
topic: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 4e9395b4551842cf75b0d1a4ec36c85930c42da5
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 1%

---

# [!DNL Consents & Preferences] tipo de datos

El tipo de datos [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (denominado en adelante &quot;el tipo de datos &quot;[!DNL Consents & Preferences]&quot;) es un tipo de datos [!DNL Experience Data Model] (XDM) diseñado para admitir la recopilación de permisos y preferencias de clientes generados por las plataformas de administración de consentimiento (CMP) y otras fuentes de sus operaciones de datos.

Este documento cubre la estructura y el uso previsto de los campos proporcionados por el tipo de datos [!DNL Consents & Preferences] .

## Requisitos previos {#prerequisites}

Este documento requiere una comprensión práctica de XDM y el uso de los esquemas en [!DNL Experience Platform]. Revise la siguiente documentación antes de continuar:

* [Información general del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Aspectos básicos de la composición del esquema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Estructura del tipo de datos {#structure}

>[!IMPORTANT]
>
>El tipo de datos [!DNL Consents & Preferences] está diseñado para cubrir una amplia gama de casos de uso de administración de preferencias y consentimiento. Como resultado, este documento describe el uso de los campos del tipo de datos en términos generales y solo realiza sugerencias sobre cómo debe interpretar el uso de estos campos. Consulte con su equipo legal de privacidad para alinear la estructura del tipo de datos con la forma en que su organización interpreta y presenta estas elecciones de consentimiento y preferencias a sus clientes.

El tipo de datos [!DNL Consents & Preferences] proporciona varios campos utilizados para capturar información de **consentimiento** y **preferencia**.

Un consentimiento es una opción que permite a un cliente especificar cómo se pueden utilizar sus datos. La mayoría de los consentimientos tienen un aspecto jurídico, ya que algunas jurisdicciones requieren la obtención de permiso antes de poder utilizar los datos de una manera determinada o requieren que el cliente tenga la opción de detener ese uso (exclusión) si no se requiere consentimiento afirmativo.

Una preferencia es una opción que permite al cliente especificar cómo se deben gestionar los distintos aspectos de su experiencia con una marca. Se dividen en dos categorías:

* **Preferencias** de personalización: Preferencias sobre cómo la marca debe personalizar las experiencias entregadas a un cliente.
* **Preferencias** de marketing: Preferencias sobre si una marca puede ponerse en contacto con un cliente a través de varios canales.

La siguiente captura de pantalla muestra cómo se representa la estructura del tipo de datos en la interfaz de usuario de Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulte la guía de [Exploración de recursos XDM](../ui/explore.md) para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que el tipo de datos [!DNL Consents & Preferences] puede procesar. En las secciones que siguen se proporciona información sobre el uso específico de cada uno de estos campos.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Puede generar datos JSON de muestra para cualquier esquema XDM que defina en Experience Platform para ayudar a visualizar cómo se deben asignar los datos de consentimiento y preferencias del cliente. Consulte la siguiente documentación para obtener más información:
>
>* [Generar datos de ejemplo en la interfaz de usuario](../ui/sample.md)
>* [Generar datos de ejemplo en la API](../api/sample-data.md)


## `consents` {#choices}

`consents` contiene varios campos que describen las preferencias y consentimientos de un cliente. Estos campos se describen en detalle en las subsecciones siguientes.

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` representa el consentimiento del cliente para que se recopilen sus datos.

```json
"collect" : {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |

### `adID`

`adID` representa el consentimiento del cliente para saber si se puede usar un ID de anunciante (IDFA o GAID) para vincular al cliente entre aplicaciones en este dispositivo.

```json
"adID" : {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |

### `share`

`share` representa el consentimiento del cliente para saber si sus datos se pueden compartir con (o vender a) terceros.

```json
"share" : {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |

### `personalize` {#personalize}

`personalize` captura las preferencias de los clientes con respecto a las formas en que se pueden utilizar sus datos para la personalización. Los clientes pueden desactivar casos de uso de personalización específicos o excluirse por completo de la personalización.

>[!IMPORTANT]
>
>`personalize` no cubre casos de uso de marketing. Por ejemplo, si un cliente decide excluirse de la personalización para todos los canales, no debería dejar de recibir comunicaciones a través de esos canales. En su lugar, los mensajes que reciben deben ser genéricos y no estar basados en su perfil.
>
>Por el mismo ejemplo, si un cliente decide excluirse del marketing directo para todos los canales (a través de `marketing`, explicado en la [siguiente sección](#marketing)), entonces ese cliente no debería recibir ningún mensaje, aunque la personalización esté permitida.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `content` | Representa las preferencias del cliente para el contenido personalizado en el sitio web o la aplicación. |
| `val` | La preferencia de personalización proporcionada por el cliente para el caso de uso especificado. En los casos en los que no sea necesario pedir al cliente que dé su consentimiento, el valor de este campo debe indicar la base sobre la que debe realizarse la personalización. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |

### `marketing` {#marketing}

`marketing` captura las preferencias del cliente con respecto a los fines de marketing para los que se pueden utilizar sus datos. Los clientes pueden excluirse de casos de uso de marketing específicos o excluirse completamente del marketing directo.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `preferred` | Indica el canal preferido del cliente para recibir comunicaciones. Consulte el [apéndice](#preferred-values) para conocer los valores aceptados. |
| `any` | Representa las preferencias del cliente para el marketing directo en su conjunto. La preferencia de consentimiento proporcionada en este campo se considera la preferencia &quot;predeterminada&quot; para cualquier canal de marketing, a menos que se sobrescriba por los subcampos adicionales proporcionados en `marketing`. Si planea utilizar opciones de consentimiento más granulares, se recomienda excluir este campo.<br><br>Si el valor se establece en  `n`, se debe ignorar toda configuración de personalización más específica. Si el valor se establece en `y`, todas las opciones de personalización más específicas también deben tratarse como `y`, a menos que se configuren explícitamente en `n`. Si el valor no está establecido, se deben respetar los valores de cada opción de personalización según se especifique. |
| `email` | Indica si el cliente acepta recibir mensajes de correo electrónico. |
| `push` | Indica si el cliente permite recibir notificaciones push. |
| `sms` | Indica si el cliente acepta recibir mensajes de texto. |
| `val` | La preferencia proporcionada por el cliente para el caso de uso especificado. En los casos en los que no sea necesario pedir al cliente que dé su consentimiento, el valor de este campo debe indicar la base sobre la que se debe llevar a cabo el caso de uso de marketing. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |
| `time` | Marca de fecha y hora ISO 8601 del momento en que se cambió la preferencia de marketing, si corresponde. Tenga en cuenta que si la marca de tiempo de cualquier preferencia individual es la misma que la proporcionada en `metadata`, este campo no se debe configurar para esa preferencia. |
| `reason` | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |

### `metadata`

`metadata` captura metadatos generales sobre las preferencias y consentimientos del cliente cada vez que se actualizaron por última vez.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propiedad | Descripción |
| --- | --- |
| `time` | Marca de tiempo ISO 8601 para la última vez que se actualizaron los consentimientos y preferencias del cliente. Este campo se puede utilizar en lugar de aplicar marcas de tiempo a las preferencias individuales para reducir la carga y la complejidad. Si se proporciona un valor `time` en una preferencia individual, se anula la marca de tiempo `metadata` de esa preferencia en particular. |

## Ingesta de datos con el tipo de datos {#ingest}

Para utilizar el tipo de datos [!DNL Consents & Preferences] para introducir datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga ese tipo de datos.

Consulte el tutorial sobre la [creación de un esquema en la interfaz de usuario](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos sobre cómo asignar tipos de datos a los campos. Una vez que haya creado un esquema que contenga un campo con el tipo de datos [!DNL Consents & Preferences] , consulte la sección sobre [la creación de un conjunto de datos](../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siguiendo los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-time Customer Profile], es necesario crear un esquema habilitado para [!DNL Profile] basado en la clase [!DNL XDM Individual Profile] que contiene el tipo de datos [!DNL Consents & Preferences]. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados anteriormente para ver los pasos específicos relacionados con los requisitos [!DNL Real-time Customer Profile] para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencias más recientes, a fin de que los perfiles de clientes se actualicen correctamente. Consulte la descripción general de [merge policy](../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencias

Cuando un cliente cambia sus consentimientos o preferencias en el sitio web, estos cambios deben recopilarse e implementarse inmediatamente mediante el [SDK web de Adobe Experience Platform](../../edge/consent/supporting-consent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe cesar inmediatamente. Si un cliente decide excluirse de la personalización, no debería haber ninguna personalización presente en la siguiente página que visite.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información de referencia adicional sobre el tipo de datos [!DNL Consents & Preferences].

### Valores aceptados para `val` {#choice-values}

La siguiente tabla describe los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí | El cliente ha elegido el consentimiento o la preferencia. En otras palabras, **dan** su consentimiento para el uso de sus datos como se indica en el consentimiento o preferencia en cuestión. |
| `n` | No | El cliente ha excluido el consentimiento o la preferencia. En otras palabras, **no** dan su consentimiento para el uso de sus datos como se indica en el consentimiento o preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un consentimiento definitivo o un valor de preferencia. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación en dos pasos. Por ejemplo, si un cliente decide recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccione un vínculo en un correo electrónico para verificar que ha proporcionado la dirección de correo electrónico correcta, momento en el que el consentimiento se actualiza a `y`.<br><br>Si este consentimiento o preferencia no utiliza un proceso de verificación de dos conjuntos, entonces la  `p` opción puede utilizarse para indicar que el cliente aún no ha respondido a la solicitud de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no ha excluido explícitamente la solicitud (es decir, se asume el consentimiento). |
| `u` | Unknown | Se desconoce la información de consentimiento o preferencias del cliente. |
| `LI` | Interés legítimo | El interés legítimo de las empresas en recopilar y procesar estos datos con el fin especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones jurídicas de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos con el fin especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recopilación de datos con el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

### Valores aceptados para `preferred` {#preferred-values}

La siguiente tabla describe los valores aceptados para `preferred`:

| Valor | Descripción |
| --- | --- |
| `email` | Mensajes de correo electrónico. |
| `push` | Notificaciones push. |
| `inApp` | Mensajes en la aplicación. |
| `sms` | Mensajes SMS. |
| `phone` | Interacciones de llamadas telefónicas. |
| `phyMail` | Correo físico. |
| `inVehicle` | Mensajes en el vehículo. |
| `inHome` | Mensajes en casa. |
| `iot` | Internet de los mensajes (IoT). |
| `social` | Contenido de medios sociales. |
| `other` | Canal que no se ajusta a una categoría estándar. |
| `none` | No hay canal preferido. |
| `unknown` | Se desconoce el canal preferido. |

### Esquema [!DNL Consents & Preferences] completo {#full-schema}

Para ver el esquema completo del tipo de datos [!DNL Consents & Preferences], consulte el [repositorio XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
