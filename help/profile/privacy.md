---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en perfil del cliente en tiempo real
type: Documentation
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes de acceso, exclusión de la venta o eliminación de sus datos personales, según lo establecido en numerosas normas de privacidad. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para el Perfil del cliente en tiempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: a713245f3228ed36f262fa3c2933d046ec8ee036
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# Procesamiento de solicitudes de privacidad en [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes de acceso, exclusión de la venta o eliminación de sus datos personales, tal como se definen en las normas de privacidad, como el Reglamento General de Protección de Datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para [!DNL Real-time Customer Profile] en Adobe Experience Platform.

>[!NOTE]
>
>Esta guía solo explica cómo realizar solicitudes de privacidad para el almacén de datos de perfil en Experience Platform. Si también planea realizar solicitudes de privacidad para el lago de datos de Platform, consulte la guía de [procesamiento de solicitudes de privacidad en Data Lake](../catalog/privacy.md) además de este tutorial.
>
>Para ver los pasos sobre cómo realizar solicitudes de privacidad para otras aplicaciones de Adobe Experience Cloud, consulte la [documentación del Privacy Service](../privacy-service/experience-cloud-apps.md).

## Primeros pasos

Se recomienda que tenga una comprensión práctica de lo siguiente [!DNL Experience Platform] antes de leer esta guía:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestiona las solicitudes de los clientes para acceder, desactivar o eliminar sus datos personales en todas las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-time Customer Profile]](home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Explicación de las áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] vincula los datos de identidad de los clientes entre sistemas y dispositivos. [!DNL Identity Service] uses **áreas de nombres de identidad** proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Un área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;correo electrónico&quot;) o asociar la identidad a una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

El servicio de identidad mantiene un almacén de áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear áreas de nombres personalizadas para adaptarlas a sus necesidades específicas.

Para obtener más información sobre áreas de nombres de identidad en [!DNL Experience Platform], consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md).

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Real-time Customer Profile] usando la variable [!DNL Privacy Service] API o IU. Antes de leer estas secciones, se recomienda revisar la [API de Privacy Service](../privacy-service/api/getting-started.md) o [IU de Privacy Service](../privacy-service/ui/overview.md) documentación para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar formato correcto a los datos de identidad de usuario enviados en las cargas de solicitud.

