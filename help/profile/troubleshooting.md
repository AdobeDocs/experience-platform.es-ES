---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Guía de solución de problemas de Perfiles de clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# Guía de solución de problemas de Perfiles de clientes en tiempo real

Este documento proporciona respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real, así como una guía de resolución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la guía de solución de problemas del [Experience Platform](../landing/troubleshooting.md).

El Perfil de clientes en tiempo real es un almacén de entidades de búsqueda genérico que combina datos de diversos activos de datos empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de clientes individuales y eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales.

## Preguntas frecuentes

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre el Perfil de los clientes en tiempo real.

### ¿Qué tipo de datos se aceptan para el Perfil del cliente en tiempo real?

Perfil acepta datos de **registros** y de series **** temporales, siempre que los datos en cuestión contengan al menos un valor de identidad que asocie los datos a una persona individual única.

Al igual que todos los servicios de plataforma, Perfil requiere que sus datos estén estructurados semánticamente bajo un esquema de modelo de datos de experiencia (XDM). A su vez, este esquema debe tener una identidad **** principal definida y estar habilitado para su uso en Perfil.

Si no está familiarizado con XDM, consulte el inicio de la descripción general [de](../xdm/home.md) XDM para obtener más información. A continuación, consulte la guía del usuario de XDM para ver los pasos sobre cómo [establecer campos](../xdm/tutorials/create-schema-ui.md#identity-field) de identidad y [habilitar un esquema para Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### ¿Dónde se almacenan los datos de Perfil?

Perfil del cliente en tiempo real mantiene su propio almacén de datos (denominado &quot;almacén de Perfiles&quot;), independiente del Data Lake que contiene otros datos de la plataforma ingerida.

### Si ya he ingerido datos en Platform, ¿puedo hacerlos disponibles en la tienda de Perfiles?

Si los datos se han ingerido en un conjunto de datos que no es de Perfil, debe volver a ingerirlos en un conjunto de datos habilitado para Perfil para que estén disponibles en el almacén de Perfiles. Es posible habilitar un conjunto de datos existente para el Perfil, pero los datos que se ingirieron antes de esa configuración aún no aparecerán en el almacén de Perfiles.

Si desea agregar datos previamente ingestados al almacén de Perfiles, siga el tutorial [de configuración del](./tutorials/dataset-configuration.md) conjunto de datos para crear un nuevo conjunto de datos o convertir un conjunto de datos existente para habilitarlo para el Perfil y luego vuelva a ingerir los datos deseados en ese conjunto de datos.

### ¿Cómo puedo realizar la vista de mis datos de Perfil ingeridos?

Existen varios métodos para ver los datos de Perfil, en función de si utiliza la API o la interfaz de usuario.

#### Uso de la API

Si conoce los ID de las entidades de Perfil a las que desea acceder, puede utilizar el extremo `/entities` (acceso de Perfil) de la API de Perfil para buscar dichas entidades. Consulte la sección sobre [entidades](./api/entities.md) en la guía para desarrolladores para obtener más información.

También puede utilizar la API de servicio de segmentación de Adobe Experience Platform para acceder a los perfiles individuales de clientes que cumplen los requisitos para una suscripción a un segmento. See the [Segmentation Service overview](../segmentation/home.md) for more information.

#### Uso de la interfaz de usuario

En la interfaz de usuario del Experience Platform, la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Perfiles]** le permite realizar vistas del recuento total de perfiles y buscar perfiles individuales por su valor de identidad. Consulte la guía [del usuario de](./ui/user-guide.md) Perfil para obtener más información.

También puede realizar la vista de una lista de los segmentos en la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Segmentos]** . Después de seleccionar un segmento, se muestra una muestra de perfiles calificados para ese segmento. A continuación, puede seleccionar cualquiera de estos perfiles para vista de sus detalles. See the [Segmentation UI overview](../segmentation/ui/overview.md) for more information.

## Códigos de error

La siguiente es una lista de mensajes de error que puede encontrar al trabajar con la API de Perfil del cliente en tiempo real. Si el error que está encontrando no aparece en esta lista, puede encontrarlo en la guía [general de solución de problemas de la](../landing/troubleshooting.md) plataforma.

### No se pudo buscar el esquema del atributo calculado para la ruta proporcionada

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando el sistema no pudo encontrar el esquema proporcionado en la carga útil de la solicitud. Asegúrese de que ha proporcionado el ID de inquilino correcto en la propiedad de la carga útil `path` y de que los valores de `schema.name` es un nombre de esquema válido.

Si no conoce su ID de inquilino, puede recuperarla siguiendo los pasos de la guía [para desarrolladores de](../xdm/api/getting-started.md)Esquema Registry.

### Ya existe una función con el mismo nombre para el esquema especificado o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la `name` propiedad proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor con un nombre único antes de intentarlo de nuevo.

### El esquema de devolución de la expresión no es el mismo que el esquema del atributo calculado en el esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la `name` propiedad proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor con un nombre único antes de intentarlo de nuevo.

### Solicitud de eliminación no válida (trabajo del sistema de Perfil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Este error se produce cuando se proporciona una carga útil no válida para un trabajo de sistema de eliminación. Asegúrese de proporcionar un conjunto de datos o un ID de lote válidos en la propiedad `dataSetID` o `batchID` de la carga útil, respectivamente. Consulte la sección sobre la [creación de una solicitud](./api/profile-system-jobs.md#create-a-delete-request) de eliminación en la guía para desarrolladores de Perfil para obtener más información.

### No se encontró el lote para el conjunto de datos de perfil

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Este error se produce cuando no se encuentra un lote válido al intentar crear una solicitud de eliminación de datos de Perfil. Compruebe que ha introducido el ID correcto para un conjunto de datos habilitado para Perfil antes de intentarlo de nuevo.

### Aún no se ha creado el destino de proyección

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Este error se produce cuando el `destinationId` proporcionado en una `POST /config/projections` solicitud no es válido. Compruebe por doble que ha proporcionado un ID de destino válido antes de intentarlo de nuevo. Para crear un nuevo destino, siga los pasos descritos en la guía para desarrolladores de [Perfil](./api/edge-projections.md#create-a-destination).

### Tipo de medio no admitido

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Este error se produce al enviar una solicitud de POST o PUT con un encabezado Content-Type no válido. Compruebe por doble que está proporcionando un valor de tipo de contenido válido para el punto final que está utilizando.

La mayoría de los extremos de Perfil aceptan &quot;application/json&quot; para el encabezado Content-Type, con las siguientes excepciones:

| Extremo | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |