---
solution: Experience Platform
title: Grupo de campos de esquema de consentimientos y preferencias
description: Obtenga información acerca del grupo de campos Esquema de consentimientos y preferencias.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL Consentimientos y preferencias] grupo de campos

[!UICONTROL Consentimientos y preferencias] es un grupo de campos estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que captura la información de consentimiento y preferencia de un cliente individual.

>[!NOTE]
>
>Dado que este grupo de campos solo es compatible con [!DNL XDM Individual Profile], no se puede utilizar para [!DNL XDM ExperienceEvent] esquemas. Si desea incluir datos de consentimiento y preferencia en el esquema de Experience Event, agregue la variable [[!UICONTROL Consentimiento para preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md) al esquema mediante el uso de una variable [grupo de campos personalizados](../../ui/resources/field-groups.md#create) en su lugar.

## Estructura del grupo de campos {#structure}

El [!UICONTROL Consentimientos y preferencias] grupo de campos proporciona un único campo de tipo de objeto, `consents`, para recopilar información sobre el consentimiento y las preferencias. Este campo amplía el [[!UICONTROL Consentimiento para preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md), eliminando el `adID` y añadir un `idSpecific` campo de asignación.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulte la guía de [exploración de recursos XDM](../../ui/explore.md) Consulte para ver los pasos sobre cómo buscar cualquier recurso XDM e inspeccionar su estructura en la interfaz de usuario de Platform.

El siguiente JSON muestra un ejemplo del tipo de datos que el [!UICONTROL Consentimientos y preferencias] el grupo de campos puede procesar. Para obtener información sobre cómo utilizar la mayoría de los campos proporcionados por el grupo de campos, consulte la guía del [Tipo de datos Consentimientos y preferencias](../../data-types/consents.md). Las subsecciones siguientes se centran en los atributos únicos que el grupo de campos añade al tipo de datos.

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
>Puede generar datos JSON de muestra para cualquier esquema XDM que defina en Experience Platform para visualizar cómo se deben asignar los datos de preferencia y consentimiento del cliente. Consulte la siguiente documentación para obtener más información:
>
>* [Generación de datos de ejemplo en la IU](../../ui/sample.md)
>* [Generar datos de ejemplo en la API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` se puede usar cuando un consentimiento o preferencia en particular no se aplica universalmente a un cliente, pero está restringido a un solo dispositivo o ID. Por ejemplo, un cliente puede excluirse de la recepción de correos electrónicos en una dirección y permitir potencialmente que se envíen correos electrónicos en otra.

>[!IMPORTANT]
>
>Consentimientos y preferencias a nivel de canal (es decir, los proporcionados en `consents` fuera de `idSpecific`) se aplican a todos los ID dentro de ese canal. Por lo tanto, todos los consentimientos y preferencias de nivel de canal afectan directamente si se respetan configuraciones equivalentes específicas del ID o del dispositivo:
>
>* Si el cliente se ha excluido en el nivel de canal, cualquier consentimiento o preferencia equivalente en `idSpecific` se ignoran.
>* Si no se establece el consentimiento o la preferencia de nivel de canal, o si el cliente ha elegido, el consentimiento o las preferencias equivalentes en `idSpecific` son honrados.

Cada clave de la `idSpecific` representa un área de nombres de identidad específica reconocida por Adobe Experience Platform Identity Service. Aunque puede definir sus propias áreas de nombres personalizadas para categorizar distintos identificadores, se recomienda utilizar una de las áreas de nombres estándar proporcionadas por el servicio de identidad para reducir los tamaños de almacenamiento de Perfil del cliente en tiempo real. Para obtener más información sobre Áreas de nombres de identidad, consulte [información general del área de nombres de identidad](../../../identity-service/features/namespaces.md) en la documentación del servicio de ID.

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

En `marketing` objetos proporcionados en el `idSpecific` , la sección `any` y `preferred` Los campos de no son compatibles. Estos campos solo se pueden configurar en el nivel de usuario. Además, la variable `idSpecific` preferencias de marketing para `email`, `sms`, y `push` no admiten `subscriptions` campos.

También existe un consentimiento que solo se puede proporcionar en la `idSpecific` sección: `adID`. Este campo se trata en la subsección siguiente.

#### `adID`

El `adID` El consentimiento representa el consentimiento del cliente para saber si se puede utilizar un ID del anunciante (IDFA o GAID) para vincular al cliente entre aplicaciones en este dispositivo. Este valor solo se puede configurar en la variable `ECID` área de nombres de identidad en `idSpecific` y no se pueden establecer para otras áreas de nombres ni en el nivel de usuario para este grupo de campos.

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

Para utilizar la variable [!UICONTROL Consentimientos y preferencias] grupo de campos para introducir datos de consentimiento de sus clientes, debe crear un conjunto de datos basado en un esquema que contenga ese grupo de campos.

Consulte el tutorial sobre [creación de un esquema en la IU](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos sobre cómo asignar grupos de campos a campos. Una vez creado un esquema que contiene un campo con la variable [!UICONTROL Consentimientos y preferencias] grupo de campos, consulte la sección sobre [creación de un conjunto de datos](../../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siga los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-Time Customer Profile], es necesario que cree un [!DNL Profile]Esquema habilitado para basado en [!DNL XDM Individual Profile] que contiene la clase [!UICONTROL Consentimientos y preferencias] grupo de campos. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales vinculados anteriormente para ver los pasos específicos relacionados con lo siguiente [!DNL Real-Time Customer Profile] requisitos para esquemas y conjuntos de datos.
>
>Además, también debe asegurarse de que las políticas de combinación estén configuradas para priorizar los conjuntos de datos que contienen los datos de consentimiento y preferencia más recientes, a fin de que los perfiles de los clientes se actualicen correctamente. Consulte la información general sobre [políticas de combinación](../../../rtcdp/profile/merge-policies.md) para obtener más información.

## Gestión de cambios de consentimiento y preferencia

Cuando un cliente cambia su consentimiento o preferencias en su sitio web, estos cambios deben recopilarse y aplicarse inmediatamente utilizando [SDK web de Adobe Experience Platform](/help/web-sdk/consent/supporting-consent.md). Si un cliente se excluye de la recopilación de datos, toda la recopilación de datos debe interrumpirse inmediatamente. Si un cliente se excluye de la personalización, no debe haber ninguna personalización presente en la siguiente página que visite.

## Pasos siguientes

Este documento abarcaba la estructura y el uso del [!UICONTROL Consentimientos y preferencias] grupo de campos. Para obtener más información sobre los demás campos proporcionados por el grupo de campos, consulte el documento sobre [[!UICONTROL Consentimiento para preferencias de privacidad, personalización y marketing] tipo de datos](../../data-types/consents.md).
