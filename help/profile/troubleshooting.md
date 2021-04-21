---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Guía de solución de problemas del perfil del cliente en tiempo real
topic-legacy: guide
type: Documentation
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real, así como una guía de solución de problemas para detectar errores comunes al trabajar con datos de perfil mediante Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Guía de solución de problemas del perfil del cliente en tiempo real

Este documento proporciona respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real, así como una guía de solución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente al combinar datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. Esto permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes para los clientes en varios canales.

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre el Perfil del cliente en tiempo real.

### ¿Qué tipo de datos se aceptan para el perfil del cliente en tiempo real?

El perfil acepta datos de **registro** y **serie temporal**, siempre que los datos en cuestión contengan al menos un valor de identidad que asocie los datos a una persona individual única.

Al igual que todos los servicios de plataforma, Profile requiere que sus datos se estructuren semánticamente en un esquema del Modelo de datos de experiencia (XDM). A su vez, este esquema debe tener una **identidad principal** definida y debe estar habilitado para utilizarse en Perfil.

Si no está familiarizado con XDM, comience con la [información general de XDM](../xdm/home.md) para obtener más información. A continuación, consulte la guía del usuario de XDM para ver los pasos sobre cómo [establecer campos de identidad](../xdm/tutorials/create-schema-ui.md#identity-field) y [habilitar un esquema para Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### ¿Dónde se almacenan los datos de perfil?

El perfil del cliente en tiempo real mantiene su propio almacén de datos (denominado &quot;almacén de perfiles&quot;), independiente del lago de datos que contiene otros datos de la plataforma ingerida.

### Si ya he introducido datos en Platform, ¿puedo hacer que esté disponible en el Almacenamiento de perfiles?

Si los datos se han ingerido en un conjunto de datos que no sea de Perfil, debe volver a ingerirlos en un conjunto de datos habilitado para Perfil para que estén disponibles en el almacén de perfiles. Es posible habilitar un conjunto de datos existente para Perfil, pero cualquier dato que se haya introducido antes de esa configuración aún no aparecerá en el almacén de perfiles.

Si desea agregar datos ingestados anteriormente al almacén de perfiles, siga el [tutorial de configuración del conjunto de datos](./tutorials/dataset-configuration.md) para crear un nuevo conjunto de datos o convertir un conjunto de datos existente para que se habilite para el perfil y, a continuación, vuelva a introducir los datos deseados en ese conjunto de datos.

### ¿Cómo puedo ver mis datos de perfil ingestados?

Existen varios métodos para ver los datos del perfil, en función de si utiliza la API o la IU.

#### Uso de la API

Si conoce los ID de las entidades de perfil a las que desea acceder, puede utilizar el extremo `/entities` (acceso de perfil) en la API de perfil para buscar esas entidades. Consulte la sección sobre [entidades](./api/entities.md) en la guía para desarrolladores para obtener más información.

También puede utilizar la API del servicio de segmentación de Adobe Experience Platform para acceder a los perfiles individuales de los clientes que cumplen los requisitos para pertenecer a un segmento. Consulte la [información general del servicio de segmentación](../segmentation/home.md) para obtener más información.

#### Uso de la interfaz de usuario

En la interfaz de usuario del Experience Platform, la pestaña **[!UICONTROL Browse]** del espacio de trabajo **[!UICONTROL Profiles]** le permite ver el recuento total de perfiles y buscar perfiles individuales por su valor de identidad. Consulte la [Guía del usuario del perfil](./ui/user-guide.md) para obtener más información.

También puede ver una lista de sus segmentos en la pestaña **[!UICONTROL Browse]** del espacio de trabajo **[!UICONTROL Segments]**. Después de seleccionar un segmento, se muestra una muestra de perfiles cualificados para ese segmento. A continuación, puede seleccionar cualquiera de estos perfiles enumerados para ver sus detalles. Consulte la [información general de la interfaz de segmentación](../segmentation/ui/overview.md) para obtener más información.

## Códigos de error

A continuación se muestra una lista de mensajes de error que puede encontrar al trabajar con la API de perfil del cliente en tiempo real. Si el error que encuentra no aparece en la lista, puede que lo encuentre en la [Guía general de solución de problemas de la plataforma](../landing/troubleshooting.md) en su lugar.

### No se pudo buscar el esquema del atributo calculado para la ruta proporcionada

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando el sistema no puede encontrar el esquema proporcionado en la carga útil de la solicitud. Asegúrese de haber proporcionado el ID de inquilino correcto en la propiedad `path` de la carga útil y de que los valores de `schema.name` sean un nombre de esquema válido.

Si no conoce su ID de inquilino, puede recuperarlo siguiendo los pasos de la [Guía para desarrolladores del Registro de Esquemas](../xdm/api/getting-started.md).

### Ya existe una función con el mismo nombre para el esquema especificado o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Sustituya el valor por un nombre único antes de volver a intentarlo.

### El esquema de devolución de la expresión no es el mismo que el esquema del atributo calculado en el esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Sustituya el valor por un nombre único antes de volver a intentarlo.

### Solicitud de eliminación no válida (trabajo del sistema de perfiles)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Este error se produce cuando se proporciona una carga útil no válida para un trabajo del sistema de eliminación. Asegúrese de proporcionar un conjunto de datos o ID de lote válidos en la propiedad `dataSetID` o `batchID` de la carga útil, respectivamente. Consulte la sección sobre [creación de una solicitud de eliminación](./api/profile-system-jobs.md#create-a-delete-request) en la guía para desarrolladores de perfiles para obtener más información.

### Lote no encontrado para el conjunto de datos de perfil

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

Este error se produce cuando no se encontró un lote válido al intentar crear una solicitud de eliminación para datos de perfil. Compruebe que ha introducido el ID correcto para un conjunto de datos habilitado para perfil antes de intentarlo de nuevo.

### Todavía no se ha creado el destino de la proyección

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Este error se produce cuando el `destinationId` proporcionado en una solicitud `POST /config/projections` no es válido. Compruebe que ha proporcionado un ID de destino válido antes de intentarlo de nuevo. Para crear un nuevo destino, siga los pasos descritos en la [Guía para desarrolladores de perfil](./api/edge-projections.md#create-a-destination).

### Tipo de medio no admitido

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Este error se produce al enviar una solicitud de POST o PUT con un encabezado de tipo de contenido no válido. Compruebe que está proporcionando un valor de tipo de contenido válido para el punto final que está utilizando.

La mayoría de los extremos de perfil aceptan &quot;application/json&quot; para el encabezado Content-Type, con las siguientes excepciones:

| Punto final | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
