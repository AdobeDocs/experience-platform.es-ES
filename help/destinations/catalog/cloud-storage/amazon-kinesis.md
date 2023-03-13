---
keywords: Amazon Kinesis;destino de kinesis;kinesis
title: Conexión de Amazon Kinesis
description: Cree una conexión saliente en tiempo real a su almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: ce20c273cb6a87264363c03611ccfdfb783e595f
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] conexión

## Información general {#overview}

>[!IMPORTANT]
>
> Este destino solo está disponible para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

El [!DNL Kinesis Data Streams] servicio por [!DNL Amazon Web Services] permite recopilar y procesar grandes flujos de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con su [!DNL Amazon Kinesis] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información acerca de [!DNL Amazon Kinesis], consulte la [Documentación de Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectarse a [!DNL Amazon Kinesis] mediante programación, consulte la [Tutorial de API de destinos de streaming](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Amazon Kinesis] Mediante la interfaz de usuario de Platform, consulte las secciones siguientes.

![Amazon Kinesis en la IU](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Amazon Kinesis], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un documento técnico que le clasifica en un segmento de &quot;alta tendencia a la conversión&quot;. Asignando el segmento en el que se encuentra el cliente potencial al [!DNL Amazon Kinesis] destino, recibiría este evento en [!DNL Amazon Kinesis]. Allí, puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial además del evento, tal como cree que funcionaría mejor con sus sistemas de TI empresariales.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para cumplir los requisitos de seguridad y conformidad de los clientes, Experience Platform proporciona una lista de direcciones IP estáticas que puede lista de permitidos para el [!DNL Amazon Kinesis] destino. Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de direcciones IP que se van a lista de permitidos.

## Requerido [!DNL Amazon Kinesis] permissions {#required-kinesis-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon Kinesis] flujos, el Experience Platform necesita permisos para las siguientes acciones:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Estos permisos se organizan a través de la variable [!DNL Kinesis] y son comprobados por Platform una vez que configura el destino de Kinesis en la interfaz de usuario de Platform.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para exportar correctamente datos a una [!DNL Kinesis] destino.

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
| `kinesis:ListStreams` | Una acción que enumera las secuencias de datos de Amazon Kinesis. |
| `kinesis:PutRecord` | Una acción que escribe un único registro de datos en un flujo de datos de Kinesis. |
| `kinesis:PutRecords` | Una acción que escribe varios registros de datos en un flujo de datos de Kinesis en una sola llamada. |

{style="table-layout:auto"}

Para obtener más información sobre el control de acceso de [!DNL Kinesis] secuencias de datos, lea lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). Al conectarse a este destino, debe proporcionar la siguiente información:

### Información de autenticación {#authentication-information}

Introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

