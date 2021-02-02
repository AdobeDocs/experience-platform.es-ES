---
keywords: Experience Platform;inicio;temas populares;evaluación de segmentos;Servicio de segmentación;segmentación;Segmentación;evaluación de un segmento;acceso a los resultados del segmento;evaluación y acceso al segmento;
solution: Experience Platform
title: Evaluar un segmento
topic: tutorial
type: Tutorial
description: Este documento proporciona un tutorial para evaluar los segmentos y acceder a los resultados de los mismos mediante la API de segmentación.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---


# Evaluar y acceder a los resultados de los segmentos

Este documento proporciona un tutorial para evaluar los segmentos y acceder a los resultados de los mismos mediante [[!DNL Segmentation API]](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos [!DNL Adobe Experience Platform] servicios que intervienen en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):: Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Encabezados requeridos

Este tutorial también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas a las API [!DNL Platform] correctamente. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluar un segmento

Una vez desarrollada, probada y guardada la definición del segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación a petición.

[La evaluación](#scheduled-evaluation)  programada (también conocida como &#39;segmentación programada&#39;) le permite crear una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la  [evaluación a ](#on-demand-evaluation) pedido implica crear un trabajo de segmento para generar la audiencia inmediatamente. A continuación se describen los pasos para cada uno de ellos.

Si aún no ha completado el [crear un segmento mediante el tutorial API de segmentación](./create-a-segment.md) o ha creado una definición de segmento mediante [Generador de segmentos](../ui/overview.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaluation}

Mediante una evaluación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un solo entorno de simulación de pruebas, no podrá usar la evaluación programada.

### Crear una programación

Al realizar una solicitud de POST al extremo `/config/schedules`, puede crear una programación e incluir la hora específica en la que se debe activar la programación.

Encontrará información más detallada sobre el uso de este extremo en la [guía del extremo de programación](../api/schedules.md#create)

### Habilitar una programación

De forma predeterminada, una programación se desactiva cuando se crea a menos que la propiedad `state` se establezca en `active` en el cuerpo de la solicitud de creación (POST). Puede habilitar una programación (establezca `state` en `active`) haciendo una solicitud de PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta de acceso.

Encontrará información más detallada sobre el uso de este extremo en la [guía del extremo de programación](../api/schedules.md#update-state)

### Actualizar la hora de programación

La temporización de programación se puede actualizar realizando una solicitud de PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

Encontrará información más detallada sobre el uso de este extremo en la [guía del extremo de programación](../api/schedules.md#update-schedule)

## Evaluación a petición

La evaluación a petición le permite crear un trabajo de segmento para generar un segmento de audiencia cuando lo necesite. A diferencia de la evaluación programada, esto solo sucederá cuando se solicite y no se repita.

### Crear un trabajo de segmento

Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia. Hace referencia a una definición de segmento, así como a cualquier directiva de combinación que controle cómo [!DNL Real-time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información diversa sobre el segmento, como los errores que se hayan producido durante el procesamiento y el tamaño final de la audiencia.

Puede crear un nuevo trabajo de segmento haciendo una solicitud de POST al extremo `/segment/jobs` en la API [!DNL Real-time Customer Profile].

Encontrará información más detallada sobre el uso de este extremo en la guía de extremo de trabajos de segmento [](../api/segment-jobs.md#create)


### Buscar estado del trabajo del segmento

Puede utilizar `id` para un trabajo de segmento específico para realizar una solicitud de búsqueda (GET) con el fin de realizar la vista del estado actual del trabajo.

Encontrará información más detallada sobre el uso de este extremo en la guía de extremo de trabajos de segmento [](../api/segment-jobs.md#get)

## Interpretar resultados de segmentos

Cuando los trabajos de segmentos se ejecutan correctamente, el mapa `segmentMembership` se actualiza para cada perfil incluido en el segmento. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se ingieren en  [!DNL Platform], lo que permite la integración con otras soluciones como  [!DNL Adobe Audience Manager].

El siguiente ejemplo muestra el aspecto del atributo `segmentMembership` para cada registro de perfil individual:

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
| `lastQualificationTime` | Marca de hora cuando se hizo la afirmación de pertenencia a segmentos y el perfil entró o salió del segmento. |
| `status` | El estado de la participación de segmentos como parte de la solicitud actual. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`existing`:: La entidad sigue estando en el segmento.</li><li>`realized`:: La entidad está ingresando al segmento.</li><li>`exited`:: La entidad está saliendo del segmento.</li></ul> |

## Acceso a los resultados de los segmentos

Se puede acceder a los resultados de un trabajo de segmento de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las siguientes secciones describen estas opciones con más detalle.

## Buscar un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo mediante la API [!DNL Real-time Customer Profile]. Los pasos completos para acceder a perfiles individuales están disponibles en el tutorial [Acceso a datos de Perfil del cliente en tiempo real mediante el tutorial API de Perfil](../../profile/api/entities.md).

## Exportar un segmento {#export}

Una vez completado correctamente un trabajo de segmentación (el valor del atributo `status` es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos en el que se pueda acceder a él y tomar medidas al respecto.

Se requieren los siguientes pasos para exportar la audiencia:

- [Crear un conjunto de datos](#create-a-target-dataset)  de destinatario: cree el conjunto de datos para albergar miembros de audiencia.
- [Generar perfiles de audiencia en el conjunto de datos](#generate-profiles-for-audience-members) : Rellene el conjunto de datos con Perfiles individuales XDM basados en los resultados de un trabajo de segmento.
- [Monitorear el progreso](#monitor-export-progress)  de exportación: compruebe el progreso actual del proceso de exportación.
- [Leer datos](#next-steps)  de audiencia: recupere los Perfiles individuales XDM resultantes que representan a los miembros de la audiencia.

### Creación de un conjunto de datos de destinatario

Al exportar una audiencia, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos se configure correctamente para garantizar que la exportación se realiza correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que se muestra a continuación). Para exportar un segmento, el conjunto de datos debe basarse en [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso la clase de Perfil individual XDM. Para obtener más información sobre los esquemas de vista de unión, consulte la sección [Perfil del cliente en tiempo real de la guía para desarrolladores de Esquema Registry](../../xdm/api/getting-started.md).

Existen dos maneras de crear el conjunto de datos necesario:

- **Uso de API:** los pasos que se siguen en este tutorial describen cómo crear un conjunto de datos que haga referencia al  [!DNL XDM Individual Profile Union Schema] uso de la  [!DNL Catalog] API.
- **Uso de la interfaz de usuario:** para utilizar la interfaz de  [!DNL Adobe Experience Platform] usuario para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos del  [tutorial de la interfaz de usuario y, a continuación, vuelva a este tutorial para continuar con los pasos para ](../ui/overview.md) generar perfiles [ ](#generate-xdm-profiles-for-audience-members) de audiencia.

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [generar perfiles de audiencia](#generate-xdm-profiles-for-audience-members).

**Formato API**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre descriptivo para el conjunto de datos. |
| `schemaRef.id` | ID de la vista de unión (esquema) con la que se asociará el conjunto de datos. |
| `fileDescription.persisted` | Un valor booleano que cuando se establece en `true`, permite que el conjunto de datos persista en la vista de unión. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene la ID única de sólo lectura generada por el sistema del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los miembros de la audiencia.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generar perfiles para miembros de audiencia {#generate-profiles}

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para que los miembros de la audiencia permanezcan en el conjunto de datos realizando una solicitud de POST al extremo `/export/jobs` de la API [!DNL Real-time Customer Profile] y proporcionando la ID del conjunto de datos y la información del segmento para los segmentos que desea exportar.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#create)

### Monitorear el progreso de exportación

Como proceso de trabajo de exportación, puede supervisar su estado realizando una solicitud de GET al extremo `/export/jobs` e incluyendo el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que el campo `status` devuelve el valor &quot;SUCCEEDED&quot;.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#get)

## Pasos siguientes

Una vez que la exportación se ha completado correctamente, los datos estarán disponibles dentro de [!DNL Data Lake] en [!DNL Experience Platform]. A continuación, puede utilizar [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) para acceder a los datos mediante el `batchId` asociado con la exportación. Según el tamaño del segmento, los datos pueden estar en fragmentos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API [!DNL Data Access] para acceder y descargar archivos por lotes, siga el [Tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede acceder a los datos de segmentos exportados correctamente mediante [!DNL Adobe Experience Platform Query Service]. Mediante la interfaz de usuario o la API RESTful, [!DNL Query Service] le permite escribir, validar y ejecutar consultas en datos dentro de [!DNL Data Lake].

Para obtener más información sobre cómo consulta de datos de audiencia, consulte la documentación de [[!DNL Query Service]](../../query-service/home.md).
