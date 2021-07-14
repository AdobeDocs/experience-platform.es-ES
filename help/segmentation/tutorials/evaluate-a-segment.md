---
keywords: Experience Platform;inicio;temas populares;evaluación de segmentos;servicio de segmentación;segmentación;segmentación;evaluación de segmentos;acceso a resultados de segmentos;evaluación y acceso a segmentos;
solution: Experience Platform
title: Evaluar y acceder a resultados de segmentos
topic-legacy: tutorial
type: Tutorial
description: Siga este tutorial para aprender a evaluar segmentos y acceder a resultados de segmentos mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---

# Evaluar y acceder a resultados de segmentos

Este documento proporciona un tutorial para evaluar segmentos y acceder a resultados de segmentos usando el [[!DNL Segmentation API]](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los distintos servicios [!DNL Adobe Experience Platform] implicados en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
- [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Encabezados requeridos

Este tutorial también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a las API [!DNL Platform]. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Las solicitudes para las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluar un segmento

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación bajo demanda.

[La evaluación programada](#scheduled-evaluation)  (también conocida como &quot;segmentación programada&quot;) le permite crear una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que  [la ](#on-demand-evaluation) evaluación bajo demanda implica crear un trabajo de segmento para crear la audiencia inmediatamente. A continuación se describen los pasos de cada uno.

Si aún no ha completado el tutorial [crear un segmento mediante la API de segmentación](./create-a-segment.md) o ha creado una definición de segmento mediante [Generador de segmentos](../ui/overview.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaluation}

A través de la evaluación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un entorno limitado único, no podrá utilizar la evaluación programada.

### Crear una programación

Al realizar una solicitud de POST al extremo `/config/schedules` , puede crear una programación e incluir la hora específica en la que se debe activar la programación.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía del extremo de las programaciones](../api/schedules.md#create)

### Activación de una programación

De forma predeterminada, una programación está inactiva cuando se crea a menos que la propiedad `state` esté establecida en `active` en el cuerpo de la solicitud de creación (POST). Puede habilitar una programación (establezca `state` en `active`) realizando una solicitud de PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía del extremo de las programaciones](../api/schedules.md#update-state)

### Actualizar la hora de programación

La temporización de programación se puede actualizar realizando una solicitud del PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía del extremo de las programaciones](../api/schedules.md#update-schedule)

## Evaluación a petición

La evaluación a petición le permite crear un trabajo de segmento para generar un segmento de audiencia siempre que lo necesite. A diferencia de la evaluación programada, esto solo ocurre cuando se solicita y no es recurrente.

### Crear un trabajo de segmento

Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia. Hace referencia a una definición de segmento, así como a cualquier política de combinación que controle cómo [!DNL Real-time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información variada sobre el segmento, como los errores que puedan haberse producido durante el procesamiento y el tamaño definitivo de la audiencia.

Puede crear un nuevo trabajo de segmento realizando una solicitud de POST al extremo `/segment/jobs` en la API [!DNL Real-time Customer Profile].

Puede encontrar información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de segmento](../api/segment-jobs.md#create)


### Buscar estado del trabajo del segmento

Puede utilizar `id` para un trabajo de segmento específico para realizar una solicitud de consulta (GET) con el fin de ver el estado actual del trabajo.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de segmento](../api/segment-jobs.md#get)

## Interpretar resultados de segmentos

Cuando los trabajos de segmentos se ejecutan correctamente, el mapa `segmentMembership` se actualiza para cada perfil incluido en el segmento. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se incorporan a  [!DNL Platform], lo que permite la integración con otras soluciones como  [!DNL Adobe Audience Manager].

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
| `lastQualificationTime` | Marca de fecha y hora en la que se hizo la afirmación de pertenencia al segmento y el perfil ingresó o salió del segmento. |
| `status` | El estado de la participación del segmento como parte de la solicitud actual. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`existing`: La entidad sigue estando en el segmento.</li><li>`realized`: La entidad está introduciendo el segmento.</li><li>`exited`: La entidad está saliendo del segmento.</li></ul> |

## Acceso a los resultados de los segmentos

Se puede acceder a los resultados de un trabajo de segmento de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las secciones siguientes describen estas opciones con más detalle.

## Buscar un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo usando la API [!DNL Real-time Customer Profile]. Los pasos completos para acceder a perfiles individuales están disponibles en el tutorial [Acceso a datos del perfil del cliente en tiempo real mediante la API de perfil](../../profile/api/entities.md).

## Exportación de segmentos {#export}

Una vez que un trabajo de segmentación se haya completado correctamente (el valor del atributo `status` es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos al que se pueda acceder y en el que se pueda actuar.

Se requieren los siguientes pasos para exportar la audiencia:

- [Crear un conjunto de datos de destinatario](#create-a-target-dataset) : cree el conjunto de datos para incluir miembros de audiencia.
- [Generar perfiles de audiencia en el conjunto de datos](#generate-profiles-for-audience-members) : rellene el conjunto de datos con perfiles individuales XDM basados en los resultados de un trabajo de segmento.
- [Monitorizar el progreso de exportación](#monitor-export-progress) : compruebe el progreso actual del proceso de exportación.
- [Leer datos de audiencia](#next-steps) : recupere los perfiles individuales XDM resultantes que representan a los miembros de su audiencia.

### Creación de un conjunto de datos de destino

Al exportar una audiencia, primero debe crearse un conjunto de datos de destino. Es importante que el conjunto de datos esté configurado correctamente para garantizar que la exportación se realice correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que aparece a continuación). Para exportar un segmento, el conjunto de datos debe basarse en [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso que es la clase de Perfil individual XDM. Para obtener más información sobre los esquemas de vista de unión, consulte la sección [Perfil del cliente en tiempo real de la guía para desarrolladores del Registro de esquemas](../../xdm/api/getting-started.md).

Existen dos maneras de crear el conjunto de datos necesario:

- **Uso de API:** los pasos siguientes de este tutorial describen cómo crear un conjunto de datos que haga referencia a  [!DNL XDM Individual Profile Union Schema] mediante la  [!DNL Catalog] API.
- **Uso de la interfaz de usuario:** para utilizar la interfaz de  [!DNL Adobe Experience Platform] usuario para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos en el  [tutorial de la ](../ui/overview.md) interfaz de usuario y, a continuación, vuelva a este tutorial para continuar con los pasos para  [generar perfiles](#generate-xdm-profiles-for-audience-members) de audiencia.

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [generar perfiles de audiencia](#generate-xdm-profiles-for-audience-members).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para mantener a los miembros de audiencia en el conjunto de datos realizando una solicitud de POST al extremo `/export/jobs` en la API [!DNL Real-time Customer Profile] y proporcionando el ID del conjunto de datos y la información del segmento para los segmentos que desea exportar.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#create)

### Monitorización del progreso de exportación

Como proceso de trabajo de exportación, puede monitorizar su estado realizando una solicitud de GET al extremo `/export/jobs` e incluyendo el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que el campo `status` devuelve el valor &quot;SUCCEEDED&quot;.

Puede encontrar información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#get)

## Pasos siguientes

Una vez finalizada correctamente la exportación, los datos están disponibles en [!DNL Data Lake] en [!DNL Experience Platform]. A continuación, puede utilizar [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) para acceder a los datos mediante el `batchId` asociado con la exportación. Dependiendo del tamaño del segmento, los datos pueden estar en trozos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API [!DNL Data Access] para acceder y descargar archivos por lotes, siga el [Tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede acceder a los datos de segmentos exportados correctamente mediante [!DNL Adobe Experience Platform Query Service]. Al usar la interfaz de usuario o la API RESTful, [!DNL Query Service] permite escribir, validar y ejecutar consultas sobre datos dentro de [!DNL Data Lake].

Para obtener más información sobre cómo consultar los datos de audiencia, consulte la documentación de [[!DNL Query Service]](../../query-service/home.md).
