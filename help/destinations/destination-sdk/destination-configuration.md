---
description: Esta configuración le permite indicar información básica como el nombre de destino, la categoría, la descripción, el logotipo, etc. Los ajustes de esta configuración también determinan cómo se autentican los usuarios de Experience Platform en el destino, cómo aparece en la interfaz de usuario de Experience Platform y las identidades que se pueden exportar al destino.
title: Opciones de configuración de destino de streaming para Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 3%

---

# Configuración de destino de streaming {#destination-configuration}

## Información general {#overview}

Esta configuración le permite indicar información esencial para su destino de flujo continuo, como el nombre de destino, categoría, descripción, etc. Los ajustes de esta configuración también determinan cómo se autentican los usuarios de Experience Platform en el destino, cómo aparece en la interfaz de usuario de Experience Platform y las identidades que se pueden exportar al destino.

Esta configuración también conecta las otras configuraciones necesarias para que funcione el destino (servidor de destino y metadatos de audiencia) con esta. Lea cómo puede hacer referencia a las dos configuraciones en una [más abajo](./destination-configuration.md#connecting-all-configurations).

Puede configurar la funcionalidad descrita en este documento utilizando `/authoring/destinations` Extremo de API. Leer [Operaciones de extremo de API de destinos](./destination-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en el extremo.

## Ejemplo de configuración de streaming {#example-configuration}

Este es un ejemplo de configuración de un destino de streaming ficticio, Moviestar, que tiene puntos finales en cuatro ubicaciones en el mundo. El destino pertenece a la categoría destinos móviles.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointRegion",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "backfillHistoricalProfileData":true
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para la tarjeta de destino en el catálogo de destinos de Experience Platform. Apunte a no más de 4-5 oraciones. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` al configurar el destino por primera vez. |

{style="table-layout:auto"}

## Configuraciones de autenticación del cliente {#customer-authentication-configurations}

Esta sección de la configuración de destinos genera el [Configurar nuevo destino](/help/destinations/ui/connect-destination.md) página de la interfaz de usuario de Experience Platform, donde los usuarios se conectan con Experience Platform a las cuentas que tienen con el . Según la opción de autenticación indicada en la variable `authType` , la página del Experience Platform se genera para los usuarios de la siguiente manera:

### Autenticación del portador

Al configurar el tipo de autenticación de portador, los usuarios deben introducir el token de portador que obtienen de su destino.

![Representación de la IU con autenticación de portador](assets/bearer-authentication-ui.png)

### Autenticación OAuth 2

Los usuarios seleccionan **[!UICONTROL Conectar con destino]** para almacenar en déclencheur el flujo de autenticación de OAuth 2 en su destino, como se muestra en el ejemplo siguiente para el destino de Audiencias personalizadas de Twitter. Para obtener información detallada sobre la configuración de la autenticación OAuth 2 en el extremo de destino, lea la [Página de autenticación de Destination SDK OAuth 2](./oauth2-authentication.md).

![Representación de la interfaz de usuario con autenticación OAuth 2](assets/oauth2-authentication-ui.png)

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Cadena | Indica la configuración utilizada para autenticar a los clientes Experience Platform en el servidor. Consulte `authType` para valores aceptados. |
| `authType` | Cadena | Los valores aceptados para los destinos de flujo continuo son:<ul><li>`BASIC`. Si el destino admite la autenticación básica, establezca `"authType":"Basic"` y  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` en el [sección de envío de destino](./destination-configuration.md).</li><li>`BEARER`. Si el destino admite la autenticación del portador, establezca `"authType":"Bearer"` y  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` en el [sección de envío de destino](./destination-configuration.md).</li><li>`OAUTH2`. Si el destino admite la autenticación OAuth 2, establezca `"authType":"OAUTH2"` y agregue los campos obligatorios para OAuth 2, como se muestra en la [Página de autenticación de Destination SDK OAuth 2](./oauth2-authentication.md). Además, establezca `"authenticationRule":"CUSTOMER_AUTHENTICATION"` en el [sección de envío de destino](./destination-configuration.md).</li> |

{style="table-layout:auto"}

## Campos de datos del cliente {#customer-data-fields}

Utilice esta sección para pedir a los usuarios que rellenen campos personalizados, específicos del destino, al conectarse al destino en la interfaz de usuario de Experience Platform. La configuración se refleja en el flujo de autenticación como se muestra a continuación.

![Flujo de autenticación de campo personalizado](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>Puede acceder a las entradas de datos del cliente y utilizarlas desde los campos de datos del cliente en la creación de plantillas. Uso de la macro `{{customerData.name}}`. Por ejemplo, si pide a los usuarios que introduzcan un campo ID de cliente, con el nombre `userId`, puede acceder a él en la plantilla mediante la macro `{{customerData.userId}}`. Vea un ejemplo de cómo se utiliza un campo de datos de cliente en la dirección URL de su extremo de API, en el [configuración del servidor de destino](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer`. |
| `title` | Cadena | Indica el nombre del campo tal como lo ven los clientes en la interfaz de usuario del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `enum` | Cadena | Procesa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `pattern` | Cadena | Aplica un motivo al campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números ni guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |

{style="table-layout:auto"}

## Atributos de IU {#ui-attributes}

Esta sección hace referencia a los elementos de la interfaz de usuario de la configuración anterior que el Adobe debe utilizar para su destino en la interfaz de usuario de Adobe Experience Platform. Vea lo siguiente:

![Imagen de la configuración de atributos de IU.](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `documentationLink` | Cadena | Hace referencia a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe utilizar `http://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe active el destino y se publique la documentación. |
| `category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, consulte [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> Tenga en cuenta que actualmente solo puede seleccionar una categoría por destino. |
| `connectionType` | Cadena | `Server-to-server` es la única opción disponible actualmente. |
| `frequency` | Cadena | Se refiere al tipo de exportación de datos compatible con el destino. Valores compatibles: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style="table-layout:auto"}

## Configuración del esquema en el paso de asignación {#schema-configuration}

![Habilitar paso de asignación](./assets/enable-mapping-step.png)

Uso de los parámetros de `schemaConfig` para habilitar el paso de asignación del flujo de trabajo de activación de destino. Mediante los parámetros que se describen a continuación, puede determinar si los usuarios Experience Platform pueden asignar atributos de perfil o identidades al esquema deseado del lado del destino.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `profileFields` | Matriz | *No se muestra en la configuración de ejemplo anterior.* Cuando se añaden variables predefinidas `profileFields`, los usuarios de Experience Platform tienen la opción de asignar atributos de Platform a los atributos predefinidos del lado del destino. |
| `profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados del lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Usar siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad de Experience Platform al esquema deseado. |

{style="table-layout:auto"}

## Identidades y atributos {#identities-and-attributes}

Los parámetros de esta sección determinan qué identidades acepta su destino. Esta configuración también rellena las identidades y atributos de destinatario en la variable [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario de Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema de destino.

Debe indicar qué [!DNL Platform] identidades que los clientes pueden exportar a su destino. Algunos ejemplos son [!DNL Experience Cloud ID], correo electrónico con hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Estos valores son [!DNL Platform] áreas de nombres de identidad que los clientes pueden asignar a áreas de nombres de identidad desde el destino. También puede indicar si los clientes pueden asignar áreas de nombres personalizadas a identidades admitidas en el destino (`acceptsCustomNamespaces: true`) y si los clientes pueden asignar atributos XDM estándar a identidades admitidas por el destino (`acceptsAttributes: true`).

Las áreas de nombres de identidad no requieren una correspondencia de 1 a 1 entre [!DNL Platform] y su destino.
Por ejemplo, los clientes podrían asignar un [!DNL Platform] [!DNL IDFA] área de nombres a [!DNL IDFA] Área de nombres de su destino o pueden asignar lo mismo [!DNL Platform] [!DNL IDFA] área de nombres a [!DNL Customer ID] área de nombres en su destino.

Obtenga más información sobre las identidades en [Resumen de área de nombres de identidad](/help/identity-service/namespaces.md).

![Procesar identidades de destino en la IU](./assets/target-identities-ui.png)

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica si los clientes pueden asignar atributos de perfil estándar a la identidad que está configurando. |
| `acceptsCustomNamespaces` | Booleano | Indica si los clientes pueden configurar áreas de nombres personalizadas en el destino. |
| `transformation` | Cadena | *No se muestra en la configuración de ejemplo*. Se utiliza, por ejemplo, cuando [!DNL Platform] el cliente tiene direcciones de correo electrónico sin formato como atributo y su plataforma solo acepta correos electrónicos con hash. En este objeto, puede ver la transformación que debe aplicarse (por ejemplo, transformar el correo electrónico a minúsculas y, a continuación, hash). Para ver un ejemplo, consulte `requiredTransformation` en el [referencia de API de configuración de destino](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Indica cuál [áreas de nombres de identidad estándar](/help/identity-service/namespaces.md#standard) (por ejemplo, IDFA) los clientes pueden asignarse a la identidad que está configurando. <br> Cuando se usa `acceptedGlobalNamespaces`, puede utilizar `"requiredTransformation":"sha256(lower($))"` para escribir direcciones de correo electrónico o números de teléfono en minúsculas y hash. |

{style="table-layout:auto"}

## Envío de destino {#destination-delivery}

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema con un nombre de usuario y una contraseña, un token de portador u otro método de autenticación. Por ejemplo, seleccionaría esta opción si también seleccionara `authType: OAUTH2` o `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear un objeto de credenciales utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | El `instanceId` de la [configuración del servidor de destino](./destination-server-api.md) se utiliza para este destino. |

{style="table-layout:auto"}

## Configuración de asignación de segmentos {#segment-mapping}

![Sección de configuración de asignación de segmentos](./assets/segment-mapping-configuration.png)

Esta sección de la configuración de destino se relaciona con la forma en que los metadatos de segmento, como nombres de segmento o ID, deben compartirse entre el Experience Platform y su destino.

A través de `audienceTemplateId`, esta sección también vincula esta configuración con el [configuración de metadatos de audiencia](./audience-metadata-management.md).

Los parámetros mostrados en la configuración anterior se describen en la sección [referencia de API de extremo de destinos](./destination-configuration-api.md).

## Política de agregación {#aggregation}

![Directiva de agregación en la plantilla de configuración](./assets/aggregation-configuration.png)

Esta sección le permite establecer las directivas de agregación que Experience Platform debe utilizar al exportar datos a su destino.

Una directiva de agregación determina cómo se combinan los perfiles exportados en las exportaciones de datos. Entre las opciones disponibles se encuentran:
* Agregación del mejor esfuerzo
* Agregación configurable (se muestra en la configuración anterior)

Lea la sección sobre [uso de plantillas](./message-format.md#using-templating) y el [ejemplos de claves de agregación](./message-format.md#template-aggregation-key) para saber cómo incluir la directiva de agregación en la plantilla de transformación de mensajes en función de la directiva de agregación seleccionada.

### Agregación del mejor esfuerzo {#best-effort-aggregation}

>[!TIP]
>
>Utilice esta opción si el extremo de la API acepta menos de 100 perfiles por llamada de API.

Esta opción funciona mejor con destinos que prefieren menos perfiles por solicitud y que prefieren aceptar más solicitudes con menos datos que menos solicitudes con más datos.

Utilice el `maxUsersPerRequest` para especificar el número máximo de perfiles que puede tomar el destino en una solicitud.

### Agregación configurable {#configurable-aggregation}

Esta opción funciona mejor si prefiere tomar lotes grandes, con miles de perfiles en la misma llamada. Esta opción también le permite agregar los perfiles exportados en función de reglas de agregación complejas.

Esta opción le permite:

* Establezca el tiempo máximo y el número máximo de perfiles que deben agregarse antes de realizar una llamada API al destino.
* Agregue los perfiles exportados asignados al destino en función de lo siguiente:
   * ID del segmento;
   * Estado del segmento;
   * Identidad o grupos de identidades.

>[!NOTE]
>
>Al utilizar la opción de agregación configurable para el destino, tenga en cuenta los valores mínimo y máximo que puede utilizar para los dos parámetros `maxBatchAgeInSecs` (mínimo 1.800 y máximo 3.600) y `maxNumEventsInBatch` (mínimo 1.000, máximo 10.000).

Para obtener una explicación detallada de los parámetros de agregación, consulte la [Operaciones de extremo de API de destinos](./destination-configuration-api.md) página de referencia, donde se describe cada parámetro.

## Cualificaciones históricas del perfil {#profile-backfill}

Puede usar el complemento `backfillHistoricalProfileData` en la configuración de destinos para determinar si las cualificaciones de perfil históricas deben exportarse a su destino.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla si los datos de perfil históricos se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`: [!DNL Platform] envía los perfiles de usuario históricos aptos para el segmento antes de activarlo. </li><li> `false`: [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento después de activarlo. </li></ul> |

{style="table-layout:auto"}

## Cómo esta configuración conecta toda la información necesaria para su destino {#connecting-all-configurations}

Algunos de los ajustes de destino deben configurarse a través del [servidor de destino](./server-and-template-configuration.md) o el [configuración de metadatos de audiencia](./audience-metadata-management.md). La configuración de destino que se describe aquí conecta todas estas configuraciones haciendo referencia a las otras dos configuraciones de la siguiente manera:

* Utilice el `destinationServerId` para hacer referencia al servidor de destino y a la configuración de plantilla establecida para el destino.
* Utilice el `audienceMetadataId` para hacer referencia a la configuración de metadatos de audiencia configurada para su destino.