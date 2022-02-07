---
keywords: Amazon Kinesis;destino de kinesis;kinesis
title: Conexión de Amazon Kinesis
description: Cree una conexión saliente en tiempo real al almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 577b42eef9d4b44b5b556ee31d22276d72c609ea
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# (Beta) [!DNL Amazon Kinesis] connection

## Información general {#overview}

>[!IMPORTANT]
>
>La variable [!DNL Amazon Kinesis] el destino en Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

La variable [!DNL Kinesis Data Streams] servicio por [!DNL Amazon Web Services] permite recopilar y procesar flujos grandes de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con su [!DNL Amazon Kinesis] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información, consulte [!DNL Amazon Kinesis], consulte la [Documentación de Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectarse a [!DNL Amazon Kinesis] mediante programación, consulte la [Tutorial de la API de destinos de flujo continuo](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Amazon Kinesis] con la interfaz de usuario de Platform, consulte las secciones siguientes.

![Amazon Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Amazon Kinesis], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un libro blanco que los califica para un segmento de &quot;alta propensión a convertir&quot;. Asignando el segmento en el que se encuentra el cliente potencial a [!DNL Amazon Kinesis] destino, recibiría este evento en [!DNL Amazon Kinesis]. En este caso, puede utilizar un enfoque propio y describir la lógica empresarial además del evento, ya que considera que funcionará mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de audiencia](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Requerido [!DNL Amazon Kinesis] permissions {#required-kinesis-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon Kinesis] flujos, el Experience Platform necesita permisos para las siguientes acciones:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Estos permisos se organizan mediante la variable [!DNL Kinesis] y Platform los comprobará una vez que haya configurado el destino de Kinesis en la interfaz de usuario de Platform.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para exportar correctamente los datos a un [!DNL Kinesis] destino.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `kinesis:ListStreams` | Acción que enumera las secuencias de datos de Amazon Kinesis. |
| `kinesis:PutRecord` | Acción que escribe un registro de datos único en un flujo de datos de Kinesis. |
| `kinesis:PutRecords` | Acción que escribe varios registros de datos en un flujo de datos de Kinesis en una sola llamada. |

Para obtener más información sobre cómo controlar el acceso a [!DNL Kinesis] flujos de datos, lea lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!DNL Amazon Web Services]clave de acceso y clave secreta**: En [!DNL Amazon Web Services], genere un `access key - secret access key` par para conceder acceso a Platform a su [!DNL Amazon Kinesis] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Indicar qué [!DNL Amazon Web Services] región a la que transmitir los datos.
* **Nombre**: Proporcione un nombre a la conexión para [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción para la conexión a [!DNL Amazon Kinesis].
* **flujo**: Proporcione el nombre de un flujo de datos existente en su [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Comportamiento de exportación del perfil {#profile-export-behavior}

El Experience Platform optimiza el comportamiento de exportación de perfiles para su [!DNL Amazon Kinesis] de destino, para exportar solo los datos a su destino cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación del segmento u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en la pertenencia a segmentos para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, un perfil que ya se había clasificado para uno de los segmentos asignados al destino se ha añadido una nueva identidad en el atributo de mapa de identidad.
* La actualización de perfil se determinó mediante un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde estén los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco perfiles nuevos se exportan incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

En cuanto a los datos exportados para un perfil determinado, es importante comprender los dos conceptos diferentes de *qué determina una exportación de datos a su [!DNL Amazon Kinesis] destino* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven como señal para una exportación de destino. Esto significa que si cualquier segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Dado que actualmente las identidades no se pueden asignar a [!DNL Amazon Kinesis] destinos, los cambios en cualquier identidad en un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es o no el mismo valor. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>Todos los segmentos (con el estado de pertenencia más reciente), independientemente de si están asignados en el flujo de datos o no, se incluyen en la `segmentMembership` objeto.</li><li>Todas las identidades del `identityMap` también se incluyen (el Experience Platform no admite actualmente la asignación de identidades en la variable [!DNL Amazon Kinesis] destino).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Por ejemplo, considere este flujo de datos como un [!DNL Amazon Kinesis] destino donde se seleccionan tres segmentos en el flujo de datos y se asignan cuatro atributos al destino.

![Flujo de datos de destino de Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino se puede determinar mediante un perfil que cumpla los requisitos de uno de los *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` (consulte [Datos exportados](#exported-data) a continuación), podrían aparecer otros segmentos sin asignar, si ese perfil en particular es miembro de ellos. Si un perfil es apto para el segmento Cliente con Autos DeLorean pero también es miembro de los segmentos de fans de películas y ciencia ficción &quot;Volver al futuro&quot; vistos, entonces estos otros dos segmentos también estarán presentes en `segmentMembership` de la exportación de datos, aunque no estén asignados en el flujo de datos.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados arriba determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Datos exportados {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a su [!DNL Amazon Kinesis] destino en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un determinado segmento, es miembro de otros dos segmentos y salió de otro segmento. La exportación también incluye el nombre del atributo de perfil, los apellidos, la fecha de nacimiento y la dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

>[!MORELIKETHIS]
>
>* [Conectarse a Amazon Kinesis y activar datos mediante la API de servicio de flujo](../../api/streaming-destinations.md)
>* [Destino de los centros de eventos de Azure](./azure-event-hubs.md)
>* [Tipos y categorías de destino](../../destination-types.md)

