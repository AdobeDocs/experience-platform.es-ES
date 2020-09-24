---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Trabajar con el tiempo de ejecución del servicio de decisiones mediante API
topic: tutorial
type: Tutorial
description: 'Este documento proporciona un tutorial para trabajar con los servicios de tiempo de ejecución de Decisioning Service mediante las API de Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---


# Trabajar con el tiempo de ejecución del servicio de decisiones mediante API

Este documento proporciona un tutorial para trabajar con los servicios de tiempo de ejecución de [!DNL Decisioning Service] utilizar las API de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los [!DNL Experience Platform] servicios que intervienen en la toma de decisiones y la determinación de la siguiente mejor oferta para presentar durante las experiencias de los clientes. Antes de comenzar este tutorial, consulte la documentación siguiente:

- [[!Servicio de decisiones DNL]](./../home.md): Proporciona el marco para agregar y eliminar ofertas y crear algoritmos para elegir lo mejor que se puede presentar durante la experiencia del cliente.
- [[!Modelo de datos de experiencia DNL (XDM)]](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [[!Lenguaje de Consulta de Perfil DNL (PQL)]](../../segmentation/pql/overview.md): PQL se utiliza para definir reglas y filtros.
- [Administrar reglas y objetos de decisiones mediante API](./entities.md): Antes de utilizar el tiempo de ejecución de los servicios de decisiones, deberá configurar las entidades relacionadas.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a las [!DNL Platform] API de forma satisfactoria.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../tutorials/authentication.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

También es necesario para solicitudes en tiempo de ejecución:

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID` es una cadena en formato UUID que es única globalmente y no debe reutilizarse para distintas llamadas de API

[!DNL Decisioning Service] está controlado por una serie de objetos comerciales que están relacionados entre sí. Todos los objetos comerciales se almacenan en el repositorio de objetos comerciales, el repositorio de objetos principales XDM. [!DNL Platform’s] Una característica clave de este repositorio es que las API son ortogonales al tipo de objeto comercial. En lugar de utilizar una API de POST, GET, PUT, PATCH o DELETE que indique el tipo de recurso en su extremo de API, solo hay 6 extremos genéricos, pero aceptan o devuelven un parámetro que indica el tipo de objeto cuando se necesita esa desambición. El esquema debe estar registrado en el repositorio, pero más allá de eso el repositorio se puede utilizar para un conjunto de tipos de objetos de composición abierta.

Las rutas de extremo de todas las API de repositorio de objetos principales XDM inicio con `https://platform.adobe.io/data/core/ode/`.

El primer elemento de ruta que sigue al punto final es el `containerId`. Este identificador se obtiene a través del extremo raíz del repositorio de objetos principales XDM `GET https://platform.adobe.io/data/core/xcore/`.

## Compilación de modelos de decisión

La activación de las entidades lógicas del negocio se produce de manera automática y continua. Tan pronto como se guarde una nueva opción en el repositorio y se marque como &quot;aprobada&quot;, será un candidato para la inclusión del conjunto de opciones disponibles. Tan pronto como se actualice una regla de decisión, el conjunto de reglas se volverá a montar y se preparará para la ejecución en tiempo de ejecución. En este paso de activación automática, se evaluarán todas las restricciones definidas por la lógica empresarial que no dependan del contexto de tiempo de ejecución. Los resultados de este paso de activación se envían a una caché en la que están disponibles para el motor de ejecución [!DNL Decisioning Service] .

### Efectos de las colocaciones, filtros y estados del ciclo vital

Las ofertas se crean continuamente, se producen cambios en su estado de ciclo vital o pueden obtener nuevas representaciones de contenido. El filtro de oferta de una actividad puede cambiar, coincidir o filtrar ofertas cuyos conjuntos de etiquetas se han actualizado. Este proceso puede estar bastante involucrado y las aplicaciones y los servicios necesitan saber cuál será el conjunto de candidatos resultante de una actividad. El motor de ejecución de decisiones proporciona una API de actividad a ofertas que filtros ofertas que no están aprobadas, que no coinciden con el filtro de oferta o que no tienen una representación para la ubicación a la que hace referencia la actividad.

**Solicitud**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Respuesta**

El parámetro `activityId` se puede repetir en la dirección URL y se pueden proporcionar hasta 30 referencias de actividad diferentes en una solicitud. La respuesta será útil para detectar cualquier circunstancia inesperada resultante de la configuración y tendrá un aspecto similar al siguiente:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Hay un pequeño retraso de unos segundos entre el momento en que se actualizaron los objetos y el momento en que la respuesta de API refleja la asignación de actividad a ofertas. La revisión de cada objeto se proporciona en la respuesta para que los clientes puedan comprobar si hay una actualización de los objetos que no se han reflejado.

### API de diagnóstico y solución de problemas

Las actividades, ofertas y reglas de elegibilidad se compilan en un formato interno (catálogo de ofertas de tiempo de ejecución) que utiliza el motor de ejecución del servicio de decisiones. La compilación puede detectar errores que no fueron detectados por las comprobaciones realizadas cuando se almacenaron los objetos y se establecieron vínculos en el repositorio de objetos principales XDM.

Se proporciona una API de diagnóstico para obtener los errores de compilación que se produjeron en ese paso y, en caso de que no haya errores para obtener información sobre cuándo se recompilaron por última vez las reglas y actividades.

**Solicitud**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

El único parámetro para esta llamada de API es `containerId`. Los resultados son todas las actualizaciones de todos los clientes que han modificado las reglas de decisión, ofertas, actividades o filtros de oferta en ese contenedor. Hay un pequeño retraso de unos segundos entre el momento en que se actualizaron los objetos y el momento en que finaliza la compilación. La última marca de tiempo de actualización y los errores se devuelven en la respuesta a la llamada de diagnóstico.

**Respuesta**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## Llamadas a la API de REST para ejecutar decisiones

La API de REST es una de las rutas para que las aplicaciones que se ejecutan sobre [!DNL Platform] la base obtengan la siguiente mejor experiencia en función de las reglas, modelos y restricciones que la organización ha establecido para sus usuarios. Las aplicaciones envían una de las identidades del perfil (ID de perfil y Área de nombres de identidad) que [!DNL Decisioning Service] buscará el perfil y la información se utilizará para aplicar la lógica empresarial. Se pueden pasar datos de contexto adicionales a la solicitud y, si se especifican en las reglas comerciales, se incluirán en los datos para tomar la decisión.

Las aplicaciones pueden lograr un mejor rendimiento al solicitar una decisión de hasta 30 actividades a la vez. Los URI de las actividades se pasan en la misma solicitud. La API de REST es sincrónica y devolverá las opciones propuestas para todas esas actividades o la opción de reserva si ninguna opción de personalización satisface las restricciones.

Es posible que dos actividades diferentes tengan la misma opción que sus &quot;mejores&quot;. Para evitar la repetición de una experiencia compuesta, de forma predeterminada, [!DNL Decisioning Service] se arbitran entre las actividades a las que se hace referencia en la misma solicitud. El arbitraje significa que para cada una de las actividades se tienen en cuenta sus opciones principales de N, pero no se propone ninguna opción más de una vez en todas esas actividades. Si dos actividades tienen la misma opción de clasificación superior, se elegirá una de ellas para que utilice su segunda opción o la tercera opción, y así sucesivamente. Estas reglas de anulación de duplicación intentan evitar que cualquiera de las actividades utilice su opción de reserva.

La solicitud de decisión contiene los argumentos de la solicitud del POST. El cuerpo tiene el formato de valor de encabezado `Content-Type` JSON `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

El esquema y la versión de la solicitud compatibles en este momento son `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. En el futuro, se proporcionarán esquemas o versiones de solicitudes adicionales.

**Solicitud**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Cuando el valor de esta propiedad opcional se establece en true, la solicitud de decisión obedece a restricciones de limitación pero no las arrastra realmente, se espera que el llamante nunca tenga la intención de presentar la propuesta al perfil. La [!DNL Decisioning Service] propuesta no registrará la propuesta como un evento oficial de decisión XDM y no aparecerá en los conjuntos de datos de sistema de informes. El valor predeterminado de esta propiedad es false y, cuando se omite la propiedad, la decisión no se considera una ejecución de prueba y, por lo tanto, se presentará al usuario final.
- **`xdm:validateContextData`** - Esta propiedad opcional activa o desactiva la validación de los datos de contexto. Si la validación está activada, para cada elemento de datos de contexto proporcionado, el esquema (basado en el `@type` campo) se recuperará del Registro XDM y el `xdm:data` objeto se validará en él.

La solicitud por este esquema contiene una matriz de URI que hace referencia a actividades de oferta, una identidad de perfil y una matriz de elementos de datos de contexto:

- **`xdm:offerActivities`** - Esta propiedad obligatoria es una matriz de objetos donde cada elemento contiene datos sobre la actividad de oferta. La actividad de oferta tiene las siguientes propiedades:
   - **`xdm:offerActivity`** - Identificador único (URI) de la actividad. Es el valor de la `@id` propiedad de la actividad de oferta.
- **`xdm:identityMap`** - Una propiedad obligatoria que contiene un objeto JSON que cumple con el esquema XDM `https://ns.adobe.com/xdm/context/identitymap`. La propiedad define un mapa donde la clave es un código de Área de nombres de identidad y el valor es una lista de identificadores de usuario final en la Área de nombres dada. Si m.
- **`xdm:contextData`** - Una propiedad opcional que contiene elementos que se describen mediante una referencia a su esquema. Cada elemento de datos de contexto de la matriz debe tener las siguientes propiedades:
   - **`@type`** - Una propiedad obligatoria que hace referencia al esquema XDM del objeto en este elemento.
   - **`xdm:data`** - Una propiedad obligatoria que contiene las propiedades del objeto según el esquema XDM proporcionado en la `@type` propiedad.

## Datos de contexto dinámicos en la toma de decisiones de solicitudes

La sección anterior indicaba cómo se pueden pasar los objetos XDM a una solicitud de decisión. A continuación se muestra un ejemplo de la matriz de objetos de contexto:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

El esquema debe haber sido construido por su organización. Para obtener más información sobre la construcción de esquemas, consulte el Tutorial [del Editor de](../../xdm/tutorials/create-schema-ui.md)Esquemas. Tu esquema estará en una Área de nombres `https://ns.adobe.com/{TENANT_ID}/schemas`.

La guía [para desarrolladores de la API de](../../xdm/tutorials/create-schema-api.md) Esquema Registry explica cómo se puede acceder a los esquemas mediante programación y cómo un desarrollador obtiene el ID de inquilino y el identificador numérico de su esquema. El número de versión es obligatorio y también lo proporcionan las API del Registro de esquema.

Un esquema definido por una organización generalmente tendrá una propiedad raíz denominada `_{TENANT_ID}`, también denominada cadena de Área de nombres del inquilino.
Tenga en cuenta que las propiedades utilizadas desde un componente de esquema global como _`https://ns.adobe.com/xdm/context/product` tienen un prefijo de Área de nombres `xdm:`. En este caso, la propiedad definida por la organización `productDetails` se construyó con ese tipo de datos. Mientras que las propiedades del inquilino están anidadas en una propiedad con el nombre de la Área de nombres del inquilino, los tipos de datos disponibles globalmente utilizan el prefijo reservado `xdm:` para evitar conflictos de nombres de propiedad.

Se pueden enumerar varios objetos de datos en la `xdm:contextData` propiedad. Cada objeto debe identificar su tipo a través de la `@type` propiedad.
Los valores de los objetos de datos de contexto están disponibles para su uso en expresiones PQL, por ejemplo, en la condición de una regla de elegibilidad. El objeto de datos de contexto debe abordarse mediante la expresión de referencia de ruta especial `@{schemaId}`. Las expresiones que siguen a esta expresión de referencia son expresiones de ruta normales que acceden a las propiedades del objeto de datos:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

En el ejemplo anterior, la variable `p` está iterando sobre la matriz de objetos marcados con el `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Tenga en cuenta que la sintaxis de PQL no utiliza prefijos en los nombres de propiedades. De forma predeterminada, se hace referencia a las propiedades globales sin el `xdm:` prefijo . Las propiedades que define su organización están anidadas en una propiedad **adicional** con el nombre de la Área de nombres del inquilino (en el ejemplo indicado por la variable `{TENANT_ID}`). Para poder hacer referencia a las propiedades definidas de forma personalizada directamente, la variable `p` está enlazada al resultado de la ruta que hace referencia a la propiedad de anidación adicional.

## Uso de registros de perfiles

Todos los registros de las entidades de evento de perfil y experiencia ya se administran en el almacén de perfiles. Al transmitir una o más identidades de perfil a la solicitud, el perfil de esas identidades será identificado y buscado desde la tienda. Los datos están disponibles automáticamente para las reglas de decisión y los modelos evaluados por la estrategia de decisión.

Para recuperar los registros de perfil y experiencia, se aplica la directiva de combinación predeterminada.
Tenga en cuenta que, después de cargar registros de perfil en el [!DNL Platform] datalake, hay un ligero retraso hasta que se puedan consultar los registros de perfil. Lo mismo ocurre con la ingesta de registros de perfiles y experiencias a través de las API de flujo, solo después de unos segundos los datos estarán disponibles para evaluar las reglas de decisión que evalúan los datos de perfil y evento de experiencia.