>[!IMPORTANT]
>
>El Privacy Service solo puede procesar [!DNL Profile] datos que utilizan una directiva de combinación que no realiza la vinculación de identidad. Consulte la sección sobre [combinar limitaciones de directivas](#merge-policy-limitations) para obtener más información.
>
>También es importante tener en cuenta que no se puede garantizar la cantidad de tiempo que una solicitud de privacidad puede tardar en completarse. Si se producen cambios en su [!DNL Profile] durante el procesamiento de una solicitud, no se puede garantizar si esos registros se procesan o no.

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier ID proporcionado dentro de `userIDs` debe utilizar un `namespace` y `type`. Un [área de nombres de identidad](#namespaces) reconocido por [!DNL Identity Service] debe estar previsto para `namespace` mientras que la variable `type` debe ser `standard` o `unregistered` (para espacios de nombres estándar y personalizados, respectivamente).

>[!NOTE]
>
>Es posible que necesite proporcionar más de un ID para cada cliente, según el gráfico de identidad y cómo se distribuyan los fragmentos de perfil en los conjuntos de datos de Platform. Consulte la siguiente sección [fragmentos de perfil](#fragments) para obtener más información.

Además, la variable `include` matriz de la carga útil de solicitud debe incluir los valores de producto para los diferentes almacenes de datos a los que se realiza la solicitud. Para eliminar los datos de perfil asociados a una identidad, la matriz debe incluir el valor `ProfileService`. Para eliminar las asociaciones de gráficos de identidad del cliente, la matriz debe incluir el valor `identity`.

>[!NOTE]
>
>Consulte la sección sobre [solicitudes de perfil y solicitudes de identidad](#profile-v-identity) más adelante en este documento para obtener información más detallada sobre los efectos de utilizar `ProfileService` y `identity` dentro de la variable `include` matriz.

La siguiente solicitud crea un nuevo trabajo de privacidad para los datos de un único cliente en la variable [!DNL Profile] tienda. Se proporcionan dos valores de identidad para el cliente en la variable `userIDs` matriz; una que utilice el estándar `Email` área de nombres de identidad y la otra utilizando una `Customer_ID` espacio de nombres. También incluye el valor del producto para [!DNL Profile] (`ProfileService`) en el `include` matriz:

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
>Platform procesa las solicitudes de privacidad en todas las [entornos limitados](../sandboxes/home.md) pertenecer a su organización. Como resultado, cualquier `x-sandbox-name` el sistema ignora el encabezado incluido en la solicitud.

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL Lago de datos AEP]** y/o **[!UICONTROL Perfil]** under **[!UICONTROL Productos]** para procesar los trabajos de los datos almacenados en la variable [!DNL Data Lake] o [!DNL Real-time Customer Profile], respectivamente.

![Se está creando una solicitud de trabajo de acceso en la interfaz de usuario, con la opción Perfil seleccionada en Productos](./images/privacy/product-value.png)

## Fragmentos de perfil en solicitudes de privacidad {#fragments}

En el [!DNL Profile] almacén de datos, los datos personales de un cliente individual a menudo estarán compuestos por varios fragmentos de perfil, que están asociados a la persona a través del gráfico de identidad. Al realizar solicitudes de privacidad al [!DNL Profile] En el almacén, es importante tener en cuenta que las solicitudes solo se procesan en el nivel de fragmento de perfil, en lugar de en todo el perfil.

Por ejemplo, imaginemos una situación en la que está almacenando datos de atributos del cliente en tres conjuntos de datos separados, que utilizan identificadores diferentes para asociar esos datos con clientes individuales:

| Nombre del conjunto de datos | Campo de identidad principal | Atributos almacenados |
| --- | --- | --- |
| Conjunto de datos 1 | `customer_id` | `address` |
| Conjunto de datos 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de datos 3 | `email_id` | `mlScore` |

Uno de los conjuntos de datos utiliza `customer_id` como identificador principal, mientras que los otros dos utilizan `email_id`. Si tuviera que enviar una solicitud de privacidad (acceso o eliminación) utilizando solo `email_id` como valor de ID de usuario, solo la variable `firstName`, `lastName`y `mlScore` se procesarían los atributos, mientras que `address` no se verán afectados.

Para garantizar que sus solicitudes de privacidad procesen todos los atributos del cliente relevantes, debe proporcionar los valores de identidad principales para todos los conjuntos de datos aplicables en los que se puedan almacenar dichos atributos (hasta un máximo de nueve ID por cliente). Consulte la sección sobre campos de identidad en la [conceptos básicos de la composición del esquema](../xdm/schema/composition.md#identity) para obtener más información sobre los campos que se marcan comúnmente como identidades.

## Eliminación del procesamiento de solicitudes {#delete}

When [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía confirmación a [!DNL Privacy Service] que la solicitud se ha recibido y los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del [!DNL Data Lake] o [!DNL Profile] almacene una vez finalizado el trabajo de privacidad. Mientras el trabajo de eliminación sigue procesándose, los datos se eliminan de forma suave y, por lo tanto, ningún usuario puede acceder a ellos [!DNL Platform] servicio. Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento del estado de los trabajos.

En futuras versiones, [!DNL Platform] enviará confirmación a [!DNL Privacy Service] después de eliminar físicamente los datos.

### Solicitudes de perfil frente a solicitudes de identidad {#profile-v-identity}

Si se realiza una solicitud de eliminación para el perfil (`ProfileService`) pero no el servicio de identidad (`identity`), el trabajo resultante elimina los datos de atributo recopilados para un cliente (o conjunto de clientes), pero no elimina las asociaciones establecidas en el gráfico de identidad.

Por ejemplo, una solicitud de eliminación que utilice el `email_id` y `customer_id` elimina todos los datos de atributos almacenados bajo esos ID. Sin embargo, cualquier dato que posteriormente se incorpore en el mismo `customer_id` seguirá estando asociado con el `email_id`, ya que la asociación sigue existiendo.

Para eliminar el perfil y todas las asociaciones de identidad de un cliente determinado, asegúrese de incluir tanto el perfil como el servicio de identidad como productos de destino en las solicitudes de eliminación.

### Combinar limitaciones de directivas {#merge-policy-limitations}

El Privacy Service solo puede procesar [!DNL Profile] datos que utilizan una directiva de combinación que no realiza la vinculación de identidad. Si utiliza la interfaz de usuario para confirmar si sus solicitudes de privacidad se están procesando, asegúrese de que está utilizando una directiva con **[!DNL None]** como su [!UICONTROL Vinculación de ID] tipo . En otras palabras, no puede usar una directiva de combinación donde [!UICONTROL Vinculación de ID] está configurado como [!UICONTROL Gráfico privado].
>![La vinculación de ID de la directiva de combinación se establece en Ninguno](./images/privacy/no-id-stitch.png)
>
## Pasos siguientes

Al leer este documento, se le han introducido los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Experience Platform]. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Para obtener información sobre el procesamiento de solicitudes de privacidad de [!DNL Platform] recursos no utilizados por [!DNL Profile], consulte el documento en [procesamiento de solicitudes de privacidad en Data Lake](../catalog/privacy.md).
