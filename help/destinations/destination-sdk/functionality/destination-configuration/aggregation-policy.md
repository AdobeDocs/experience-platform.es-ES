---
description: Aprenda a configurar una directiva de agregación para determinar cómo se deben agrupar y agrupar las solicitudes HTTP al destino.
title: Política de agregación
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# Política de agregación

Para garantizar la máxima eficacia al exportar datos al extremo de la API, puede utilizar varios ajustes para agregar perfiles exportados en lotes más grandes o más pequeños, agruparlos por identidad y otros casos de uso. Esto también le permite adaptar las exportaciones de datos a cualquier limitación descendente del extremo de la API (limitación de velocidad, número de identidades por llamada de API, etc.).

Utilice la agregación configurable para profundizar en la configuración proporcionada por el Destination SDK o utilice la agregación de los mejores esfuerzos para indicar al Destination SDK que agrupe las llamadas de API lo mejor que pueda.

Al crear un destino en tiempo real (flujo continuo) con Destination SDK, puede configurar cómo se deben combinar los perfiles exportados en las exportaciones resultantes. Este comportamiento está determinado por la configuración de la directiva de agregación.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puede configurar la configuración de la directiva de agregación mediante el `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las configuraciones de directiva de agregación admitidas que puede utilizar para su destino.

Después de leer este documento, consulte la documentación de [uso de plantillas](../../functionality/destination-server/message-format.md#using-templating) y [ejemplos clave de agregación](../../functionality/destination-server/message-format.md#template-aggregation-key) para comprender cómo incluir la política de agregación en la plantilla de transformación de mensajes en función de la política de agregación seleccionada.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | No |

## Mejor agregación de esfuerzos {#best-effort-aggregation}

La mejor agregación de esfuerzo funciona mejor para destinos que prefieren menos perfiles por solicitud y prefieren aceptar más solicitudes con menos datos que menos solicitudes con más datos.

La configuración de ejemplo siguiente muestra la mejor configuración de agregación de esfuerzo. Para ver un ejemplo de agregación configurable, consulte la [agregación configurable](#configurable-aggregation) para obtener más información. Los parámetros aplicables a la agregación del mejor esfuerzo se documentan en la siguiente tabla.

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
| `aggregationType` | Cadena | Indica el tipo de directiva de agregación que debe utilizar el destino. Tipos de agregación compatibles: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Número entero | El Experience Platform puede acumular varios perfiles exportados en una sola llamada HTTP. <br><br>Este valor indica el número máximo de perfiles que su extremo debe recibir en una sola llamada HTTP. Tenga en cuenta que esta es una agregación de mejor esfuerzo. Por ejemplo, si especifica el valor 100, Platform podría enviar cualquier número de perfiles menores que 100 en una llamada. <br><br> Si el servidor no acepta varios usuarios por solicitud, establezca este valor en `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establezca este indicador como `true` si el servidor solo acepta una identidad por llamada, para un área de nombres de identidad determinada. |

{style="table-layout:auto"}

>[!TIP]
>
>Agregue el mejor esfuerzo si el extremo de la API acepta menos de 100 perfiles por llamada de API.

## Agregación configurable {#configurable-aggregation}

La agregación configurable funciona mejor si prefiere realizar lotes grandes, con miles de perfiles en la misma llamada. Esta opción también le permite agregar los perfiles exportados en función de reglas de agregación complejas.

La configuración de ejemplo siguiente muestra una configuración de agregación configurable. Para ver un ejemplo de agregación de mejor esfuerzo, consulte la [agregación del mejor esfuerzo](#best-effort-aggregation) para obtener más información. Los parámetros aplicables a la agregación configurable se documentan en la siguiente tabla.

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
| `aggregationType` | Cadena | Indica el tipo de directiva de agregación que debe utilizar el destino. Tipos de agregación compatibles: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establezca este indicador como `true` si el servidor solo acepta una identidad por llamada, para un área de nombres de identidad determinada. |
| `configurableAggregation.maxBatchAgeInSecs` | Número entero | Se utiliza en combinación con `maxNumEventsInBatch`, este parámetro determina cuánto tiempo debe esperar el Experience Platform hasta enviar una llamada de API al extremo. <ul><li>Valor mínimo (segundos): 1800</li><li>Valor máximo (segundos): 3600</li></ul> Por ejemplo, si utiliza el valor máximo para ambos parámetros, el Experience Platform esperará 3600 segundos O hasta que haya 10 000 perfiles cualificados antes de realizar la llamada de API, lo que suceda primero. |
| `configurableAggregation.maxNumEventsInBatch` | Número entero | Se usa junto con `maxBatchAgeInSecs`, este parámetro determina cuántos perfiles calificados se deben agregar en una llamada de API. <ul><li>Valor mínimo: 1000</li><li>Valor máximo: 10000</li></ul> Por ejemplo, si utiliza el valor máximo para ambos parámetros, el Experience Platform esperará 3600 segundos O hasta que haya 10 000 perfiles cualificados antes de realizar la llamada de API, lo que suceda primero. |
| `configurableAggregation.aggregationKey` | - | Permite acumular los perfiles exportados asignados al destino según los parámetros descritos a continuación. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Establezca este parámetro como `true` si desea agrupar perfiles exportados a su destino por ID de segmento. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Establezca este parámetro y `includeSegmentId` a `true`, si desea agrupar perfiles exportados a su destino por ID de segmento y estado del segmento. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Establezca este parámetro como `true` si desea agrupar perfiles exportados al destino por el área de nombres de identidad. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Establezca este parámetro como `true` si desea que los perfiles exportados se agreguen en grupos en función de una sola identidad (GAID, IDFA, números de teléfono, correo electrónico, etc.). |
| `configurableAggregation.aggregationKey.groups` | Matriz | Cree listas de grupos de identidad si desea agrupar perfiles exportados a su destino por grupos de áreas de nombres de identidad. Por ejemplo, puede combinar perfiles que contengan los identificadores móviles IDFA y GAID en una llamada a su destino y correos electrónicos en otra utilizando la configuración que se muestra en el ejemplo anterior. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo puede configurar las políticas de agregación para su destino.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Configuración de autenticación de cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)