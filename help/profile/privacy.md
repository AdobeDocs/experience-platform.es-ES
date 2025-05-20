---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en el perfil del cliente en tiempo real
type: Documentation
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según se define en numerosas regulaciones de privacidad. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para el Perfil del cliente en tiempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6eaa384feb1b84e6081f03cb4de9687ad26f437d
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 1%

---

# Procesamiento de solicitud de privacidad en [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes para acceder a sus datos personales, excluirse de la venta o eliminarlos según lo establecido por las normas de privacidad como el Reglamento general de protección de datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para [!DNL Real-Time Customer Profile] en Adobe Experience Platform.

>[!NOTE]
>
>Esta guía solo explica cómo realizar solicitudes de privacidad para el almacén de datos de perfil en Experience Platform. Si también planea realizar solicitudes de privacidad para el lago de datos de Experience Platform, consulte la guía sobre [procesamiento de solicitudes de privacidad en el lago de datos](../catalog/privacy.md) además de este tutorial.
>
>Para ver los pasos de cómo realizar solicitudes de privacidad para otras aplicaciones de Adobe Experience Cloud, consulte la [documentación de Privacy Service](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>La solicitud de privacidad de esta guía **no** abarca entidades B2B que no sean personas.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes [!DNL Experience Platform] componentes:

* [[!DNL Privacy Service]](../privacy-service/home.md): administra las solicitudes de los clientes para acceder a sus datos personales, excluirse de la venta o eliminarlos en todas las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Explicación de los espacios de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] vincula los datos de identidad de los clientes entre sistemas y dispositivos. [!DNL Identity Service] utiliza **áreas de nombres de identidad** para proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Un área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un ID de Adobe Advertising Cloud (&quot;AdCloud&quot;) o un ID de Adobe Target (&quot;TNTID&quot;).

El servicio de identidad mantiene un almacén de áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;correo electrónico&quot; y &quot;ECID&quot;), mientras que su organización también puede crear áreas de nombres personalizadas para adaptarlas a sus necesidades particulares.

Para obtener más información sobre áreas de nombres de identidad en [!DNL Experience Platform], vea la [descripción general del área de nombres de identidad](../identity-service/features/namespaces.md).

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Real-Time Customer Profile] mediante la API o la interfaz de usuario de [!DNL Privacy Service]. Antes de leer estas secciones, debes revisar o tener en cuenta la [API de Privacy Service](../privacy-service/api/getting-started.md) o la [IU de Privacy Service](../privacy-service/ui/overview.md). Estos documentos proporcionan pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar formato adecuado a los datos de identidad de usuario enviados en las cargas útiles de solicitud.

