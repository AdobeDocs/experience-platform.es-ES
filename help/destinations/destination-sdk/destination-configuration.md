---
description: Esta configuración le permite indicar información básica como el nombre de destino, la categoría, la descripción, el logotipo y mucho más. Los ajustes de esta configuración también determinan cómo se autentican los usuarios Experience Platform en el destino, cómo aparece en la interfaz de usuario del Experience Platform y las identidades que se pueden exportar al destino.
title: Opciones de configuración de destino para el SDK de destino
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 4%

---

# Configuración de destino {#destination-configuration}

## Información general {#overview}

Esta configuración le permite indicar información básica como el nombre de destino, la categoría, la descripción, el logotipo y mucho más. Los ajustes de esta configuración también determinan cómo se autentican los usuarios Experience Platform en el destino, cómo aparece en la interfaz de usuario del Experience Platform y las identidades que se pueden exportar al destino.

Puede configurar la funcionalidad descrita en este documento utilizando el extremo `/authoring/destinations` de la API. Lea [Destinations API endpoint operations](./destination-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Ejemplo de configuración {#example-configuration}

A continuación se muestra un ejemplo de configuración para un destino ficticio, Moviestar, que tiene extremos en cuatro ubicaciones del mundo. El destino pertenece a la categoría destinos móviles . Las secciones siguientes desglosan cómo se construye esta configuración.

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
         "name":"endpointsInstance",
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
         "acceptsCustomNamespaces":true
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
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
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
   }
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo de Experience Platform. |
| `description` | Cadena | Proporcione una descripción que el Adobe utilizará en el catálogo de destinos del Experience Platform para su tarjeta de destino. Apunte a no más de 4-5 frases. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Utilice `TEST` la primera vez que configure el destino. |

## Configuraciones de autenticación de clientes {#customer-authentication-configurations}

Esta sección genera la página de cuenta en la interfaz de usuario de Experience Platform, donde los usuarios se conectan Experience Platform a las cuentas que tienen con el destino. Según la opción de autenticación que indique en el campo `authType`, la página Experience Platform se genera para los usuarios de la siguiente manera:

**Autenticación del portador**

Los usuarios deben introducir el token al portador que obtienen de su destino.

![Renderización de la interfaz de usuario con autenticación del portador](./assets/bearer-authentication-ui.png)

**Autenticación OAuth 2**

Los usuarios seleccionan **[!UICONTROL Conectarse al destino]** para almacenar en déclencheur el flujo de autenticación de OAuth 2 en el destino.

![Renderización de la interfaz de usuario con autenticación OAuth 2](./assets/oauth2-authentication-ui.png)


| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Cadena | Indica la configuración utilizada para autenticar a los clientes Experience Platform en el servidor. Consulte `authType` a continuación para conocer los valores aceptados. |
| `authType` | Cadena | Los valores aceptados son `OAUTH2, BEARER`. <br><ul><li> Si el destino admite la autenticación OAuth 2, seleccione el valor `OAUTH2` y añada los campos obligatorios para OAuth 2, como se muestra en la página de autenticación del SDK de destino OAuth 2. Además, debe seleccionar `authenticationRule=CUSTOMER_AUTHENTICATION` en la sección [envío de destino](./destination-configuration.md). </li><li>Para la autenticación del portador, seleccione `BEARER` y `authenticationRule=CUSTOMER_AUTHENTICATION` en la sección [envío de destino](./destination-configuration.md).</li></ul> |

## Campos de datos del cliente {#customer-data-fields}

Esta sección permite a los socios introducir campos personalizados. En la configuración de ejemplo anterior, `customerDataFields` requiere que los usuarios seleccionen un punto final en el flujo de autenticación e indiquen su ID de cliente con el destino. La configuración se refleja en el flujo de autenticación como se muestra a continuación:

![Flujo de autenticación de campo personalizado](./assets/custom-field-authentication-flow.png)

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer`. |
| `title` | Cadena | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `enum` | Cadena | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `pattern` | Cadena | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |

## Atributos de interfaz de usuario {#ui-attributes}

Esta sección se refiere a los elementos de IU de la configuración anterior que el Adobe debe utilizar para el destino en la interfaz de usuario de Adobe Experience Platform. Consulte a continuación:

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `documentationLink` | Cadena | Se refiere a la página de documentación de [Destinations Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Utilice `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe utilizar `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Cadena | `Server-to-server` actualmente es la única opción disponible. |
| `frequency` | Cadena | `Streaming` actualmente es la única opción disponible. |

## Configuración del esquema en el paso de asignación {#schema-configuration}

![Habilitar paso de asignación](./assets/enable-mapping-step.png)

Utilice los parámetros de `schemaConfig` para habilitar el paso de asignación del flujo de trabajo de activación de destino. Mediante los parámetros que se describen a continuación, puede determinar si los usuarios Experience Platform pueden asignar atributos de perfil o identidades al esquema deseado en el lado del destino.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `profileFields` | Matriz | *No se muestra en la configuración de ejemplo anterior.* Al agregar predefinidos  `profileFields`, los usuarios tendrán la opción de asignar atributos de Experience Platform a los atributos predefinidos en el lado del destino. |
| `profileRequired` | Booleano | Utilice `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en el lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Utilice siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Utilice `true` si los usuarios deben poder asignar áreas de nombres de identidad del Experience Platform al esquema deseado. |

## Identidades y atributos {#identities-and-attributes}

Los parámetros de esta sección determinan cómo se rellenan las identidades y los atributos de destino en el paso de asignación de la interfaz de usuario del Experience Platform, donde los usuarios asignan sus esquemas XDM al esquema en el destino.

Adobe necesita saber qué [!DNL Platform] identidades podrán exportar los clientes a su destino. Algunos ejemplos son [!DNL Experience Cloud ID], correo electrónico con hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Estos valores son [!DNL Platform] áreas de nombres de identidad que los clientes pueden asignar a áreas de nombres de identidad desde su destino.

Las áreas de nombres de identidad no requieren una correspondencia de 1 a 1 entre [!DNL Platform] y el destino.
Por ejemplo, los clientes podrían asignar un espacio de nombres [!DNL Platform] [!DNL IDFA] a un espacio de nombres [!DNL IDFA] desde el destino, o pueden asignar el mismo espacio de nombres [!DNL Platform] [!DNL IDFA] a un espacio de nombres [!DNL Customer ID] en el destino.

Obtenga más información en la [descripción general del área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es).

![Representar identidades de objetivo en la interfaz de usuario](./assets/target-identities-ui.png)

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica si el destino acepta atributos de perfil estándar. Normalmente, estos atributos se resaltan en la documentación de nuestros socios. |
| `acceptsCustomNamespaces` | Booleano | Indica si los clientes pueden configurar áreas de nombres personalizadas en el destino. |
| `allowedAttributesTransformation` | Cadena | *No se muestra en la configuración* de ejemplo. Se utiliza, por ejemplo, cuando el cliente [!DNL Platform] tiene direcciones de correo electrónico simples como atributo y la plataforma solo acepta correos electrónicos con hash. Aquí es donde proporcionaría la transformación que debe aplicarse (por ejemplo, transformar el correo electrónico a minúsculas y luego a hash). |
| `acceptedGlobalNamespaces` | - | *No se muestra en la configuración* de ejemplo. Se utiliza para casos en los que la plataforma acepta [áreas de nombres de identidad estándar](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por ejemplo, IDFA), por lo que puede restringir a los usuarios de Platform a que solo seleccionen estas áreas de nombres de identidad. |

## Entrega de destino {#destination-delivery}

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationRule` | Cadena | Indica cómo se conectan los clientes [!DNL Platform] con el destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilice `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en su sistema mediante un nombre de usuario y contraseña, un token al portador u otro método de autenticación. Por ejemplo, puede seleccionar esta opción si también selecciona `authType: OAUTH2` o `authType:BEARER` en `customerAuthenticationConfigurations`. </li><li> Utilice `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre el Adobe y el destino y el cliente [!DNL Platform] no necesita proporcionar ninguna credencial de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la configuración [Credentials](./credentials-configuration.md). </li><li>Utilice `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | `instanceId` de la [configuración del servidor de destino](./destination-server-api.md) utilizada para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla si los datos del perfil histórico se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`:  [!DNL Platform] envía los perfiles de usuario históricos que cumplen los requisitos para el segmento antes de que se active el segmento. </li><li> `false`:  [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento una vez activado el segmento. </li></ul> |

## Configuración de asignación de segmentos {#segment-mapping}

![Sección de configuración de asignación de segmentos](./assets/segment-mapping-configuration.png)

Esta sección de la configuración de destino se relaciona con la forma en que los metadatos de segmento, como los nombres o ID de segmentos, deben compartirse entre el Experience Platform y el destino.

A través de `audienceTemplateId`, esta sección también vincula esta configuración con la [configuración de metadatos de audiencia](./audience-metadata-management.md).

Los parámetros que se muestran en la configuración anterior se describen en la [referencia de API de extremo de destinos](./destination-configuration-api.md).

## Política de agregación {#aggregation}

![Directiva de agregación en la plantilla de configuración](./assets/aggregation-configuration.png)

Esta sección le permite establecer las políticas de agregación que utilizará el Experience Platform al exportar datos a su destino.

Una política de agregación determina cómo se combinan los perfiles exportados en las exportaciones de datos. Entre las opciones disponibles se encuentran:
* Mejor agregación de esfuerzos
* Agregación configurable (tal y como se muestra en la configuración anterior)

### Mejor agregación de esfuerzos {#best-effort-aggregation}

>[!TIP]
>
>Utilice esta opción si el extremo de la API acepta menos de 100 perfiles por llamada de API.

Esta opción funciona mejor para destinos que prefieren menos perfiles por solicitud y prefieren tomar más solicitudes con menos datos que menos solicitudes con más datos.

Utilice el parámetro `maxUsersPerRequest` para especificar el número máximo de perfiles que el destino puede tener en una solicitud.

### Agregación configurable {#configurable-aggregation}

Esta opción funciona mejor si prefiere tomar lotes grandes, con miles de perfiles en la misma llamada. Esta opción también le permite agregar los perfiles exportados en función de reglas de agregación complejas.

Esta opción le permite:
* Establezca el tiempo y el número máximos de perfiles que se agregarán antes de que se realice una llamada de API al destino.
* Agregue los perfiles exportados asignados al destino en función de:
   * ID de segmento
   * estado del segmento
   * identidad o grupos de identidades

Para obtener explicaciones detalladas de los parámetros de agregación, consulte la página de referencia [Destinations API endpoint operations](./destination-configuration-api.md), donde se describe cada parámetro.

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
