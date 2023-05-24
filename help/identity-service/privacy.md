---
keywords: Experience Platform;inicio;temas populares
title: Procesamiento de solicitudes de privacidad en Identity Service
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según se define en numerosas regulaciones de privacidad. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para Identity Service.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---

# Procesamiento de solicitudes de privacidad en [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según se define en las regulaciones de privacidad como el Reglamento general de protección de datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para [!DNL Identity Service] en Adobe Experience Platform.

>[!NOTE]
>
>Esta guía solo explica cómo realizar solicitudes de privacidad para el almacén de datos de ID en Experience Platform. Si también planea realizar solicitudes de privacidad para el lago de datos de Platform o [!DNL Real-Time Customer Profile], consulte la guía de [procesamiento de solicitudes de privacidad en el lago de datos](../catalog/privacy.md) y a la guía de [procesamiento de solicitudes de privacidad para el perfil](../profile/privacy.md) además de este tutorial.
>
>Para ver los pasos sobre cómo realizar solicitudes de privacidad para otras aplicaciones de Adobe Experience Cloud, consulte la [Documentación del Privacy Service](../privacy-service/experience-cloud-apps.md).

## Primeros pasos

Se recomienda tener una comprensión práctica de lo siguiente [!DNL Experience Platform] servicios antes de leer esta guía:

* [[!DNL Privacy Service]](../privacy-service/home.md): administra las solicitudes de los clientes para acceder, desactivar la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Explicación de áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] vincula los datos de identidad del cliente entre sistemas y dispositivos. [!DNL Identity Service] utiliza **áreas de nombres de identidad** proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Un área de nombres puede representar un concepto genérico como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad mantiene un almacén de áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;correo electrónico&quot; y &quot;ECID&quot;), mientras que su organización también puede crear áreas de nombres personalizadas para adaptarlas a sus necesidades particulares.

Para obtener más información sobre áreas de nombres de identidad en [!DNL Experience Platform], consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md).

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Identity Service] uso del [!DNL Privacy Service] API o IU. Antes de leer estas secciones, se recomienda encarecidamente que revise las [API de Privacy Service](../privacy-service/api/getting-started.md) o [IU de Privacy Service](../privacy-service/ui/overview.md) documentación para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar formato adecuado a los datos de usuario en las cargas útiles de solicitud.

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier ID proporcionado en `userIDs` debe utilizar un específico de `namespace` y `type`. Un válido [área de nombres de identidad](#namespaces) reconocido por [!DNL Identity Service] debe proporcionarse para el `namespace` mientras que el valor `type` debe ser `standard` o `unregistered` (para áreas de nombres estándar y personalizadas, respectivamente).

Además, la variable `include` La matriz de la carga útil de la solicitud debe incluir los valores de producto de los diferentes almacenes de datos a los que se realiza la solicitud. Al realizar solicitudes a [!DNL Identity], la matriz debe incluir el valor `Identity`.

La siguiente solicitud crea un nuevo trabajo de privacidad con arreglo al RGPD para los datos de un solo cliente en [!DNL Identity] tienda. Se proporcionan dos valores de identidad para el cliente en `userIDs` matriz; una que usa el estándar `Email` área de nombres de identidad y otra que utiliza una `ECID` , También incluye el valor de producto para [!DNL Identity] (`Identity`) en el `include` matriz:

>[!TIP]
>
>Al eliminar un área de nombres personalizada mediante la API, debe especificar el símbolo de identidad como el área de nombres, en lugar del nombre para mostrar.

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

### Uso de la IU

>[!TIP]
>
>Al eliminar un área de nombres personalizada mediante la interfaz de usuario de, debe especificar el símbolo de identidad como el área de nombres en lugar del nombre para mostrar. Además, no puede eliminar áreas de nombres personalizadas en la interfaz de usuario para zonas protegidas que no sean de producción.

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL Identidad]** bajo **[!UICONTROL Productos]** para procesar trabajos para datos almacenados en [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Eliminar procesamiento de solicitudes

Cuándo [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía confirmación a [!DNL Privacy Service] que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. La eliminación de la identidad individual se basa en el área de nombres o el valor de ID proporcionados. Además, la eliminación se realiza para todas las zonas protegidas asociadas a una organización determinada.

Dependiendo de si también ha incluido el Perfil del cliente en tiempo real (`ProfileService`) y el lago de datos (`aepDataLake`) como productos en su solicitud de privacidad para Identity Service (`identity`), se eliminan del sistema diferentes conjuntos de datos relacionados con la identidad en momentos potencialmente diferentes:

| Productos incluidos | Efectos |
| --- | --- |
| `identity` solamente | El gráfico de identidad asociado con la identidad proporcionada se elimina inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. El perfil construido a partir de ese gráfico de identidad aún se mantiene, pero no se actualizará a medida que se incorporen nuevos datos, ya que las asociaciones de identidad ahora se eliminan. Los datos asociados con el perfil también permanecen en el lago de datos. |
| `identity` y `ProfileService` | El gráfico de identidad y su perfil asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. Los datos asociados con el perfil permanecen en el lago de datos. |
| `identity` y `aepDataLake` | El gráfico de identidad asociado con la identidad proporcionada se elimina inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. El perfil construido a partir de ese gráfico de identidad aún se mantiene, pero no se actualizará a medida que se incorporen nuevos datos, ya que las asociaciones de identidad ahora se eliminan.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, ningún usuario puede acceder a ellos [!DNL Platform] servicio. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |
| `identity`, `ProfileService`, y `aepDataLake` | El gráfico de identidad y su perfil asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, ningún usuario puede acceder a ellos [!DNL Platform] servicio. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |

Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento de estados de trabajos.

## Pasos siguientes

Al leer este documento, se le han introducido los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Identity Service]. Para obtener información sobre el procesamiento de solicitudes de privacidad para otros [!DNL Experience Cloud] aplicaciones, consulte el documento sobre [[!DNL Privacy Service] and [!DNL Experience Cloud] aplicaciones](../privacy-service/experience-cloud-apps.md).
