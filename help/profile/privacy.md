---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en el perfil del cliente en tiempo real
type: Documentation
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según se define en numerosas regulaciones de privacidad. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para el Perfil del cliente en tiempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: d41606e4df297d11b4e0e755363d362e075e862c
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Procesamiento de solicitudes de privacidad en [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según se define en las regulaciones de privacidad como el Reglamento general de protección de datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para [!DNL Real-Time Customer Profile] en Adobe Experience Platform.

>[!NOTE]
>
>Esta guía solo explica cómo realizar solicitudes de privacidad para el almacén de datos de perfil en Experience Platform. Si también planea realizar solicitudes de privacidad para el lago de datos de Platform, consulte la guía de [procesamiento de solicitudes de privacidad en el lago de datos](../catalog/privacy.md) además de este tutorial.
>
>Para ver los pasos sobre cómo realizar solicitudes de privacidad para otras aplicaciones de Adobe Experience Cloud, consulte la [Documentación del Privacy Service](../privacy-service/experience-cloud-apps.md).

## Primeros pasos

Esta guía requiere una comprensión práctica de lo siguiente [!DNL Platform] componentes:

* [[!DNL Privacy Service]](../privacy-service/home.md): administra las solicitudes de los clientes para acceder, desactivar la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Explicación de áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] vincula los datos de identidad del cliente entre sistemas y dispositivos. [!DNL Identity Service] utiliza **áreas de nombres de identidad** proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Un área de nombres puede representar un concepto genérico como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad mantiene un almacén de áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;correo electrónico&quot; y &quot;ECID&quot;), mientras que su organización también puede crear áreas de nombres personalizadas para adaptarlas a sus necesidades particulares.

Para obtener más información sobre áreas de nombres de identidad en [!DNL Experience Platform], consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md).

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Real-Time Customer Profile] uso del [!DNL Privacy Service] API o IU. Antes de leer estas secciones, se recomienda encarecidamente que revise las [API de Privacy Service](../privacy-service/api/getting-started.md) o [IU de Privacy Service](../privacy-service/ui/overview.md) documentación para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar formato correctamente a los datos de identidad de usuario enviados en las cargas útiles de solicitud.