![Imagen de la pantalla de la IU que muestra los campos completados para los detalles de autenticación de Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]clave de acceso y clave secreta**: en [!DNL Amazon Web Services], genere un `access key - secret access key` par para conceder acceso de plataforma a su [!DNL Amazon Kinesis] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Región]**: Indique qué [!DNL Amazon Web Services] región a la que se transmitirán los datos.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Incluir nombres de segmentos"
>abstract="Cambie la opción si desea que la exportación de datos incluya los nombres de los segmentos que está exportando. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Incluir marcas de tiempo de segmentos"
>abstract="Cambie si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los segmentos, así como la marca de tiempo UNIX cuando los segmentos se asignaron al destino para la activación. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino de Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Nombre]**: proporcione un nombre para la conexión a [!DNL Amazon Kinesis]
* **[!UICONTROL Descripción]**: Proporcione una descripción para la conexión a [!DNL Amazon Kinesis].
* **[!UICONTROL Transmitir]**: Proporcione el nombre de un flujo de datos existente en su [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.
* **[!UICONTROL Incluir nombres de segmentos]**: cambie si desea que la exportación de datos incluya los nombres de los segmentos que está exportando. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.
* **[!UICONTROL Incluir marcas de tiempo de segmentos]**: Marque esta opción si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los segmentos, así como la marca de tiempo UNIX cuando los segmentos se asignaron al destino para la activación. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Comportamiento de exportación de perfil {#profile-export-behavior}

El Experience Platform optimiza el comportamiento de exportación de perfiles a [!DNL Amazon Kinesis] destino, para exportar solo datos a su destino cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación de segmentos u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en el abono de segmentos para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, a un perfil que ya se había clasificado para uno de los segmentos asignados al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

Con respecto a los datos que se exportan para un perfil determinado, es importante comprender los dos conceptos diferentes de *qué determina una exportación de datos a su [!DNL Amazon Kinesis] destino* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven de referencia para una exportación de destino. Esto significa que si algún segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Dado que las identidades no se pueden asignar actualmente a [!DNL Amazon Kinesis] destinos, los cambios en cualquier identidad de un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es el mismo valor o no. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>El `segmentMembership` El objeto incluye el segmento asignado en el flujo de datos de activación, para el cual el estado del perfil ha cambiado después de un evento de calificación o salida de segmento. Tenga en cuenta que otros segmentos no asignados para los que el perfil cumple los requisitos pueden formar parte de la exportación de destino, si estos segmentos pertenecen al mismo [política de combinación](/help/profile/merge-policies/overview.md) como el segmento asignado en el flujo de datos de activación. </li><li>Todas las identidades en `identityMap` también se incluyen los objetos de (actualmente, el Experience Platform no admite la asignación de identidades en [!DNL Amazon Kinesis] destino).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

Por ejemplo, considere este flujo de datos como una [!DNL Amazon Kinesis] destino en el que se seleccionan tres segmentos en el flujo de datos y se asignan cuatro atributos al destino.

![Flujo de datos de destino de Amazon Kinesis](../../assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que cumpla los requisitos de uno de los siguientes criterios o que salga de él *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` objeto (consulte [Datos exportados](#exported-data) , podrían aparecer otros segmentos no asignados, si ese perfil en particular es miembro de ellos y si comparten la misma política de combinación que el segmento que activó la exportación. Si un perfil cumple los requisitos para la **Cliente con coches DeLorean** segmento, pero también es miembro del **Visto &quot;Volver al futuro&quot;** película y **Aficionados a la ciencia ficción** segmentos, estos otros dos segmentos también estarán presentes en el `segmentMembership` objeto de la exportación de datos, aunque no estén asignados en el flujo de datos, si comparten la misma política de combinación con el **Cliente con coches DeLorean** segmento.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados anteriormente determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Relleno de datos históricos {#historical-data-backfill}

Al agregar un segmento nuevo a un destino existente o al crear un destino nuevo y asignar segmentos a él, Experience Platform exporta datos históricos de calificación de segmentos al destino. Perfiles aptos para el segmento *antes* el segmento se añadió al destino y se exportó al destino en un plazo aproximado de una hora.

## Datos exportados {#exported-data}

Su exportado [!DNL Experience Platform] Los datos de aterrizan en su [!DNL Amazon Kinesis] destino en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un segmento determinado, es miembro de otros dos segmentos y ha salido de otro segmento. La exportación también incluye el atributo de perfil nombre, apellidos, fecha de nacimiento y dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

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

A continuación, se muestran más ejemplos de datos exportados, según la configuración de la interfaz de usuario seleccionada en el flujo de destino de conexión para **[!UICONTROL Incluir nombres de segmentos]** y **[!UICONTROL Incluir marcas de tiempo de segmentos]** opciones:

+++ El ejemplo de exportación de datos siguiente incluye nombres de segmento en la variable `segmentMembership` sección

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ El ejemplo de exportación de datos siguiente incluye marcas de tiempo de segmentos en la variable `segmentMembership` sección

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Límites y directiva de reintentos {#limits-retry-policy}

En el 95 por ciento de los casos, Experience Platform intenta ofrecer una latencia de rendimiento de menos de 10 minutos para los mensajes enviados correctamente con una tasa de menos de 10 000 solicitudes por segundo para cada flujo de datos a un destino HTTP.

En caso de solicitudes fallidas al destino de la API HTTP, el Experience Platform almacena las solicitudes fallidas y las reintenta dos veces para enviar las solicitudes al extremo.

>[!MORELIKETHIS]
>
>* [Conéctese a Amazon Kinesis y active los datos mediante la API de Flow Service](../../api/streaming-destinations.md)
>* [Azure Event Hubs destination](./azure-event-hubs.md)
>* [Tipos y categorías de destino](../../destination-types.md)

