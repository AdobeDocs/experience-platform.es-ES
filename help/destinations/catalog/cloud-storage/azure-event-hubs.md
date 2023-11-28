---
keywords: destino de Azure Event Hub;azure Event Hub;azure event Hub
title: Conexión de Azure Event Hubs
description: Cree una conexión saliente en tiempo real con su [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde el Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3e2dc51e768d6bcfeedbc26e04997dc46c852e4d
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 5%

---

# [!DNL Azure Event Hubs] conexión

## Información general {#overview}

>[!IMPORTANT]
>
> Este destino solo está disponible para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) clientes.

[!DNL Azure Event Hubs] es una plataforma de streaming de big data y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptador de almacenamiento/agrupamiento.

Puede crear una conexión saliente en tiempo real con su [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información acerca de [!DNL Azure Event Hubs], consulte la [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] mediante programación, consulte la [Tutorial de API de destinos de streaming](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Azure Event Hubs] Mediante la interfaz de usuario de Platform, consulte las secciones siguientes.

![AWS Kinesis en la IU](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Azure Event Hubs], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un documento técnico que le clasifica en un segmento de &quot;alta tendencia a la conversión&quot;. Al asignar la audiencia a la que pertenece el cliente potencial al [!DNL Azure Event Hubs] destino, recibiría este evento en [!DNL Azure Event Hubs]. Allí, puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial además del evento, tal como cree que funcionaría mejor con sus sistemas de TI empresariales.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para cumplir los requisitos de seguridad y conformidad de los clientes, Experience Platform proporciona una lista de direcciones IP estáticas que puede lista de permitidos para el [!DNL Azure Event Hubs] destino. Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de direcciones IP que se van a lista de permitidos.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). Al conectarse a este destino, debe proporcionar la siguiente información:

### Información de autenticación {#authentication-information}

#### Autenticación estándar {#standard-authentication}

