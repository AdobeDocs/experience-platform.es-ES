---
title: Conexión de API HTTP
keywords: flujo continuo;
description: Utilice el destino de la API HTTP en Adobe Experience Platform para enviar datos de perfil al extremo HTTP de terceros para ejecutar sus propios análisis o realizar cualquier otra operación que necesite en datos de perfil exportados fuera del Experience Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Conexión de API HTTP

## Información general {#overview}

>[!IMPORTANT]
>
> Este destino solo está disponible para [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

El destino de la API HTTP es un [!DNL Adobe Experience Platform] destino de flujo continuo que le ayuda a enviar datos de perfil a extremos HTTP de terceros.

Para enviar datos de perfil a extremos HTTP, primero debe [conectarse al destino](#connect-destination) en [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

El destino de la API HTTP le permite exportar datos de perfil XDM y segmentos de audiencia a extremos HTTP genéricos. Aquí puede ejecutar sus propios análisis o realizar cualquier otra operación que necesite en datos de perfil exportados fuera del Experience Platform.

Los extremos HTTP pueden ser sistemas propios de los clientes o soluciones de terceros.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de asignación de la variable [flujo de trabajo de activación de destino](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

Para utilizar el destino de la API HTTP para exportar datos fuera del Experience Platform, debe cumplir los siguientes requisitos previos:

* Debe tener un extremo HTTP que admita la API de REST.
* El extremo HTTP debe admitir el esquema de perfil del Experience Platform. No se admite ninguna transformación en un esquema de carga útil de terceros en el destino de API HTTP. Consulte la [datos exportados](#exported-data) para ver un ejemplo del esquema de salida del Experience Platform.
* El extremo HTTP debe admitir encabezados.

>[!TIP]
>
> También puede utilizar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar una integración y enviar datos de perfil de Experience Platform a un extremo HTTP.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para cumplir los requisitos de seguridad y cumplimiento de los clientes, Experience Platform proporciona una lista de IP estáticas que puede lista de permitidos para el destino de la API HTTP. Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de las direcciones IP a lista de permitidos.

## Tipos de autenticación compatibles {#supported-authentication-types}

El destino de la API HTTP admite varios tipos de autenticación en el extremo HTTP:

* extremo HTTP sin autenticación;
* Autenticación del token del portador;
* [Credenciales de cliente de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticación con el formulario de cuerpo, con [!DNL client ID], [!DNL client secret] y [!DNL grant type] en el cuerpo de la solicitud HTTP, como se muestra en el ejemplo siguiente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenciales de cliente de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con autorización básica, con un encabezado de autorización que contiene la dirección URL codificada [!DNL client ID] y [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concesión de contraseña de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Conectarse al destino {#connect-destination}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). Al conectarse a este destino, debe proporcionar la siguiente información:

### Información de autenticación {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo de credenciales del cliente"
>abstract="Select **Formulario de cuerpo codificado** para incluir el ID de cliente y el secreto de cliente en el cuerpo de la solicitud o **Autorización básica** para incluir el ID de cliente y el secreto de cliente en un encabezado de autorización. Vea ejemplos en la documentación."

#### Autenticación de token del portador {#bearer-token-authentication}

Si selecciona la opción **[!UICONTROL Token portador]** tipo de autenticación para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectarse al destino]**:

![Imagen de la pantalla de la interfaz de usuario en la que puede conectarse al destino de la API HTTP mediante autenticación de token al portador](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token portador]**: inserte el token al portador para autenticarse en su ubicación HTTP.

#### Sin autenticación {#no-authentication}

Si selecciona la opción **[!UICONTROL Ninguna]** tipo de autenticación para conectarse al extremo HTTP:

![Imagen de la pantalla de la interfaz de usuario en la que puede conectarse al destino de la API HTTP sin autenticarse](../../assets/catalog/http/http-api-authentication-none.png)

Cuando seleccione esta autenticación abierta, solo deberá seleccionar **[!UICONTROL Conectarse al destino]** y se establece la conexión con el punto final.

#### Autenticación de contraseña de OAuth 2 {#oauth-2-password-authentication}

Si selecciona la opción **[!UICONTROL Contraseña de OAuth 2]** tipo de autenticación para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectarse al destino]**:

![Imagen de la pantalla de la interfaz de usuario en la que puede conectarse al destino de la API HTTP mediante OAuth 2 con autenticación de contraseña](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Dirección URL del token de acceso]**: Dirección URL de su lado que emite acceso a tokens y, opcionalmente, actualice los tokens.
* **[!UICONTROL ID de cliente]**: La variable [!DNL client ID] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Secreto del cliente]**: La variable [!DNL client secret] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para acceder al extremo HTTP.
* **[!UICONTROL Contraseña]**: La contraseña para acceder al extremo HTTP.

#### Autenticación de credenciales de cliente de OAuth 2 {#oauth-2-client-credentials-authentication}

Si selecciona la opción **[!UICONTROL Credenciales de cliente de OAuth 2]** tipo de autenticación para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectarse al destino]**:

![Imagen de la pantalla de la interfaz de usuario en la que puede conectarse al destino de la API HTTP mediante OAuth 2 con autenticación de Credenciales de cliente](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL Dirección URL del token de acceso]**: Dirección URL de su lado que emite acceso a tokens y, opcionalmente, actualice los tokens.
* **[!UICONTROL ID de cliente]**: La variable [!DNL client ID] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Secreto del cliente]**: La variable [!DNL client secret] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Tipo de credenciales de cliente]**: Seleccione el tipo de concesión de credenciales de cliente de OAuth2 que admita el punto final:
   * **[!UICONTROL Formulario de cuerpo codificado]**: En este caso, la variable [!DNL client ID] y [!DNL client secret] se incluyen *en el cuerpo de la solicitud* enviado a su destino. Para ver un ejemplo, consulte la [Tipos de autenticación compatibles](#supported-authentication-types) para obtener más información.
   * **[!UICONTROL Autorización básica]**: En este caso, la variable [!DNL client ID] y [!DNL client secret] se incluyen *en un `Authorization` header* después de ser codificado base64 y enviado a su destino. Para ver un ejemplo, consulte la [Tipos de autenticación compatibles](#supported-authentication-types) para obtener más información.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Encabezados"
>abstract="Introduzca los encabezados personalizados que desea incluir en las llamadas de destino, siguiendo este formato: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Extremo HTTP"
>abstract="Dirección URL del extremo HTTP al que desea enviar los datos de perfil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Incluir nombres de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya los nombres de los segmentos que está exportando. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Incluir marcas de hora de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los segmentos, así como la marca de tiempo UNIX cuando los segmentos se asignaron al destino para la activación. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parámetros de consulta"
>abstract="De forma opcional, puede agregar parámetros de consulta a la dirección URL del extremo HTTP. Dé este formato a los parámetros de consulta que utilice: `parameter1=value&parameter2=value`."

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nombre]**: Escriba un nombre por el cual reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: Escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Encabezados]**: Introduzca los encabezados personalizados que desea incluir en las llamadas de destino, siguiendo este formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Extremo HTTP]**: Dirección URL del extremo HTTP al que desea enviar los datos de perfil.
* **[!UICONTROL Parámetros de consulta]**: De forma opcional, puede agregar parámetros de consulta a la dirección URL del extremo HTTP. Dé este formato a los parámetros de consulta que utilice: `parameter1=value&parameter2=value`.
* **[!UICONTROL Incluir nombres de segmentos]**: Alterne si desea que la exportación de datos incluya los nombres de los segmentos que está exportando. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.
* **[!UICONTROL Incluir marcas de hora de segmentos]**: Alterne si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los segmentos, así como la marca de tiempo UNIX cuando los segmentos se asignaron al destino para la activación. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la [Datos exportados](#exported-data) más abajo.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#attributes}

En el [[!UICONTROL Seleccionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) paso, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

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

## Relleno de datos históricos {#historical-data-backfill}

Cuando agrega un segmento nuevo a un destino existente, o cuando crea un destino nuevo y le asigna segmentos, el Experience Platform exporta los datos históricos de clasificación de segmentos al destino. Perfiles que cumplen los requisitos del segmento *before* el segmento se agregó al destino se exporta al destino en aproximadamente una hora.

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

A continuación se muestran más ejemplos de datos exportados, según la configuración de la interfaz de usuario que seleccione en el flujo de destino de conexión para **[!UICONTROL Incluir nombres de segmentos]** y **[!UICONTROL Incluir marcas de hora de segmentos]** opciones:

+++ El ejemplo de exportación de datos que se muestra a continuación incluye nombres de segmento en la variable `segmentMembership` sección

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

+++ El ejemplo de exportación de datos que se muestra a continuación incluye marcas de hora de segmento en la variable `segmentMembership` sección

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

## Límites y política de reintentos {#limits-retry-policy}

En el 95 % de las veces, el Experience Platform intenta ofrecer una latencia de rendimiento inferior a 10 minutos para los mensajes enviados correctamente con una tasa inferior a 10 000 solicitudes por segundo para cada flujo de datos a un destino HTTP.

En caso de que haya solicitudes fallidas en el destino de la API HTTP, el Experience Platform almacena las solicitudes fallidas y los reintentos dos veces para enviar las solicitudes al extremo.