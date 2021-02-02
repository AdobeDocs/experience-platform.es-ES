---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Guía de resolución de problemas de Perfiles del cliente en tiempo real
topic: guide
type: Documentation
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real, así como una guía de solución de problemas para los errores comunes al trabajar con datos de Perfil mediante Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Guía de solución de problemas de Perfiles de clientes en tiempo real

Este documento proporciona respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real, así como una guía de resolución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios en Adobe Experience Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual mediante la combinación de datos de varios canales, incluso en línea, sin conexión, CRM y de terceros. Esto permite a los especialistas en mercadotecnia impulsar experiencias coordinadas, coherentes y relevantes para los clientes en varios canales.

## Preguntas frecuentes

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre el Perfil de los clientes en tiempo real.

### ¿Qué tipo de datos se aceptan para el Perfil del cliente en tiempo real?

Perfil acepta datos de **registros** y **series temporales**, siempre y cuando los datos en cuestión contengan al menos un valor de identidad que asocie los datos a una persona individual única.

Al igual que todos los servicios de plataforma, Perfil requiere que sus datos estén estructurados semánticamente bajo un esquema de modelo de datos de experiencia (XDM). A su vez, este esquema debe tener una **identidad principal** definida y estar habilitado para su uso en Perfil.

Si no está familiarizado con XDM, inicio con la [información general de XDM](../xdm/home.md) para obtener más información. A continuación, consulte la guía del usuario de XDM para ver los pasos sobre cómo [establecer campos de identidad](../xdm/tutorials/create-schema-ui.md#identity-field) y [habilitar un esquema para Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### ¿Dónde se almacenan los datos de Perfil?

Perfil del cliente en tiempo real mantiene su propio almacén de datos (denominado &quot;almacén de Perfiles&quot;), independiente del Data Lake que contiene otros datos de la plataforma ingerida.

### Si ya he ingerido datos en Platform, ¿puedo hacerlos disponibles en la tienda de Perfiles?

Si los datos se han ingerido en un conjunto de datos que no es de Perfil, debe volver a ingerirlos en un conjunto de datos habilitado para Perfil para que estén disponibles en el almacén de Perfiles. Es posible habilitar un conjunto de datos existente para el Perfil, pero los datos que se ingirieron antes de esa configuración aún no aparecerán en el almacén de Perfiles.

Si desea agregar datos ingestados anteriormente al almacén de Perfiles, siga el [tutorial de configuración de conjuntos de datos](./tutorials/dataset-configuration.md) para crear un nuevo conjunto de datos o convertir un conjunto de datos existente para habilitarlo para el Perfil y luego vuelva a ingerir los datos deseados en ese conjunto de datos.

### ¿Cómo puedo realizar la vista de mis datos de Perfil ingeridos?

Existen varios métodos para ver los datos de Perfil, en función de si utiliza la API o la interfaz de usuario.

#### Uso de la API

Si conoce los ID de las entidades de Perfil a las que desea acceder, puede utilizar el extremo `/entities` (acceso de Perfil) en la API de Perfil para buscar dichas entidades. Consulte la sección sobre [entidades](./api/entities.md) en la guía para desarrolladores para obtener más información.

También puede utilizar la API de servicio de segmentación de Adobe Experience Platform para acceder a los perfiles individuales de clientes que cumplen los requisitos para una suscripción a un segmento. Consulte la [información general del servicio de segmentación](../segmentation/home.md) para obtener más información.

#### Uso de la interfaz de usuario

En la interfaz de usuario del Experience Platform, la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Perfiles]** permite realizar la vista del recuento total de perfiles y buscar perfiles individuales según su valor de identidad. Consulte la [guía del usuario de Perfil](./ui/user-guide.md) para obtener más información.

También puede realizar la vista de una lista de los segmentos en la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Segmentos]**. Después de seleccionar un segmento, se muestra una muestra de perfiles calificados para ese segmento. A continuación, puede seleccionar cualquiera de estos perfiles para vista de sus detalles. Consulte la [información general de la interfaz de usuario de segmentación](../segmentation/ui/overview.md) para obtener más información.

## Códigos de error

La siguiente es una lista de mensajes de error que puede encontrar al trabajar con la API de Perfil del cliente en tiempo real. Si el error que está encontrando no aparece aquí, puede encontrarlo en la [Guía general de solución de problemas de la plataforma](../landing/troubleshooting.md) en su lugar.

### No se pudo buscar el esquema del atributo calculado para la ruta proporcionada

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando el sistema no pudo encontrar el esquema proporcionado en la carga útil de la solicitud. Asegúrese de que ha proporcionado el ID de inquilino correcto en la propiedad `path` de la carga útil y de que los valores de `schema.name` es un nombre de esquema válido.

Si no conoce su ID de inquilino, puede recuperarla siguiendo los pasos de la [guía para desarrolladores del Registro de Esquemas](../xdm/api/getting-started.md).

### Ya existe una función con el mismo nombre para el esquema especificado o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor con un nombre único antes de intentarlo de nuevo.

### El esquema de devolución de la expresión no es el mismo que el esquema del atributo calculado en el esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor con un nombre único antes de intentarlo de nuevo.

### Solicitud de eliminación no válida (trabajo del sistema de Perfil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Este error se produce cuando se proporciona una carga útil no válida para un trabajo de sistema de eliminación. Asegúrese de proporcionar un conjunto de datos o un ID de lote válidos en las propiedades `dataSetID` o `batchID` de la carga útil, respectivamente. Consulte la sección sobre [creación de una solicitud de eliminación](./api/profile-system-jobs.md#create-a-delete-request) en la guía para desarrolladores de Perfil para obtener más información.

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

Este error se produce cuando el `destinationId` proporcionado en una solicitud `POST /config/projections` no es válido. Compruebe por doble que ha proporcionado un ID de destino válido antes de intentarlo de nuevo. Para crear un nuevo destino, siga los pasos descritos en la [guía para desarrolladores de Perfil](./api/edge-projections.md#create-a-destination).

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