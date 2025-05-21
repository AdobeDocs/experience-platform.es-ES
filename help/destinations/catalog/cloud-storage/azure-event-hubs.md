---
keywords: destino de Azure Event Hub;azure Event Hub;azure event Hub
title: Conexión de Azure Event Hubs
description: Cree una conexión saliente en tiempo real a su  [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 678f80445212edc1edd3f4799999990ddcc2a039
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 5%

---

# [!DNL Azure Event Hubs] conexión

## Información general {#overview}

>[!IMPORTANT]
>
> Este destino solo está disponible para los clientes de [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es).

[!DNL Azure Event Hubs] es una plataforma de transmisión de datos y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptador de almacenamiento/agrupamiento.

Puede crear una conexión saliente en tiempo real a su almacenamiento de [!DNL Azure Event Hubs] para transmitir datos desde Adobe Experience Platform.

* Para obtener más información acerca de [!DNL Azure Event Hubs], consulte la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] mediante programación, consulte el [tutorial de la API de destinos de transmisión](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Azure Event Hubs] mediante la interfaz de usuario de Experience Platform, consulte las secciones siguientes.

![AWS Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Al usar destinos de streaming como [!DNL Azure Event Hubs], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a los sistemas que elija.

Por ejemplo, un cliente potencial descargó un documento técnico que le clasifica en un segmento de &quot;alta tendencia a la conversión&quot;. Al asignar la audiencia a la que pertenece el posible cliente en el destino [!DNL Azure Event Hubs], recibirá este evento en [!DNL Azure Event Hubs]. Allí, puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial además del evento, tal como cree que funcionaría mejor con sus sistemas de TI empresariales.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para cumplir los requisitos de seguridad y conformidad de los clientes, Experience Platform proporciona una lista de direcciones IP estáticas que puede lista de permitidos para el destino [!DNL Azure Event Hubs]. Consulte la [lista de permitidos de direcciones IP para destinos de streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de direcciones IP para lista de permitidos.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). Al conectarse a este destino, debe proporcionar la siguiente información:

### Información de autenticación {#authentication-information}

#### Autenticación estándar {#standard-authentication}

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de autenticación estándar de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Si selecciona el tipo de **[!UICONTROL autenticación estándar]** para conectarse a su extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

* **[!UICONTROL Nombre de clave SAS]**: Nombre de la regla de autorización, que también se conoce como nombre de clave SAS.
* **[!UICONTROL Clave SAS]**: La clave principal del espacio de nombres de Event Hubs. El `sasPolicy` al que corresponde `sasKey` debe tener los derechos de **manage** configurados para que se rellene la lista de Event Hubs. Obtenga información acerca de la autenticación en [!DNL Azure Event Hubs] con claves SAS en la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espacio de nombres]**: complete su área de nombres [!DNL Azure Event Hubs]. Obtenga información acerca de [!DNL Azure Event Hubs] áreas de nombres en la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Autenticación de firma de acceso compartido (SAS) {#sas-authentication}

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de autenticación estándar de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Si selecciona el tipo de **[!UICONTROL autenticación estándar]** para conectarse a su extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

* **[!UICONTROL Nombre de clave SAS]**: Nombre de la regla de autorización, que también se conoce como nombre de clave SAS.
* **[!UICONTROL Clave SAS]**: La clave principal del espacio de nombres de Event Hubs. El `sasPolicy` al que corresponde `sasKey` debe tener los derechos de **manage** configurados para que se rellene la lista de Event Hubs. Obtenga información acerca de la autenticación en [!DNL Azure Event Hubs] con claves SAS en la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espacio de nombres]**: complete su área de nombres [!DNL Azure Event Hubs]. Obtenga información acerca de [!DNL Azure Event Hubs] áreas de nombres en la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nombre del centro de eventos]**: Rellene el nombre de [!DNL Azure Event Hub] Obtenga información acerca de [!DNL Azure Event Hubs] nombres en [Microsoft documentation](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Incluir nombres de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya los nombres del público que está exportando. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Incluir marcas de tiempo de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los públicos, así como la marca de tiempo UNIX cuando los públicos se asignaron al destino para la activación. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nombre]**: escriba un nombre para la conexión con [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes de nivel Premium&quot;, &quot;Clientes interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: proporcione un nombre para la secuencia a su destino [!DNL Azure Event Hubs].
* **[!UICONTROL Incluir nombres de segmentos]**: Cambie la opción si desea que la exportación de datos incluya los nombres de las audiencias que está exportando. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la sección [Datos exportados](#exported-data) más abajo.
* **[!UICONTROL Incluir marcas de tiempo de segmentos]**: actívela si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron las audiencias, así como la marca de tiempo UNIX cuando las audiencias se asignaron al destino para la activación. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la sección [Datos exportados](#exported-data) más abajo.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* [La evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) no se admite actualmente en las exportaciones al destino de Azure Event Hubs. [Más información](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consulte [Activar datos de audiencia en destinos de exportación de perfiles de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Comportamiento de exportación de perfil {#profile-export-behavior}

Experience Platform optimiza el comportamiento de exportación de perfiles a su destino [!DNL Azure Event Hubs] para exportar solo datos a su destino cuando se han producido actualizaciones relevantes en un perfil tras la calificación de la audiencia u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en el abono a audiencia de al menos una de las audiencias asignadas al destino. Por ejemplo, el perfil cumple los requisitos de una de las audiencias asignadas al destino o ha salido de una de las audiencias asignadas al destino.
* La actualización de perfil se determinó mediante un cambio en el [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, a un perfil que ya estaba cualificado para una de las audiencias asignadas al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si una audiencia asignada al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

Con respecto a los datos que se exportan para un perfil determinado, es importante entender los dos conceptos diferentes de *qué determina una exportación de datos a su [!DNL Azure Event Hubs] destino* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven de referencia para una exportación de destino. Esto significa que si el estado de `segmentMembership` de un perfil cambia a `realized` o `exiting`, o si se actualiza cualquier atributo asignado, se iniciará una exportación de destino.</li><li>Dado que las identidades no se pueden asignar actualmente a [!DNL Azure Event Hubs] destinos, los cambios en cualquier identidad de un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es el mismo valor o no. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>El objeto `segmentMembership` incluye el segmento asignado en el flujo de datos de activación, para el cual el estado del perfil ha cambiado después de un evento de calificación o salida de segmento. Tenga en cuenta que otros segmentos no asignados para los que el perfil cumple los requisitos pueden formar parte de la exportación de destino, si estos segmentos pertenecen a la misma [política de combinación](/help/profile/merge-policies/overview.md) que el segmento asignado en el flujo de datos de activación. </li><li>También se incluyen todas las identidades del objeto `identityMap` (Experience Platform no admite actualmente la asignación de identidades en el destino [!DNL Azure Event Hubs]).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

Por ejemplo, considere este flujo de datos a un destino [!DNL Azure Event Hubs] donde se seleccionan tres audiencias en el flujo de datos y se asignan cuatro atributos al destino.

![Flujo de datos de destino de Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que califique para uno de los *tres segmentos asignados* o que salga de él. Sin embargo, en la exportación de datos, en el objeto `segmentMembership` (consulte la sección [Datos exportados](#exported-data) más abajo), podrían aparecer otras audiencias no asignadas, si ese perfil en particular es miembro de ellas y si comparten la misma política de combinación que la audiencia que activó la exportación. Si un perfil cumple los requisitos para la audiencia de **Cliente con DeLorean Cars**, pero también es miembro de los segmentos de película **Visto &quot;Volver al futuro&quot;** y **fans de ciencia ficción**, entonces estas otras dos audiencias también estarán presentes en el objeto `segmentMembership` de la exportación de datos, aunque no estén asignadas en el flujo de datos, si comparten la misma política de combinación con el segmento **Cliente con DeLorean Cars**.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados anteriormente determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Relleno de datos históricos {#historical-data-backfill}

Al agregar una audiencia nueva a un destino existente o al crear un destino nuevo y asignarle audiencias, Experience Platform exporta al destino los datos de calificación de audiencias históricas. Los perfiles que cumplen los requisitos para la audiencia *antes de* que la audiencia se agregó al destino se exportan al destino en un plazo aproximado de una hora.

## Datos exportados {#exported-data}

Los datos de [!DNL Experience Platform] exportados llegan a su destino [!DNL Azure Event Hubs] en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un segmento determinado, es miembro de otros dos segmentos y ha salido de otro segmento. La exportación también incluye el atributo de perfil nombre, apellidos, fecha de nacimiento y dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

A continuación se muestran más ejemplos de datos exportados, según la configuración de la interfaz de usuario que seleccione en el flujo de destino de conexión para las opciones **[!UICONTROL Incluir nombres de segmentos]** e **[!UICONTROL Incluir marcas de tiempo de segmentos]**:

+++ La muestra de exportación de datos siguiente incluye nombres de audiencia en la sección `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ La muestra de exportación de datos siguiente incluye marcas de tiempo de audiencia en la sección `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

En caso de solicitudes fallidas al destino de la API HTTP, Experience Platform almacena las solicitudes fallidas y las reintenta dos veces para enviar las solicitudes al extremo.

>[!MORELIKETHIS]
>
>* [Conéctese a Azure Event Hubs y active los datos mediante la API de Flow Service](../../api/streaming-destinations.md)
>* [Destino de AWS Kinesis](./amazon-kinesis.md)
>* [Tipos y categorías de destino](../../destination-types.md)
