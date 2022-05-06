---
keywords: Experience Platform;home;popular topics;segment evaluation;Segmentation Service;segmentation;Segmentation;evaluate a segment;access segment results;evaluate and access segment;
solution: Experience Platform
title: Evaluar y acceder a resultados de segmentos
topic-legacy: tutorial
type: Tutorial
description: Siga este tutorial para aprender a evaluar segmentos y acceder a resultados de segmentos mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Evaluate and access segment results

Este documento proporciona un tutorial para evaluar segmentos y acceder a resultados de segmentos usando la variable [[!DNL Segmentation API]](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de las distintas [!DNL Adobe Experience Platform] servicios relacionados con la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Provides a unified, customer profile in real time based on aggregated data from multiple sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Allows you to build audience segments from [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Encabezados requeridos

Este tutorial también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] API. Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluar un segmento {#evaluate-a-segment}

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación bajo demanda.

[Evaluación programada](#scheduled-evaluation) (también conocido como &quot;segmentación programada&quot;) le permite crear una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que [evaluación a petición](#on-demand-evaluation) implica crear un trabajo de segmento para crear la audiencia inmediatamente. A continuación se describen los pasos de cada uno.

Si aún no ha completado el [crear un segmento mediante la API de segmentación](./create-a-segment.md) tutorial o se ha creado una definición de segmento mediante [Generador de segmentos](../ui/overview.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaluation}

A través de la evaluación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] en un entorno limitado, no se puede utilizar la evaluación programada.

### Crear una programación

Haciendo una solicitud de POST al `/config/schedules` , puede crear una programación e incluir la hora específica en la que se debe activar la programación.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [guía de extremo sobre programaciones](../api/schedules.md#create)

### Activación de una programación

De forma predeterminada, una programación está inactiva cuando se crea a menos que el `state` la propiedad se establece en `active` en el cuerpo de la solicitud create (POST). Puede activar una programación (establezca la variable `state` a `active`) realizando una solicitud de PATCH al `/config/schedules` y incluyendo el ID de la programación en la ruta.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [guía de extremo sobre programaciones](../api/schedules.md#update-state)

### Actualizar la hora de programación

La temporización de programación se puede actualizar realizando una solicitud del PATCH al `/config/schedules` y incluyendo el ID de la programación en la ruta.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [guía de extremo sobre programaciones](../api/schedules.md#update-schedule)

## Evaluación a petición

On-demand evaluation allows you to create a segment job in order to generate an audience segment whenever you require it. Unlike scheduled evaluation, this will happen only when requested and is not recurring.

### Crear un trabajo de segmento

A segment job is an asynchronous process that creates an audience segment on demand. Hace referencia a una definición de segmento, así como a cualquier política de combinación que controle cómo [!DNL Real-time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información variada sobre el segmento, como los errores que puedan haberse producido durante el procesamiento y el tamaño definitivo de la audiencia. Es necesario ejecutar un trabajo de segmento cada vez que desee actualizar la audiencia que actualmente se califica para la definición del segmento.

Puede crear un nuevo trabajo de segmento realizando una solicitud de POST al `/segment/jobs` en la variable [!DNL Real-time Customer Profile] API.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [guía de extremo de trabajos de segmentos](../api/segment-jobs.md#create)

### Buscar estado del trabajo del segmento

Puede usar la variable `id` para que un trabajo de segmento específico realice una solicitud de consulta (GET) para ver el estado actual del trabajo.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [guía de extremo de trabajos de segmentos](../api/segment-jobs.md#get)

## Interpretar resultados de segmentos

Cuando los trabajos de segmentos se ejecutan correctamente, la variable `segmentMembership` se actualiza para cada perfil incluido en el segmento. `segmentMembership` también almacena cualquier segmento de audiencia preevaluada que se incorpore en [!DNL Platform], lo que permite la integración con otras soluciones como [!DNL Adobe Audience Manager].

El siguiente ejemplo muestra la variable `segmentMembership` tiene el siguiente aspecto para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `lastQualificationTime` | Marca de fecha y hora en la que se hizo la afirmación de pertenencia al segmento y el perfil ingresó o salió del segmento. |
| `status` | The status of segment participation as part of the current request. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`existing`: La entidad sigue estando en el segmento.</li><li>`realized`: La entidad está introduciendo el segmento.</li><li>`exited`: La entidad está saliendo del segmento.</li></ul> |

## Acceso a los resultados de los segmentos

Se puede acceder a los resultados de un trabajo de segmento de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las secciones siguientes describen estas opciones con más detalle.

## Buscar un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo usando la variable [!DNL Real-time Customer Profile] API. Los pasos completos para acceder a perfiles individuales están disponibles en la [Acceso a los datos del perfil del cliente en tiempo real mediante la API de perfil](../../profile/api/entities.md) tutorial.

## Exportación de segmentos {#export}

After a segmentation job has successfully completed (the value of the `status` attribute is &quot;SUCCEEDED&quot;), you can export your audience to a dataset where it can be accessed and acted upon.

Se requieren los siguientes pasos para exportar la audiencia:

- [Create a target dataset](#create-a-target-dataset) - Create the dataset to hold audience members.
- [Generación de perfiles de audiencia en el conjunto de datos](#generate-profiles) : complete el conjunto de datos con Perfiles individuales XDM basándose en los resultados de un trabajo de segmento.
- [Monitorización del progreso de exportación](#monitor-export-progress) - Compruebe el progreso actual del proceso de exportación.
- [Read audience data](#next-steps) - Retrieve the resulting XDM Individual Profiles representing the members of your audience.

### Creación de un conjunto de datos de destino {#create-dataset}

Al exportar una audiencia, primero debe crearse un conjunto de datos de destino. Es importante que el conjunto de datos esté configurado correctamente para garantizar que la exportación se realice correctamente.

One of the key considerations is the schema upon which the dataset is based (`schemaRef.id` in the API sample request below). Para exportar un segmento, el conjunto de datos debe basarse en la variable [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso que es la clase de Perfil individual XDM. For more information on union view schemas, please see the [Real-time Customer Profile section of the Schema Registry developer guide](../../xdm/api/getting-started.md).

Existen dos maneras de crear el conjunto de datos necesario:

- **Uso de API:** Los pasos que siguen en este tutorial describen cómo crear un conjunto de datos que haga referencia a la variable [!DNL XDM Individual Profile Union Schema] usando la variable [!DNL Catalog] API.
- **Uso de la IU:** Para usar la variable [!DNL Adobe Experience Platform] interfaz de usuario para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos de la sección [Tutorial de la interfaz de usuario](../ui/overview.md) y, a continuación, vuelva a este tutorial para continuar con los pasos de [generación de perfiles de audiencia](#generate-profiles).

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [generación de perfiles de audiencia](#generate-profiles).

**Formato de API**

```http
POST /dataSets
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos, que proporciona parámetros de configuración en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre descriptivo para el conjunto de datos. |
| `schemaRef.id` | El ID de la vista de unión (esquema) con la que se asociará el conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID único de solo lectura generado por el sistema del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los miembros de la audiencia.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generación de perfiles para miembros de audiencia {#generate-profiles}

Una vez que tenga un conjunto de datos que persista en la unión, puede crear un trabajo de exportación para mantener a los miembros de la audiencia en el conjunto de datos realizando una solicitud de POST al `/export/jobs` en la variable [!DNL Real-time Customer Profile] y proporcionando el ID del conjunto de datos y la información del segmento para los segmentos que desea exportar.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [exportar guía de extremo de trabajos](../api/export-jobs.md#create)

### Monitorización del progreso de exportación

Como proceso de trabajo de exportación, puede monitorizar su estado realizando una solicitud de GET al `/export/jobs` y incluyendo `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez finalizado el `status` devuelve el valor &quot;SUCCEEDED&quot;.

Puede encontrar información más detallada sobre el uso de este extremo en la sección [exportar guía de extremo de trabajos](../api/export-jobs.md#get)

## Pasos siguientes

Una vez finalizada correctamente la exportación, los datos están disponibles en el [!DNL Data Lake] en [!DNL Experience Platform]. A continuación, puede usar la variable [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acceder a los datos mediante la variable `batchId` asociado a la exportación. Dependiendo del tamaño del segmento, los datos pueden estar en trozos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo usar la variable [!DNL Data Access] API para acceder y descargar archivos por lotes, siga la [Tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede acceder a los datos de segmentos exportados correctamente mediante [!DNL Adobe Experience Platform Query Service]. Uso de la interfaz de usuario o la API RESTful, [!DNL Query Service] permite escribir, validar y ejecutar consultas sobre datos dentro de la variable [!DNL Data Lake].

Para obtener más información sobre cómo consultar los datos de audiencia, consulte la documentación de [[!DNL Query Service]](../../query-service/home.md).
