---
solution: Experience Platform
title: Grupo de campos de esquema consentimientos y preferencias
description: Este documento proporciona una descripción general del grupo de campos de esquema Consentimientos y Preferencias .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL Consentimientos y preferencias] grupo de campos

[!UICONTROL Consentimientos y preferencias] es un grupo de campos estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que captura la información de consentimiento y preferencias de un cliente individual.

>[!NOTE]
>
>Dado que este grupo de campos solo es compatible con [!DNL XDM Individual Profile], no se puede usar para [!DNL XDM ExperienceEvent] esquemas. Si desea incluir datos de consentimiento y preferencias en el esquema de eventos de experiencia, agregue la variable [[!UICONTROL Consentimiento para las preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md) al esquema mediante el uso de un [grupo de campos personalizados](../../ui/resources/field-groups.md#create) en su lugar.

## Estructura del grupo de campo {#structure}

La variable [!UICONTROL Consentimientos y preferencias] grupo de campos proporciona un único campo de tipo objeto, `consents`, para capturar información de consentimiento y preferencias. Este campo amplía la variable [[!UICONTROL Consentimiento para las preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md), eliminando `adID` y adición de `idSpecific` campo map .

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulte la guía de [exploración de recursos XDM](../../ui/explore.md) a para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que el [!UICONTROL Consentimientos y preferencias] grupo de campos puede procesarse. Para obtener información sobre cómo utilizar la mayoría de los campos proporcionados por el grupo de campos, consulte la guía de [Tipo de datos consentimientos y preferencias](../../data-types/consents.md). Las subsecciones siguientes se centran en los atributos únicos que el grupo de campos agrega al tipo de datos.

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


### `idSpecific`

`idSpecific` se puede utilizar cuando un consentimiento o preferencia en particular no se aplica universalmente a un cliente, pero está restringido a un único dispositivo o ID. Por ejemplo, un cliente puede desactivar la recepción de correos electrónicos a una dirección, mientras que posiblemente permita el envío de correos electrónicos a otra.

>[!IMPORTANT]
>
>Consentimientos y preferencias de nivel de canal (es decir, los proporcionados en `consents` fuera de `idSpecific`) se aplican a todos los ID de ese canal. Por lo tanto, todos los consentimientos y preferencias de nivel de canal afectan directamente a si se respetan configuraciones equivalentes específicas del dispositivo o ID:
>
>* Si el cliente se ha excluido en el nivel de canal, cualquier consentimiento o preferencias equivalente en `idSpecific` se ignoran.
>* Si no se establece el consentimiento o la preferencia de nivel de canal o si el cliente ha elegido, entonces el equivalente consiente o preferencias en `idSpecific` son respetados.


Cada clave de la variable `idSpecific` representa un área de nombres de identidad específica reconocida por el servicio de identidad de Adobe Experience Platform. Aunque puede definir sus propios espacios de nombres personalizados para categorizar distintos identificadores, se recomienda utilizar uno de los espacios de nombres estándar proporcionados por Identity Service para reducir los tamaños de almacenamiento para el perfil del cliente en tiempo real. Para obtener más información sobre las áreas de nombres de identidad, consulte la [información general del área de nombres de identidad](../../../identity-service/namespaces.md) en la documentación del servicio de identidad.

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
  "ECID": {
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

Within `marketing` los objetos proporcionados en el `idSpecific` , la variable `any` y `preferred` no son compatibles. Estos campos solo se pueden configurar a nivel de usuario. Además, la variable `idSpecific` preferencias de marketing para `email`, `sms`y `push` no es compatible `subscriptions` campos.

También hay un consentimiento que solo puede proporcionarse en la variable `idSpecific` sección: `adID`. Este campo se trata en la subsección siguiente.

#### `adID`

La variable `adID` consentimiento representa el consentimiento del cliente para saber si se puede usar un ID de anunciante (IDFA o GAID) para vincular al cliente entre aplicaciones en este dispositivo. Este valor solo se puede configurar en la sección `ECID` área de nombres de identidad en la `idSpecific` y no se pueden configurar para otras áreas de nombres o a nivel de usuario para este grupo de campos.

```json
"idSpecific": {
  "ECID": {
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

## Ingesta de datos mediante el grupo de campos {#ingest}

Para usar la variable [!UICONTROL Consentimientos y preferencias] grupo de campos para introducir datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga ese grupo de campos.

Consulte el tutorial en [creación de un esquema en la interfaz de usuario](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos sobre cómo asignar grupos de campos a campos. Una vez que haya creado un esquema que contenga un campo con la variable [!UICONTROL Consentimientos y preferencias] grupo de campos, consulte la sección de [creación de un conjunto de datos](../../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siga los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-Time Customer Profile], es necesario que cree un [!DNL Profile]esquema habilitado según el [!DNL XDM Individual Profile] clase que contiene el [!UICONTROL Consentimientos y preferencias] grupo de campos. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados anteriormente para ver los pasos específicos relacionados con [!DNL Real-Time Customer Profile] requisitos para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencias más recientes, a fin de que los perfiles de clientes se actualicen correctamente. Consulte la descripción general sobre [combinar directivas](../../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencias

Cuando un cliente cambia sus consentimientos o preferencias en el sitio web, estos cambios deben recopilarse e implementarse inmediatamente mediante el [SDK web de Adobe Experience Platform](../../../edge/consent/supporting-consent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe cesar inmediatamente. Si un cliente decide excluirse de la personalización, no debería haber ninguna personalización presente en la siguiente página que visite.

## Pasos siguientes

Este documento abarcaba la estructura y el uso del [!UICONTROL Consentimientos y preferencias] grupo de campos. Para obtener más información sobre los demás campos proporcionados por el grupo de campos, consulte el documento en la [[!UICONTROL Consentimiento para las preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md).
