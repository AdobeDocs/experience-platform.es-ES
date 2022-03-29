---
keywords: Destino del centro de eventos de Azure;centro de eventos de azure;azure eventhub
title: (Beta) [!DNL Azure Event Hubs] connection
description: Cree una conexión saliente en tiempo real con su [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde el Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: b2ac26589527313ec9f3cf84126e3e23da6c7b83
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 1%

---

# (Beta) [!DNL Azure Event Hubs] connection

## Información general {#overview}

>[!IMPORTANT]
>
>La variable [!DNL Azure Event Hubs] el destino en Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

[!DNL Azure Event Hubs] es una plataforma de transmisión de grandes datos y un servicio de ingesta de eventos. It can receive and process millions of events per second. Data sent to an event hub can be transformed and stored by using any real-time analytics provider or batching/storage adapters.

You can create a real-time outbound connection to your [!DNL Azure Event Hubs] storage to stream data from Adobe Experience Platform.

* Para obtener más información, consulte [!DNL Azure Event Hubs], consulte la [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] mediante programación, consulte la [Tutorial de la API de destinos de flujo continuo](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Azure Event Hubs] con la interfaz de usuario de Platform, consulte las secciones siguientes.

![AWS Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Azure Event Hubs], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

For example, a prospect downloaded a white-paper which qualifies them into a &quot;high-propensity to convert&quot; segment. Asignando el segmento en el que se encuentra el cliente potencial a [!DNL Azure Event Hubs] destino, recibiría este evento en [!DNL Azure Event Hubs]. There, you can employ a do-it-yourself approach and describe business logic on top of the event, as you think would work best with your enterprise IT systems.

## Export type and frequency {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | You are exporting all members of a segment, together with the desired schema fields (for example: email address, phone number, last name), as chosen in the select profile attributes screen of the [destination activation workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Streaming destinations are &quot;always on&quot; API-based connections. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para satisfacer los requisitos de seguridad y cumplimiento de los clientes, Experience Platform proporciona una lista de IP estáticas que puede lista de permitidos para [!DNL Azure Event Hubs] destino. Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de las direcciones IP a lista de permitidos.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Connection parameters {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre de clave SAS]**: El nombre de la regla de autorización, que también se conoce como nombre de clave SAS.
* **[!UICONTROL Clave de SAS]**: La clave principal del espacio de nombres de los centros de eventos. The `sasPolicy` that the `sasKey` corresponds to must have **manage** rights configured in order for the Event Hubs list to be populated. Obtenga información sobre cómo autenticarse en [!DNL Azure Event Hubs] con claves SAS en la variable [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Área de nombres]**: Rellene su [!DNL Azure Event Hubs] espacio de nombres. Learn about [!DNL Azure Event Hubs] namespaces in the [Microsoft documentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nombre]**: Rellene un nombre para la conexión con [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: Proporcione una descripción de la conexión.  Examples: &quot;Premium tier customers&quot;, &quot;Customers interested in kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Provide a name for the stream to your [!DNL Azure Event Hubs] destination.

## Activate segments to this destination {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Comportamiento de exportación del perfil {#profile-export-behavior}

El Experience Platform optimiza el comportamiento de exportación de perfiles para su [!DNL Azure Event Hubs] de destino, para exportar solo los datos a su destino cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación del segmento u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en la pertenencia a segmentos para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* The profile update was determined by a change in the [identity map](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, un perfil que ya se había clasificado para uno de los segmentos asignados al destino se ha añadido una nueva identidad en el atributo de mapa de identidad.
* La actualización de perfil se determinó mediante un cambio en los atributos de al menos uno de los atributos asignados al destino. For example, one of the attributes mapped to the destination in the mapping step is added to a profile.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde estén los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco perfiles nuevos se exportan incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

Regarding the data that is exported for a given profile, it is important to understand the two different concepts of *what determines a data export to your [!DNL Azure Event Hubs] destination* and *which data is included in the export*.

| Qué determina una exportación de destino | What is included in the destination export |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven como señal para una exportación de destino. Esto significa que si cualquier segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Since identities cannot currently be mapped to [!DNL Azure Event Hubs] destinations, changes in any identity on a given profile also determine destination exports.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es o no el mismo valor. This means that an overwrite on an attribute is considered a change even if the value itself has not changed.</li></ul> | <ul><li>Todos los segmentos (con el estado de pertenencia más reciente), independientemente de si están asignados en el flujo de datos o no, se incluyen en la `segmentMembership` objeto.</li><li>Todas las identidades del `identityMap` también se incluyen (el Experience Platform no admite actualmente la asignación de identidades en la variable [!DNL Azure Event Hubs] destino).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

For example, consider this dataflow to an [!DNL Azure Event Hubs] destination where three segments are selected in the dataflow, and four attributes are mapped to the destination.

![Amazon Kinesis destination dataflow](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino se puede determinar mediante un perfil que cumpla los requisitos de uno de los *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` (consulte [Datos exportados](#exported-data) a continuación), podrían aparecer otros segmentos sin asignar, si ese perfil en particular es miembro de ellos. Si un perfil es apto para el segmento Cliente con Autos DeLorean pero también es miembro de los segmentos de fans de películas y ciencia ficción &quot;Volver al futuro&quot; vistos, entonces estos otros dos segmentos también estarán presentes en `segmentMembership` de la exportación de datos, aunque no estén asignados en el flujo de datos.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados arriba determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Exported data {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a su [!DNL Azure Event Hubs] destino en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un determinado segmento, es miembro de otros dos segmentos y salió de otro segmento. La exportación también incluye el nombre del atributo de perfil, los apellidos, la fecha de nacimiento y la dirección de correo electrónico personal. The identities for this profile are ECID and email.

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
>* [Connect to Azure Event Hubs and activate data using the Flow Service API](../../api/streaming-destinations.md)
>* [Destino de AWS Kinesis](./amazon-kinesis.md)
>* [Tipos y categorías de destino](../../destination-types.md)

