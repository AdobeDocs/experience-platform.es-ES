---
keywords: streaming; destino HTTP
title: Conexión de API HTTP
description: Utilice el destino de la API HTTP en Adobe Experience Platform para enviar datos de perfil al extremo HTTP de terceros para ejecutar sus propios análisis o realizar cualquier otra operación que pueda necesitar en los datos de perfil exportados fuera de Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 678f80445212edc1edd3f4799999990ddcc2a039
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 8%

---

# Conexión de API HTTP

## Información general {#overview}

>[!IMPORTANT]
>
> Este destino solo está disponible para los clientes de [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es).

El destino de la API HTTP es un destino de flujo [!DNL Adobe Experience Platform] que le ayuda a enviar datos de perfil a extremos HTTP de terceros.

Para enviar datos de perfil a los extremos HTTP, primero debe [conectarse al destino](#connect-destination) en [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

El destino de la API HTTP permite exportar datos de perfil XDM y audiencias a extremos HTTP genéricos. Aquí puede ejecutar sus propios análisis o realizar cualquier otra operación que pueda necesitar en los datos de perfil exportados fuera de Experience Platform.

Los extremos HTTP pueden ser sistemas propios de los clientes o soluciones de terceros.

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
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla de asignación de [flujo de trabajo de activación de destino](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para utilizar el destino de la API HTTP para exportar datos desde Experience Platform, debe cumplir los siguientes requisitos previos:

* Debe tener un extremo HTTP que admita la API de REST.
* El extremo HTTP debe admitir el esquema de perfil de Experience Platform. No se admite ninguna transformación a un esquema de carga útil de terceros en el destino de la API HTTP. Consulte la sección [datos exportados](#exported-data) para ver un ejemplo del esquema de salida de Experience Platform.
* El extremo HTTP debe admitir encabezados.

>[!TIP]
>
> También puede usar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar una integración y enviar datos de perfil de Experience Platform a un extremo HTTP.

## Compatibilidad con el protocolo mTLS y certificado {#mtls-protocol-support}

Puede usar [!DNL Mutual Transport Layer Security] ([!DNL mTLS]) para garantizar una seguridad mejorada en las conexiones salientes a las conexiones de destino de la API HTTP.

[!DNL mTLS] es un método de seguridad de extremo a extremo para la autenticación mutua que garantiza que ambas partes que comparten información son quienes dicen ser antes de que se compartan los datos. [!DNL mTLS] incluye un paso adicional en comparación con [!DNL TLS], en el cual el servidor también solicita el certificado del cliente y lo verifica al final.

Si desea usar [!DNL mTLS] con [!DNL HTTP API] destinos, la dirección de servidor que puso en la página [detalles de destino](#destination-details) debe tener los protocolos [!DNL TLS] deshabilitados y solamente [!DNL mTLS] habilitados. Si el protocolo [!DNL TLS] 1.2 sigue habilitado en el extremo, no se envía ningún certificado para la autenticación del cliente. Esto significa que para usar [!DNL mTLS] con su destino [!DNL HTTP API], el extremo del servidor de &quot;recepción&quot; debe ser un extremo de conexión habilitado solo para [!DNL mTLS].

### Recuperar e inspeccionar detalles del certificado {#certificate}

Si desea inspeccionar los detalles del certificado, como [!DNL Common Name] (CN) y [!DNL Subject Alternative Names] (SAN), para la validación adicional de terceros, utilice la API para recuperar el certificado y extraer esos campos de la respuesta.

Consulte la [documentación de extremo de certificado público](../../../data-governance/mtls-api/public-certificate-endpoint.md) para obtener más información.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allowlist}

Para cumplir los requisitos de seguridad y cumplimiento de normas de los clientes, Experience Platform proporciona una lista de direcciones IP estáticas que puede lista de permitidos para el destino de la API HTTP. Consulte la [lista de permitidos de direcciones IP para destinos de streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obtener la lista completa de direcciones IP para lista de permitidos.

## Tipos de autenticación admitidos {#supported-authentication-types}

El destino de la API HTTP admite varios tipos de autenticación en el extremo HTTP:

* Punto final HTTP sin autenticación;
* Autenticación de token de portador;
* Autenticación de [credenciales de cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con el formulario de cuerpo, con [!DNL client ID], [!DNL client secret] y [!DNL grant type] en el cuerpo de la solicitud HTTP, como se muestra en el ejemplo siguiente.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenciales de cliente de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) con autorización básica, con un encabezado de autorización que contiene [!DNL client ID] y [!DNL client secret] con codificación de dirección URL.

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concesión de contraseña de OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Conexión al destino {#connect-destination}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). Al conectarse a este destino, debe proporcionar la siguiente información:

### Información de autenticación {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo de credenciales del cliente"
>abstract="Seleccione **Formulario de cuerpo codificado** para incluir el ID de cliente y el secreto de cliente en el cuerpo de la solicitud o **Autorización básica** para incluir el ID de cliente y el secreto de cliente en un encabezado de autorización. Vea ejemplos en la documentación."

#### Autenticación de token de portador {#bearer-token-authentication}

Si selecciona el tipo de autenticación **[!UICONTROL Token de portador]** para conectarse a su extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectarse al destino]**:

![Imagen de la pantalla de la interfaz de usuario donde puede conectarse al destino de la API HTTP mediante la autenticación de token de portador.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token de portador]**: inserte el token de portador para autenticarse en la ubicación HTTP.

#### Sin autenticación {#no-authentication}

Si selecciona el tipo de autenticación **[!UICONTROL None]** para conectarse al extremo HTTP:

![Imagen de la pantalla de la interfaz de usuario donde puede conectarse al destino de la API HTTP sin utilizar autenticación.](../../assets/catalog/http/http-api-authentication-none.png)

Cuando selecciona esta apertura de autenticación, solo necesita seleccionar **[!UICONTROL Conectarse al destino]** y se establece la conexión con su extremo.

#### Autenticación de contraseña de OAuth 2 {#oauth-2-password-authentication}

Si selecciona el tipo de autenticación **[!UICONTROL OAuth 2 Password]** para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

![Imagen de la pantalla de la interfaz de usuario donde puede conectarse al destino de la API HTTP mediante OAuth 2 con autenticación de contraseña.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL de token de acceso]**: URL del lado del usuario que emite tokens de acceso y, opcionalmente, tokens de actualización.
* **[!UICONTROL ID de cliente]**: El [!DNL client ID] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Secreto de cliente]**: El [!DNL client secret] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para acceder a su extremo HTTP.
* **[!UICONTROL Contraseña]**: La contraseña para acceder a su extremo HTTP.

#### Autenticación de credenciales de cliente de OAuth 2 {#oauth-2-client-credentials-authentication}

Si selecciona el tipo de autenticación **[!UICONTROL Credenciales del cliente de OAuth 2]** para conectarse al extremo HTTP, introduzca los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

![Imagen de la pantalla de la interfaz de usuario donde puede conectarse al destino de la API HTTP mediante OAuth 2 con autenticación de credenciales de cliente.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>Al usar la autenticación [!UICONTROL Credenciales del cliente de OAuth 2], la [!UICONTROL URL del token de acceso] puede tener un máximo de un parámetro de consulta. Si agrega una [!UICONTROL URL de token de acceso] con más parámetros de consulta, pueden surgir problemas al conectarse al punto de conexión.

* **[!UICONTROL URL de token de acceso]**: URL del lado del usuario que emite tokens de acceso y, opcionalmente, tokens de actualización.
* **[!UICONTROL ID de cliente]**: El [!DNL client ID] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Secreto de cliente]**: El [!DNL client secret] que su sistema asigna a Adobe Experience Platform.
* **[!UICONTROL Tipo de credenciales de cliente]**: seleccione el tipo de concesión de credenciales de cliente de OAuth2 admitida por el extremo:
   * **[!UICONTROL Formulario de cuerpo codificado]**: En este caso, [!DNL client ID] y [!DNL client secret] se incluyen *en el cuerpo de la solicitud* enviada a su destino. Para ver un ejemplo, consulte la sección [Tipos de autenticación admitidos](#supported-authentication-types).
   * **[!UICONTROL Autorización básica]**: En este caso, [!DNL client ID] y [!DNL client secret] se incluyen *en un encabezado `Authorization`* después de ser codificados en Base64 y enviados a su destino. Para ver un ejemplo, consulte la sección [Tipos de autenticación admitidos](#supported-authentication-types).

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Encabezados"
>abstract="Introduzca los encabezados personalizados que desea incluir en las llamadas de destino, siguiendo este formato: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Punto final HTTP"
>abstract="Dirección URL del punto final HTTP al que desea enviar los datos de perfil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Incluir nombres de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya los nombres del público que está exportando. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Incluir marcas de tiempo de segmentos"
>abstract="Alterne si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron los públicos, así como la marca de tiempo UNIX cuando los públicos se asignaron al destino para la activación. Vea la documentación de un ejemplo de exportación de datos con esta opción seleccionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parámetros de consulta"
>abstract="De forma opcional, puede añadir parámetros de consulta a la dirección URL del punto final HTTP. Aplique este formato a los parámetros de consulta que utilice: `parameter1=value&parameter2=value`."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino HTTP.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nombre]**: escriba un nombre para reconocer este destino en el futuro.
* **[!UICONTROL Descripción]**: escribe una descripción que te ayudará a identificar este destino en el futuro.
* **[!UICONTROL Encabezados]**: escriba los encabezados personalizados que desee incluir en las llamadas de destino, con este formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Punto final HTTP]**: Dirección URL del punto final HTTP al que desea enviar los datos de perfil.
* **[!UICONTROL Parámetros de consulta]**: de forma opcional, puede agregar parámetros de consulta a la dirección URL del extremo HTTP. Aplique este formato a los parámetros de consulta que utilice: `parameter1=value&parameter2=value`.
* **[!UICONTROL Incluir nombres de segmentos]**: Cambie la opción si desea que la exportación de datos incluya los nombres de las audiencias que está exportando. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la sección [Datos exportados](#exported-data) más abajo.
* **[!UICONTROL Incluir marcas de tiempo de segmentos]**: actívela si desea que la exportación de datos incluya la marca de tiempo UNIX cuando se crearon y actualizaron las audiencias, así como la marca de tiempo UNIX cuando las audiencias se asignaron al destino para la activación. Para ver un ejemplo de exportación de datos con esta opción seleccionada, consulte la sección [Datos exportados](#exported-data) más abajo.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* [La evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) no se admite actualmente en las exportaciones al destino de la API HTTP. [Más información](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consulte [Activar datos de audiencia en destinos de exportación de perfiles de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#attributes}

En el paso [[!UICONTROL Seleccionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

## Comportamiento de exportación de perfil {#profile-export-behavior}

Experience Platform optimiza el comportamiento de exportación de perfiles a su destino de API HTTP para exportar solo datos a su punto final de API cuando se han producido actualizaciones relevantes de un perfil tras la calificación de la audiencia u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó mediante un cambio en el abono a audiencia de al menos una de las audiencias asignadas al destino. Por ejemplo, el perfil cumple los requisitos de una de las audiencias asignadas al destino o ha salido de una de las audiencias asignadas al destino.
* La actualización de perfil se determinó mediante un cambio en el [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, a un perfil que ya estaba cualificado para una de las audiencias asignadas al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si una audiencia asignada al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación {#what-determines-export-what-is-included}

Con respecto a los datos que se exportan para un perfil determinado, es importante entender los dos conceptos diferentes de *qué determina una exportación de datos a su destino de API HTTP* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven de referencia para una exportación de destino. Esto significa que si el estado de `segmentMembership` de un perfil cambia a `realized` o `exiting`, o si se actualiza cualquier atributo asignado, se iniciará una exportación de destino.</li><li>Dado que las identidades no se pueden asignar actualmente a destinos de API HTTP, los cambios en cualquier identidad de un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es el mismo valor o no. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>El objeto `segmentMembership` incluye el segmento asignado en el flujo de datos de activación, para el cual el estado del perfil ha cambiado después de un evento de calificación o salida de segmento. Tenga en cuenta que otros segmentos no asignados para los que el perfil cumple los requisitos pueden formar parte de la exportación de destino, si estos segmentos pertenecen a la misma [política de combinación](/help/profile/merge-policies/overview.md) que el segmento asignado en el flujo de datos de activación. </li><li>También se incluyen todas las identidades en el objeto `identityMap` (Experience Platform no admite actualmente la asignación de identidades en el destino de la API HTTP).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

Por ejemplo, considere este flujo de datos para un destino HTTP en el que se seleccionen tres audiencias en el flujo de datos y se asignen cuatro atributos al destino.

![Ejemplo de flujo de datos de destino de API HTTP.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que califique para uno de los *tres segmentos asignados* o que salga de él. Sin embargo, en la exportación de datos, en el objeto `segmentMembership` (consulte la sección [Datos exportados](#exported-data) más abajo), podrían aparecer otras audiencias no asignadas, si ese perfil en particular es miembro de ellas y si comparten la misma política de combinación que la audiencia que activó la exportación. Si un perfil se califica para el segmento **Cliente con DeLorean Cars**, pero también es miembro de los segmentos de la película **Visto &quot;Volver al futuro&quot;** y **fans de ciencia ficción**, entonces estas otras dos audiencias también estarán presentes en el objeto `segmentMembership` de la exportación de datos, aunque no estén asignadas en el flujo de datos, si comparten la misma política de combinación con el segmento **Cliente con DeLorean Cars**.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados anteriormente determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

## Relleno de datos históricos {#historical-data-backfill}

Al agregar una audiencia nueva a un destino existente o al crear un destino nuevo y asignarle audiencias, Experience Platform exporta al destino los datos de calificación de audiencias históricas. Los perfiles que cumplen los requisitos para la audiencia *antes de* que la audiencia se agregó al destino se exportan al destino en un plazo aproximado de una hora.

## Datos exportados {#exported-data}

Los datos de [!DNL Experience Platform] exportados llegan a su destino [!DNL HTTP] en formato JSON. Por ejemplo, la exportación siguiente contiene un perfil que se ha clasificado para un segmento determinado, es miembro de otros dos segmentos y ha salido de otro segmento. La exportación también incluye el atributo de perfil nombre, apellidos, fecha de nacimiento y dirección de correo electrónico personal. Las identidades de este perfil son ECID y correo electrónico.

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