![Imagen de la pantalla de la IU que muestra los campos completados para los detalles de autenticación estándar de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Si selecciona la opción **[!UICONTROL Autenticación estándar]** escriba para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

* **[!UICONTROL Nombre de clave SAS]**: Nombre de la regla de autorización, que también se conoce como nombre de clave SAS.
* **[!UICONTROL Clave SAS]**: la clave principal del área de nombres de Event Hubs. El `sasPolicy` que el `sasKey` corresponde a debe tener **administrar** derechos configurados para que se rellene la lista Event Hubs. Obtenga información sobre la autenticación en [!DNL Azure Event Hubs] con claves SAS en el [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Área de nombres]**: Rellene el [!DNL Azure Event Hubs] namespace. Más información [!DNL Azure Event Hubs] áreas de nombres en [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Autenticación de firma de acceso compartido (SAS) {#sas-authentication}

![Imagen de la pantalla de la IU que muestra los campos completados para los detalles de autenticación estándar de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Si selecciona la opción **[!UICONTROL Autenticación estándar]** escriba para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

* **[!UICONTROL Nombre de clave SAS]**: Nombre de la regla de autorización, que también se conoce como nombre de clave SAS.
* **[!UICONTROL Clave SAS]**: la clave principal del área de nombres de Event Hubs. El `sasPolicy` que el `sasKey` corresponde a debe tener **administrar** derechos configurados para que se rellene la lista Event Hubs. Obtenga información sobre la autenticación en [!DNL Azure Event Hubs] con claves SAS en el [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Área de nombres]**: Rellene el [!DNL Azure Event Hubs] namespace. Más información [!DNL Azure Event Hubs] áreas de nombres en [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nombre del hub de eventos]**: Rellene el [!DNL Azure Event Hub] nombre . Más información [!DNL Azure Event Hubs] nombres en la [Documentación de Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

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

![Imagen de la pantalla de la IU que muestra los campos completados para los detalles de destino de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nombre]**: Rellene un nombre para la conexión a [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: Proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes de nivel Premium&quot;, &quot;Clientes interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Proporcione un nombre para la secuencia a su [!DNL Azure Event Hubs] destino.
* **[!UICONTROL Incluir nombres de segmentos]**: cambie si desea que la exportación de datos incluya los nombres de las audiencias que está exportando. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.
* **[!UICONTROL Incluir marcas de tiempo de segmentos]**: Marque esta opción si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron las audiencias, así como la marca de tiempo UNIX cuando las audiencias se asignaron al destino para la activación. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* [Evaluación de directiva de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) actualmente no es compatible con las exportaciones al destino de Azure Event Hubs. [Más información](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consulte [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Comportamiento de exportación de perfil {#profile-export-behavior}

El Experience Platform optimiza el comportamiento de exportación de perfiles a [!DNL Azure Event Hubs] Destino, para exportar datos únicamente a su destino cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación de audiencia u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en el abono a audiencia de al menos una de las audiencias asignadas al destino. Por ejemplo, el perfil cumple los requisitos de una de las audiencias asignadas al destino o ha salido de una de las audiencias asignadas al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, a un perfil que ya estaba cualificado para una de las audiencias asignadas al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si una audiencia asignada al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

Con respecto a los datos que se exportan para un perfil determinado, es importante comprender los dos conceptos diferentes de *qué determina una exportación de datos a su [!DNL Azure Event Hubs] destino* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y audiencias asignados sirven de referencia para una exportación de destino. Esto significa que si alguna audiencia asignada cambia de estado (de `null` hasta `realized` o de `realized` hasta `exiting`) o se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Dado que las identidades no se pueden asignar actualmente a [!DNL Azure Event Hubs] destinos, los cambios en cualquier identidad de un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es el mismo valor o no. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>El `segmentMembership` incluye la audiencia asignada en el flujo de datos de activación, cuyo estado del perfil ha cambiado después de un evento de calificación o salida de audiencia. Tenga en cuenta que otras audiencias sin asignar para las que el perfil cumple los requisitos pueden formar parte de la exportación de destino, si estas audiencias pertenecen a la misma [política de combinación](/help/profile/merge-policies/overview.md) como la audiencia asignada en el flujo de datos de activación. </li><li>Todas las identidades en `identityMap` también se incluyen los objetos de (actualmente, el Experience Platform no admite la asignación de identidades en [!DNL Azure Event Hubs] destino).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

Por ejemplo, considere este flujo de datos como una [!DNL Azure Event Hubs] destino en el que se seleccionan tres audiencias en el flujo de datos y se asignan cuatro atributos al destino.

![Flujo de datos de destino de Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que cumpla los requisitos de uno de los siguientes criterios o que salga de él *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` objeto (consulte [Datos exportados](#exported-data) , podrían aparecer otras audiencias no asignadas, si ese perfil en particular es miembro de ellas y si comparten la misma política de combinación que la audiencia que activó la exportación. Si un perfil cumple los requisitos para la **Cliente con coches DeLorean** pero también es miembro de la **Visto &quot;Volver al futuro&quot;** película y **Aficionados a la ciencia ficción** segmentos, estas otras dos audiencias también estarán presentes en el `segmentMembership` objeto de la exportación de datos, aunque no estén asignados en el flujo de datos, si comparten la misma política de combinación con el **Cliente con coches DeLorean** segmento.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados anteriormente determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Relleno de datos históricos {#historical-data-backfill}

Cuando se añade una audiencia nueva a un destino existente o se crea un destino nuevo y se le asignan audiencias, Experience Platform exporta al destino los datos históricos de cualificación de audiencias. Perfiles que cumplen los requisitos para la audiencia *antes* la audiencia añadida al destino se exporta al destino en un plazo aproximado de una hora.

## Datos exportados {#exported-data}

Su exportado [!DNL Experience Platform] Los datos de aterrizan en su [!DNL Azure Event Hubs] destino en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un segmento determinado, es miembro de otros dos segmentos y ha salido de otro segmento. La exportación también incluye el atributo de perfil nombre, apellidos, fecha de nacimiento y dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

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

A continuación, se muestran más ejemplos de datos exportados, según la configuración de la interfaz de usuario seleccionada en el flujo de destino de conexión para **[!UICONTROL Incluir nombres de segmentos]** y **[!UICONTROL Incluir marcas de tiempo de segmentos]** opciones:

+++ La muestra de exportación de datos siguiente incluye nombres de audiencia en la variable `segmentMembership` sección

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

+++ El ejemplo de exportación de datos siguiente incluye marcas de tiempo de audiencia en `segmentMembership` sección

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

En caso de solicitudes fallidas al destino de la API HTTP, el Experience Platform almacena las solicitudes fallidas y las reintenta dos veces para enviar las solicitudes al extremo.

>[!MORELIKETHIS]
>
>* [Conéctese a Azure Event Hubs y active los datos mediante la API de Flow Service](../../api/streaming-destinations.md)
>* [AWS Kinesis destination](./amazon-kinesis.md)
>* [Tipos y categorías de destino](../../destination-types.md)
