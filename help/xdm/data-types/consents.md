---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;consentimiento;preferencias;Preferencias;privacidad;exclusiones;marketingPreferences;optOutType;baseOfProcessing;consentimiento;consentimiento
title: Tipo de datos de consentimientos y preferencias
description: El tipo de datos Consentimiento para preferencias de privacidad, personalización y marketing está diseñado para admitir la recopilación de permisos y preferencias de clientes generadas por Plataformas de administración de consentimiento (CMP) y otras fuentes a partir de las operaciones de datos.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 1%

---

# [!UICONTROL Consentimientos y preferencias] tipo de datos

El [!UICONTROL Consentimiento para preferencias de privacidad, personalización y marketing] tipo de datos (en lo sucesivo, &quot;el[!UICONTROL Consentimientos y preferencias] tipo de datos&quot;) es un [!DNL Experience Data Model] (XDM) que está diseñado para admitir la recopilación de permisos y preferencias de clientes generadas por las Plataformas de administración de consentimiento (CMP) y otras fuentes a partir de las operaciones de datos.

Este documento describe la estructura y el uso previsto de los campos proporcionados por el [!UICONTROL Consentimientos y preferencias] tipo de datos.

## Requisitos previos {#prerequisites}

Este documento requiere una comprensión práctica de XDM y del uso de los esquemas en [!DNL Experience Platform]. Revise la siguiente documentación antes de continuar:

* [Información general del sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Conceptos básicos de composición de esquemas](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Estructura de tipo de datos {#structure}

>[!IMPORTANT]
>
>El [!UICONTROL Consentimientos y preferencias] El tipo de datos de está diseñado para cubrir una amplia gama de casos de uso de administración de preferencias y consentimiento. Como resultado, este documento describe el uso de los campos del tipo de datos en términos generales y solo realiza sugerencias sobre cómo interpretar el uso de estos campos. Consulte con su equipo jurídico de privacidad para alinear la estructura del tipo de datos con la forma en que su organización interpreta y presenta estas opciones de consentimiento y preferencia a sus clientes.

El [!UICONTROL Consentimientos y preferencias] El tipo de datos de proporciona varios campos utilizados para capturar **consentimiento** y **preferencia** información.

Un consentimiento es una opción que permite a un cliente especificar cómo se pueden utilizar sus datos. La mayoría de los consentimientos tienen un aspecto legal, en el sentido de que algunas jurisdicciones requieren la obtención de un permiso antes de que los datos puedan utilizarse de una manera determinada, o requieren que el cliente tenga la opción de detener ese uso (exclusión) si no se requiere un consentimiento afirmativo.

Una preferencia es una opción que permite al cliente especificar cómo se deben gestionar los distintos aspectos de su experiencia con una marca. Se dividen en dos categorías:

* **Preferencias de personalización**: Preferencias sobre cómo la marca debe personalizar las experiencias entregadas a un cliente.
* **Preferencias de marketing**: Preferencias con respecto a si una marca puede ponerse en contacto con un cliente a través de varios canales.

La siguiente captura de pantalla muestra cómo se representa la estructura del tipo de datos en la interfaz de usuario de Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulte la guía de [exploración de recursos XDM](../ui/explore.md) Consulte para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que el [!UICONTROL Consentimientos y preferencias] el tipo de datos puede procesar. En las secciones siguientes se proporciona información sobre el uso específico de cada uno de estos campos.

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
>* [Generación de datos de ejemplo en la IU](../ui/sample.md)
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

`collect` representa el consentimiento del cliente para que se recopilen sus datos.

```json
"collect": {
  "val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte la [apéndice](#choice-values) para valores y definiciones aceptados. |

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
| `idType` | El tipo de ID de anuncio: `IDFA` para el ID de Apple para anunciantes o `GAID` para el ID del anunciante de Google, también conocido como ID del anunciante de Android (AAID). |
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte la [apéndice](#choice-values) para valores y definiciones aceptados. |

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
| `val` | La opción de consentimiento proporcionada por el cliente para este caso de uso. Consulte la [apéndice](#choice-values) para valores y definiciones aceptados. |

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
| `val` | La preferencia de personalización proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que proporcione el consentimiento, el valor de este campo debe indicar la base sobre la que debe realizarse la personalización. Consulte la [apéndice](#choice-values) para valores y definiciones aceptados. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` registra las preferencias de los clientes con respecto a para qué fines de marketing se pueden utilizar sus datos. Los clientes pueden excluirse de casos de uso de marketing específicos o excluirse completamente del marketing directo.

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
| `preferred` | Indica el canal preferido del cliente para recibir comunicaciones. Consulte la [apéndice](#preferred-values) para valores aceptados. |
| `any` | Representa las preferencias del cliente para el marketing directo en su conjunto. La preferencia de consentimiento proporcionada en este campo se considera la preferencia &quot;predeterminada&quot; para cualquier canal de marketing, a menos que se anule con subcampos adicionales proporcionados en `marketing`. Si planea utilizar opciones de consentimiento más granulares, se recomienda excluir este campo.<br><br>Si el valor se establece en `n`Por lo tanto, se deben ignorar todos los ajustes de personalización más específicos. Si el valor se establece en `y`, todas las opciones de personalización específicas también deben tratarse como `y`, a menos que se establezca explícitamente como `n`. Si el valor no está establecido, los valores de cada opción de personalización deben respetarse según se haya especificado. |
| `email` | Indica si el cliente acepta recibir mensajes de correo electrónico. |
| `push` | Indica si el cliente permite recibir notificaciones push. |
| `sms` | Indica si el cliente acepta recibir mensajes de texto. |
| `val` | La preferencia proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que proporcione el consentimiento, el valor de este campo debe indicar la base sobre la que debe llevarse a cabo el caso de uso de marketing. Consulte la [apéndice](#choice-values) para valores y definiciones aceptados. |
| `time` | Una marca de tiempo ISO 8601 de cuándo cambió la preferencia de marketing, si corresponde. Tenga en cuenta que si la marca de tiempo de cualquier preferencia individual es la misma que la proporcionada en `metadata`, este campo no se debe definir para esa preferencia. |
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
| `time` | Una marca de tiempo ISO 8601 para la última vez que se actualizó cualquiera de los consentimientos y preferencias del cliente. Este campo se puede utilizar en lugar de aplicar marcas de tiempo a las preferencias individuales para reducir la carga y la complejidad. Proporcionar un `time` El valor de una preferencia individual anula el valor de `metadata` marca de tiempo de esa preferencia en particular. |

{style="table-layout:auto"}

## Ingesta de datos mediante el tipo de datos {#ingest}

Para utilizar la variable [!UICONTROL Consentimientos y preferencias] tipo de datos para introducir datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga ese tipo de datos.

Consulte el tutorial sobre [creación de un esquema en la IU](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos sobre cómo asignar tipos de datos a los campos. Una vez creado un esquema que contiene un campo con la variable [!UICONTROL Consentimientos y preferencias] tipo de datos, consulte la sección sobre [creación de un conjunto de datos](../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siga los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-Time Customer Profile], es necesario que cree un [!DNL Profile]Esquema habilitado para basado en [!DNL XDM Individual Profile] que contiene la clase [!UICONTROL Consentimientos y preferencias] tipo de datos. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados anteriormente para ver los pasos específicos relacionados con lo siguiente [!DNL Real-Time Customer Profile] requisitos para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencia más recientes, a fin de que los perfiles de los clientes se actualicen correctamente. Consulte la información general sobre [políticas de combinación](../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencia

Cuando un cliente cambia su consentimiento o preferencias en su sitio web, estos cambios deben recopilarse y aplicarse inmediatamente utilizando [SDK web de Adobe Experience Platform](../../edge/consent/supporting-consent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe interrumpirse inmediatamente. Si un cliente se excluye de la personalización, no debe haber ninguna personalización presente en la siguiente página que visite.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información de referencia adicional sobre [!UICONTROL Consentimientos y preferencias] tipo de datos.

### Valores aceptados para `val` {#choice-values}

En la tabla siguiente se describen los valores aceptados para `val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí (adhesión) | El cliente ha elegido el consentimiento o la preferencia. En otras palabras, **hacer** el consentimiento para el uso de sus datos según lo indicado por el consentimiento o preferencia en cuestión. |
| `n` | No (exclusión) | El cliente ha optado por no participar en el consentimiento o la preferencia. En otras palabras, **no** el consentimiento para el uso de sus datos según lo indicado por el consentimiento o preferencia en cuestión. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un consentimiento final o un valor de preferencia. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación de dos pasos. Por ejemplo, si un cliente decide recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccionen un vínculo en un correo electrónico para verificar que han proporcionado la dirección de correo electrónico correcta, momento en el que el consentimiento se actualizaría a `y`.<br><br>Si este consentimiento o preferencia no utiliza un proceso de verificación de dos conjuntos, la variable `p` choice se puede utilizar para indicar que el cliente aún no ha respondido a la solicitud de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` en la primera página de un sitio web, antes de que el cliente haya respondido a la solicitud de consentimiento. En jurisdicciones que no requieren consentimiento explícito, también puede utilizarlo para indicar que el cliente no se ha excluido explícitamente (es decir, se asume el consentimiento). |
| `u` | Desconocido | Se desconoce el consentimiento o la información de preferencias del cliente. |
| `dy` | El valor predeterminado es Sí (inclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una opción de inclusión (&quot;Sí&quot;) de forma predeterminada. En otras palabras, se asume el consentimiento hasta que el cliente indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `dn` | Valor predeterminado de No (exclusión) | El cliente no ha proporcionado un valor de consentimiento por sí mismo y se trata como una exclusión (&quot;No&quot;) de forma predeterminada. En otras palabras, se supone que el cliente ha denegado el consentimiento hasta que indique lo contrario.<br><br>Tenga en cuenta que si las leyes o los cambios en la política de privacidad de su compañía resultan en cambios en los valores predeterminados de algunos o todos los usuarios, debe actualizar manualmente todos los perfiles que contengan valores predeterminados. |
| `LI` | Interés legítimo | El interés comercial legítimo de recopilar y procesar estos datos para el propósito especificado supera el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos para el propósito especificado es necesaria para cumplir con las obligaciones legales de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos para el propósito especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recogida de datos para el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

{style="table-layout:auto"}

### Valores aceptados para `preferred` {#preferred-values}

En la tabla siguiente se describen los valores aceptados para `preferred`:

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
| `iot` | Mensajes del Internet de las cosas (IoT). |
| `social` | Contenido de medios sociales. |
| `other` | Un canal que no cabe en una categoría estándar. |
| `none` | No hay canal preferido. |
| `unknown` | Se desconoce el canal preferido. |

{style="table-layout:auto"}

### Completo [!UICONTROL Consentimientos y preferencias] esquema {#full-schema}

Para ver el esquema completo de [!UICONTROL Consentimientos y preferencias] tipo de datos, consulte la [repositorio XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
