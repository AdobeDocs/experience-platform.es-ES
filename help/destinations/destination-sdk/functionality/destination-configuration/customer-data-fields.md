---
description: Obtenga información sobre cómo crear campos de entrada en la interfaz de usuario de Experience Platform que permitan a los usuarios especificar información diversa relevante para conectarse y exportar datos a su destino.
title: Campos de datos del cliente
exl-id: 7f5b8278-175c-4ab8-bf67-8132d128899e
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 5%

---

# Configurar los datos introducidos por el usuario mediante los campos de datos del cliente

Al conectarse al destino en la interfaz de usuario de Experience Platform, es posible que necesite que los usuarios proporcionen detalles de configuración específicos o seleccionen las opciones específicas que pone a su disposición. En Destination SDK, estas opciones se denominan campos de datos de clientes.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Casos de uso para campos de datos de clientes {#use-cases}

Utilice los campos de datos del cliente para una variedad de casos de uso en los que necesite que los usuarios introduzcan datos en la interfaz de usuario de Experience Platform. Por ejemplo, utilice campos de datos de clientes cuando los usuarios necesiten proporcionar:

* Nombres y rutas del bloque de almacenamiento en la nube, para destinos basados en archivos.
* El formato aceptado por los campos de datos del cliente.
* Tipos de compresión de archivos disponibles que los usuarios pueden seleccionar.
* Listas de extremos disponibles para integraciones en tiempo real (flujo).

Puede configurar los campos de datos del cliente mediante la variable `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todos los tipos de configuración de campos de datos del cliente admitidos que puede utilizar para el destino y muestra lo que los clientes verán en la interfaz de usuario de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Al crear sus propios campos de datos de cliente, puede utilizar los parámetros descritos en la tabla siguiente para configurar su comportamiento.

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|------|---|
| `name` | Cadena | Requerido | Proporcione un nombre para el campo personalizado que está introduciendo. Este nombre no está visible en la interfaz de usuario de Platform, a menos que la variable `title` falta un campo o está vacío. |
| `type` | Cadena | Requerido | Indica el tipo de campo personalizado que está introduciendo. Valores aceptados: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | Cadena | Opcional | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario de Platform. Si este campo está vacío o falta, la interfaz de usuario hereda el nombre del campo del `name` valor. |
| `description` | Cadena | Opcional | Proporcione una descripción para el campo personalizado. Esta descripción no es visible en la interfaz de usuario de Platform. |
| `isRequired` | Booleano | Opcional | Indica si los usuarios deben proporcionar un valor para este campo en el flujo de trabajo de configuración de destino. |
| `pattern` | Cadena | Opcional | Aplica un motivo al campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números ni guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `enum` | Cadena | Opcional | Procesa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `default` | Cadena | Opcional | Define el valor predeterminado a partir de un `enum` lista. |
| `hidden` | Booleano | Opcional | Indica si el campo de datos del cliente se muestra o no en la interfaz de usuario. |
| `unique` | Booleano | Opcional | utilice este parámetro cuando necesite crear un campo de datos de cliente cuyo valor debe ser único en todos los flujos de datos de destino configurados por la organización de un usuario. Por ejemplo, el campo **[!UICONTROL Alias de integración]** en el destino [Personalización](../../../catalog/personalization/custom-personalization.md) debe ser único, lo que significa que dos flujos de datos independientes a este destino no pueden tener el mismo valor para este campo. |
| `readOnly` | Booleano | Opcional | Indica si el cliente puede cambiar el valor del campo o no. |

{style="table-layout:auto"}

En el ejemplo siguiente, la variable `customerDataFields` define dos campos que los usuarios deben introducir en la interfaz de usuario de Platform al conectarse al destino:

* `Account ID`: un ID de cuenta de usuario para la plataforma de destino.
* `Endpoint region`: el extremo regional de la API a la que se conectarán. El `enum` crea un menú desplegable con los valores definidos dentro de disponibles para que los usuarios los seleccionen.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

La experiencia de IU resultante se muestra en la siguiente imagen.

![Imagen de la interfaz de usuario que muestra un ejemplo de campos de datos del cliente.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Nombres y descripciones de las conexiones de destino {#names-description}

Al crear un nuevo destino, el Destination SDK agrega automáticamente **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** a la pantalla de conexión de destino en la interfaz de usuario de Platform. Como puede ver en el ejemplo anterior, la variable **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** Los campos de se representan en la interfaz de usuario sin incluirse en la configuración de los campos de datos del cliente.

>[!IMPORTANT]
>
>Si añade **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** en la configuración de los campos de datos del cliente, los usuarios los verán duplicados en la interfaz de usuario.

## Ordenar campos de datos de clientes {#ordering}

El orden en que se agregan los campos de datos del cliente en la configuración de destino se refleja en la interfaz de usuario de Platform.

Por ejemplo, la configuración siguiente se refleja en consecuencia en la interfaz de usuario, y las opciones se muestran en el orden **[!UICONTROL Nombre]**, **[!UICONTROL Descripción]**, **[!UICONTROL Nombre del cubo]**, **[!UICONTROL Ruta de carpeta]**, **[!UICONTROL Tipo de archivo]**, **[!UICONTROL Formato de compresión]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![Imagen que muestra el orden de las opciones de formato de archivo en la interfaz de usuario de Experience Platform.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Agrupar campos de datos de clientes {#grouping}

Puede agrupar varios campos de datos de clientes en una sección. Al configurar la conexión con el destino en la interfaz de usuario de, los usuarios pueden ver y beneficiarse de una agrupación visual de campos similares.

Para ello, utilice `"type": "object"` para crear el grupo y recopilar los campos de datos de cliente deseados dentro de una `properties` , como se muestra en la siguiente imagen, donde la agrupación **[!UICONTROL Opciones de CSV]** está resaltado.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Imagen que muestra la agrupación de campos de datos del cliente en la IU.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Creación de selectores desplegables para los campos de datos del cliente {#dropdown-selectors}

En situaciones en las que desee permitir que los usuarios seleccionen entre varias opciones, como qué carácter debe utilizarse para delimitar los campos en archivos CSV, puede añadir campos desplegables a la interfaz de usuario.

Para ello, utilice el `namedEnum` como se muestra a continuación y configure un `default` valor de las opciones que puede seleccionar el usuario.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Grabación de pantalla que muestra un ejemplo de selectores desplegables creados con la configuración que se muestra arriba.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Creación de selectores desplegables dinámicos para los campos de datos del cliente {#dynamic-dropdown-selectors}

En situaciones en las que desee llamar dinámicamente a una API y utilizar la respuesta para rellenar dinámicamente las opciones en un menú desplegable, puede utilizar un selector desplegable dinámico.

Los selectores desplegables dinámicos tienen un aspecto idéntico al de [selectores desplegables normales](#dropdown-selectors) en la interfaz de usuario. La única diferencia es que los valores se recuperan dinámicamente de una API.

Para crear un selector desplegable dinámico, debe configurar dos componentes:

**Paso 1.** [Creación de un servidor de destino](../../authoring-api/destination-server/create-destination-server.md#dynamic-dropdown-servers) con un `responseFields` para la llamada de API dinámica, como se muestra a continuación.

```json
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":" <--YOUR-API-ENDPOINT-PATH--> "
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

**Paso 2.** Utilice el `dynamicEnum` como se muestra a continuación. En el ejemplo siguiente, la variable `User` El menú desplegable se recupera mediante el servidor dinámico.


```json {line-numbers="true" highlight="13-21"}
"customerDataFields": [
  {
    "name": "integrationId",
    "title": "Integration ID",
    "type": "string",
    "isRequired": true
  },
  {
    "name": "userId",
    "title": "User",
    "type": "string",
    "isRequired": true,
    "dynamicEnum": {
      "queryParams": [
        "integrationId"
      ],
      "destinationServerId": "<~dynamic-field-server-id~>",
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "value": "$.list",
      "responseFormat": "NAME_VALUE"
    }
  }
]
```

Configure las variables `destinationServerId` al ID del servidor de destino creado en el paso 1. Puede ver el ID del servidor de destino en la respuesta de [recuperar una configuración de servidor de destino](../../authoring-api/destination-server/retrieve-destination-server.md) Llamada de API.

## Crear campos de datos de clientes condicionales {#conditional-options}

Puede crear campos de datos de clientes condicionales, que se muestran en el flujo de trabajo de activación solo cuando los usuarios seleccionan una opción determinada.

Por ejemplo, puede crear opciones de formato de archivo condicional para que se muestren únicamente cuando los usuarios seleccionen un tipo de exportación de archivo específico.

La configuración siguiente crea una agrupación condicional para las opciones de formato de archivo CSV. Las opciones del archivo CSV solo se muestran cuando el usuario selecciona CSV como tipo de archivo deseado para la exportación.

Para establecer un campo como condicional, utilice el `conditional` como se muestra a continuación:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

En un contexto más amplio, puede ver el `conditional` que se utiliza en la configuración de destino siguiente, junto con el campo `fileType` cadena y el `csvOptions` objeto en el que se define.

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

A continuación, puede ver la pantalla de la interfaz de usuario resultante, en función de la configuración anterior. Cuando el usuario selecciona el tipo de archivo CSV, en la interfaz de usuario se muestran opciones de formato de archivo adicionales que hacen referencia al tipo de archivo CSV.

![Grabación de pantalla que muestra la opción de formato de archivo condicional para archivos CSV.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Acceso a campos de datos de clientes con plantillas {#accessing-templatized-fields}

Cuando el destino requiera la entrada del usuario, debe proporcionar una selección de campos de datos de clientes a los usuarios, que pueden rellenar a través de la interfaz de usuario de Platform. A continuación, debe configurar el servidor de destino para que lea correctamente los datos introducidos por el usuario en los campos de datos del cliente. Esto se realiza mediante campos con plantillas.

Los campos con plantilla utilizan el formato `{{customerData.fieldName}}`, donde `fieldName` es el nombre del campo de datos del cliente desde el que está leyendo la información. Todos los campos de datos de clientes con plantilla van precedidos de `customerData.` y entre llaves dobles `{{ }}`.

Por ejemplo, consideremos la siguiente configuración de destino de Amazon S3:

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Esta configuración solicita a los usuarios que escriban su [!DNL Amazon S3] nombre del bloque y ruta de la carpeta en sus respectivos campos de datos del cliente.

Para que el Experience Platform se conecte correctamente a [!DNL Amazon S3]Sin embargo, el servidor de destino debe estar configurado para leer los valores de estos dos campos de datos de clientes, como se muestra a continuación:

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

Los valores con plantillas `{{customerData.bucketName}}` y `{{customerData.path}}` lea los valores proporcionados por el usuario para que el Experience Platform pueda conectarse correctamente a la plataforma de destino.

Para obtener más información sobre cómo configurar el servidor de destino para que lea campos con plantillas, consulte la documentación sobre [campos no codificados frente a campos con plantillas](../destination-server/server-specs.md#templatized-fields).

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo puede permitir a los usuarios introducir información en la interfaz de usuario de Experience Platform a través de los campos de datos de los clientes. Ahora también sabe cómo seleccionar el campo de datos del cliente adecuado para su caso de uso y configurar, ordenar y agrupar campos de datos de clientes en la interfaz de usuario de Platform.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authorization.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