>[!IMPORTANT]
>
>Privacy Service solo puede procesar datos de [!DNL Profile] mediante una directiva de combinación que no realice la vinculación de identidad. Consulte la sección sobre [limitaciones de la política de combinación](#merge-policy-limitations) para obtener más información.
>
>Tenga en cuenta que las solicitudes de privacidad se procesan de forma asíncrona dentro de los requisitos regulatorios y que la cantidad de tiempo que tardan en completarse puede variar. Si se producen cambios en los datos de [!DNL Profile] mientras se sigue procesando una solicitud, no se garantiza que esos registros entrantes también se procesen en esa solicitud. Solo se garantiza la eliminación de los perfiles que se mantienen en el lago de datos o en el almacén de perfiles en el momento en que se solicita el trabajo de privacidad. Si ingiere datos de perfil relacionados con el asunto de una solicitud de eliminación durante el trabajo de eliminación, no se garantiza que se eliminen todos los fragmentos de perfil.
>Es responsabilidad del cliente tener en cuenta los datos entrantes en Experience Platform o el servicio de perfil en el momento de una solicitud de eliminación, ya que esos datos se insertarán en los almacenes de registros. Debe ser prudente con la ingesta de datos que se han eliminado o que se están eliminando.

### Uso de la API

Al crear solicitudes de trabajo en la API, los identificadores proporcionados en `userIDs` deben usar un `namespace` y un `type` específicos. Se debe proporcionar un [área de nombres de identidad](#namespaces) válida reconocida por [!DNL Identity Service] para el valor `namespace`, mientras que `type` debe ser `standard` o `unregistered` (para áreas de nombres estándar y personalizadas, respectivamente).

>[!NOTE]
>
>Es posible que tenga que proporcionar más de un ID para cada cliente, en función del gráfico de identidades y de cómo se distribuyen los fragmentos de perfil en los conjuntos de datos de Experience Platform. Consulte la siguiente sección [fragmentos de perfil](#fragments) para obtener más información.

Además, la matriz `include` de la carga útil de la solicitud debe incluir los valores de producto de los diferentes almacenes de datos a los que se realiza la solicitud. Para eliminar los datos de perfil asociados a una identidad, la matriz debe incluir el valor `ProfileService`. Para eliminar las asociaciones de gráficos de identidad del cliente, la matriz debe incluir el valor `identity`.

>[!NOTE]
>
>Consulte la sección sobre [solicitudes de perfil y solicitudes de identidad](#profile-v-identity) más adelante en este documento para obtener información más detallada sobre los efectos de usar `ProfileService` y `identity` en la matriz `include`.

La siguiente solicitud crea un nuevo trabajo de privacidad para los datos de un único cliente en el almacén [!DNL Profile]. Se proporcionan dos valores de identidad para el cliente en la matriz `userIDs`; uno con el área de nombres de identidad `Email` estándar y el otro con un área de nombres `Customer_ID` personalizada. También incluye el valor de producto de [!DNL Profile] (`ProfileService`) en la matriz `include`:

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Experience Platform procesa las solicitudes de privacidad en todas las [zonas protegidas](../sandboxes/home.md) que pertenecen a su organización. Como resultado, el sistema ignora cualquier encabezado `x-sandbox-name` incluido en la solicitud.

**Respuesta del producto**

En el caso del servicio de perfil, una vez completado el trabajo de privacidad, se devuelve una respuesta en formato JSON con información sobre los ID de usuario solicitados.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### Uso de la IU

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL AEP Data Lake]** y/o **[!UICONTROL Perfil]** en **[!UICONTROL Productos]** para procesar los trabajos de los datos almacenados en el lago de datos o [!DNL Real-Time Customer Profile], respectivamente.

![Se está creando una solicitud de trabajo de acceso en la interfaz de usuario, con la opción Perfil seleccionada en Productos](./images/privacy/product-value.png)

## Fragmentos de perfil en solicitudes de privacidad {#fragments}

En el almacén de datos de [!DNL Profile], los datos personales de un cliente individual a menudo se compondrán de varios fragmentos de perfil, que se asocian con la persona a través del gráfico de identidad. Al realizar solicitudes de privacidad en el almacén de [!DNL Profile], es importante tener en cuenta que las solicitudes solo se procesan en el nivel de fragmento de perfil, en lugar de en todo el perfil.

Por ejemplo, piense en una situación en la que almacene datos de atributos del cliente en tres conjuntos de datos independientes, que utilizan identificadores diferentes para asociar esos datos a clientes individuales:

| Nombre del conjunto de datos | Campo de identidad principal | Atributos almacenados |
| --- | --- | --- |
| Conjunto de datos 1 | `customer_id` | `address` |
| Conjunto de datos 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de datos 3 | `email_id` | `mlScore` |

Uno de los conjuntos de datos usa `customer_id` como identificador principal, mientras que los otros dos usan `email_id`. Si enviara una solicitud de privacidad (acceso o eliminación) utilizando solamente `email_id` como valor de id. de usuario, solo se procesarían los atributos `firstName`, `lastName` y `mlScore`, mientras que `address` no se vería afectado.

Para garantizar que las solicitudes de privacidad procesen todos los atributos de cliente relevantes, debe proporcionar los valores de identidad principales para todos los conjuntos de datos aplicables en los que se puedan almacenar dichos atributos (hasta un máximo de nueve ID por cliente). Consulte la sección sobre campos de identidad en los [conceptos básicos de la composición de esquemas](../xdm/schema/composition.md#identity) para obtener más información sobre los campos que comúnmente se marcan como identidades.

## Eliminar procesamiento de solicitudes {#delete}

Cuando [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Experience Platform] envía una confirmación a [!DNL Privacy Service] de que la solicitud se ha recibido y de que los datos afectados se han marcado para su eliminación. Los registros se eliminan una vez completado el trabajo de privacidad.

>[!IMPORTANT]
>
>Las solicitudes de eliminación de privacidad no son instantáneas y pueden variar según los servicios involucrados y otros factores de impacto, como la ubicación geográfica. El plazo para la finalización de los trabajos de privacidad puede oscilar entre 15 y 45 días, pero no está garantizado.

Dependiendo de si también incluyó el servicio de identidad (`identity`) y el lago de datos (`aepDataLake`) como productos en su solicitud de privacidad para el perfil (`ProfileService`), se quitarán del sistema diferentes conjuntos de datos relacionados con el perfil en momentos potencialmente diferentes:

| Productos incluidos | Efectos |
| --- | --- |
| Solo `ProfileService` | El perfil se considera eliminado inmediatamente cuando Privacy Service envía la confirmación de que la solicitud de eliminación se ha completado. Sin embargo, el gráfico de identidad del perfil sigue existiendo y el perfil puede reconstruirse potencialmente a medida que se incorporan nuevos datos con las mismas identidades. Los datos no identificables personalmente asociados con el perfil también permanecen en el lago de datos. |
| `ProfileService` y `identity` | El perfil y su gráfico de identidad asociado se eliminan inmediatamente en cuanto Privacy Service envía la confirmación de que la solicitud de eliminación se ha completado. Los datos no identificables personalmente asociados con el perfil también permanecen en el lago de datos. |
| `ProfileService` y `aepDataLake` | El perfil se elimina inmediatamente en cuanto Privacy Service envía la confirmación de que la solicitud de eliminación se ha completado. Sin embargo, el gráfico de identidad del perfil sigue existiendo y el perfil puede reconstruirse potencialmente a medida que se incorporan nuevos datos con las mismas identidades.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan en blanco y, por lo tanto, ningún servicio de [!DNL Experience Platform] puede obtener acceso a ellos. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |
| `ProfileService`, `identity` y `aepDataLake` | El perfil y su gráfico de identidad asociado se eliminan inmediatamente en cuanto Privacy Service envía la confirmación de que la solicitud de eliminación se ha completado.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan en blanco y, por lo tanto, ningún servicio de [!DNL Experience Platform] puede obtener acceso a ellos. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |

Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento de estados de trabajos.

### Solicitudes de perfil frente a solicitudes de identidad {#profile-v-identity}

Si se realiza una solicitud de eliminación para el perfil (`ProfileService`) pero no para el servicio de identidad (`identity`), el trabajo resultante quita los datos de atributo recopilados para un cliente (o conjunto de clientes) pero no quita las asociaciones establecidas en el gráfico de identidad.

Por ejemplo, una solicitud de eliminación que usa `email_id` y `customer_id` de un cliente quita todos los datos de atributo almacenados en esos identificadores. Sin embargo, cualquier dato que se incorpore posteriormente bajo el mismo(a) `customer_id` se seguirá asociando con el(la) `email_id` apropiado(a), ya que la asociación aún existe.

Para eliminar el perfil y todas las asociaciones de identidad de un cliente determinado, asegúrese de incluir tanto el perfil como el servicio de identidad como productos de destino en las solicitudes de eliminación.

### Limitaciones de políticas de combinación {#merge-policy-limitations}

Privacy Service solo puede procesar datos de [!DNL Profile] mediante una directiva de combinación que no realice la vinculación de identidad. Si utiliza la interfaz de usuario para confirmar si se están procesando sus solicitudes de privacidad, asegúrese de utilizar una directiva con **[!DNL None]** como tipo de [!UICONTROL vinculación de ID]. En otras palabras, no puede usar una política de combinación en la que [!UICONTROL vinculación de ID] esté establecida en [!UICONTROL gráfico privado].

>![La vinculación de ID de la política de combinación se ha establecido en Ninguno](./images/privacy/no-id-stitch.png)

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Experience Platform]. Para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad, siga leyendo la documentación proporcionada en esta guía.

Para obtener información sobre el procesamiento de solicitudes de privacidad para recursos de [!DNL Experience Platform] que no usa [!DNL Profile], consulte el documento sobre el procesamiento de [solicitudes de privacidad en el lago de datos](../catalog/privacy.md).
