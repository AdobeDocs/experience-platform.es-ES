---
solution: Experience Platform
title: Evaluar y acceder a los resultados del segmento
type: Tutorial
description: Siga este tutorial para aprender a evaluar las definiciones de segmentos y acceder a los resultados de la segmentación mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 2%

---

# Evaluación y acceso a resultados de definición de segmentos

Este documento proporciona un tutorial para evaluar definiciones de segmentos y acceder a estos resultados mediante [[!DNL Segmentation API]](../api/getting-started.md).

## Introducción

Este tutorial requiere una comprensión práctica de los distintos servicios de [!DNL Adobe Experience Platform] implicados en la creación de audiencias. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite crear audiencias a partir de los datos de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente. Para utilizar la segmentación de la mejor manera posible, asegúrate de que tus datos se incorporen como perfiles y eventos según las [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Encabezados obligatorios

Este tutorial también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de [!DNL Experience Platform]. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Las solicitudes a las API [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluación de una definición de segmento {#evaluate-a-segment}

Una vez que haya desarrollado, probado y guardado la definición del segmento, puede evaluarla mediante la evaluación programada o la evaluación bajo demanda.

[La evaluación programada](#scheduled-evaluation) (también conocida como &quot;segmentación programada&quot;) le permite crear una programación recurrente para ejecutar un trabajo de exportación a una hora específica, mientras que la [evaluación bajo demanda](#on-demand-evaluation) implica la creación de un trabajo de segmento para generar la audiencia inmediatamente. A continuación se describen los pasos de cada uno.

Si todavía no ha completado el tutorial [crear una definición de segmento con la API de segmentación](./create-a-segment.md) o ha creado una definición de segmento con [Generador de segmentos](../ui/segment-builder.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaluation}

Mediante la evaluación programada, su organización puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE]
>
>La evaluación programada se puede habilitar para las zonas protegidas con un máximo de cinco (5) políticas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco políticas de combinación para [!DNL XDM Individual Profile] en un solo entorno de zona protegida, no podrá utilizar la evaluación programada.

### Creación de una programación

Al realizar una petición POST al extremo `/config/schedules`, puede crear una programación e incluir la hora específica en que se debe activar la programación.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de programaciones](../api/schedules.md#create)

### Habilitar una programación

De manera predeterminada, una programación está inactiva cuando se crea a menos que la propiedad `state` se establezca en `active` en el cuerpo de la solicitud de creación (POST). Puede habilitar una programación (establecer `state` en `active`) realizando una petición PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de programaciones](../api/schedules.md#update-state)

### Actualizar la hora de programación

El tiempo de programación se puede actualizar realizando una petición PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de programaciones](../api/schedules.md#update-schedule)

## Evaluación a la carta

La evaluación bajo demanda le permite crear un trabajo de segmentación para generar una audiencia siempre que lo necesite. A diferencia de la evaluación programada, esto solo ocurrirá cuando se solicite y no sea recurrente.

### Creación de un trabajo de segmentación

Un trabajo de segmentación es un proceso asincrónico que crea un segmento de audiencia bajo demanda. Hace referencia a una definición de segmento, así como a cualquier política de combinación que controle cómo [!DNL Real-Time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmentación se completa correctamente, puede recopilar información diversa acerca de la definición del segmento, como los errores que se hayan podido producir durante el procesamiento y el tamaño final de la audiencia. Se debe ejecutar un trabajo de segmento cada vez que desee actualizar la audiencia a la que se clasifica actualmente la definición del segmento.

Puede crear un nuevo trabajo de segmento realizando una petición POST al extremo `/segment/jobs` en la API [!DNL Real-Time Customer Profile].

Encontrará información más detallada sobre el uso de este extremo en la guía de extremo de [trabajos de segmentación](../api/segment-jobs.md#create)

### Búsqueda del estado del trabajo del segmento

Puede utilizar `id` para un trabajo de segmento específico con el fin de realizar una solicitud de búsqueda (GET) y ver el estado actual del trabajo.

Encontrará información más detallada sobre el uso de este extremo en la guía de extremo de [trabajos de segmentación](../api/segment-jobs.md#get)

## Interpretar resultados del trabajo del segmento

Cuando se ejecutan correctamente los trabajos del segmento, el mapa `segmentMembership` se actualiza para cada perfil incluido en la definición del segmento. `segmentMembership` también almacena cualquier audiencia preevaluada que se haya introducido en [!DNL Experience Platform], lo que permite la integración con otras soluciones como [!DNL Adobe Audience Manager].

El ejemplo siguiente muestra el aspecto del atributo `segmentMembership` para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | La marca de tiempo cuando se realizó la afirmación del abono del segmento y el perfil entró o salió de la definición del segmento. |
| `status` | El estado de participación de la definición del segmento como parte de la solicitud actual. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`realized`: la entidad cumple los requisitos para la definición del segmento.</li><li>`exited`: la entidad está saliendo de la definición del segmento.</li></ul> |

>[!NOTE]
>
>Cualquier pertenencia a segmento que esté en estado `exited` durante más de 30 días, según el `lastQualificationTime`, estará sujeta a eliminación.

## Acceder a resultados de trabajo de segmentos

Se puede acceder a los resultados de un trabajo de segmentación de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las siguientes secciones describen estas opciones con más detalle.

## Búsqueda de un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo mediante la API [!DNL Real-Time Customer Profile]. Los pasos completos para acceder a perfiles individuales están disponibles en el tutorial [Acceder a los datos del perfil del cliente en tiempo real mediante la API de perfil](../../profile/api/entities.md).

## Exportación de un segmento {#export}

Una vez que un trabajo de segmentación se haya completado correctamente (el valor del atributo `status` es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos al que se pueda acceder y sobre el que se pueda actuar.

Se requieren los siguientes pasos para exportar la audiencia:

- [Crear un conjunto de datos de destinatario](#create-a-target-dataset): cree el conjunto de datos para albergar miembros de audiencia.
- [Generar perfiles de audiencia en el conjunto de datos](#generate-profiles): rellene el conjunto de datos con perfiles individuales XDM en función de los resultados de un trabajo de segmentación.
- [Supervisar progreso de exportación](#monitor-export-progress) - Compruebe el progreso actual del proceso de exportación.
- [Leer datos de audiencia](#next-steps) - Recupere los perfiles individuales XDM resultantes que representan a los miembros de su audiencia.

### Crear un conjunto de datos de destinatario {#create-dataset}

Al exportar una audiencia, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos esté configurado correctamente para garantizar que la exportación se realice correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que aparece a continuación). Para exportar una definición de segmento, el conjunto de datos debe basarse en [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso la clase XDM Individual Profile. Para obtener más información sobre los esquemas de vista de unión, consulte la sección [Perfil del cliente en tiempo real de la guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md).

Existen dos formas de crear el conjunto de datos necesario:

- **Usar API:** Los pasos que siguen en este tutorial describen cómo crear un conjunto de datos que hace referencia a [!DNL XDM Individual Profile Union Schema] mediante la API [!DNL Catalog].
- **Uso de la interfaz de usuario:** Para usar la interfaz de usuario de [!DNL Adobe Experience Platform] para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos del [tutorial de la interfaz de usuario](../ui/overview.md) y, a continuación, vuelva a este tutorial para continuar con los pasos para [generar perfiles de audiencia](#generate-profiles).

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente al paso para [generar perfiles de audiencia](#generate-profiles).

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

Una vez que tenga un conjunto de datos que persiste en la unión, puede crear un trabajo de exportación para mantener los miembros de la audiencia en el conjunto de datos realizando una petición POST al extremo `/export/jobs` en la API [!DNL Real-Time Customer Profile] y proporcionando la información del ID del conjunto de datos y la definición del segmento para las definiciones de segmento que desea exportar.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#create)

### Monitorización del progreso de exportación

Como procesos de trabajo de exportación, puede supervisar su estado realizando una petición GET al extremo `/export/jobs` e incluyendo `id` del trabajo de exportación en la ruta. El trabajo de exportación se ha completado una vez que el campo `status` devuelve el valor &quot;CORRECTO&quot;.

Encontrará información más detallada sobre el uso de este extremo en la [guía de extremo de trabajos de exportación](../api/export-jobs.md#get)

## Pasos siguientes

Una vez que la exportación se haya completado correctamente, los datos estarán disponibles en [!DNL Data Lake] en [!DNL Experience Platform]. A continuación, puede usar [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para obtener acceso a los datos mediante el `batchId` asociado con la exportación. Según el tamaño de la definición del segmento, los datos pueden estar en fragmentos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso acerca de cómo usar la API [!DNL Data Access] para obtener acceso y descargar archivos por lotes, siga el [tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede tener acceso a los datos de definición de segmento exportados correctamente usando [!DNL Adobe Experience Platform Query Service]. Al usar la interfaz de usuario o la API RESTful, [!DNL Query Service] le permite escribir, validar y ejecutar consultas sobre datos dentro de [!DNL Data Lake].

Para obtener más información sobre cómo consultar datos de audiencia, consulte la documentación sobre [[!DNL Query Service]](../../query-service/home.md).
