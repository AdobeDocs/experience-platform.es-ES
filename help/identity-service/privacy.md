---
keywords: Experience Platform;inicio;temas populares
title: Procesamiento de solicitudes de privacidad en el servicio de identidad
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes de acceso, exclusión de la venta o eliminación de sus datos personales, según lo establecido en numerosas normas de privacidad. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para el servicio de identidad.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---

# Procesamiento de solicitudes de privacidad en [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes de acceso, exclusión de la venta o eliminación de sus datos personales, tal como se definen en las normas de privacidad, como el Reglamento General de Protección de Datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para [!DNL Identity Service] en Adobe Experience Platform.

>[!NOTE]
>
>Esta guía solo explica cómo realizar solicitudes de privacidad para el almacén de datos de identidad en Experience Platform. Si también planea realizar solicitudes de privacidad para el lago de datos de Platform o [!DNL Real-Time Customer Profile], consulte la guía de [procesamiento de solicitudes de privacidad en el lago de datos](../catalog/privacy.md) y a la guía de [procesamiento de solicitudes de privacidad para Perfil](../profile/privacy.md) además de este tutorial.
>
>Para ver los pasos sobre cómo realizar solicitudes de privacidad para otras aplicaciones de Adobe Experience Cloud, consulte la [documentación del Privacy Service](../privacy-service/experience-cloud-apps.md).

## Primeros pasos

Se recomienda que tenga una comprensión práctica de lo siguiente [!DNL Experience Platform] antes de leer esta guía:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestiona las solicitudes de los clientes para acceder, desactivar o eliminar sus datos personales en todas las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Explicación de las áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] vincula los datos de identidad de los clientes entre sistemas y dispositivos. [!DNL Identity Service] uses **áreas de nombres de identidad** proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Un área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad mantiene un almacén de áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear áreas de nombres personalizadas para adaptarlas a sus necesidades específicas.

Para obtener más información sobre áreas de nombres de identidad en [!DNL Experience Platform], consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md).

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Identity Service] usando la variable [!DNL Privacy Service] API o IU. Antes de leer estas secciones, se recomienda revisar la [API de Privacy Service](../privacy-service/api/getting-started.md) o [IU de Privacy Service](../privacy-service/ui/overview.md) documentación para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar formato correcto a los datos de usuario en las cargas de solicitud.

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier ID proporcionado dentro de `userIDs` debe utilizar un `namespace` y `type`. Un [área de nombres de identidad](#namespaces) reconocido por [!DNL Identity Service] debe estar previsto para `namespace` mientras que la variable `type` debe ser `standard` o `unregistered` (para espacios de nombres estándar y personalizados, respectivamente).

Además, la variable `include` matriz de la carga útil de solicitud debe incluir los valores de producto para los diferentes almacenes de datos a los que se realiza la solicitud. Al realizar solicitudes para [!DNL Identity], la matriz debe incluir el valor `Identity`.

La siguiente solicitud crea un nuevo trabajo de privacidad en el RGPD para los datos de un único cliente en la variable [!DNL Identity] tienda. Se proporcionan dos valores de identidad para el cliente en la variable `userIDs` matriz; una que utilice el estándar `Email` área de nombres de identidad y la otra utilizando un `ECID` namespace, también incluye el valor de producto para [!DNL Identity] (`Identity`) en el `include` matriz:

>[!TIP]
>
>Al eliminar un espacio de nombres personalizado mediante la API, debe especificar el símbolo de identidad como el espacio de nombres, en lugar del nombre para mostrar.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Uso de la interfaz de usuario

>[!TIP]
>
>Al eliminar un área de nombres personalizada mediante la interfaz de usuario, debe especificar el símbolo de identidad como área de nombres, en lugar del nombre para mostrar. Además, no puede eliminar espacios de nombres personalizados en la interfaz de usuario para entornos limitados que no sean de producción.

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL Identidad]** under **[!UICONTROL Productos]** para procesar los trabajos de los datos almacenados en [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Eliminación del procesamiento de solicitudes

When [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía confirmación a [!DNL Privacy Service] que la solicitud se ha recibido y los datos afectados se han marcado para su eliminación. La eliminación de la identidad individual se basa en el espacio de nombres o el valor de ID proporcionados. Además, la eliminación tiene lugar para todos los entornos limitados asociados a una organización de IMS determinada.

Dependiendo de si también ha incluido Perfil del cliente en tiempo real (`ProfileService`) y el lago de datos (`aepDataLake`) como productos en su solicitud de privacidad para el servicio de identidad (`identity`), diferentes conjuntos de datos relacionados con la identidad se eliminan del sistema en momentos potencialmente diferentes:

| Productos incluidos | Efectos |
| --- | --- |
| `identity` only | El gráfico de identidad asociado con la identidad proporcionada se elimina inmediatamente en cuanto Platform envía la confirmación de que se recibió la solicitud de eliminación. El perfil construido a partir de ese gráfico de identidad sigue conservándose, pero no se actualizará cuando se introduzcan nuevos datos, ya que las asociaciones de identidad se han eliminado. Los datos asociados con el perfil también permanecen en el lago de datos. |
| `identity` y `ProfileService` | El gráfico de identidad y su perfil asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se recibió la solicitud de eliminación. Los datos asociados con el perfil permanecen en el lago de datos. |
| `identity` y `aepDataLake` | El gráfico de identidad asociado con la identidad proporcionada se elimina inmediatamente en cuanto Platform envía la confirmación de que se recibió la solicitud de eliminación. El perfil construido a partir de ese gráfico de identidad sigue conservándose, pero no se actualizará cuando se introduzcan nuevos datos, ya que las asociaciones de identidad se han eliminado.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, no es accesible para ninguno [!DNL Platform] servicio. Una vez completado el trabajo, los datos se eliminan completamente del lago de datos. |
| `identity`, `ProfileService`, y `aepDataLake` | El gráfico de identidad y su perfil asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se recibió la solicitud de eliminación.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, no es accesible para ninguno [!DNL Platform] servicio. Una vez completado el trabajo, los datos se eliminan completamente del lago de datos. |

Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento del estado de los trabajos.

## Pasos siguientes

Al leer este documento, se le han introducido los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Identity Service]. Para obtener información sobre el procesamiento de solicitudes de privacidad de otros [!DNL Experience Cloud] aplicaciones, consulte el documento en [[!DNL Privacy Service] and [!DNL Experience Cloud] aplicaciones](../privacy-service/experience-cloud-apps.md).
