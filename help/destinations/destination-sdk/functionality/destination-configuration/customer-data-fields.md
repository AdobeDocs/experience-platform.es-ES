---
description: Aprenda a crear campos de entrada en la interfaz de usuario del Experience Platform que permitan a los usuarios especificar información relevante para la conexión y exportación de datos al destino.
title: Campos de datos del cliente
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# Configuración de los datos introducidos por el usuario a través de los campos de datos del cliente

Al conectarse a su destino en la interfaz de usuario del Experience Platform, es posible que necesite que sus usuarios proporcionen detalles de configuración específicos o que seleccionen opciones específicas que ponga a su disposición. En Destination SDK, estas opciones se denominan campos de datos del cliente.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) para ver las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Casos de uso para campos de datos de clientes {#use-cases}

Utilice los campos de datos del cliente para una serie de casos de uso en los que necesita que los usuarios introduzcan datos en la interfaz de usuario del Experience Platform. Por ejemplo, utilice campos de datos de clientes cuando los usuarios necesiten proporcionar:

* Nombres y rutas de compartimento de almacenamiento en la nube para destinos basados en archivos.
* El formato aceptado por los campos de datos del cliente.
* Tipos de compresión de archivos disponibles que los usuarios pueden seleccionar.
* Listas de extremos disponibles para integraciones en tiempo real (flujo continuo).

Puede configurar los campos de datos del cliente mediante la variable `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todos los tipos de configuración de campos de datos de cliente compatibles que puede utilizar para el destino y muestra lo que verán los clientes en la interfaz de usuario del Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Al crear sus propios campos de datos de cliente, puede utilizar los parámetros descritos en la tabla siguiente para configurar su comportamiento.

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|------|---|
| `name` | Cadena | Requerido | Proporcione un nombre para el campo personalizado que está introduciendo. Este nombre no está visible en la interfaz de usuario de Platform, a menos que el `title` El campo está vacío o falta. |
| `type` | Cadena | Requerido | Indica el tipo de campo personalizado que está introduciendo. Valores aceptados: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | Cadena | Opcional | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario de Platform. Si este campo está vacío o falta, la interfaz de usuario hereda el nombre del campo del `name` valor. |
| `description` | Cadena | Opcional | Proporcione una descripción para el campo personalizado. Esta descripción no está visible en la interfaz de usuario de Platform. |
| `isRequired` | Booleano | Opcional | Indica si se requiere que los usuarios proporcionen un valor para este campo en el flujo de trabajo de configuración de destino. |
| `pattern` | Cadena | Opcional | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `enum` | Cadena | Opcional | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `default` | Cadena | Opcional | Define el valor predeterminado de un `enum` lista. |
| `hidden` | Booleano | Opcional | Indica si el campo de datos del cliente se muestra en la interfaz de usuario o no. |
| `unique` | Booleano | Opcional | Utilice este parámetro cuando necesite crear un campo de datos de cliente cuyo valor debe ser único en todos los flujos de datos de destino configurados por la organización de un usuario. Por ejemplo, la variable **[!UICONTROL Alias de integración]** en el campo [Personalización personalizada](../../../catalog/personalization/custom-personalization.md) el destino debe ser único, lo que significa que dos flujos de datos independientes a este destino no pueden tener el mismo valor para este campo. |
| `readOnly` | Booleano | Opcional | Indica si el cliente puede cambiar o no el valor del campo. |

{style="table-layout:auto"}

En el ejemplo siguiente, la variable `customerDataFields` define dos campos que los usuarios deben introducir en la interfaz de usuario de Platform al conectarse al destino:

* `Account ID`: Un ID de cuenta de usuario para la plataforma de destino.
* `Endpoint region`: Punto final regional de la API a la que se conectarán. La variable `enum` crea un menú desplegable con los valores definidos dentro de disponibles para que los usuarios los seleccionen.

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

![Imagen de interfaz de usuario que muestra un ejemplo de campos de datos de clientes.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Nombres y descripciones de conexiones de destino {#names-description}

Al crear un nuevo destino, el Destination SDK agrega automáticamente **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** a la pantalla de conexión de destino en la interfaz de usuario de Platform. Como puede ver en el ejemplo anterior, la variable **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** los campos se procesan en la interfaz de usuario sin incluirse en la configuración de los campos de datos del cliente.

>[!IMPORTANT]
>
>Si agrega **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** en la configuración de los campos de datos del cliente, los usuarios los verán duplicados en la interfaz de usuario.

## Ordenar campos de datos del cliente {#ordering}

El orden en que se agregan los campos de datos del cliente en la configuración de destino se refleja en la interfaz de usuario de Platform.

Por ejemplo, la configuración siguiente se refleja en consecuencia en la interfaz de usuario, con las opciones que se muestran en el orden **[!UICONTROL Nombre]**, **[!UICONTROL Descripción]**, **[!UICONTROL Nombre del depósito]**, **[!UICONTROL Ruta de carpeta]**, **[!UICONTROL Tipo de archivo]**, **[!UICONTROL Formato de compresión]**.

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

![Imagen que muestra el orden de las opciones de formato de archivo en la interfaz de usuario del Experience Platform.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Agrupar campos de datos de clientes {#grouping}

Puede agrupar varios campos de datos de clientes dentro de una sección. Al configurar la conexión con el destino en la interfaz de usuario, los usuarios pueden ver y beneficiarse de una agrupación visual de campos similares.

Para ello, utilice `"type": "object"` para crear el grupo y recopilar los campos de datos de cliente deseados dentro de un `properties` , como se muestra en la imagen siguiente, donde la agrupación **[!UICONTROL Opciones de CSV]** está resaltado.

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

![Imagen que muestra la agrupación de campos de datos de clientes en la interfaz de usuario.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Creación de selectores desplegables para campos de datos de clientes {#dropdown-selectors}

En los casos en los que desee permitir que los usuarios seleccionen entre varias opciones, por ejemplo, qué carácter debe utilizarse para delimitar los campos de los archivos CSV, puede agregar campos desplegables a la interfaz de usuario.

Para ello, utilice el `namedEnum` como se muestra a continuación y configure un `default` para las opciones que el usuario puede seleccionar.

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

![La grabación de pantalla muestra un ejemplo de selectores desplegables creados con la configuración que se muestra arriba.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Creación de campos de datos de cliente condicionales {#conditional-options}

Puede crear campos de datos de cliente condicionales, que se muestran en el flujo de trabajo de activación solo cuando los usuarios seleccionan una determinada opción.

Por ejemplo, puede crear opciones de formato de archivo condicionales para que se muestren solo cuando los usuarios seleccionen un tipo de exportación de archivo específico.

La configuración siguiente crea una agrupación condicional para las opciones de formato de archivo CSV. Las opciones del archivo CSV solo se muestran cuando el usuario selecciona el CSV como tipo de archivo deseado para la exportación.

Para definir un campo como condicional, utilice la variable `conditional` como se muestra a continuación:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

En un contexto más amplio, puede ver la variable `conditional` campo que se utiliza en la configuración de destino a continuación, junto con la variable `fileType` y `csvOptions` objeto en el que está definido.

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

A continuación, puede ver la pantalla de IU resultante, según la configuración anterior. Cuando el usuario selecciona el CSV de tipo de archivo, en la interfaz de usuario se muestran opciones adicionales de formato de archivo que hacen referencia al tipo de archivo CSV.

![La grabación de pantalla muestra la opción de formato de archivo condicional para archivos CSV.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Acceso a los campos de datos del cliente con plantillas {#accessing-templatized-fields}

Cuando el destino requiera la introducción de datos por parte del usuario, debe proporcionar una selección de campos de datos de clientes a los usuarios que puedan rellenar mediante la interfaz de usuario de Platform. A continuación, debe configurar el servidor de destino para que lea correctamente los datos introducidos por el usuario en los campos de datos del cliente. Esto se realiza a través de campos con plantilla.

Los campos con plantilla utilizan el formato `{{customerData.fieldName}}`, donde `fieldName` es el nombre del campo de datos del cliente desde el que está leyendo información. Todos los campos de datos de clientes con plantillas van precedidos de `customerData.` y entre llaves dobles `{{ }}`.

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

Esta configuración indica a los usuarios que introduzcan sus [!DNL Amazon S3] nombre de bloque y ruta de carpeta en sus respectivos campos de datos de cliente.

Para que el Experience Platform se conecte correctamente a [!DNL Amazon S3], el servidor de destino debe estar configurado para leer los valores de estos dos campos de datos de cliente, como se muestra a continuación:

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

Los valores con plantilla `{{customerData.bucketName}}` y `{{customerData.path}}` lea los valores proporcionados por el usuario para que el Experience Platform pueda conectarse correctamente a la plataforma de destino.

Para obtener más información sobre cómo configurar el servidor de destino para que lea los campos con plantilla, consulte la documentación de [campos predefinidos frente a campos con plantilla](../destination-server/server-specs.md#templatized-fields).

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo puede permitir que los usuarios introduzcan información en la interfaz de usuario del Experience Platform a través de los campos de datos del cliente. Ahora también sabe cómo seleccionar el campo de datos del cliente correcto para su caso de uso y configurar, ordenar y agrupar campos de datos del cliente en la interfaz de usuario de Platform.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)