---
description: Las especificaciones de servidor y plantilla se pueden configurar en Adobe Experience Platform Destination SDK a través del punto final común `/authoring/destination-servers`.
title: Opciones de configuración para especificaciones de servidor y plantilla en Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# Opciones de configuración para destinos de flujo continuo especificaciones de servidor y plantilla

## Información general {#overview}

Las especificaciones del servidor y la plantilla se pueden configurar en Adobe Experience Platform Destination SDK a través del punto final común `/authoring/destination-servers`. Lectura [Operaciones de extremo de la API de destinos](./destination-server-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Especificaciones del servidor {#server-specs}

![Configuración del servidor resaltada](./assets/server-configuration.png)

Los clientes podrán activar datos desde Adobe Experience Platform a su destino mediante exportaciones HTTP. La configuración del servidor contiene información sobre el servidor que recibe los mensajes (el servidor de su parte).

Este proceso envía datos de usuario como una serie de mensajes HTTP a la plataforma de destino. Los parámetros siguientes forman la plantilla de especificaciones del servidor HTTP.

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | *Requerido.* Representa un nombre descriptivo del servidor, visible solo para el Adobe. Este nombre no es visible para socios o clientes. Ejemplo `Moviestar destination server`. |
| `destinationServerType` | Cadena | *Requerido.* Establecer como `URL_BASED` para destinos de flujo continuo. |
| `templatingStrategy` | Cadena | *Requerido.* <ul><li>Uso `PEBBLE_V1` si utiliza una macro en lugar de un valor fijo en la variable `value` campo . Utilice esta opción si tiene un punto final como: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Uso `NONE` si no se necesita ninguna transformación en el lado del Adobe, por ejemplo, si tiene un punto final como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que se debe conectar el Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Especificaciones de plantilla {#template-specs}

![Configuración de plantilla resaltada](./assets/template-configuration.png)

La especificación de plantilla le permite configurar cómo dar formato al mensaje exportado a su destino. Adobe utiliza un idioma de plantilla similar al [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar los campos del esquema XDM en un formato compatible con el destino. Para obtener más información sobre la transformación, visite los vínculos siguientes:

* [Formato del mensaje](./message-format.md)
* [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos ](./message-format.md#using-templating)

>[!TIP]
>
>El Adobe ofrece un [herramienta para desarrolladores](./create-template.md) esto le ayuda a crear y probar una plantilla de transformación de mensaje.

## Configuración de ejemplo de destino de transmisión  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `httpMethod` | Cadena | *Requerido.* Método que Adobe utilizará en las llamadas al servidor. Las opciones son `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `value` | Cadena | *Requerido.* Esta cadena es la versión con caracteres de escape que transforma los datos de los clientes de Platform al formato que el servicio espera. <br> Para obtener información sobre cómo escribir la plantilla, lea la [Uso de la sección de plantilla](./message-format.md#using-templating). <br> Para obtener más información sobre el escape de caracteres, consulte la sección [RFC JSON estándar, sección siete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para ver un ejemplo de transformación sencilla, consulte la sección [Atributos de perfil](./message-format.md#attributes) transformación. |
| `contentType` | Cadena | *Requerido.* El tipo de contenido que acepta el servidor. Es muy probable que este valor `application/json`. |

{style=&quot;table-layout:auto&quot;}