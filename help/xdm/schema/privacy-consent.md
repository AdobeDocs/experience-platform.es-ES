---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: Información general sobre la combinación de privacidad
description: El tipo de datos Privacidad/Preferencias de marketing (Consentimiento) está diseñado para admitir la recopilación de permisos y preferencias del cliente generados por las plataformas de gestión de consentimiento (CMP) y otras fuentes de sus operaciones de datos.
topic: guide
translation-type: tm+mt
source-git-commit: ba045a635f840c62980288a1a3ad5015f54121da
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 1%

---


# [!DNL Consents & Preferences] descripción general del tipo de datos

El tipo [!DNL Privacy/Marketing Preferences (Consent)] de datos (en lo sucesivo denominado &quot;[!DNL Consents & Preferences] tipo de datos&quot;) es un tipo de datos [!DNL Experience Data Model] (XDM) destinado a admitir la recopilación de permisos y preferencias de clientes generados por las plataformas de gestión de consentimiento (CMP) y otras fuentes de sus operaciones de datos.

El presente documento abarca la estructura y el uso previsto de los campos proporcionados por el tipo de [!DNL Consents & Preferences] datos.

>[!IMPORTANT]
>
>El tipo de datos está diseñado para abarcar una serie de casos de uso de consentimiento y gestión de preferencias. [!DNL Consents & Preferences] Como resultado, este documento describe el uso de los campos del tipo de datos en términos generales, y sólo hace sugerencias sobre cómo interpretar el uso de estos campos. Consulte con su equipo legal de privacidad para alinear la estructura del tipo de datos con la forma en que su organización interpreta y presenta estas opciones de consentimiento y preferencias a sus clientes.

## Requisitos previos  {#prerequisites}

Este documento requiere una comprensión práctica de XDM y el uso de los esquemas en [!DNL Experience Platform]. Revise la siguiente documentación antes de continuar:

* [Descripción general del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Conceptos básicos de la composición de esquemas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Estructura del tipo de datos {#structure}

El tipo de datos [!DNL Consents & Preferences] proporciona varios campos utilizados para capturar información de **consentimiento** y **preferencias** .

Un consentimiento es una opción que permite al cliente especificar cómo se pueden utilizar sus datos. La mayoría de los consentimientos tienen un aspecto jurídico, ya que algunos ordenamientos exigen la obtención de permisos antes de que los datos puedan utilizarse de una manera determinada, o exigen que el cliente tenga la opción de dejar de utilizarlos (exclusión) si no se requiere el consentimiento afirmativo.

Una preferencia es una opción que permite al cliente especificar cómo se deben gestionar los diferentes aspectos de su experiencia con una marca. Estas se incluyen en dos categorías:

* **Preferencias** de personalización: Preferencias sobre cómo la marca debe personalizar las experiencias que se envían a un cliente.
* **Preferencias** de marketing: Preferencias sobre si una marca puede comunicarse con un cliente a través de varios canales.

El siguiente JSON muestra un ejemplo del tipo de datos que puede procesar el tipo [!DNL Consents & Preferences] de datos. En las secciones siguientes se proporciona información sobre el uso específico de cada uno de estos campos.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:any": {
        "xdm:val": "y",
      },
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>El ejemplo anterior pretende ilustrar la estructura de los datos que se envían [!DNL Platform] a través del tipo de [!DNL Consents & Preferences] datos, para dar contexto al resto de este documento, que explica los principales campos proporcionados por el tipo de datos. El esquema completo de la estructura del tipo de datos puede encontrarse en el [apéndice](#full-schema) a efectos de referencia.

## xdm:consolas {#choices}

`xdm:consents` contiene varios campos que describen las preferencias y los consentimientos de un cliente. Estos campos se describen con más detalle en las subsecciones siguientes.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:any": {
      "xdm:val": "y",
    },
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collect

`xdm:collect` representa el consentimiento del cliente para que se recopilen sus datos.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:val` | La opción de consentimiento proporcionado por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y las definiciones aceptados. |

### xdm:adID

`xdm:adID` representa el consentimiento del cliente para saber si se puede utilizar un ID de anunciante (IDFA o GAID) para vincular al cliente entre aplicaciones de este dispositivo.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:val` | La opción de consentimiento proporcionado por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y las definiciones aceptados. |

### xdm:share

`xdm:share` representa el consentimiento del cliente para saber si sus datos pueden compartirse con (o venderse a) terceros.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:val` | La opción de consentimiento proporcionado por el cliente para este caso de uso. Consulte el [apéndice](#choice-values) para conocer los valores y las definiciones aceptados. |

### xdm:personalizar {#personalize}

`xdm:personalize` captura las preferencias de los clientes con respecto a las formas en que se pueden utilizar sus datos para la personalización. Los clientes pueden exclusión casos de uso de personalización específicos o exclusión la personalización por completo.

>[!IMPORTANT]
>
>`xdm:personalize` no cubre casos de uso de la mercadotecnia. Por ejemplo, si un cliente exclusión la personalización de todos los canales, no debe dejar de recibir comunicaciones a través de esos canales. Más bien, los mensajes que reciben deben ser genéricos y no estar basados en su perfil.
>
>En el mismo ejemplo, si un cliente exclusión la mercadotecnia directa para todos los canales (a través de `xdm:marketing`, según se explica en la [siguiente sección](#marketing)), ese cliente no debería recibir ningún mensaje, aunque se permita la personalización.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:content` | Representa las preferencias del cliente para el contenido personalizado en el sitio web o la aplicación. |
| `xdm:val` | La preferencia de personalización proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que dé su consentimiento, el valor de este campo debe indicar la base sobre la que debe realizarse la personalización. Consulte el [apéndice](#choice-values) para conocer los valores y las definiciones aceptados. |

### xdm:marketing {#marketing}

`xdm:marketing` captura las preferencias del cliente con respecto a los fines de mercadotecnia para los que se pueden utilizar sus datos. Los clientes pueden exclusión casos específicos de uso de mercadotecnia o exclusión completamente la mercadotecnia directa.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:preferred` | Indica el canal preferido del cliente para recibir comunicaciones. Consulte el [apéndice](#preferred-values) para los valores aceptados. |
| `xdm:any` | Representa las preferencias del cliente para la mercadotecnia directa en su conjunto. La preferencia de consentimiento proporcionada en este campo se considera la preferencia &quot;predeterminada&quot; para cualquier canal de mercadotecnia, a menos que se sobrescriba con subcampos adicionales proporcionados en `xdm:marketing`. Si planea utilizar opciones de consentimiento más granulares, se recomienda excluir este campo.<br><br>Si el valor se establece en `n`, se debe omitir toda la configuración de personalización más específica. Si el valor se establece en `y`, todas las opciones de personalización más específicas también se deben tratar como `y`, a menos que se establezcan explícitamente en `n`. Si el valor no está establecido, los valores de cada opción de personalización deben respetarse tal como se especifica. |
| `xdm:email` | Indica si el cliente acepta recibir mensajes de correo electrónico. |
| `xdm:push` | Indica si el cliente permite recibir notificaciones push. |
| `xdm:sms` | Indica si el cliente acepta recibir mensajes de texto. |
| `xdm:val` | La preferencia proporcionada por el cliente para el caso de uso especificado. En los casos en que no sea necesario pedir al cliente que dé su consentimiento, el valor de este campo debe indicar la base sobre la que debe llevarse a cabo el caso de uso de la comercialización. Consulte el [apéndice](#choice-values) para conocer los valores y las definiciones aceptados. |
| `xdm:time` | Marca de hora ISO 8601 del momento en que se cambió la preferencia de marketing, si procede. Tenga en cuenta que si la marca de tiempo de cualquier preferencia individual es la misma que la proporcionada en `xdm:metadata`, este campo no se debe definir para esa preferencia. |
| `xdm:reason` | Cuando un cliente exclusión un caso de uso de marketing, este campo de cadena representa el motivo por el que el cliente exclusión. |

### xdm:idSpecific

`xdm:idSpecific` puede utilizarse cuando un consentimiento o preferencia particular no se aplica universalmente a un cliente, pero está restringido a un solo dispositivo o ID. Por ejemplo, un cliente puede exclusión la recepción de correos electrónicos en una dirección, mientras que posiblemente permita los correos electrónicos en otra.

>[!IMPORTANT]
>
>Las preferencias y los consentimientos de nivel de canal (es decir, los proporcionados en `xdm:consents` fuera de `xdm:idSpecific`) se aplican a los ID dentro de ese canal. Por lo tanto, todos los consentimientos y preferencias de nivel de canal afectan directamente a la configuración equivalente de ID o dispositivo específico:
>
>* Si el cliente ha exclusión en el nivel de canal, se ignora cualquier consentimiento o preferencias equivalentes en `xdm:idSpecific` .
>* Si no se establece la preferencia o el consentimiento a nivel de canal o si el cliente ha adhesión, se respetan las preferencias o consentimientos equivalentes en `xdm:idSpecific` .


Cada clave del `xdm:idSpecific` objeto representa una Área de nombres de identidad específica reconocida por Adobe Experience Platform Identity Service. Aunque puede definir sus propias Áreas de nombres personalizadas para categorizar distintos identificadores, se recomienda utilizar una de las Áreas de nombres estándar proporcionadas por Identity Service para reducir los tamaños de almacenamiento para el Perfil de clientes en tiempo real. Para obtener más información sobre las Áreas de nombres de identidad, consulte la información general [sobre la Área de nombres de](../../identity-service/namespaces.md) identidad en la documentación del servicio de identidad.

Las claves de cada objeto de Área de nombres representan los valores de identidad únicos para los que el cliente ha establecido preferencias. Cada valor de identidad puede contener un conjunto completo de consentimientos y preferencias, con el mismo formato que `xdm:consents`.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metadatos

`xdm:metadata` captura metadatos generales sobre las preferencias y los consentimientos del cliente cada vez que se actualizaron por última vez.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:time` | Marca de hora de la última vez que se actualizó cualquiera de las preferencias y consentimientos del cliente. Este campo se puede utilizar en lugar de aplicar marcas de hora a preferencias individuales para reducir la carga y la complejidad. Si se proporciona un `xdm:time` valor en una preferencia individual, se anula la `xdm:metadata` marca de tiempo de esa preferencia concreta. |

## Ingesta de datos mediante el tipo de datos {#ingest}

Para utilizar el tipo de datos [!DNL Consents & Preferences] a fin de ingestar datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga ese tipo de datos.

Consulte el tutorial sobre la [creación de un esquema en la interfaz de usuario](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos para asignar tipos de datos a los campos. Una vez creado un esquema que contiene un campo con el tipo de datos, consulte la sección sobre la [!DNL Consents & Preferences] creación de un conjunto de datos [](../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siguiendo los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-time Customer Profile], es necesario crear un esquema [!DNL Profile]habilitado en función de la [!DNL XDM Individual Profile] clase que contiene el tipo de [!DNL Consents & Preferences] datos. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales relacionados anteriormente para ver los pasos específicos relacionados con [!DNL Real-time Customer Profile] los requisitos para esquemas y conjuntos de datos.
>
>Además, debe asegurarse de que las políticas de combinación están configuradas para priorizar los conjuntos de datos que contienen los datos de preferencias y consentimiento más recientes, a fin de que los perfiles de los clientes se actualicen correctamente. Consulte la información general sobre las políticas [de](../../rtcdp/profile/merge-policies.md) combinación para obtener más información.

## Gestión del consentimiento y los cambios de preferencias

Cuando un cliente cambia sus consentimientos o preferencias en el sitio web, estos cambios deben recopilarse y aplicarse inmediatamente mediante el SDK [web de](../../edge/consent/supporting-consent.md)Adobe Experience Platform. Si un cliente exclusión la recopilación de datos, toda la recopilación de datos debe cesar inmediatamente. Si un cliente exclusión la personalización, no debería haber ninguna personalización presente en la página siguiente que visite.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información de referencia adicional sobre el tipo de [!DNL Consents & Preferences] datos.

### Valores aceptados para xdm:val {#choice-values}

La siguiente tabla describe los valores aceptados para `xdm:val`:

| Valor | Título | Descripción |
| --- | --- | --- |
| `y` | Sí | El cliente ha adhesión el consentimiento o la preferencia. En otras palabras, **consienten** en utilizar sus datos como se indica en el consentimiento o preferencia de que se trate. |
| `n` | No | El cliente ha exclusión el consentimiento o la preferencia. En otras palabras, **no consienten** en utilizar sus datos como se indica en el consentimiento o preferencia de que se trate. |
| `p` | Verificación pendiente | El sistema aún no ha recibido un consentimiento definitivo o un valor de preferencia. Esto se utiliza generalmente como parte de un consentimiento que requiere una verificación de dos pasos. Por ejemplo, si un cliente opta por recibir correos electrónicos, ese consentimiento se establece en `p` hasta que seleccione un vínculo en un mensaje de correo electrónico para verificar que ha proporcionado la dirección de correo electrónico correcta, momento en el cual se actualizará el consentimiento a `y`.<br><br>Si este consentimiento o preferencia no utiliza un proceso de verificación de dos conjuntos, la `p` opción puede utilizarse para indicar que el cliente no ha respondido aún al pedido de consentimiento. Por ejemplo, puede establecer automáticamente el valor en `p` la primera página de un sitio web, antes de que el cliente haya respondido al mensaje de consentimiento. En las jurisdicciones que no requieren consentimiento explícito, también puede utilizarla para indicar que el cliente no ha exclusión explícitamente (en otras palabras, se asume el consentimiento). |
| `u` | Unknown | Se desconoce el consentimiento o la información de preferencias del cliente. |
| `LI` | Interés legítimo | El interés legítimo de las empresas en recopilar y procesar estos datos con el fin especificado es mayor que el daño potencial que supone para la persona. |
| `CT` | Contrato | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones contractuales con la persona. |
| `CP` | Cumplimiento de una obligación legal | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones jurídicas de la empresa. |
| `VI` | Interés vital del individuo | La recopilación de datos con el fin especificado es necesaria para proteger los intereses vitales de la persona. |
| `PI` | Interés público | La recopilación de datos con el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |

### Valores aceptados para xdm:preferidos {#preferred-values}

La siguiente tabla describe los valores aceptados para `xdm:preferred`:

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
| `iot` | Mensajes de Internet de cosas (IoT). |
| `social` | Contenido de los medios sociales. |
| `other` | Un canal que no encaja en una categoría estándar. |
| `none` | Ningún canal preferido. |
| `unknown` | Se desconoce el canal preferido. |

### Esquema [!DNL Consents & Preferences] completo {#full-schema}

Para vista del esquema completo del tipo de [!DNL Consents & Preferences] datos, consulte el repositorio [](https://github.com/adobe/xdm/blob/master/components/datatypes/consentpreferences.schema.json)oficial XDM.