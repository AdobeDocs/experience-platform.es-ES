---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en Perfil del cliente en tiempo real
topic: overview
translation-type: tm+mt
source-git-commit: f7abccb677294e1595fb35c27e03c30eb968082a
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---


# Procesamiento de solicitud de privacidad en [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales, según lo establecido en las regulaciones de privacidad, tales como el Reglamento General de Protección de Datos (RGPD) y [!DNL California Consumer Privacy Act] (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad de [!DNL Real-time Customer Profile].

## Primeros pasos

Antes de leer esta guía, se recomienda que conozca los siguientes [!DNL Experience Platform] servicios:

* [[!Privacy Service DNL]](home.md): Gestiona las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales en todas las aplicaciones de Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [[!Perfil del cliente en tiempo real de DNL]](../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Explicación de las Áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] une los datos de identidad de los clientes entre sistemas y dispositivos. [!DNL Identity Service] utiliza Áreas de nombres **de** identidad para proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service mantiene un almacén de Áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las Áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;Correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear Áreas de nombres personalizadas para satisfacer sus necesidades específicas.

Para obtener más información sobre las Áreas de nombres de identidad en [!DNL Experience Platform], consulte la información general [sobre la Área de nombres de](../identity-service/namespaces.md)identidad.

## Envío de solicitudes {#submit}

Las secciones siguientes describen cómo realizar solicitudes de privacidad para [!DNL Real-time Customer Profile] utilizar la [!DNL Privacy Service] API o la interfaz de usuario. Antes de leer estas secciones, se recomienda encarecidamente que revise la documentación de la API [de](../privacy-service/api/getting-started.md) Privacy Service o de la interfaz de usuario [de](../privacy-service/ui/overview.md) Privacy Service para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluido cómo dar un formato adecuado a los datos de identidad de usuario enviados en las cargas de la solicitud.

>[!IMPORTANT]
>
>El Privacy Service solo puede procesar [!DNL Profile] datos mediante una directiva de combinación que no realiza la vinculación de identidad. Si utiliza la interfaz de usuario para confirmar si las solicitudes de privacidad se están procesando, asegúrese de que está utilizando una directiva con &quot;[!DNL None]&quot; como tipo de [!UICONTROL identificación] . En otras palabras, no se puede usar una directiva de combinación en la que la vinculación [!UICONTROL de ID] esté configurada en &quot;Gráficoprivado&quot;.
>
>![](./images/privacy/no-id-stitch.png)

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier ID que se proporcione en `userIDs` debe utilizar un `namespace` y `type`específico. Se debe proporcionar una Área de nombres [de](#namespaces) identidad válida reconocida por [!DNL Identity Service] el `namespace` valor, mientras que el `type` debe ser `standard` o `unregistered` (para Áreas de nombres estándar y personalizadas, respectivamente).

>[!NOTE]
>
>Es posible que deba proporcionar más de un ID para cada cliente, según el gráfico de identidad y la forma en que se distribuyen los fragmentos de perfil en los conjuntos de datos de la plataforma. Consulte la siguiente sección Fragmentos [de](#fragments) perfil para obtener más información.

Además, la `include` matriz de la carga útil de la solicitud debe incluir los valores del producto para los diferentes almacenes de datos a los que se realiza la solicitud. Al realizar solicitudes al [!DNL Data Lake], la matriz debe incluir el valor &quot;ProfileService&quot;.

La siguiente solicitud crea un nuevo trabajo de privacidad para los datos de un único cliente en la [!DNL Profile] tienda. Se proporcionan dos valores de identidad para el cliente en la `userIDs` matriz; una con la Área de nombres de identidad estándar `Email` y otra con una `Customer_ID` Área de nombres personalizada. También incluye el valor de producto para [!DNL Profile] (`ProfileService`) en la `include` matriz:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL AEP Data Lake]** y/o **[!UICONTROL Perfil]** en **[!UICONTROL Productos]** para procesar los trabajos de datos almacenados en los [!DNL Data Lake] o [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Fragmentos de perfil en solicitudes de privacidad {#fragments}

En el almacén de [!DNL Profile] datos, los datos personales de un cliente individual a menudo estarán compuestos de varios fragmentos de perfil, que se asocian con la persona a través del gráfico de identidad. Al realizar solicitudes de privacidad en la [!DNL Profile] tienda, es importante tener en cuenta que las solicitudes solo se procesan en el nivel de fragmento de perfil, en lugar de en todo el perfil.

Por ejemplo: considere una situación en la que está almacenando datos de atributos del cliente en tres conjuntos de datos independientes, que utilizan identificadores diferentes para asociar esos datos con clientes individuales:

| Nombre del conjunto de datos | Campo de identidad principal | Atributos almacenados |
| --- | --- | --- |
| Conjunto de datos 1 | `customer_id` | `address` |
| Conjunto de datos 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de datos 3 | `email_id` | `mlScore` |

Uno de los conjuntos de datos utiliza `customer_id` como identificador principal, mientras que los otros dos utilizan `email_id`. Si enviara una solicitud de privacidad (acceso o eliminación) utilizando únicamente `email_id` como valor de ID de usuario, solo se procesarían los atributos `firstName`, `lastName`y `mlScore` , aunque no `address` se verían afectados.

Para garantizar que las solicitudes de privacidad procesen todos los atributos del cliente relevantes, debe proporcionar los valores de identidad principales para todos los conjuntos de datos aplicables en los que se puedan almacenar dichos atributos (hasta un máximo de nueve ID por cliente). Consulte la sección sobre campos de identidad en los [conceptos básicos de la composición](../xdm/schema/composition.md#identity) de esquemas para obtener más información sobre los campos que se suelen marcar como identidades.

>[!NOTE]
>
>Si está utilizando diferentes [entornos](../sandboxes/home.md) limitados para almacenar [!DNL Profile] los datos, debe realizar una solicitud de privacidad independiente para cada entorno limitado, indicando el nombre apropiado del entorno limitado en el `x-sandbox-name` encabezado.

## Eliminar procesamiento de solicitud

Cuando [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía una confirmación de [!DNL Privacy Service] que la solicitud se ha recibido y los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del almacén [!DNL Data Lake] o [!DNL Profile] almacén una vez finalizado el trabajo de privacidad. Mientras el trabajo de eliminación sigue procesándose, los datos se eliminan de forma suave y, por lo tanto, ningún [!DNL Platform] servicio puede acceder a ellos. Consulte la [[!DNL Privacy Service] documentación](../privacy-service/home.md#monitor) para obtener más información sobre el seguimiento de los estados de los trabajos.

>[!IMPORTANT]
>
>Aunque una solicitud de eliminación correcta elimina los datos de atributos recopilados para un cliente (o conjunto de clientes), la solicitud no elimina las asociaciones establecidas en el gráfico de identidad.
>
>Por ejemplo, una solicitud de eliminación que utiliza el nombre de un cliente `email_id` y `customer_id` elimina todos los datos de atributos almacenados en dichos ID. Sin embargo, los datos que posteriormente se ingieran en el mismo `customer_id` se seguirán asociando con los datos correspondientes `email_id`, ya que la asociación sigue existiendo.

En futuras versiones, [!DNL Platform] enviará confirmación a [!DNL Privacy Service] después de que se hayan eliminado físicamente los datos.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en [!DNL Experience Platform]. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Para obtener información sobre el procesamiento de solicitudes de privacidad de [!DNL Platform] recursos que no utiliza [!DNL Profile], consulte el documento sobre el procesamiento de solicitudes de [privacidad en Data Lake](../catalog/privacy.md).