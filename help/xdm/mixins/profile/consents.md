---
solution: Experience Platform
title: Mezcla de preferencias de privacidad/personalización/marketing (consentimientos)
topic-legacy: overview
description: Este documento proporciona una descripción general de la combinación de privacidad, personalización y preferencias de marketing (consentimientos).
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2238'
ht-degree: 1%

---

# [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixto

[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] (en lo sucesivo, la  [!DNL Privacy & Consents] mezcla) es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md), que se utiliza para recoger el consentimiento del cliente y la información sobre preferencias.

>[!NOTE]
>
>Dado que esta mezcla solo es compatible con [!DNL XDM Individual Profile], no se puede utilizar para esquemas [!DNL XDM ExperienceEvent]. Si desea incluir datos de consentimiento y preferencias en el esquema de Experience Event, añada el [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] tipo de datos](../../data-types/consents.md) al esquema mediante el uso de una [mezcla personalizada](../../ui/resources/mixins.md#create) en su lugar.

## Estructura de la mezcla {#structure}

>[!IMPORTANT]
>
>La [!DNL Consents & Preferences] mezcla está diseñada para cubrir una serie de casos de uso de consentimiento y gestión de preferencias. Como resultado, este documento describe el uso de los campos de la mezcla en términos generales, y solamente hace sugerencias sobre cómo debe interpretar el uso de estos campos. Consulte con su equipo legal de privacidad para alinear la estructura de la mezcla con la manera en que su organización interpreta y presenta estas elecciones de consentimiento y preferencias a sus clientes.

La mezcla [!DNL Consents & Preferences] proporciona varios campos utilizados para capturar información de **consentimiento** y **preferencia**.

Un consentimiento es una opción que permite a un cliente especificar cómo se pueden utilizar sus datos. La mayoría de los consentimientos tienen un aspecto jurídico, ya que algunas jurisdicciones requieren la obtención de permiso antes de poder utilizar los datos de una manera determinada o requieren que el cliente tenga la opción de detener ese uso (exclusión) si no se requiere consentimiento afirmativo.

Una preferencia es una opción que permite al cliente especificar cómo se deben gestionar los distintos aspectos de su experiencia con una marca. Se dividen en dos categorías:

* **Preferencias** de personalización: Preferencias sobre cómo la marca debe personalizar las experiencias entregadas a un cliente.
* **Preferencias** de marketing: Preferencias sobre si una marca puede ponerse en contacto con un cliente a través de varios canales.

La siguiente captura de pantalla muestra cómo se representa la estructura de la mezcla en la interfaz de usuario de Platform:

![](../../images/mixins/consent.png)

>[!TIP]
>
>Consulte la guía de [Exploración de recursos XDM](../../ui/explore.md) para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que puede procesar la mezcla [!DNL Consents & Preferences]. En las secciones que siguen se proporciona información sobre el uso específico de cada uno de estos campos.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
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
>* [Generar datos de ejemplo en la interfaz de usuario](../../ui/sample.md)
>* [Generar datos de ejemplo en la API](../../api/sample-data.md)


## Casos de uso del campo

Los casos de uso previstos para cada uno de estos campos se proporcionan en las secciones siguientes.

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
| `email` | Indica si el cliente acepta recibir mensajes de correo electrónico. El cliente también puede proporcionar preferencias para suscripciones individuales dentro de este canal. Consulte la sección sobre [suscripciones](#subscriptions) más abajo para obtener más información. |
| `push` | Indica si el cliente permite recibir notificaciones push. El cliente también puede proporcionar preferencias para suscripciones individuales dentro de este canal. Consulte la sección sobre [suscripciones](#subscriptions) más abajo para obtener más información. |
| `sms` | Indica si el cliente acepta recibir mensajes de texto. El cliente también puede proporcionar preferencias para suscripciones individuales dentro de este canal. Consulte la sección sobre [suscripciones](#subscriptions) más abajo para obtener más información. |
| `val` | La preferencia proporcionada por el cliente para el caso de uso especificado. En los casos en los que no sea necesario pedir al cliente que dé su consentimiento, el valor de este campo debe indicar la base sobre la que se debe llevar a cabo el caso de uso de marketing. Consulte el [apéndice](#choice-values) para conocer los valores y definiciones aceptados. |
| `time` | Marca de fecha y hora ISO 8601 del momento en que se cambió la preferencia de marketing, si corresponde. Tenga en cuenta que si la marca de tiempo de cualquier preferencia individual es la misma que la proporcionada en `metadata`, este campo no se debe configurar para esa preferencia. |
| `reason` | Cuando un cliente se excluye de un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente se excluyó. |

#### `subscriptions` {#subscriptions}

Las propiedades `email`, `push` y `sms` del objeto `marketing` pueden representar suscripciones de cliente para esos canales individuales. Para ello, agregue una propiedad `subscriptions` al canal de marketing en cuestión.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de suscripción. Puede ser cualquier cadena descriptiva, siempre que tenga 15 caracteres o menos. |
| `subscribers` | Campo opcional de tipo asignación que representa un conjunto de identificadores (como direcciones de correo electrónico o números de teléfono) que se han suscrito a una suscripción determinada. Cada clave de este objeto representa el identificador en cuestión y contiene dos subpropiedades: <ul><li>`time`: Marca de tiempo ISO 8601 del momento de la suscripción de la identidad, si procede.</li><li>`source`: Origen del suscriptor. Puede ser cualquier cadena descriptiva, siempre que tenga 15 caracteres o menos.</li></ul> |


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

### `idSpecific`

`idSpecific` se puede utilizar cuando un consentimiento o preferencia en particular no se aplica universalmente a un cliente, pero está restringido a un único dispositivo o ID. Por ejemplo, un cliente puede desactivar la recepción de correos electrónicos a una dirección, mientras que posiblemente permita el envío de correos electrónicos a otra.

>[!IMPORTANT]
>
>Las preferencias y consentimientos de nivel de canal (es decir, los proporcionados en `consents` fuera de `idSpecific`) se aplican a los ID dentro de ese canal. Por lo tanto, todos los consentimientos y preferencias de nivel de canal afectan directamente a si se respetan configuraciones equivalentes específicas del dispositivo o ID:
>
>* Si el cliente se ha excluido en el nivel de canal, se omiten todos los consentimientos o preferencias equivalentes de `idSpecific`.
>* Si no se establece el consentimiento o la preferencia a nivel de canal o si el cliente ha elegido, se respetan las preferencias o consentimientos equivalentes de `idSpecific`.


Cada clave del objeto `idSpecific` representa un área de nombres de identidad específica reconocida por el servicio de identidad de Adobe Experience Platform. Aunque puede definir sus propios espacios de nombres personalizados para categorizar distintos identificadores, se recomienda utilizar uno de los espacios de nombres estándar proporcionados por Identity Service para reducir los tamaños de almacenamiento para el perfil del cliente en tiempo real. Para obtener más información sobre los áreas de nombres de identidad, consulte la [descripción general del área de nombres de identidad](../../../identity-service/namespaces.md) en la documentación del servicio de identidad.

Las claves de cada objeto de área de nombres representan los valores de identidad únicos para los que el cliente ha establecido preferencias. Cada valor de identidad puede contener un conjunto completo de consentimientos y preferencias, con el mismo formato que `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Dentro de los objetos `marketing` proporcionados en la sección `idSpecific` , los campos `any` y `preferred` no son compatibles. Estos campos solo se pueden configurar a nivel de usuario. Además, las `idSpecific` preferencias de marketing para `email`, `sms` y `push` no admiten los campos `subscriptions`.

También hay un consentimiento que solo se puede proporcionar en la sección `idSpecific`: `adID`. Este campo se trata en la subsección siguiente.

#### `adID`

El consentimiento `adID` representa el consentimiento del cliente para saber si se puede usar un ID de anunciante (IDFA o GAID) para vincular al cliente entre aplicaciones en este dispositivo. Este valor solo se puede configurar en el área de nombres de identidad `ECID` en la sección `idSpecific` y no se puede establecer para otros áreas de nombres o a nivel de usuario para esta mezcla.

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>No se espera que establezca este valor directamente, ya que el SDK de Adobe Experience Platform Mobile lo establece automáticamente cuando corresponde.

## Ingesta de datos utilizando la mezcla {#ingest}

Para utilizar la mezcla [!DNL Consents & Preferences] para introducir datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga esa mezcla.

Consulte el tutorial sobre la [creación de un esquema en la interfaz de usuario](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos sobre cómo asignar mezclas a campos. Una vez que haya creado un esquema que contenga un campo con la mezcla [!DNL Consents & Preferences] , consulte la sección sobre [la creación de un conjunto de datos](../../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siguiendo los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-time Customer Profile], es necesario crear un esquema habilitado para [!DNL Profile] basado en la clase [!DNL XDM Individual Profile] que contiene la mezcla [!DNL Consents & Preferences]. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados anteriormente para ver los pasos específicos relacionados con los requisitos [!DNL Real-time Customer Profile] para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencias más recientes, a fin de que los perfiles de clientes se actualicen correctamente. Consulte la descripción general de [merge policy](../../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencias

Cuando un cliente cambia sus consentimientos o preferencias en el sitio web, estos cambios deben recopilarse e implementarse inmediatamente mediante el [SDK web de Adobe Experience Platform](../../../edge/consent/supporting-consent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe cesar inmediatamente. Si un cliente decide excluirse de la personalización, no debería haber ninguna personalización presente en la siguiente página que visite.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información de referencia adicional sobre la mezcla [!DNL Consents & Preferences].

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

Para ver el esquema completo de la mezcla [!DNL Consents & Preferences], consulte el [repositorio XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
