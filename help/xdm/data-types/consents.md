---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;consentimiento;preferencias;Preferencias;privacidadExclusiones;marketingPreferencias;optOutType;baseOfProcessing;consentimiento;consentimiento
title: Tipo de datos de consentimientos y preferencias
description: El tipo de datos Consentimiento para preferencias de privacidad, Personalization y marketing está diseñado para admitir la recopilación de permisos y preferencias de clientes que generan las plataformas de administración de consentimiento (CMP) y otras fuentes a partir de las operaciones de datos.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 0%

---

# [!UICONTROL Consentimientos y preferencias] tipo de datos

El tipo de datos [!UICONTROL Consentimiento para preferencias de privacidad, Personalization y marketing] (en adelante, el tipo de datos &quot;[!UICONTROL Consentimientos y preferencias]&quot;) es un tipo de datos [!DNL Experience Data Model] (XDM) que está diseñado para admitir la recopilación de permisos y preferencias de clientes generados por las Plataformas de administración de consentimiento (CMP) y otras fuentes a partir de las operaciones de datos.

Este documento describe la estructura y el uso previsto de los campos proporcionados por el tipo de datos [!UICONTROL Consentimientos y preferencias].

## Requisitos previos {#prerequisites}

Este documento requiere una comprensión práctica de XDM y el uso de los esquemas en [!DNL Experience Platform]. Revise la siguiente documentación antes de continuar:

* [Información general del sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Conceptos básicos de composición de esquemas](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Estructura de tipo de datos {#structure}

>[!IMPORTANT]
>
>El tipo de datos [!UICONTROL Consentimientos y preferencias] está diseñado para cubrir una amplia gama de casos de uso de administración de preferencias y consentimiento. Como resultado, este documento describe el uso de los campos del tipo de datos en términos generales y solo realiza sugerencias sobre cómo interpretar el uso de estos campos. Consulte con su equipo jurídico de privacidad para alinear la estructura del tipo de datos con la forma en que su organización interpreta y presenta estas opciones de consentimiento y preferencia a sus clientes.

El tipo de datos [!UICONTROL Consentimientos y preferencias] proporciona varios campos utilizados para capturar información de **consentimiento** y **preferencia**.

Un consentimiento es una opción que permite a un cliente especificar cómo se pueden utilizar sus datos. La mayoría de los consentimientos tienen un aspecto legal, en el sentido de que algunas jurisdicciones requieren la obtención de un permiso antes de que los datos puedan utilizarse de una manera determinada, o requieren que el cliente tenga la opción de detener ese uso (exclusión) si no se requiere un consentimiento afirmativo.

Una preferencia es una opción que permite al cliente especificar cómo se deben gestionar los distintos aspectos de su experiencia con una marca. Se dividen en dos categorías:

* **Preferencias de Personalization**: preferencias con respecto a cómo la marca debe personalizar las experiencias que se entregan a un cliente.
* **Preferencias de marketing**: preferencias sobre si una marca puede ponerse en contacto con un cliente a través de varios canales.

La siguiente captura de pantalla muestra cómo se representa la estructura del tipo de datos en la interfaz de usuario de Experience Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulte la guía de [exploración de recursos XDM](../ui/explore.md) para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Experience Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que el tipo de datos [!UICONTROL Consentimientos y preferencias] puede procesar. En las secciones siguientes se proporciona información sobre el uso específico de cada uno de estos campos.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
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
>Puede generar datos JSON de muestra para cualquier esquema XDM que defina en Experience Platform para visualizar cómo se deben asignar los datos de preferencia y consentimiento del cliente. Consulte la siguiente documentación para obtener más información:
>
>* [Generar datos de ejemplo en la interfaz de usuario](../ui/sample.md)
>* [Generar datos de ejemplo en la API](../api/sample-data.md)

## `consents` {#choices}

`consents` contiene varios campos que describen los consentimientos y preferencias de un cliente. Estos campos se describen con más detalle en las subsecciones siguientes.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
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

`collect` representa el consentimiento del cliente para recopilar sus datos.

```json
"collect": {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para ver los valores y definiciones aceptados. |

{style="table-layout:auto"}

### `adID`

`adID` representa el consentimiento del cliente para saber si se puede usar un ID de anunciante para vincular al cliente entre aplicaciones en este dispositivo.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `idType` | El tipo de id. de anuncio `IDFA` para el id. de Apple para anunciantes o `GAID` para el id. de anunciante de Google, también conocido como id. de anunciante de Android (AAID). |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para ver los valores y definiciones aceptados. |

{style="table-layout:auto"}

### `share`

`share` representa el consentimiento del cliente para saber si sus datos se pueden compartir con (o vender a) segundas o terceras partes.

```json
"share": {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para ver los valores y definiciones aceptados. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` registra las preferencias de los clientes con respecto a las formas en que sus datos pueden utilizarse para la personalización. Los clientes pueden excluirse de casos de uso de personalización específicos o excluirse por completo de la personalización.

>[!IMPORTANT]
>
>`personalize` no cubre los casos de uso de marketing. Por ejemplo, si un cliente excluye la personalización de todos los canales, no debe dejar de recibir comunicaciones a través de esos canales. En su lugar, los mensajes que reciben deben ser genéricos y no basados en su perfil.
>
>En el mismo ejemplo, si un cliente excluye el marketing directo para todos los canales (a través de `marketing`, explicado en la [sección siguiente](#marketing)), ese cliente no debería recibir ningún mensaje, aunque se permita la personalización.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `content` | Representa las preferencias del cliente para el contenido personalizado del sitio web o aplicación. |
| `val` | La preferencia de personalización proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que proporcione el consentimiento, el valor de este campo debe indicar la base sobre la que debe realizarse la personalización. Consulte el [apéndice](#choice-values) para ver los valores y definiciones aceptados. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` registra las preferencias de los clientes con respecto a los fines de marketing para los que se pueden usar sus datos. Los clientes pueden excluirse de casos de uso de marketing específicos o excluirse completamente del marketing directo.

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
| `preferred` | Indica el canal preferido del cliente para recibir comunicaciones. Consulte el [apéndice](#preferred-values) para obtener los valores aceptados. |
| `any` | Representa las preferencias del cliente para el marketing directo en su conjunto. La preferencia de consentimiento proporcionada en este campo se considera la preferencia &quot;predeterminada&quot; para cualquier canal de marketing, a menos que se sobrescriba con subcampos adicionales proporcionados en `marketing`. Si planea utilizar opciones de consentimiento más granulares, se recomienda excluir este campo.<br><br>Si el valor se establece en `n`, se deben ignorar todos los ajustes de personalización más específicos. Si el valor se establece en `y`, todas las opciones de personalización específicas también deben tratarse como `y`, a menos que se establezcan explícitamente como `n`. Si el valor no está establecido, los valores de cada opción de personalización deben respetarse según se haya especificado. |
| `email` | Indica si el cliente acepta recibir mensajes de correo electrónico. |
| `push` | Indica si el cliente permite recibir notificaciones push. |
| `sms` | Indica si el cliente acepta recibir mensajes de texto. |
| `val` | La preferencia proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que proporcione el consentimiento, el valor de este campo debe indicar la base sobre la que debe llevarse a cabo el caso de uso de marketing. Consulte el [apéndice](#choice-values) para ver los valores y definiciones aceptados. |
| `time` | Una marca de tiempo ISO 8601 de cuándo cambió la preferencia de marketing, si corresponde. Tenga en cuenta que si la marca de tiempo de cualquier preferencia individual es la misma que la proporcionada en `metadata`, este campo no debe establecerse para esa preferencia. |
| `reason` | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |

{style="table-layout:auto"}

### `metadata`

`metadata` captura metadatos generales sobre los consentimientos y preferencias del cliente la última vez que se actualizaron.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propiedad | Descripción |
| --- | --- |
| `time` | Una marca de tiempo ISO 8601 para la última vez que se actualizó cualquiera de los consentimientos y preferencias del cliente. Este campo se puede utilizar en lugar de aplicar marcas de tiempo a las preferencias individuales para reducir la carga y la complejidad. Si se proporciona un valor `time` en una preferencia individual, se anulará la marca de tiempo `metadata` para esa preferencia en particular. |

{style="table-layout:auto"}

## Ingesta de datos mediante el tipo de datos {#ingest}

Para usar el tipo de datos [!UICONTROL Consentimientos y preferencias] para introducir datos de consentimiento de tus clientes, debes crear un conjunto de datos basado en un esquema que contenga ese tipo de datos.

Consulte el tutorial de [creación de un esquema en la interfaz de usuario](https://www.adobe.com/go/xdm-schema-editor-tutorial-en_es) para ver los pasos sobre cómo asignar tipos de datos a los campos. Una vez que haya creado un esquema que contiene un campo con el tipo de datos [!UICONTROL Consentimientos y preferencias], consulte la sección sobre [creación de un conjunto de datos](../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siguiendo los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-Time Customer Profile], debe crear un esquema habilitado para [!DNL Profile] basado en la clase [!DNL XDM Individual Profile] que contiene el tipo de datos [!UICONTROL Consentimientos y preferencias]. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados arriba para ver los pasos específicos relacionados con los requisitos de [!DNL Real-Time Customer Profile] para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencia más recientes, a fin de que los perfiles de los clientes se actualicen correctamente. Consulte la descripción general de [políticas de combinación](../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencia

Cuando un cliente cambia sus consentimientos o preferencias en su sitio web, estos cambios deben recopilarse y aplicarse de inmediato mediante [Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe interrumpirse inmediatamente. Si un cliente se excluye de la personalización, no debe haber ninguna personalización presente en la siguiente página que visite.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información de referencia adicional sobre el tipo de datos [!UICONTROL Consentimientos y preferencias].

### Valores aceptados para `val` {#choice-values}

En la tabla siguiente se describen los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí (adhesión) | El cliente ha elegido el consentimiento o la preferencia. En otras palabras, **consienten** el uso de sus datos según lo indicado por el consentimiento o preferencia en cuestión. |
| `n` | No (exclusión) | El cliente ha optado por no participar en el consentimiento o la preferencia. En otras palabras, **no** consienten el uso de sus datos como lo indica el consentimiento o la preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un consentimiento final o un valor de preferencia. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación de dos pasos. Por ejemplo, si un cliente opta por recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccione un vínculo en un correo electrónico para comprobar que ha proporcionado la dirección de correo electrónico correcta, momento en el que el consentimiento se actualizará a `y`.<br><br>Si este consentimiento o preferencia no utiliza un proceso de verificación de dos conjuntos, se puede usar la opción `p` para indicar que el cliente aún no ha respondido a la solicitud de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no se ha excluido explícitamente (es decir, se asume el consentimiento).<br><br> Aunque este valor se puede ingerir en [!DNL Profile] mediante otros mecanismos, como la transmisión por secuencias, **no se admite** para la recopilación de datos o la recopilación de consentimiento en [!DNL Edge Network]. Aunque no se puede enviar explícitamente el valor `p`, el evento [[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md) sigue administrando la cola de eventos y el evento se envía a [!DNL Edge Network] una vez que el consentimiento del usuario final es explícitamente `in`. |
| `u` | Desconocido | Se desconoce el consentimiento o la información de preferencias del cliente. |
| `dy` | El valor predeterminado es Sí (inclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una opción de inclusión (&quot;Sí&quot;) de forma predeterminada. En otras palabras, se asume el consentimiento hasta que el cliente indique lo contrario.<br><br>Tenga en cuenta que si las leyes o cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `dn` | Valor predeterminado de No (exclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una exclusión (&quot;No&quot;) de forma predeterminada. En otras palabras, se supone que el cliente ha denegado el consentimiento hasta que indique lo contrario.<br><br>Tenga en cuenta que si las leyes o cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `LI` | Interés legítimo | El interés comercial legítimo de recopilar y procesar estos datos para el propósito especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones legales de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos para el propósito especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recogida de datos para el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

{style="table-layout:auto"}

### Valores aceptados para `preferred` {#preferred-values}

En la tabla siguiente se describen los valores aceptados para `preferred`. Los valores de `preferred` indican el canal preferido del cliente para recibir comunicaciones que le informarían sobre la recopilación de datos, las políticas de privacidad y las opciones de personalización.

| Valor | Descripción |
| --- | --- |
| `email` | Esta preferencia indica el consentimiento del cliente para recibir mensajes por correo electrónico. |
| `push` | Esta preferencia indica el consentimiento del cliente para recibir notificaciones push. Son mensajes o alertas enviados directamente a su dispositivo, a menudo una aplicación móvil. |
| `inApp` | Esta preferencia indica el consentimiento del cliente para recibir mensajes en la aplicación. Estos mensajes se envían dentro de una aplicación móvil o web y proporcionan información mientras el usuario participa activamente en la aplicación. |
| `sms` | Esta preferencia indica el consentimiento del cliente para recibir mensajes a través de SMS (servicio de mensajes cortos). Son mensajes de texto enviados a su teléfono móvil. |
| `phone` | Esta preferencia indica el consentimiento del cliente para recibir comunicaciones a través de interacciones de llamada telefónica. |
| `phyMail` | Esta preferencia indica el consentimiento del cliente para recibir materiales por correo físico. |
| `inVehicle` | Esta preferencia indica el consentimiento del cliente para recibir notificaciones mientras está en su vehículo. Estos mensajes podrán enviarse a través de sistemas de información y entretenimiento del vehículo u otros canales de comunicación dentro del vehículo. |
| `inHome` | Esta preferencia indica el consentimiento del cliente para recibir mensajes en casa. Estos mensajes pueden enviarse a través de dispositivos inteligentes para el hogar u otros canales de comunicación basados en el hogar. |
| `iot` | Esta preferencia indica el consentimiento del cliente para recibir mensajes relacionados con el Internet de las cosas (IoT). Estos mensajes pueden enviarse a través de dispositivos y sistemas conectados dentro de su entorno. |
| `social` | Esta preferencia indica el consentimiento del cliente para recibir comunicaciones a través de plataformas de medios sociales. |
| `other` | Esta preferencia incluye los canales que no se ajustan a las categorías estándar. Representa canales de comunicación alternativos o especializados que pueden ser específicos de una empresa o industria en particular. |
| `none` | Esta preferencia indica que el cliente no tiene un canal de comunicación preferido. |
| `unknown` | Esta preferencia significa que el canal de comunicación preferido del cliente no se conoce o no se ha especificado. Esto puede ocurrir si el cliente no ha proporcionado consentimiento explícito o información de preferencia. |

{style="table-layout:auto"}

### Esquema completo de [!UICONTROL consentimientos y preferencias] {#full-schema}

Para ver el esquema completo del tipo de datos [!UICONTROL Consentimientos y preferencias], consulte el [repositorio XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
