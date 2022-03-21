---
keywords: flujo continuo;
title: Conexión de API HTTP
description: El destino de la API HTTP en Adobe Experience Platform le permite enviar datos de perfil a extremos HTTP de terceros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: c2e726a7e66267bf8f301014ae30dedd7472c693
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Conexión de API HTTP (Beta)

>[!IMPORTANT]
>
>El destino de la API HTTP en Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

El destino de la API HTTP es un [!DNL Adobe Experience Platform] destino de flujo continuo que le ayuda a enviar datos de perfil a extremos HTTP de terceros.

Para enviar datos de perfil a extremos HTTP, primero debe [conectarse al destino](#connect-destination) en [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

El destino HTTP está dirigido a clientes que necesitan exportar datos de perfil XDM y segmentos de audiencia a extremos HTTP genéricos.

Los extremos HTTP pueden ser sistemas propios de los clientes o soluciones de terceros.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Póngase en contacto con los representantes de Adobe o con el Servicio de atención al cliente de Adobe si desea habilitar la funcionalidad beta de destino de la API HTTP para su empresa.

Para utilizar el destino de la API HTTP para exportar datos fuera del Experience Platform, debe cumplir los siguientes requisitos previos:

* Debe tener un extremo HTTP que admita la API de REST.
* El extremo HTTP debe admitir el esquema de perfil del Experience Platform. No se admite ninguna transformación en un esquema de carga útil de terceros en el destino de API HTTP. Consulte la [datos exportados](#exported-data) para ver un ejemplo del esquema de salida del Experience Platform.
* El extremo HTTP debe admitir encabezados.
* El extremo HTTP debe admitir [Credenciales de cliente de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticación. Este requisito es válido mientras el destino de la API HTTP está en la fase beta.
* Las credenciales del cliente deben incluirse en el cuerpo de las solicitudes de POST al extremo, como se muestra en el ejemplo siguiente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


También puede utilizar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar una integración y enviar datos de perfil de Experience Platform a un extremo HTTP.

## Conectarse al destino {#connect-destination}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL httpEndpoint]**: el [!DNL URL] del extremo HTTP al que desea enviar los datos de perfil.
   * De forma opcional, puede agregar parámetros de consulta al [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: el [!DNL URL] del extremo HTTP utilizado para [!DNL OAuth2] autenticación.
* **[!UICONTROL ID de cliente]**: el [!DNL clientID] parámetro utilizado en [!DNL OAuth2] credenciales del cliente.
* **[!UICONTROL Secreto del cliente]**: el [!DNL clientSecret] parámetro utilizado en [!DNL OAuth2] credenciales del cliente.

   >[!NOTE]
   >
   >Solo [!DNL OAuth2] actualmente se admiten credenciales de cliente.

* **[!UICONTROL Nombre]**: introduzca un nombre por el que reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Encabezados personalizados]**: introduzca los encabezados personalizados que desee incluir en las llamadas de destino, siguiendo este formato: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >La implementación actual requiere al menos un encabezado personalizado. Esta limitación se resolverá en una actualización futura.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#attributes}

En el [[!UICONTROL Seleccionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) paso, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

## Consideraciones del producto {#product-considerations}

El Experience Platform no transmite datos a extremos HTTP a través de un conjunto fijo de IP estáticas. Por lo tanto, Adobe no puede proporcionar una lista de IP estáticas que se pueden lista de permitidos para el destino de API HTTP.

## Comportamiento de exportación del perfil {#profile-export-behavior}

Experience Platform optimiza el comportamiento de exportación del perfil al destino de la API HTTP para exportar solo los datos al extremo de la API cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación del segmento u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en la pertenencia a segmentos para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, un perfil que ya se había clasificado para uno de los segmentos asignados al destino se ha añadido una nueva identidad en el atributo de mapa de identidad.
* La actualización de perfil se determinó mediante un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde estén los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco perfiles nuevos se exportan incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

En cuanto a los datos exportados para un perfil determinado, es importante comprender los dos conceptos diferentes de *qué determina una exportación de datos a su destino de API HTTP* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven como señal para una exportación de destino. Esto significa que si cualquier segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Dado que actualmente las identidades no se pueden asignar a destinos de API HTTP, los cambios en cualquier identidad en un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es o no el mismo valor. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>Todos los segmentos (con el estado de pertenencia más reciente), independientemente de si están asignados en el flujo de datos o no, se incluyen en la `segmentMembership` objeto.</li><li>Todas las identidades del `identityMap` también se incluyen (actualmente, el Experience Platform no admite la asignación de identidad en el destino de API HTTP).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Por ejemplo, considere este flujo de datos a un destino HTTP donde se seleccionan tres segmentos en el flujo de datos y se asignan cuatro atributos al destino.

![Flujo de datos de destino de la API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino se puede determinar mediante un perfil que cumpla los requisitos de uno de los *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` (consulte [Datos exportados](#exported-data) a continuación), podrían aparecer otros segmentos sin asignar, si ese perfil en particular es miembro de ellos. Si un perfil es apto para el segmento Cliente con Autos DeLorean pero también es miembro de los segmentos de fans de películas y ciencia ficción &quot;Volver al futuro&quot; vistos, entonces estos otros dos segmentos también estarán presentes en `segmentMembership` de la exportación de datos, aunque no estén asignados en el flujo de datos.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados arriba determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Datos exportados {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a su [!DNL HTTP] destino en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un determinado segmento, es miembro de otros dos segmentos y salió de otro segmento. La exportación también incluye el nombre del atributo de perfil, los apellidos, la fecha de nacimiento y la dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

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
