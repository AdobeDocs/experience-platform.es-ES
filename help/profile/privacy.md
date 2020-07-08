---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en Perfil del cliente en tiempo real
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Procesamiento de solicitudes de privacidad en Perfil del cliente en tiempo real

Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales, según lo establecido en las regulaciones de privacidad, como la Regulación General de Protección de Datos (RGPD) y la Ley de Privacidad del Consumidor de California (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de las solicitudes de privacidad para el Perfil del cliente en tiempo real.

## Primeros pasos

Se recomienda que conozca bien los siguientes servicios de Experience Platform antes de leer esta guía:

* [Privacy Service](home.md): Gestiona las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [Servicio](../identity-service/home.md)de identidad: Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil](../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Explicación de las Áreas de nombres de identidad {#namespaces}

Adobe Experience Platform Identity Service une los datos de identidad del cliente entre sistemas y dispositivos. Identity Service utiliza Áreas de nombres **de** identidad para proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un ID de Advertising Cloud de Adobe (&quot;AdCloud&quot;) o un ID de Adobe Target (&quot;TNTID&quot;).

Identity Service mantiene un almacén de Áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las Áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;Correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear Áreas de nombres personalizadas para satisfacer sus necesidades específicas.

Para obtener más información sobre Áreas de nombres de identidad en Experience Platform, consulte la descripción general [de la Área de nombres de](../identity-service/namespaces.md)identidad.

## Envío de solicitudes {#submit}

>[!NOTE]
>
>Esta sección trata cómo crear solicitudes de privacidad para el almacén de datos de Perfil. Se recomienda encarecidamente que revise la documentación de la API [de](../privacy-service/api/getting-started.md) Privacy Service o de la interfaz de usuario [de](../privacy-service/ui/overview.md) Privacy Service para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluida la forma correcta de dar formato a los datos de identidad de usuario enviados en las cargas de solicitud.

La siguiente sección describe cómo realizar solicitudes de privacidad para el Perfil de clientes en tiempo real y el Data Lake mediante la API de Privacy Service o la interfaz de usuario.

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier `userIDs` que se proporcione debe utilizar un valor específico `namespace` y `type` dependiendo del almacén de datos al que se apliquen. Los ID del almacén de Perfiles deben utilizar &quot;estándar&quot; o &quot;personalizado&quot; para su `type` valor, y una Área de nombres [de](#namespaces) identidad válida reconocida por Identity Service para su `namespace` valor.


Además, la `include` matriz de la carga útil de la solicitud debe incluir los valores del producto para los diferentes almacenes de datos a los que se realiza la solicitud. Al realizar solicitudes al lago de datos, la matriz debe incluir el valor &quot;ProfileService&quot;.

La siguiente solicitud crea un nuevo trabajo de privacidad tanto para el Perfil del cliente en tiempo real, mediante la Área de nombres de identidad &quot;Correo electrónico&quot; estándar. También incluye el valor del producto para el Perfil en la `include` matriz:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **AEP Data Lake** y/o **Perfil** en _Productos_ para procesar los trabajos de datos almacenados en Data Lake o en Real-time Customer Perfil, respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Eliminar procesamiento de solicitud

Cuando el Experience Platform recibe una solicitud de eliminación del Privacy Service, Platform envía una confirmación al Privacy Service de que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del Data Lake o del almacén de Perfiles en un plazo de siete días. Durante ese período de siete días, los datos se eliminan de forma suave y, por lo tanto, ningún servicio de Platform puede acceder a ellos.

En futuras versiones, Platform enviará una confirmación al Privacy Service después de que se hayan eliminado físicamente los datos.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad en Experience Platform. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Para obtener información sobre el procesamiento de solicitudes de privacidad de recursos de Platform que no utiliza Perfil, consulte el documento sobre el procesamiento de solicitudes de [privacidad en Data Lake](../catalog/privacy.md).