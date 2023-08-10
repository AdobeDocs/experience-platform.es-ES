---
description: Obtenga información sobre cómo configurar una directiva de agregación para determinar cómo se deben agrupar y agrupar las solicitudes HTTP al destino.
title: Política de agregación
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 2%

---


# Política de agregación

Para garantizar la máxima eficacia al exportar datos al extremo de la API, puede utilizar varias configuraciones para acumular perfiles exportados en lotes más grandes o más pequeños, agruparlos por identidad y otros casos de uso. Esto también le permite adaptar las exportaciones de datos a cualquier limitación descendente de su punto final de API (limitación de velocidad, número de identidades por llamada de API, etc.).

Utilice la agregación configurable para profundizar en la configuración proporcionada por el Destination SDK o utilice la agregación de mejor esfuerzo para indicar al Destination SDK que agrupe las llamadas de API lo mejor que pueda.

Al crear un destino en tiempo real (de flujo continuo) con Destination SDK, puede configurar cómo se deben combinar los perfiles exportados en las exportaciones resultantes. Este comportamiento está determinado por la configuración de la directiva de agregación.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puede configurar las opciones de la directiva de agregación mediante el `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las configuraciones de directiva de agregación admitidas que puede utilizar para el destino.

Después de leer este documento, consulte la documentación sobre [uso de plantillas](../../functionality/destination-server/message-format.md#using-templating) y el [ejemplos de claves de agregación](../../functionality/destination-server/message-format.md#template-aggregation-key) para saber cómo incluir la directiva de agregación en la plantilla de transformación de mensajes en función de la directiva de agregación seleccionada.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | No |

## Agregación del mejor esfuerzo {#best-effort-aggregation}

La agregación de mejor esfuerzo funciona mejor para los destinos que prefieren menos perfiles por solicitud y que preferirían aceptar más solicitudes con menos datos que menos solicitudes con más datos.

La configuración de ejemplo siguiente muestra una configuración de agregación de mejor esfuerzo. Para ver un ejemplo de agregación configurable, consulte la [agregación configurable](#configurable-aggregation) sección. Los parámetros aplicables a la agregación del mejor esfuerzo se documentan en la tabla siguiente.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `aggregationType` | Cadena | Indica el tipo de directiva de agregación que debe utilizar el destino. Tipos de agregación admitidos: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Número entero | El Experience Platform puede acumular varios perfiles exportados en una sola llamada HTTP. <br><br>Este valor indica el número máximo de perfiles que debe recibir el extremo en una sola llamada HTTP. Tenga en cuenta que se trata de una agregación de mejor esfuerzo. Por ejemplo, si especifica el valor 100, Platform puede enviar cualquier número de perfiles inferior a 100 en una llamada. <br><br> Si el servidor no acepta varios usuarios por solicitud, establezca este valor en `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establecer este indicador en `true` si el servidor solo acepta una identidad por llamada, para un área de nombres de identidad determinada. |

{style="table-layout:auto"}

>[!TIP]
>
>Realice la agregación del mejor esfuerzo si el extremo de la API acepta menos de 100 perfiles por llamada de API.

## Agregación configurable {#configurable-aggregation}

La agregación configurable funciona mejor si prefiere utilizar lotes grandes, con miles de perfiles en la misma llamada. Esta opción también le permite agregar los perfiles exportados en función de reglas de agregación complejas.

La configuración de ejemplo siguiente muestra una configuración de agregación configurable. Para ver un ejemplo de agregación de esfuerzo máximo, consulte la [agregación de mejor esfuerzo](#best-effort-aggregation) sección. Los parámetros aplicables a la agregación configurable se documentan en la siguiente tabla.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `aggregationType` | Cadena | Indica el tipo de directiva de agregación que debe utilizar el destino. Tipos de agregación admitidos: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establecer este indicador en `true` si el servidor solo acepta una identidad por llamada, para un área de nombres de identidad determinada. |
| `configurableAggregation.maxBatchAgeInSecs` | Número entero | Se utiliza en combinación con `maxNumEventsInBatch`, este parámetro determina cuánto tiempo debe esperar el Experience Platform hasta enviar una llamada de API al extremo. <ul><li>Valor mínimo (segundos): 1800</li><li>Valor máximo (segundos): 3600</li></ul> Por ejemplo, si utiliza el valor máximo para ambos parámetros, Experience Platform esperará 3600 segundos O hasta que haya 10000 perfiles cualificados antes de realizar la llamada de API, lo que ocurra primero. |
| `configurableAggregation.maxNumEventsInBatch` | Número entero | Utilizado en conjunto con `maxBatchAgeInSecs`Sin embargo, este parámetro determina cuántos perfiles cualificados deben agregarse en una llamada de API. <ul><li>Valor mínimo: 1000</li><li>Valor máximo: 10000</li></ul> Por ejemplo, si utiliza el valor máximo para ambos parámetros, Experience Platform esperará 3600 segundos O hasta que haya 10000 perfiles cualificados antes de realizar la llamada de API, lo que ocurra primero. |
| `configurableAggregation.aggregationKey` | - | Permite agregar los perfiles exportados asignados al destino en función de los parámetros que se describen a continuación. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Establezca este parámetro en `true` si desea agrupar perfiles exportados a su destino por ID de audiencia. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Establezca este parámetro y `includeSegmentId` hasta `true`, si desea agrupar perfiles exportados a su destino por ID de audiencia y estado de audiencia. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Establezca este parámetro en `true` si desea agrupar perfiles exportados a su destino por área de nombres de identidad. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Establezca este parámetro en `true` si desea que los perfiles exportados se agreguen en grupos en función de una sola identidad (GAID, IDFA, números de teléfono, correo electrónico, etc.). |
| `configurableAggregation.aggregationKey.groups` | Matriz | Cree listas de grupos de identidad si desea agrupar perfiles exportados a su destino por grupos de áreas de nombres de identidad. Por ejemplo, puede combinar perfiles que contengan los identificadores móviles IDFA y GAID en una llamada a su destino y correos electrónicos en otra mediante la configuración que se muestra en el ejemplo anterior. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería tener una mejor comprensión de cómo puede configurar las directivas de agregación para su destino.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Configuración de autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)