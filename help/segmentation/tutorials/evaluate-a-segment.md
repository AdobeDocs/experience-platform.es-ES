---
keywords: Experience Platform;inicio;temas populares;evaluación de segmentos;servicio de segmentación;segmentación;segmentación;evaluar un segmento;acceder a los resultados del segmento;evaluar y acceder al segmento;
solution: Experience Platform
title: Evaluar y acceder a los resultados del segmento
type: Tutorial
description: Siga este tutorial para aprender a evaluar segmentos y acceder a resultados de segmentos mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 378f9260703d388976054431a76ac285724a9ae3
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Evaluación y acceso a los resultados del segmento

Este documento proporciona un tutorial para evaluar segmentos y acceder a los resultados de segmentos mediante el [[!DNL Segmentation API]](../api/getting-started.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los distintos [!DNL Adobe Experience Platform] servicios implicados en la creación de segmentos de audiencia. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): le permite generar segmentos de audiencia a partir de [!DNL Real-Time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Encabezados obligatorios

Este tutorial también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Platform] API. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluación de un segmento {#evaluate-a-segment}

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede evaluar el segmento mediante la evaluación programada o la evaluación bajo demanda.

[Evaluación programada](#scheduled-evaluation) (también conocida como &quot;segmentación programada&quot;) permite crear una programación recurrente para ejecutar un trabajo de exportación a una hora específica, mientras que [evaluación a la carta](#on-demand-evaluation) implica crear un trabajo de segmento para crear la audiencia inmediatamente. A continuación se describen los pasos de cada uno.

Si todavía no ha completado la [Cree un segmento con la API de segmentación](./create-a-segment.md) tutorial o creación de una definición de segmento utilizando [Generador de segmentos](../ui/overview.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaluation}

Mediante la evaluación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE]
>
>La evaluación programada se puede habilitar para zonas protegidas con un máximo de cinco (5) políticas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco políticas de combinación para [!DNL XDM Individual Profile] en un solo entorno de zona protegida, no podrá utilizar la evaluación programada.

### Creación de una programación

Realizando una solicitud de POST a `/config/schedules` punto final, puede crear una programación e incluir la hora específica en la que se debe activar.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de programaciones](../api/schedules.md#create)

### Habilitar una programación

De forma predeterminada, una programación está inactiva cuando se crea a menos que `state` La propiedad se establece en `active` en el cuerpo de la solicitud crear (POST). Puede activar una programación (establezca el `state` hasta `active`) realizando una solicitud de PATCH a `/config/schedules` e incluir el ID de la programación en la ruta.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de programaciones](../api/schedules.md#update-state)

### Actualizar la hora de programación

El horario de programación se puede actualizar realizando una solicitud del PATCH al `/config/schedules` e incluir el ID de la programación en la ruta.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de programaciones](../api/schedules.md#update-schedule)

## Evaluación a la carta

La evaluación bajo demanda le permite crear un trabajo de segmentación para generar un segmento de audiencia siempre que lo necesite. A diferencia de la evaluación programada, esto solo ocurrirá cuando se solicite y no sea recurrente.

### Creación de un trabajo de segmentación

Un trabajo de segmentación es un proceso asincrónico que crea un segmento de audiencia bajo demanda. Hace referencia a una definición de segmento, así como a cualquier política de combinación que controle el modo en que [!DNL Real-Time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmentación se completa correctamente, puede recopilar información diversa acerca del segmento, como los errores que se hayan podido producir durante el procesamiento y el tamaño final de la audiencia. Se debe ejecutar un trabajo de segmento cada vez que desee actualizar la audiencia que actualmente cumple los requisitos para la definición del segmento.

Puede crear un nuevo trabajo de segmentación realizando una solicitud de POST a `/segment/jobs` punto final en la [!DNL Real-Time Customer Profile] API.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de trabajos de segmento](../api/segment-jobs.md#create)

### Búsqueda del estado del trabajo del segmento

Puede usar el complemento `id` para que un trabajo de segmento específico realice una solicitud de consulta (GET) para ver el estado actual del trabajo.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de trabajos de segmento](../api/segment-jobs.md#get)

## Interpretación de resultados de segmentos

Cuando los trabajos de segmentos se ejecutan correctamente, la variable `segmentMembership` el mapa se actualiza para cada perfil incluido en el segmento. `segmentMembership` también almacena cualquier segmento de audiencia evaluado previamente que se haya introducido en [!DNL Platform], permitiendo la integración con otras soluciones como [!DNL Adobe Audience Manager].

El siguiente ejemplo muestra lo que puede hacer el `segmentMembership` Este atributo tiene el siguiente aspecto para cada registro de perfil individual:

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
| `lastQualificationTime` | La marca de tiempo cuando se realizó la afirmación del abono del segmento y el perfil entró o salió del segmento. |
| `status` | El estado de la participación en el segmento como parte de la solicitud actual. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`existing`: la entidad sigue estando en el segmento.</li><li>`realized`: la entidad está introduciendo el segmento.</li><li>`exited`: la entidad está saliendo del segmento.</li></ul> |

>[!NOTE]
>
>Cualquier pertenencia a segmento que esté en la variable `exited` estado durante más de 30 días, según el `lastQualificationTime`, estará sujeto a eliminación.

## Acceso a resultados de segmentos

Se puede acceder a los resultados de un trabajo de segmentación de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las siguientes secciones describen estas opciones con más detalle.

## Búsqueda de un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo usando el complemento [!DNL Real-Time Customer Profile] API. Los pasos completos para acceder a perfiles individuales están disponibles en la [Acceso a datos de perfil del cliente en tiempo real mediante la API de perfil](../../profile/api/entities.md) tutorial.

## Exportación de un segmento {#export}

Después de que un trabajo de segmentación se haya completado correctamente (el valor de `status` atributo es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos al que se pueda acceder y sobre el que se pueda actuar.

Se requieren los siguientes pasos para exportar la audiencia:

- [Crear un conjunto de datos de destinatario](#create-a-target-dataset) : cree el conjunto de datos para albergar miembros de audiencia.
- [Generar perfiles de audiencia en el conjunto de datos](#generate-profiles) : Rellene el conjunto de datos con perfiles individuales XDM en función de los resultados de un trabajo de segmentación.
- [Monitorización del progreso de exportación](#monitor-export-progress) - Comprobar el progreso actual del proceso de exportación.
- [Leer datos de audiencia](#next-steps) : Recupere los perfiles individuales XDM resultantes que representan a los miembros de la audiencia.

### Crear un conjunto de datos de destinatario {#create-dataset}

Al exportar una audiencia, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos esté configurado correctamente para garantizar que la exportación se realice correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de ejemplo de API que aparece a continuación). Para exportar un segmento, el conjunto de datos debe basarse en la variable [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso la clase XDM Individual Profile. Para obtener más información sobre los esquemas de vista de unión, consulte la [Sección Perfil del cliente en tiempo real de la guía para desarrolladores de Registro de esquemas](../../xdm/api/getting-started.md).

Existen dos formas de crear el conjunto de datos necesario:

- **Uso de API:** Los pasos siguientes en este tutorial describen cómo crear un conjunto de datos que haga referencia a la variable [!DNL XDM Individual Profile Union Schema] uso del [!DNL Catalog] API.
- **Uso de la interfaz de usuario:** Para usar la variable [!DNL Adobe Experience Platform] interfaz de usuario para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos en la [Tutorial de IU](../ui/overview.md) y vuelva a este tutorial para continuar con los pasos para [generación de perfiles de audiencia](#generate-profiles).

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso de [generación de perfiles de audiencia](#generate-profiles).

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
| `name` | Nombre descriptivo del conjunto de datos. |
| `schemaRef.id` | El ID de la vista de unión (esquema) a la que se asociará el conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID único de solo lectura generado por el sistema del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los miembros de la audiencia.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generar perfiles para los miembros de la audiencia {#generate-profiles}

Una vez que tenga un conjunto de datos que persiste en la unión, puede crear un trabajo de exportación para mantener los miembros de la audiencia en el conjunto de datos realizando una solicitud del POST a `/export/jobs` punto final en la [!DNL Real-Time Customer Profile] y proporciona el ID del conjunto de datos y la información del segmento para los segmentos que desea exportar.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#create)

### Monitorización del progreso de exportación

Como procesa un trabajo de exportación, puede monitorizar su estado realizando una solicitud de GET a `/export/jobs` punto final e incluir el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que `status` devuelve el valor &quot;SUCCEEDED&quot;.

Encontrará información más detallada sobre el uso de este punto de conexión en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#get)

## Pasos siguientes

Una vez que la exportación se haya completado correctamente, los datos estarán disponibles en el [!DNL Data Lake] in [!DNL Experience Platform]. A continuación, puede utilizar la variable [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acceder a los datos utilizando `batchId` asociado con la exportación. Según el tamaño del segmento, los datos pueden estar en fragmentos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso acerca de cómo usar el complemento [!DNL Data Access] API para acceder y descargar archivos por lotes, siga las [Tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede acceder a los datos de segmentos exportados correctamente mediante [!DNL Adobe Experience Platform Query Service]. Uso de la interfaz de usuario o la API de RESTful, [!DNL Query Service] permite escribir, validar y ejecutar consultas sobre datos dentro de [!DNL Data Lake].

Para obtener más información sobre cómo consultar datos de audiencia, consulte la documentación sobre [[!DNL Query Service]](../../query-service/home.md).
