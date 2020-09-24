---
keywords: Experience Platform;home;popular topics;manage decisioning;decisioning objects api;manage decisioning objects
solution: Experience Platform
title: Administrar entidades del servicio de decisiones mediante API
topic: tutorial
type: Tutorial
description: 'Este documento proporciona un tutorial para trabajar con las entidades comerciales de Decisioning Service mediante las API de Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---


# Administrar reglas y objetos de decisiones mediante API

Este documento proporciona un tutorial para trabajar con las entidades comerciales de [!DNL Decisioning Service] utilizar las API de Adobe Experience Platform.

El tutorial consta de dos partes:

- Las API de repositorio genéricas para administrar objetos comerciales se introducen en la [primera parte](#managing-repository-entities-using-apis). Estas API son genéricas en el sentido de que proporcionan capacidades de creación, lectura, actualización, eliminación y búsqueda para **cualquier** tipo de objeto comercial. Se describe el modelo general de API y se explica la relación con el lenguaje de aplicación de hipertexto (HAL).

- Aplicando los conocimientos sobre las API de repositorio, la [segunda parte](#creating-and-managing-offer-decisioning-entities-using-apis) se centra en las entidades comerciales que se administran mediante las API de repositorio. Con las mismas API aplicadas, la única diferencia entre administrar dos entidades diferentes, como una actividad y una regla comercial, es la carga útil de solicitud y respuesta, además de los valores de encabezado necesarios que indican el tipo de objeto que se administra.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los [!DNL Experience Platform] servicios y las convenciones de API. El [!DNL Platform] repositorio es un servicio que utilizan otros [!DNL Platform] servicios para almacenar objetos comerciales y diversos tipos de metadatos. Proporciona una forma segura y flexible de administrar y consulta esos objetos para que los utilicen varios servicios de tiempo de ejecución. El [!DNL Decisioning Service] es uno de esos. Antes de comenzar este tutorial, consulte la documentación siguiente:

- [[!Modelo de datos de experiencia DNL (XDM)]](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [[!Servicio de decisiones DNL]](./../home.md): Explica los conceptos y componentes utilizados para la toma de decisiones sobre experiencias en general y para la toma de decisiones sobre Ofertas en particular. Ilustra las estrategias utilizadas para elegir la mejor opción para presentar durante la experiencia del cliente.
- [[!Lenguaje de Consulta de Perfil DNL (PQL)]](../../segmentation/pql/overview.md): PQL es un lenguaje potente para escribir expresiones sobre instancias de XDM. PQL se utiliza para definir las reglas de decisión.

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
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Convenciones de API de repositorio

[!DNL Decisioning Service] está controlado por una serie de objetos comerciales que están relacionados entre sí. Todos los objetos comerciales se almacenan en el repositorio de objetos [!DNL Platform’s] comerciales. Una característica clave de este repositorio es que las API son ortogonales al tipo de objeto comercial. En lugar de utilizar una API de POST, GET, PUT, PATCH o DELETE que indique el tipo de recurso en su extremo de API, solo hay 6 extremos genéricos, pero aceptan o devuelven un parámetro que indica el tipo de objeto cuando se necesita esa desambición. El esquema debe estar registrado en el repositorio, pero más allá de eso el repositorio se puede utilizar para un conjunto de tipos de objetos de composición abierta.

Además de los encabezados enumerados anteriormente, las API para crear, leer, actualizar, eliminar y consulta de objetos de repositorio tienen las siguientes convenciones:

- Las rutas de extremo para todas las API de repositorio inicio con `https://platform.adobe.io/data/core/xcore/`.

Los formatos de carga útil de API se negocian con un `Accept` o `Content-Type` encabezado. Los formatos de mensaje en el encabezado `Accept` o `Content-Type` se indican mediante un valor `application/vnd.adobe.platform.xcore.{FORMAT}+json` donde {FORMAT} depende de la solicitud de la API del repositorio o del mensaje de respuesta específicos, según la siguiente tabla.

| Variante FORMAT | Descripción de la entidad de solicitud o respuesta |
| --- | --- |
| <br>seguido de un parámetro `schema={schemaId}` | El mensaje contiene una instancia descrita por un Esquema JSON que se indica mediante el esquema del parámetro format. La instancia se envuelve en una propiedad JSON `_instance`. Las demás propiedades de nivel superior de la carga útil de respuesta especifican la información del repositorio que está disponible para todos los recursos.  Los mensajes que cumplen el formato HAL tienen una `_links` propiedad que contiene referencias en formato HAL. |
| `patch.hal` | El mensaje contiene una carga útil de PATCH JSON suponiendo que la instancia que se va a revisar es compatible con HAL. Esto significa que no sólo se pueden revisar las propiedades de instancia de la instancia, sino también los vínculos HAL de la instancia. Tenga en cuenta que hay restricciones en las propiedades que el cliente puede actualizar. |
| `home.hal` | El mensaje contiene una representación con formato JSON de un recurso de documento principal para el repositorio. |
| xdm.receipt | El mensaje contiene una respuesta con formato JSON para una operación de creación, actualización (completa y parche) o eliminación. Los recibos contienen datos de control que indican la revisión de la instancia en forma de ETag. |

El uso de cada variante **de** formato depende de la API específica:

| API | Encabezado Content-Type | Aceptar encabezado |
| --- | --- | --- |
| Crear Contenedor <br/>de creación de instancia | `hal`<br/>con parámetro esquema | `xdm.receipt` |
| Actualizar Contenedor<br/>de InstanceUpdate | `hal`<br/>con parámetro esquema | `xdm.receipt` |
| Instancia de parche | `patch.hal` | `xdm.receipt` |
| Eliminar contenedor<br/>instanceDelete | N/D | `xdm.receipt` |
| Leer Contenedor<br/>InstanceRead | N/D | `hal` con `schema` parámetro |
| Lista,<br/>instanciascontenedores de lista | N/D | `hal` con `schema` parámetro especial `https://ns.adobe.com/experience/xcore/hal/results` |
| Instancias de búsqueda | N/D | hal con parámetro especial `schema` `https://ns.adobe.com/experience/xcore/hal/results` |
| Leer raíz de repo | N/D | `home.hal` |

Para las API de creación, actualización y lectura de contenedor, el esquema del parámetro de formato tiene el valor `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` es el primer parámetro de ruta para las API de instancia. Todas las entidades comerciales residen en lo que se denomina contenedor. Un contenedor es un mecanismo de aislamiento para separar las diferentes preocupaciones. El primer elemento de ruta para las API de instancia del repositorio que sigue al punto final general es el `containerId`. El identificador se obtiene a partir de la lista de contenedores a los que puede acceder el llamador. Por ejemplo, la API para crear una instancia en un contenedor es `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

La lista de contenedores accesibles se obtiene llamando al extremo raíz del repositorio &quot;/&quot; con una solicitud de GET HTTP usando los encabezados estándar.

## Administración del acceso a los contenedores

Un administrador puede agrupar entidades principales, recursos y permisos de acceso similares en perfiles. Esto reduce la carga de administración y es compatible con la interfaz de usuario [del Admin Console de](https://adminconsole.adobe.com)Adobe. Debe ser administrador de productos de Adobe Experience Platform en su organización para crear perfiles y asignarles usuarios.

Es suficiente crear perfiles de productos que coincidan con determinados permisos en un solo paso y, a continuación, simplemente agregar usuarios a esos perfiles. Los perfiles actúan como grupos a los que se han concedido permisos y todos los usuarios reales o técnicos de ese grupo heredan esos permisos.

### Contenedores de lista accesibles para usuarios e integraciones

Cuando el administrador haya concedido acceso a contenedores para usuarios regulares o integraciones, esos contenedores aparecerán en la llamada lista &quot;Principal&quot; del repositorio. La lista puede ser diferente para diferentes usuarios o integraciones, ya que es un subconjunto de todos los contenedores accesibles para el llamante. La lista de contenedores puede filtrarse por su asociación a contextos de productos. Se llama al parámetro filter `product` y se puede repetir. Si se proporciona más de un filtro de contexto de producto, se devolverá la unión de los contenedores que tienen asociaciones con cualquiera de los contextos de producto determinados. Tenga en cuenta que un solo contenedor se puede asociar a varios contextos de producto.

El contexto para los [!DNL Platform][!DNL Decisioning Service] contenedores es actualmente `dma_offers`.

>[!NOTE]
>
>El contexto para [!DNL Platform Decisioning Containers] pronto cambiará a `acp`. El filtrado es opcional, pero los filtros solo `dma_offers` requerirán modificaciones en una versión futura. Para prepararse para este cambio, los clientes no deben usar filtros o aplicar ambos contextos de producto como filtro.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Respuesta**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Observe los elementos `instanceId` enumerados en los elementos de resultados. Se utiliza como `containerId` parámetro en las API para leer y manipular objetos comerciales normales.

La lista ya se filtra para los usuarios por sus privilegios de acceso, pero se puede filtrar más mediante una consulta de propiedades.

## API genéricas para administrar entidades

### Creación de instancias

La API para crear una nueva instancia en el repositorio toma un parámetro de `containerId` ruta e identifica el tipo de instancia en el `Content-Type` encabezado con el parámetro esquema.

Las propiedades de instancia se proporcionan en la carga útil envuelta en la `_instance` propiedad. Las propiedades de instancia deben ser válidas para el esquema JSON con el identificador de esquema especificado.

La propiedad HAL `_links` debe estar presente pero puede estar vacía. Esto significa que no hay vínculos personalizados definidos para esta instancia.

**Solicitud**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Respuesta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

La respuesta contiene la instanceId del objeto que se acaba de crear. Este instanceId es inmutable, siempre asignado por el repositorio y globalmente único. El valor sirve como identificador físico.

Además, se devuelve un identificador de recurso universal (URI) en la `@id` propiedad de la carga útil de respuesta si el esquema tiene dicha propiedad. Cada instancia debe tener una propiedad que actúe como URI y clave principal de la instancia. Este identificador lo utiliza otra instancia para formar relaciones con la nueva instancia, incluso en diferentes tipos. En la versión actual, los URI son generados por el repositorio y están contenidos en la `@id` propiedad. Las versiones futuras pueden relajar esta regla y permitir a los clientes administrar sus propios valores de URI y asignar un nombre a la propiedad que la contiene.

Tenga en cuenta que estos URI no son direcciones URL y no proporcionan una forma de recuperar directamente el recurso. Para indicar ese aspecto, el URI lleva el prefijo un esquema de URI que no especifica un protocolo de recuperación. Sin embargo, los URI pueden utilizarse para buscar la instancia con una consulta.

La respuesta REST tendrá un encabezado Location que contiene un componente URL que puede utilizarse para recuperar la instancia que se acaba de crear. Este componente es una referencia URI relativa y debe aplicarse al URI base del repositorio. El URI base se devuelve en el `Content-Base` encabezado.

La `repo:etag` propiedad especifica la revisión de la instancia. Este valor se puede utilizar en operaciones de actualización para reforzar la coherencia. El encabezado HTTP `If-Match` se puede utilizar para agregar una condición a una llamada de API de PUT o PATCH que garantice que no hubo ningún otro cambio en la instancia que pudiera sobrescribirse accidentalmente. El `repo:etag` valor se devuelve con cada llamada de creación, lectura, actualización, eliminación y consulta. El valor se utiliza como valor en el ` If-Match` encabezado, según [RFC7232 Sección 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

Las propiedades restantes indican qué cuenta y clave de API se utilizaron para crear y modificar la instancia por última vez. Dado que la instancia fue creada por esta llamada, los valores respectivos son los de la solicitud.

### Buscar una instancia por ID

Con la URL en el encabezado Ubicación devuelta con la llamada Crear, una aplicación puede buscar una instancia.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Aunque `instanceId` se proporciona como parámetro de ruta, las aplicaciones, siempre que sea posible, no deben construir la ruta por sí mismas y, en su lugar, seguir los vínculos a instancias incluidas en las operaciones de lista y búsqueda. Para más detalles, véanse las secciones ‎ 6.4.4 y ‎ 6.4.6.

**Respuesta**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Las propiedades JSON de la instancia se envuelven en la propiedad `_instance` y las demás propiedades de nivel raíz contienen metadatos sobre la instancia.

El recurso también contiene una matriz de ID de esquema JSON. Esta matriz indica los esquemas JSON con los que se valida esta instancia.

Cada instancia contiene un vínculo HAL del tipo de relación self que corresponde con la relación de propiedad registrada de IANA (tal como se define en [RFC5988]).

**Prueba de revisiones más recientes de una instancia**

El valor actual `eTag` de la instancia se devuelve con la respuesta; permite a los clientes ejecutar operaciones condicionales en la instancia, ya sea para evitar recuperar el mismo estado de recurso o para evitar sobrescribir los valores de una revisión posterior sin que el cliente lo sepa.

La API de búsqueda permite a un cliente especificar un parámetro `If-None-Match` de encabezado. Consulte la definición de este parámetro HTTP estándar [RFC2616]. El valor de la etiqueta entity que especifica un cliente es el valor que recibió con la respuesta más reciente, ya sea desde una llamada a la API de actualización, lectura, lista o búsqueda. Tenga en cuenta que el `etag` valor debe ser opaco para el cliente y debe proporcionarse como una cadena, entre comillas.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

La API de repositorio responderá con un estado 304 No modificado cuando la última revisión de la instancia sea esa con la etiqueta dada.

### Instancias de lista para un esquema: clasificación y paginación

Los clientes no podrán realizar un seguimiento de las instancias que están creando y, por lo tanto, acceder a ellas mediante su instanceId físico. El uso de la API de instancia de lectura será la excepción. Los clientes tampoco saben qué instancias han creado otros clientes.

Un patrón de acceso más típico será pasar página a través del conjunto de todas las instancias.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Respuesta**

La respuesta depende del `{schemaId}` especificado. Por ejemplo, para &quot;https<span></span>://ns.adobe.com/experience/oferta-management/oferta-actividad&amp;id=xcore:oferta-actividad:fa24f9e8fc15c73&quot;, la respuesta es similar a la siguiente.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>El resultado contiene las instancias para el esquema determinado o la primera página de esta lista. Tenga en cuenta que las instancias pueden cumplir más de un esquema y, por lo tanto, pueden aparecer en más de una lista.

Los recursos de página son transitorios y de solo lectura; no se pueden actualizar ni eliminar. El modelo de paginación proporciona acceso aleatorio a subconjuntos de listas grandes durante un período de tiempo prolongado sin mantener ningún estado por cliente.

Para acceder a una lista de instancia por página de esta manera, debe ser posible definir una ordenación estable en las entradas enumeradas por esa lista de instancia. Tenga en cuenta que &quot;estable&quot; no significa que las instancias aparezcan en una página predeterminada. De hecho, cuando se forma un orden de páginas ordenando instancias según una propiedad P y un cliente actualiza esta propiedad P, otro cliente puede volver a llegar a esta instancia en una página diferente mientras realiza la paginación a través de la lista. En otras palabras, el modelo favorece la obtención de resultados más actuales.

Sin embargo, cuando el criterio de ordenación se basa en una propiedad no modificable, un criterio de ordenación &quot;estable&quot; garantiza que se alcancen todas las instancias que existían al principio de la operación de paginación (a menos que se hayan eliminado al llegar a la página). Cuando este criterio de ordenación se encuentra en una propiedad que aumenta de forma monótona, también se alcanzarán las instancias que se creen después de iniciar la operación de paginación.

Un cliente puede proporcionar sugerencias sobre el tamaño de página que desea, pero depende completamente del repositorio proporcionar más o menos instancias con la página que devuelve. Para garantizar el orden estable, el servicio debe agregar o eliminar elementos de la página para que el valor de la propiedad sort sea diferente a través de los límites de la página. De este modo, la página siguiente no volverá a contener algunos elementos de la última página o, en el peor de los casos, se quedaría atascada con los mismos elementos en cada página.

La paginación se controla mediante los siguientes parámetros:

- **`orderBy`**:: Contiene una lista ordenada y separada por comas de las propiedades por las que se ordena la lista de la instancia. La primera propiedad se utiliza para la ordenación principal, la segunda propiedad para resolver vínculos en la ordenación principal, etc. Cuando se especifica una propiedad que tiene un valor único por instancia, los vínculos no son posibles y se puede producir un salto de página después de cada elemento. El nombre de una propiedad puede ir precedido de un `+` signo de orden ascendente o `-` de orden descendente. Si el nombre de la propiedad no tiene un prefijo, el resultado se ordena en orden ascendente. Si no `orderBy` se especifica en la solicitud, el repositorio utilizará la propiedad instanceId física en su lugar.
- **`start`**:: Los clientes utilizan el parámetro inicio para definir la página que desean recuperar. El parámetro inicio determina el comienzo de la página deseada. La respuesta contendrá instancias que comienzan con aquellas que tienen un valor de `orderBy` propiedad estrictamente bueno (para ascendente) o estrictamente menor que (para descendente) el valor especificado. Cuando no se especifica el parámetro de consulta, el valor predeterminado es un valor instanceId que se ordena antes del primer identificador de instancia posible y, por lo tanto, este valor se omite de la primera página.
- **`limit`**:: especifica un entero positivo como indicio del número máximo de elementos que se deben devolver para una solicitud determinada. El tamaño de respuesta real puede ser más pequeño o mayor, ya que se ve limitado por la necesidad de proporcionar un funcionamiento fiable del parámetro de inicio

### Filtrado de listas

Es posible filtrar los resultados de lista y se produce independientemente del mecanismo de paginación. Los filtros simplemente omiten las instancias en el orden de las listas o solicitan explícitamente incluir solo las instancias que cumplen una condición determinada. Un cliente puede solicitar que la expresión de propiedades se utilice como filtro o puede especificar una lista de URI que se utilizarán como valores de la clave principal de las instancias.

- **`property`**:: Contiene una ruta de nombre de propiedad seguida de un operador de comparación seguido de un valor. <br/>
La lista de instancias devueltas contiene aquellas para las que la expresión se evalúa como verdadera. Por ejemplo, suponiendo que la instancia tiene una propiedad payload 
`status` y los valores posibles son `draft`, `approved`, `archived` y `deleted` luego el parámetro de consulta `property=_instance.status==approved` devuelve solo las instancias para las que se aprueba el estado. <br/>
<br/>
La propiedad que se va a comparar con el valor dado se identifica como una ruta. Los componentes de ruta individuales están separados por ".", como: `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Para las propiedades que tienen valores de cadena, numéricos o de fecha y hora, los operadores permitidos son: `==`, `!=`, `<`, `<=`, `>` y `>=`. Además, para propiedades con un valor de cadena, se `~` puede utilizar un operador. El `~` operador coincide con la propiedad dada según una expresión regular. El valor de cadena de la propiedad debe coincidir con la expresión **completa** de las entidades que se incluirán en los resultados filtrados. Por ejemplo, buscar la cadena `cars` en cualquier lugar dentro del valor de propiedad requiere que la expresión regular sea `.*cars.*`. Sin el encabezado o el final `.*`, solo las entidades coincidirán con las que tengan un valor de propiedad que comience o termine con `cars`, respectivamente. Para el `~` operador, la comparación de caracteres de letras no distingue entre mayúsculas y minúsculas. Para todos los demás operadores, la comparación distingue entre mayúsculas y minúsculas.<br/><br/>
No solo se pueden usar propiedades de carga útil de instancia en expresiones de filtro. Las propiedades de los sobres se comparan de la misma manera, por ejemplo: `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
El parámetro de `property` consulta se puede repetir para que se apliquen varias condiciones de filtro, por ejemplo, para devolver todas las instancias que se modificaron por última vez después de una fecha determinada y antes de una fecha determinada. Los valores de esas expresiones deben tener codificación de dirección URL. Si no se da ninguna expresión y el nombre de la propiedad simplemente aparece en la lista, los elementos que cumplen los requisitos son aquellos que tienen una propiedad con el nombre dado.<br/>
<br/>

- **`id`**:: A veces, es necesario filtrar una lista por el URI de las instancias. El parámetro de `property` consulta se puede usar para filtrar una instancia, pero para obtener más de una instancia, se puede proporcionar una lista de URI a la solicitud. El `id` parámetro se repite y cada incidencia especifica un valor de URI, `id={URI_1}&id={URI_2},…` los valores de URI deben tener codificación de URL.

Los resultados paginados se devolverán como un tipo mime especial `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Respuesta**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

La respuesta contiene la lista de elementos de resultado dentro de los resultados de la propiedad JSON junto a dos propiedades que indican el número de resultados en esta página y el número total de elementos en la lista filtrada empezando por la página que se acaba de devolver.

### Búsqueda de texto completo y consultas estructuradas

En los casos en que los clientes deseen proporcionar condiciones de filtro más complejas y buscar instancias por términos contenidos en propiedades de cadena, el repositorio oferta una API de búsqueda más potente.

**Solicitud**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Además de los parámetros de paginación y filtrado de las API de lista, esta API permite a los clientes añadir texto completo y parámetros de consulta booleanos.

La búsqueda de texto completo se controla mediante los siguientes parámetros:

- **`q`**:: Contiene una lista sin ordenar separada por espacios de términos que se normalizan antes de compararlos con cualquier propiedad de cadena de las instancias. Las propiedades de cadena se analizan para los términos y esos términos también se normalizan. La consulta de búsqueda intenta coincidir con uno o más de los términos especificados en el `q` parámetro. Los caracteres +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, :, / tienen un significado especial para determinar los límites de la palabra dentro de la cadena de consulta y se debe aplicar una barra invertida cuando aparezca en un token que debe coincidir con el carácter. La cadena de consulta se puede rodear de comillas de doble para buscar coincidencias exactas de la cadena y para evitar caracteres especiales.
- **`field`**:: Si los términos de búsqueda solo deben coincidir con un subconjunto de las propiedades, el parámetro field puede indicar la ruta a esa propiedad. El parámetro se puede repetir para indicar más de una propiedad con la que se debe hacer coincidir.
- **`qop`**:: Contiene un parámetro de control que se utiliza para modificar el comportamiento coincidente de la búsqueda. Cuando el parámetro se establece en y luego todos los términos de búsqueda deben coincidir y cuando el parámetro está ausente o su valor se define en o cuando cualquiera de los términos puede contar para una coincidencia.

### Actualización y parches de instancias

Para actualizar una instancia, un cliente puede sobrescribir la lista completa de propiedades a la vez o utilizar una solicitud de PATCH JSON para manipular valores de propiedades individuales, incluidas listas.

En ambos casos, la dirección URL de la solicitud especifica la ruta a la instancia física y, en ambos casos, la respuesta será una carga útil de recepción JSON como la devuelta por la operación [de](#create-instances)creación. Un cliente debería preferiblemente utilizar el encabezado `Location` o un vínculo HAL que recibió de una llamada API anterior para este objeto como la ruta de URL completa para esta API. Si esto no es posible, el cliente puede construir la dirección URL desde el `containerId` y el `instanceId`.

**Solicitud** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Solicitud** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

La solicitud del PATCH aplica las instrucciones y, a continuación, valida la entidad resultante con el esquema y las mismas reglas de entidad e integridad referencial que la solicitud del PUT.

**Control de ediciones de valores de propiedad**

Puede evitar que las propiedades se establezcan durante la creación o la actualización, mediante las anotaciones siguientes:

- **`"meta:usereditable"`**:: Booleano: cuando una solicitud se origina en un agente de usuario que identifica al llamador con un usuario o un token de acceso técnico de cuenta, las propiedades con las que se anotan no `"meta:usereditable": false` deben estar presentes en la carga útil. Si lo son, no deben tener un valor diferente al establecido actualmente. Si los valores difieren, la solicitud de actualización o de parche se rechaza con el estado 422 Entidad no procesable.
- **`"meta:immutable"`**:: Booleano: las propiedades que se anotan con `"meta:immutable": true` no se pueden cambiar una vez establecidas. Esto se aplica a las solicitudes procedentes de un usuario final, una integración técnica de cuenta o un servicio especial.

**Prueba de actualización simultánea**

Hay condiciones en las que varios clientes intentan actualizar una instancia al mismo tiempo. El repositorio se gestiona en un clúster de nodos computacionales sin administración central de transacciones. Para evitar que un cliente escriba una instancia que esté escrita simultáneamente por otro cliente, los clientes pueden utilizar una actualización condicional o una solicitud de parche. Al especificar la `etag` cadena en el encabezado `If-Match` el repositorio se asegura de que sólo la primera solicitud se realiza correctamente y que las solicitudes posteriores de otros clientes que utilicen el mismo `etag` valor no se completen. El `etag` valor cambia con cada modificación de la instancia. Los clientes deben recuperar la instancia para obtener el valor más reciente `etag` y, a continuación, solo un cliente de muchos que intentaron la actualización puede tener éxito con ese valor. Otros clientes serán rechazados con el mensaje 409 Conflict.

### Eliminación de instancias

Las instancias se pueden eliminar con una llamada de DELETE. Un cliente debería preferiblemente utilizar el encabezado `Location` o un vínculo HAL que recibió de una llamada API anterior para esto como la ruta completa de la dirección URL. Si esto no es posible, el cliente puede construir la dirección URL desde el `containerId` y el `instanceId`.

**Solicitud**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Respuesta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Al recibir una solicitud de eliminación, el repositorio comprueba si hay otras instancias, de cualquier esquema, y sigue haciendo referencia a la instancia que se va a eliminar. En un sistema distribuido y de alta disponibilidad, la integridad referencial no se puede comprobar inmediatamente. Cuando hay relaciones de clave externa definidas, las comprobaciones se realizarán asincrónicamente. Esto da como resultado una respuesta ligeramente retrasada al resultado de la solicitud de eliminación. Cuando se realizan estas comprobaciones, la respuesta inmediata incluye el estado 202 Aceptado y un vínculo para comprobar el resultado de la operación de eliminación en el `Location` encabezado. Un cliente debe entonces comprobar el resultado de ese vínculo.

Si se encuentra una instancia que hace referencia a la instancia que se está eliminando, el resultado será un rechazo de la operación de eliminación. Si no se detecta ninguna otra referencia de clave externa, la eliminación se completa. Si el resultado aún no se ha decidido, la respuesta indicará que por otra respuesta 202 aceptada con el mismo `Location` encabezado y pedirá al cliente que siga comprobando. Cuando se determine el resultado, la respuesta indicará que con un estado de 200 OK y la carga útil de la respuesta contendrá el resultado de la solicitud de eliminación original. Tenga en cuenta que la respuesta 200 Ok solo significa que se conoce el resultado y que el cuerpo de respuesta contendrá la confirmación o rechazo de la solicitud de eliminación.

## Creación de ofertas y sus subcomponentes

Las API descritas en la sección anterior se aplican uniformemente a todos los tipos de objetos comerciales. La única diferencia entre, digamos, crear una oferta y una actividad sería el `content-type` encabezado que indica el esquema JSON de la carga útil JSON de la solicitud que cumple con el esquema. Por lo tanto, las secciones siguientes sólo tendrán que centrarse en esos esquemas y en las relaciones entre ellos.

Al utilizar las API con el tipo de contenido `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, las propiedades de la instancia se incrustan en la `_instance` propiedad junto a la cual hay una `_links` propiedad. Será el formato general en el que se representarán todas las instancias:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Por razones de brevedad, en todos los fragmentos de JSON solo se ilustran las propiedades de instancia y solo cuando se requiere se muestran las propiedades de envoltorio y la sección _links.

### Propiedades de oferta general

Las ofertas son un tipo de opción de decisión y el esquema de ofertas JSON hereda las propiedades de opción estándar que tendrá cada instancia de opción.

- **`@id`** - Un identificador único para cada opción que es la clave principal y se utiliza para hacer referencia a la opción de otros objetos. Esta propiedad se asigna cuando se crea la instancia, es inmutable y no editable.
- **`xdm:name`** - Cada opción tiene un nombre que se utiliza con fines de búsqueda y visualización. El nombre no es inmutable y no se puede utilizar para identificar la instancia de forma exclusiva. El nombre se puede seleccionar libremente pero debe ser único en todas las instancias de oferta.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` si la oferta es una oferta de reserva.

Cada instancia de oferta puede tener un conjunto opcional de propiedades que solo son características para esa instancia. Las diferentes ofertas pueden tener claves diferentes para esas propiedades, pero los valores deben ser cadenas. Estas propiedades se pueden usar en reglas de decisión y segmentación. También son accesibles para reunir la experiencia decidida para personalizar aún más los mensajes.

### Ciclo de vida de oferta

Existe un flujo de transición de estado simple que seguirán todas las Opciones. Inicios en un estado de borrador y cuando estén listos, su estado se establecerá en aprobado. Una vez pasada la fecha de finalización, se pueden mover al estado archivado. En ese estado, se pueden eliminar o reutilizar moviéndolas de nuevo al estado de redacción.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Esta propiedad se utiliza para la administración del ciclo vital de la instancia. El valor representa un estado de flujo de trabajo que se utiliza para indicar si la oferta aún está en construcción (valor = borrador), se puede considerar generalmente en tiempo de ejecución (valor = aprobado) o si no se debe seguir utilizando (valor = archivado).

Una operación de PATCH simple en la instancia se utiliza normalmente para manipular una `xdm:status` propiedad:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` si la oferta es una oferta de reserva.

### Representaciones y colocaciones

Las ofertas son opciones de decisión que tienen representaciones de contenido. Cuando se toma una decisión, la opción se selecciona y su identificador se utiliza para obtener el contenido o las referencias de contenido para la colocación que se debe proporcionar. Una oferta puede tener más de una representación, pero cada una de ellas debe tener una referencia de ubicación diferente. Esto garantiza que con una ubicación determinada la representación se pueda determinar sin ambigüedades.
Durante la operación de decisión, la colocación se determina junto con el objeto de actividad. Las ofertas que no están representadas con esa ubicación como referencia se eliminan automáticamente de la lista de opciones.

Antes de agregar representaciones a una oferta, deben existir instancias de colocación. Estas instancias se crean con el identificador`https://ns.adobe.com/experience/offer-management/offer-placement`de esquema.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` si la oferta es una oferta de reserva.

Una instancia **de ubicación** puede tener las siguientes propiedades:

- **`xdm:name`** - Contiene el nombre asignado para que la ubicación haga referencia a él en interacciones humanas e interfaces de usuario.
- **`xdm:description`** - Se utiliza para transmitir intenciones legibles por el usuario sobre cómo se utiliza el contenido de esta ubicación en el envío general de mensajes. Cuando los canales de envío definen nuevas colocaciones, pueden agregar más información en esta propiedad para que un creador de contenido pueda crear o seleccionar el contenido en consecuencia. Esas instrucciones no se interpretan ni se aplican formalmente. Esta propiedad sirve simplemente como un lugar para comunicar las intenciones.
- **`xdm:channel`** - La URI de un canal. El canal indica dónde se va a entregar el contenido dinámico. La restricción de canal se utiliza para transmitir no sólo dónde se utilizará la oferta sino también para determinar el editor de contenido o el validador que se utiliza para la experiencia.
- **`xdm:componentType`** - Un identificador de modelo, es decir, URI, para el contenido que se puede mostrar en la ubicación descrita por esta colocación. Los tipos de componente son: vínculo de imagen, html o texto sin formato. Cada tipo de componente puede implicar un conjunto específico de propiedades (un modelo) que puede tener el elemento de contenido. La lista de los tipos de componente se puede ampliar. Existen tres valores de tipo de componente predefinidos:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, Una restricción para los tipos de papel de los componentes que se esperan en esta ubicación. Podría haber más de un tipo de medio para un tipo de componente, como distintos formatos de imagen.

**Los elementos de representación** de una oferta tienen una estructura de objetos en la propiedad array `xdm:representations`. Cada elemento puede tener las siguientes propiedades:

- **`xdm:placement`** - Esta propiedad contiene la referencia a la instancia de colocación. El valor se comprueba cuando se agrega la representación a la oferta. Debe existir una instancia de colocación con ese URI y no debe marcarse como eliminada. Además, se realiza una comprobación para garantizar que una instancia de oferta no tenga dos representaciones con el mismo valor para su referencia de ubicación.
- **`xdm:components`** - Los componentes de contenido son los fragmentos asociados a una representación de la oferta en particular. Estos fragmentos se utilizan posteriormente para componer la experiencia del usuario final. Tenga en cuenta que el Servicio de decisiones por sí solo no constituye la experiencia completa del usuario final. Las siguientes propiedades forman parte del modelo de cada componente.
   - **`@type`** - esta propiedad identifica el tipo de componente. Otro nombre para este concepto es el modelo de fragmento de contenido. El `@type` de un componente es simplemente un URI para un modelo definido por la aplicación o el servicio que está montando la experiencia del usuario final.
   - **`repo:id`** - esta propiedad contiene un identificador global único e inmutable para el recurso principal del componente en el repositorio donde se almacena el recurso.
   - **`repo:name`** - Esta propiedad contiene un nombre legible para el recurso en el repositorio. Este nombre está definido por el usuario y no está garantizado que sea único.
   - **`repo:resolveURL`** - esta propiedad contiene un localizador de recursos único para leer el recurso en un repositorio de contenido. Esto facilitará la obtención del recurso sin que el cliente comprenda qué API llamar. La URL devuelve los bytes del recurso principal del recurso.
   - **`dc:format`** - esta propiedad proviene de la iniciativa Dublin Core Metadata. El formato puede utilizarse para determinar el software, el hardware u otro equipo necesario para mostrar o utilizar el recurso. La práctica recomendada es seleccionar un valor de un vocabulario controlado (por ejemplo, la lista de tipos de medios de Internet que definen los formatos de los equipos).
   - **`dc:language`** - Esta propiedad contiene el idioma o los idiomas del recurso. Los idiomas se especifican en el código de idioma tal como se define en IETF RFC 3066.

Existen tres tipos de componente predefinidos expresados en la `@type` propiedad:

- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-text
- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-html

Según el valor de la `@type` propiedad, `xdm:components` contendrá propiedades adicionales:

- **`xdm:linkURL`** - Presente cuando el componente es un vínculo de imagen. Esta propiedad contendrá el vínculo asociado a la imagen y el que `user-agent` navegará cuando el usuario final interactúe con el contenido de la oferta.
- **`xdm:copyline`** - Se utiliza cuando el componente es un texto. Además de hacer referencia a un recurso de texto, por ejemplo, para Ofertas de texto de formulario largas que pueden tener formato, se puede almacenar directamente una cadena de texto corta en la propiedad xdm:copyline.

Los clientes pueden utilizar propiedades adicionales para establecer y evaluar las instrucciones de administración de contexto. Por ejemplo, el cliente de la biblioteca de IU de Oferta agrega las siguientes propiedades opcionales para gestionar la visualización con mayor facilidad:

- Dentro de cada elemento de la `xdm:components` matriz, el cliente de la interfaz de usuario de la biblioteca de Ofertas agrega las siguientes propiedades. Estas propiedades no deben eliminarse ni manipularse sin comprender el impacto en la interfaz de usuario:
   - **`offerui:previewThumbnail`** - Se trata de una propiedad opcional que utiliza la interfaz de usuario de la biblioteca de Ofertas para mostrar una representación del recurso. Esta representación no es la misma que el propio recurso. Por ejemplo, el contenido puede ser HTML y la representación es una imagen de mapa de bits que solo muestra una aproximación. Esta representación (de menor calidad) se muestra dentro del bloque de representación de la oferta.

Un ejemplo de operación de PATCH en una instancia de oferta muestra cómo manipular las representaciones:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer` o `https://ns.adobe.com/experience/offer-management/fallback-offer` si la oferta es una oferta de reserva.

La operación de PATCH puede fallar cuando `xdm:representations` todavía no hay ninguna propiedad. En ese caso, la operación de adición anterior podría ir precedida por otra operación de adición que cree la `xdm:representations` matriz o la operación de adición única establezca la matriz directamente.
Los esquemas y las propiedades que se describen se utilizan para todos los tipos de ofertas, ofertas de personalización y ofertas de reserva. En las dos secciones siguientes se explican los aspectos de las ofertas de personalización y las reglas de decisión.

## Configuración de restricciones de oferta

### Restricciones del calendario

Las opciones de decisión en general pueden proporcionar un inicio y una fecha y hora de finalización que sirvan como restricción del calendario. Las propiedades están incrustadas en la propiedad `xdm:selectionConstraint`:

- **`xdm:startDate`** - Esta propiedad indica la fecha y hora del inicio. El valor es una cadena con formato según las reglas RFC 3339, es decir, como esta marca de tiempo: &quot;2019-06-13T11:21:23.356Z&quot;.
Las opciones de decisión que no hayan alcanzado la fecha y hora de inicio todavía no se considerarán elegibles en la decisión.
- **`xdm:endDate`** - Esta propiedad indica la fecha y hora de finalización. El valor es una cadena con formato según las reglas RFC 3339, es decir, como esta marca de tiempo: &quot;2019-07-13T11:00:00.000Z&quot;Las opciones de decisión que han pasado la fecha y hora de finalización ya no se consideran elegibles en el proceso de toma de decisiones.

El cambio de una restricción de calendario se puede realizar con la siguiente llamada de PATCH:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. Las ofertas de reserva no tienen restricciones.

### Restricciones de límite

Una restricción de límite es un componente de una opción de decisión que define los parámetros para el límite. El límite es el proceso de limitar cuántas veces se puede proponer una opción, para un perfil individual y para todos los perfiles. Las propiedades contienen un valor entero que debe ser bueno o igual a 1. Las propiedades se anidan dentro de una propiedad `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Un límite máximo global es la limitación de cuántas veces se puede proponer una oferta en su totalidad.
- **`xdm:profileCap`** - Un límite de perfil es una limitación para la cantidad de veces que se puede proponer una oferta a un determinado perfil.

La configuración o el cambio de la restricción de límite en una oferta de personalización se puede realizar con la siguiente llamada de PATCH:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. Las ofertas de reserva no tienen restricciones.

Para eliminar los valores de límite, la operación &quot;agregar&quot; se sustituye por la operación &quot;eliminar&quot;. Tenga en cuenta que los valores de límite existen de forma individual y también se pueden definir o eliminar individualmente.

### Limitaciones de elegibilidad

Las ofertas se pueden seleccionar condicionalmente en el proceso de decisión. Cuando una oferta de personalización tiene una referencia a una regla de elegibilidad, la condición de la regla debe evaluarse como verdadera para que el objeto de oferta se considere para un perfil determinado. Las reglas de elegibilidad se crean y administran independientemente de las opciones de decisión y se puede hacer referencia a la misma regla desde varias ofertas de personalización.

La referencia a la regla está incrustada en la propiedad `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Esta propiedad contiene una referencia a una regla de elegibilidad. El valor es el `@id` de una instancia de esquemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

También se puede añadir y eliminar una regla con una operación de PATCH:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. Las ofertas de reserva no tienen restricciones.

Tenga en cuenta que la regla de elegibilidad está incrustada en la propiedad junto con las restricciones de calendario `xdm:selectionConstraint` . Las operaciones de PATCH no deben intentar quitar toda la `SelectionConstraint` propiedad.

## Definición de la prioridad de una oferta

Las opciones de decisión calificativas se clasificarán para determinar la mejor opción para el perfil determinado. Para admitir la clasificación y proporcionar un valor predeterminado en caso de que la clasificación no pueda determinarse mediante otro mecanismo, se puede establecer una prioridad base para cada oferta de personalización.
La prioridad base está incrustada en la propiedad `xdm:rank`:

- **`xdm:priority`** - Esta propiedad representa el orden predeterminado en el que se selecciona una oferta sobre otra en caso de que no se conozca ningún orden de clasificación específico del perfil. Si después de comparar el valor de prioridad dos o más ofertas de personalización siguen vinculadas, una se elige al azar y se utiliza en la propuesta de oferta. El valor de esta propiedad debe ser un número entero bueno o igual a 0.

El ajuste de la prioridad base se puede realizar con la siguiente llamada de PATCH:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. Las ofertas de reserva no tienen propiedades de clasificación.

## Administración de reglas de decisión

Las reglas de elegibilidad reúnen las condiciones que se evalúan para determinar si una determinada opción de decisión es elegible para un perfil determinado. La asociación de una regla a una o varias opciones de decisión define implícitamente que para esta opción la regla debe evaluarse como verdadera para que la opción se considere para este usuario. La regla puede contener pruebas en atributos de perfil, puede evaluar expresiones que impliquen eventos de experiencia para este perfil y puede incluir datos de contexto que se pasaron a la solicitud de decisión. Por ejemplo: una condición puede describirse como:

> &quot;Incluya a personas que tengan el estatus de élite y hayan volado en un vuelo tres veces en los últimos 6 meses que tengan el número de vuelo del vuelo actual&quot;.

Las instancias se crean con el identificador de esquemahttps://ns.adobe.com/experience/offer-management/eligibility-rule. La `_instance` propiedad de la llamada de creación o actualización es similar a:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

El valor de la propiedad de condición de la regla contiene una expresión PQL. Se hace referencia a los datos de contexto mediante la expresión de ruta especial @{schemaID}.

Las reglas se alinean naturalmente con los segmentos en la regla [!DNL Experience Platform] y, a menudo, una regla simplemente reutiliza la intención de un segmento probando la propiedad de un `segmentMembership` perfil. La `segmentMembership` propiedad contiene los resultados de las condiciones de segmentos que ya se han evaluado. Esto permite que una organización defina una vez sus audiencias específicas de dominio, les asigne un nombre y evalúe las condiciones una vez.

## Administración de colecciones de ofertas

### Creación de etiquetas y ofertas de etiquetado

Las ofertas pueden organizarse en colecciones en las que cada colección define la condición de filtro que se aplicará. Actualmente, la expresión de filtro de una colección puede tener uno de los dos formularios:

1. El `@id` parámetro de la oferta debe coincidir con uno de una lista de identificadores para que la oferta esté en la colección. Este filtro es simplemente una lista desglosada de los URI de las ofertas de la colección.
2. Una oferta puede tener una lista de referencias de etiquetas y el filtro de la colección consta de una lista de etiquetas. La oferta se encuentra en la colección cuando:\
   a. cualquiera de las etiquetas del filtro coincide con una de las etiquetas de la oferta\
   b. todas las etiquetas del filtro coinciden con una de las etiquetas de la oferta

Las etiquetas son instancias sencillas a las que se pueden vincular las instancias de oferta. Son instancias por su cuenta con un nombre para mostrarlas. El nombre debe ser único en todas las instancias para facilitar la visualización en la interfaz de usuario.

Los objetos de etiqueta sirven para establecer una categorización entre las opciones de decisión (ofertas). Muchas ofertas pueden vincular una etiqueta y una oferta puede tener muchas referencias de etiqueta. Una categoría de ofertas se establece haciendo referencia a todas las ofertas relacionadas con un conjunto determinado de instancias de etiquetas.

Las instancias de etiquetas se crean con el identificador de esquemahttps://ns.adobe.com/experience/offer-management/tag. La `_instance` propiedad de la llamada de creación o actualización es similar a:

```json
{
  "xdm:name": "credit card"
} 
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/tag`.


Se puede crear una instancia de oferta con la lista de referencias de etiquetas como:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Como alternativa, una oferta se puede revisar para cambiar su lista de etiquetas:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

En ambos casos, consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Tenga en cuenta que la `xdm:tags` propiedad ya debe existir para que la operación de adición se realice correctamente. No existen etiquetas en una instancia en la que la operación de PATCH puede agregar primero la propiedad array y luego agregar una referencia de etiqueta a esa matriz.

### Definir filtros para colecciones de ofertas

Las instancias de filtro se crean con el identificador de esquemahttps://ns.adobe.com/experience/offer-management/offer-filter. La `_instance` propiedad de la llamada de creación o actualización puede tener el siguiente aspecto:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Esta propiedad indica si el filtro se configura con etiquetas o hace referencia directa a ofertas por sus ID. Cuando el filtro está configurado para utilizar etiquetas, el tipo de filtro puede indicar si todas las etiquetas deben coincidir con las de una oferta determinada o si alguna de las etiquetas dadas es suficiente para que la oferta cumpla los requisitos para el filtro. Los valores válidos de esta propiedad enum son:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Una propiedad contiene una matriz de URI que son referencias a instancias de oferta o instancias de etiqueta, según el valor de `xdm:filterType`. .

La siguiente llamada ilustra cómo se ve la `_instance` propiedad de la llamada de creación o actualización en caso de que se haga referencia directamente a ofertas:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Administración de actividades

Se utiliza una actividad de oferta para controlar el proceso de toma de decisiones. Especifica el filtro de oferta aplicado al inventario total para reducir las ofertas por tema/categoría, la ubicación para reducir el inventario a aquellas ofertas que encajan en el espacio reservado y especifica una opción de reserva en caso de que las restricciones combinadas descalifiquen todas las opciones de personalización disponibles (ofertas).

Las instancias de actividad se crean con el identificador`https://ns.adobe.com/experience/offer-management/offer-activity`de esquema. La `_instance` propiedad de la llamada de creación o actualización es similar a:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Esta propiedad obligatoria contiene el nombre de la actividad. El nombre se muestra en varias interfaces de usuario.
- **`xdm:status`** - Esta propiedad se utiliza para la administración del ciclo vital de la instancia. El valor representa un estado de flujo de trabajo que se utiliza para indicar si la actividad aún está en construcción (valor = borrador), se puede considerar generalmente en tiempo de ejecución (valor = activo) o si no se debe seguir utilizando (valor = archivado).
- **`xdm:placement`** - Una propiedad obligatoria que contiene una referencia a una ubicación de oferta que se aplica al inventario cuando se toma una decisión en el contexto de esta actividad. El valor es el URI (`@id`) de la ubicación de oferta que se utiliza.
- **`xdm:filter`** - Una propiedad obligatoria que contiene una referencia a un filtro de oferta que se aplica al inventario cuando se toma una decisión en el contexto de esta actividad. El valor es el URI (`@id`) del filtro de oferta que se utiliza.
- **`xdm:fallback`** - Una propiedad obligatoria que contiene una referencia a una oferta de reserva. Se utiliza una oferta de reserva cuando la toma de decisiones para esta actividad no califica ninguna de las ofertas de personalización. El valor es el URI (`@id`) de una instancia de oferta de reserva.

### Administración de ofertas de reserva

Para poder crear instancias de actividad, debe existir una oferta de reserva que cumpla los requisitos para la colocación de la actividad. Las instancias de oferta de reserva se crean con el identificador`https://ns.adobe.com/experience/offer-management/fallback-offer`de esquema. La `_instance` propiedad de la llamada de creación o actualización contiene las mismas propiedades generales que tiene una oferta de personalización, pero no puede tener ninguna otra restricción.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Consulte [Actualización y parche de instancias](#updating-and-patching-instances) para obtener la sintaxis completa de cURL. El `schemaId` parámetro debe ser `https://ns.adobe.com/experience/offer-management/fallback-offer`.