>[!IMPORTANT]
>
>El Privacy Service solo puede procesar [!DNL Profile] datos que utilizan una política de combinación que no realiza la vinculación de identidad. Consulte la sección sobre [limitaciones de políticas de combinación](#merge-policy-limitations) para obtener más información.
>
>Tenga en cuenta que la cantidad de tiempo que puede tardar una solicitud de privacidad en completarse. **no puede** estar garantizado. Si se producen cambios en su [!DNL Profile] no se puede garantizar que se procesen o no los datos mientras se sigue procesando una solicitud.

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier ID proporcionado en `userIDs` debe utilizar un específico de `namespace` y `type`. Un válido [área de nombres de identidad](#namespaces) reconocido por [!DNL Identity Service] debe proporcionarse para el `namespace` mientras que el valor `type` debe ser `standard` o `unregistered` (para áreas de nombres estándar y personalizadas, respectivamente).

>[!NOTE]
>
>Es posible que tenga que proporcionar más de un ID para cada cliente, según el gráfico de identidades y la forma en que se distribuyen los fragmentos de perfil en los conjuntos de datos de Platform. Consulte la siguiente sección [fragmentos de perfil](#fragments) para obtener más información.

Además, la variable `include` La matriz de la carga útil de la solicitud debe incluir los valores de producto de los diferentes almacenes de datos a los que se realiza la solicitud. Para eliminar los datos de perfil asociados a una identidad, la matriz debe incluir el valor `ProfileService`. Para eliminar las asociaciones de gráficos de identidad del cliente, la matriz debe incluir el valor `identity`.

>[!NOTE]
>
>Consulte la sección sobre [solicitudes de perfil y solicitudes de identidad](#profile-v-identity) más adelante en este documento para obtener información más detallada sobre los efectos del uso de `ProfileService` y `identity` dentro de `include` matriz.

La siguiente solicitud crea un nuevo trabajo de privacidad para los datos de un solo cliente en [!DNL Profile] tienda. Se proporcionan dos valores de identidad para el cliente en `userIDs` matriz; una que usa el estándar `Email` área de nombres de identidad y otras que utilizan un área de nombres personalizada `Customer_ID` namespace. También incluye el valor del producto para [!DNL Profile] (`ProfileService`) en el `include` matriz:

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
>Platform procesa las solicitudes de privacidad en todas las aplicaciones [zonas protegidas](../sandboxes/home.md) pertenece a su organización. Como resultado, cualquier `x-sandbox-name` el sistema ignora el encabezado incluido en la solicitud.

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

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL Lago de datos de AEP]** y/o **[!UICONTROL Perfil]** bajo **[!UICONTROL Productos]** para procesar trabajos para datos almacenados en el lago de datos o [!DNL Real-Time Customer Profile], respectivamente.

![Se está creando una solicitud de trabajo de acceso en la interfaz de usuario, con la opción Perfil seleccionada en Productos](./images/privacy/product-value.png)

## Fragmentos de perfil en solicitudes de privacidad {#fragments}

En el [!DNL Profile] del almacén de datos, los datos personales de un cliente individual a menudo estarán compuestos por varios fragmentos de perfil, que se asocian con la persona a través del gráfico de identidad. Al realizar solicitudes de privacidad a [!DNL Profile] En el almacén de, es importante tener en cuenta que las solicitudes solo se procesan en el nivel de perfil-fragmento en lugar de en todo el perfil.

Por ejemplo, piense en una situación en la que almacene datos de atributos del cliente en tres conjuntos de datos independientes, que utilizan identificadores diferentes para asociar esos datos a clientes individuales:

| Nombre del conjunto de datos | Campo de identidad principal | Atributos almacenados |
| --- | --- | --- |
| Conjunto de datos 1 | `customer_id` | `address` |
| Conjunto de datos 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de datos 3 | `email_id` | `mlScore` |

Uno de los conjuntos de datos utiliza `customer_id` como identificador principal, mientras que los otros dos utilizan `email_id`. Si enviara una solicitud de privacidad (de acceso o eliminación) utilizando solo `email_id` como valor de ID de usuario, solo el `firstName`, `lastName`, y `mlScore` se procesarían los atributos, mientras que `address` no se vería afectado.

Para garantizar que las solicitudes de privacidad procesen todos los atributos de cliente relevantes, debe proporcionar los valores de identidad principales para todos los conjuntos de datos aplicables en los que se puedan almacenar dichos atributos (hasta un máximo de nueve ID por cliente). Consulte la sección sobre campos de identidad en la [conceptos básicos de composición de esquemas](../xdm/schema/composition.md#identity) para obtener más información sobre los campos que suelen marcarse como identidades.

## Eliminar procesamiento de solicitudes {#delete}

Cuándo [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía confirmación a [!DNL Privacy Service] que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. Los registros se eliminan una vez completado el trabajo de privacidad.

Dependiendo de si también ha incluido el servicio de identidad (`identity`) y el lago de datos (`aepDataLake`) como productos en su solicitud de privacidad para el perfil (`ProfileService`), se eliminan del sistema diferentes conjuntos de datos relacionados con el perfil en momentos potencialmente diferentes:

| Productos incluidos | Efectos |
| --- | --- |
| `ProfileService` solamente | El perfil se elimina inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. Sin embargo, el gráfico de identidad del perfil sigue existiendo y el perfil puede reconstruirse potencialmente a medida que se incorporan nuevos datos con las mismas identidades. Los datos asociados con el perfil también permanecen en el lago de datos. |
| `ProfileService` y `identity` | El perfil y su gráfico de identidad asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. Los datos asociados con el perfil permanecen en el lago de datos. |
| `ProfileService` y `aepDataLake` | El perfil se elimina inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación. Sin embargo, el gráfico de identidad del perfil sigue existiendo y el perfil puede reconstruirse potencialmente a medida que se incorporan nuevos datos con las mismas identidades.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, ningún usuario puede acceder a ellos [!DNL Platform] servicio. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |
| `ProfileService`, `identity`, y `aepDataLake` | El perfil y su gráfico de identidad asociado se eliminan inmediatamente en cuanto Platform envía la confirmación de que se ha recibido la solicitud de eliminación.<br><br>Cuando el producto del lago de datos responde que la solicitud se recibió y se está procesando actualmente, los datos asociados con el perfil se eliminan de forma suave y, por lo tanto, ningún usuario puede acceder a ellos [!DNL Platform] servicio. Una vez finalizado el trabajo, los datos se eliminan por completo del lago de datos. |

Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento de estados de trabajos.

### Solicitudes de perfil frente a solicitudes de identidad {#profile-v-identity}

Si se realiza una solicitud de eliminación para el perfil (`ProfileService`) pero no el servicio de identidad (`identity`), el trabajo resultante elimina los datos de atributos recopilados para un cliente (o conjunto de clientes), pero no elimina las asociaciones establecidas en el gráfico de identidad.

Por ejemplo, una solicitud de eliminación que utiliza la `email_id` y `customer_id` elimina todos los datos de atributos almacenados en esos ID. Sin embargo, cualquier dato que se incorpore posteriormente en el mismo `customer_id` se seguirán asociando con el `email_id`, ya que la asociación sigue existiendo.

Para eliminar el perfil y todas las asociaciones de identidad de un cliente determinado, asegúrese de incluir tanto el perfil como el servicio de identidad como productos de destino en las solicitudes de eliminación.

### Limitaciones de políticas de combinación {#merge-policy-limitations}

El Privacy Service solo puede procesar [!DNL Profile] datos que utilizan una política de combinación que no realiza la vinculación de identidad. Si utiliza la interfaz de usuario de para confirmar si se están procesando sus solicitudes de privacidad, asegúrese de utilizar una directiva con **[!DNL None]** como su [!UICONTROL Vinculación de ID] escriba. En otras palabras, no puede utilizar una política de combinación en las que [!UICONTROL Vinculación de ID] se establece en [!UICONTROL Gráfico privado].
>![La vinculación de ID de la política de combinación se establece en Ninguno](./images/privacy/no-id-stitch.png)
>
## Pasos siguientes

Al leer este documento, se le han introducido los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Experience Platform]. Para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad, siga leyendo la documentación proporcionada a través de esta guía.

Para obtener información sobre el procesamiento de solicitudes de privacidad para [!DNL Platform] recursos no utilizados por [!DNL Profile], consulte el documento sobre [procesamiento de solicitudes de privacidad en el lago de datos](../catalog/privacy.md).
