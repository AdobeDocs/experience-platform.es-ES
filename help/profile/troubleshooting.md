---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API
title: Guía de resolución de problemas del perfil del cliente en tiempo real
type: Documentation
description: Este documento proporciona respuestas a las preguntas frecuentes acerca del Perfil del cliente en tiempo real, así como una guía de solución de problemas para errores comunes al trabajar con datos de perfil mediante Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Guía de solución de problemas del Perfil del cliente en tiempo real

Este documento proporciona respuestas a las preguntas frecuentes acerca del Perfil del cliente en tiempo real, así como una guía de solución de problemas para errores comunes. Si tiene alguna pregunta o solución de problemas relacionada con otros servicios de Adobe Experience Platform, consulte la [guía de solución de problemas de Experience Platform](../landing/troubleshooting.md).

Con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. Esto permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes para los clientes en varios canales.

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca del Perfil del cliente en tiempo real.

### ¿Qué tipos de datos se aceptan para el perfil del cliente en tiempo real?

El perfil acepta datos de **registro** y **series temporales**, siempre que los datos en cuestión contengan al menos un valor de identidad que asocie los datos con una persona individual única.

Al igual que todos los servicios de Experience Platform, el perfil requiere que sus datos estén estructurados semánticamente con un esquema Experience Data Model (XDM). A su vez, este esquema debe tener una **identidad principal** definida y habilitada para su uso en el perfil.

Si no está familiarizado con XDM, comience con la [descripción general de XDM](../xdm/home.md) para obtener más información. A continuación, consulte la guía del usuario de XDM para ver los pasos sobre cómo [establecer campos de identidad](../xdm/tutorials/create-schema-ui.md#identity-field) y [habilitar un esquema para el perfil](../xdm/tutorials/create-schema-ui.md#profile).

### ¿Dónde se almacenan los datos del perfil?

El perfil del cliente en tiempo real mantiene su propio almacén de datos (denominado &quot;almacén de perfiles&quot;), independiente del lago de datos que contiene otros datos de Experience Platform ingeridos.

### Si ya he introducido datos en Experience Platform, ¿puedo ponerlos a disposición en el almacén de perfiles?

Si los datos se han introducido en un conjunto de datos que no es de perfil, debe volver a introducirlos en un conjunto de datos con perfil habilitado para que estén disponibles en el almacén de perfiles. Es posible habilitar un conjunto de datos existente para el perfil, pero los datos que se hayan introducido antes de esa configuración aún no aparecerán en el almacén de perfiles.

Si desea agregar datos ingeridos anteriormente al almacén de perfiles, siga el [tutorial de configuración del conjunto de datos](./tutorials/dataset-configuration.md) para crear un nuevo conjunto de datos o convertir un conjunto de datos existente para que esté habilitado para el perfil, y luego vuelva a ingerir los datos deseados en ese conjunto de datos.

### ¿Cómo puedo ver los datos de perfil ingeridos?

Existen varios métodos para ver los datos de perfil, en función de si utiliza la API o la interfaz de usuario.

#### Uso de la API

Si conoce los identificadores de las entidades de perfil a las que desea acceder, puede usar el extremo `/entities` (acceso al perfil) en la API del perfil para buscar esas entidades. Consulte la sección sobre [entidades](./api/entities.md) en la guía para desarrolladores para obtener más información.

También puede utilizar la API del servicio de segmentación de Adobe Experience Platform para acceder a los perfiles individuales de los clientes que cumplen los requisitos para ser miembros de una audiencia. Consulte la [descripción general del servicio de segmentación](../segmentation/home.md) para obtener más información.

#### Uso de la IU

En la interfaz de usuario de Experience Platform, la pestaña **[!UICONTROL Examinar]** del área de trabajo **[!UICONTROL Perfiles]** le permite ver el recuento total de perfiles y buscar perfiles individuales por su valor de identidad. Consulte la [Guía de usuario de perfil](./ui/user-guide.md) para obtener más información.

También puede ver una lista de sus audiencias en la ficha **[!UICONTROL Examinar]** del área de trabajo de **[!UICONTROL Audiencias]**. Después de seleccionar una audiencia, se muestra una muestra de perfiles cualificados para esa audiencia. A continuación, puede seleccionar cualquiera de estos perfiles para ver sus detalles. Consulte la [descripción general de la interfaz de usuario de segmentación](../segmentation/ui/overview.md) para obtener más información.

## Códigos de error

A continuación se muestra una lista de mensajes de error que pueden surgir al trabajar con la API del perfil del cliente en tiempo real. Si el error que encuentra no aparece en la lista, puede encontrarlo en la [guía general de solución de problemas de Experience Platform](../landing/troubleshooting.md).

### No se pudo buscar el esquema del atributo calculado para la ruta proporcionada

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando el sistema no encuentra el esquema proporcionado en la carga útil de la solicitud. Asegúrese de haber proporcionado el ID de inquilino correcto en la propiedad `path` de la carga útil y de que los valores de `schema.name` sean un nombre de esquema válido.

Si no conoce su ID de inquilino, puede recuperarlo siguiendo los pasos de la [Guía para desarrolladores de Schema Registry](../xdm/api/getting-started.md).

### Ya existe una función con el mismo nombre para el esquema especificado o definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor por un nombre único antes de intentarlo de nuevo.

### El esquema de devolución de la expresión no es lo mismo que el esquema del atributo calculado en el esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Al crear un nuevo atributo calculado, este error se produce cuando la propiedad `name` proporcionada ya se está utilizando para el esquema indicado en `schema.name`. Reemplace el valor por un nombre único antes de intentarlo de nuevo.

### Solicitud de eliminación no válida (trabajo del sistema de perfiles)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Este error se produce cuando se proporciona una carga útil no válida para un trabajo de eliminación del sistema. Asegúrese de proporcionar un conjunto de datos o un ID de lote válido en la propiedad `dataSetID` o `batchID` de la carga útil, respectivamente. Consulte la sección sobre [creación de una solicitud de eliminación](./api/profile-system-jobs.md#create-a-delete-request) en la Guía para desarrolladores de perfiles para obtener más información.

### No se ha encontrado ningún lote para el conjunto de datos de perfil

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

Este error se produce cuando no se encuentra un lote válido al intentar crear una solicitud de eliminación de datos de perfil. Compruebe que ha introducido el ID correcto para un conjunto de datos con perfil habilitado antes de intentarlo de nuevo.

### Tipo de medios no compatible

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Este error se produce al enviar una petición POST o PUT con un encabezado de tipo de contenido no válido. Compruebe que está proporcionando un valor de Content-Type válido para el extremo que está utilizando.

La mayoría de los extremos del perfil aceptan &quot;application/json&quot; para el encabezado Content-Type, con las siguientes excepciones:

| Punto de conexión | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
