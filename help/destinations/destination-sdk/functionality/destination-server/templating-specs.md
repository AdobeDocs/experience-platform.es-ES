---
description: Obtenga información sobre cómo dar formato a las solicitudes HTTP enviadas al extremo. Utilice el extremo /authoring/destination-servers para configurar las especificaciones de creación de plantillas del servidor de destino en Adobe Experience Platform Destination SDK.
title: Plantillas de especificaciones para destinos creados con Destination SDK
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---

# Especificaciones de plantilla para destinos creados con Destination SDK

Utilice la parte de especificación de plantilla de la configuración del servidor de destino para configurar cómo dar formato a las solicitudes HTTP enviadas al destino.

En una especificación de plantilla puede definir cómo transformar los campos de atributos de perfil entre el esquema XDM y el formato que admite su plataforma.

Las especificaciones de plantilla forman parte de la configuración del servidor de destino para destinos en tiempo real (flujo).

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Puede configurar las especificaciones de la plantilla para su destino mediante el `/authoring/destination-servers` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Actualizar la configuración de un servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | No |

## Configuración de una especificación de plantilla {#configure-template-spec}

El Adobe utiliza un lenguaje de plantilla similar al siguiente [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar los campos del esquema XDM en un formato compatible con el destino.

![Configuración de plantilla resaltada](../../assets/functionality/destination-server/template-configuration.png)

Para obtener más información sobre la transformación, visite los siguientes vínculos:

* [Formato del mensaje](message-format.md)
* [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a audiencias](message-format.md#using-templating)

>[!TIP]
>
>El Adobe ofrece un [herramienta para desarrolladores](../../testing-api/streaming-destinations/create-template.md) que le ayudará a crear y probar una plantilla de transformación de mensajes.

Consulte a continuación un ejemplo de una plantilla de solicitud HTTP, junto con descripciones de cada parámetro individual.

```json
{
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
| `httpMethod` | Cadena | *Requerido.* El método que utilizará el Adobe en las llamadas a su servidor. Métodos admitidos: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Cadena | *Requerido.* En su lugar, utilice `PEBBLE_V1`. |
| `value` | Cadena | *Requerido.* Esta cadena es la versión con caracteres de escape de la plantilla que da formato a las solicitudes HTTP enviadas por Platform al formato esperado por su destino. <br> Para obtener información sobre cómo escribir la plantilla, lea la sección sobre [uso de plantillas](message-format.md#using-templating). <br> Para obtener más información sobre el escape de caracteres, consulte la [Estándar JSON RFC, sección siete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para ver un ejemplo de transformación simple, consulte la [atributos de perfil](message-format.md#attributes) transformación. |
| `contentType` | Cadena | *Requerido.* El tipo de contenido que acepta el servidor. Según el tipo de salida que produzca la plantilla de transformación, puede ser cualquiera de las admitidas [Tipos de contenido de aplicación HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application). En la mayoría de los casos, este valor debe establecerse en `application/json`. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué es una especificación de plantilla y cómo puede configurarla.

Para obtener más información acerca de los demás componentes del servidor de destino, consulte los siguientes artículos:

* [Especificaciones del servidor para destinos creados con Destination SDK](server-specs.md)
* [Formato del mensaje](message-format.md)
* [Configuración de formato de archivo](file-formatting.md)
