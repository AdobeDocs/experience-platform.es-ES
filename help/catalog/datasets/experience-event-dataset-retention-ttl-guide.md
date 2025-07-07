---
title: Administrar la retención de conjuntos de datos de Experience Event en el lago de datos mediante TTL
description: Obtenga información sobre cómo evaluar, establecer y administrar la retención de conjuntos de datos de evento de experiencia en el lago de datos mediante configuraciones de tiempo de vida (TTL) con API de Adobe Experience Platform. Esta guía explica cómo la caducidad a nivel de fila TTL admite políticas de retención de datos, optimiza la eficiencia del almacenamiento y garantiza una administración eficaz del ciclo de vida de los datos. También proporciona casos de uso y prácticas recomendadas para ayudarle a aplicar el TTL de forma eficaz.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 65a132609bc30233ac9f7efbe1981d4f75f3acb9
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---

# Administrar la retención de conjuntos de datos de Experience Event en el lago de datos mediante TTL

La administración eficiente de los datos es fundamental para obtener un rendimiento óptimo, un control de costes y la integridad de los datos. Utilice el Tiempo de vida de retención de conjuntos de datos de evento de experiencia (TTL) para aplicar una caducidad de nivel de fila, lo que elimina automáticamente los registros obsoletos de los conjuntos de datos en el lago de datos y garantiza una eficiencia y una relevancia de datos óptimas.

Esta guía explica cómo evaluar, establecer y administrar TTL mediante la API del servicio de catálogo. Aprenderá cuándo y por qué aplicar TTL, cómo configurar y actualizar valores TTL mediante llamadas a la API y prácticas recomendadas para garantizar una implementación eficaz.

>[!IMPORTANT]
>
>TTL está diseñado para optimizar la administración del ciclo de vida de los datos y la eficiencia del almacenamiento. No es una herramienta de cumplimiento y no se debe confiar en ella para los requisitos regulatorios. El cumplimiento suele requerir estrategias de gobernanza de datos más amplias.

## Razones para utilizar TTL para la administración de datos de nivel de fila

A medida que los conjuntos de datos aumentan, la administración eficiente de los datos cobra cada vez más importancia para preservar el rendimiento, controlar los costes y mantener la relevancia de los datos. La caducidad de datos a nivel de fila basada en TTL automatiza la limpieza de datos al eliminar registros obsoletos sin intervención manual para ayudar a optimizar el almacenamiento y mejorar la eficiencia del sistema.

TTL es útil cuando se administran datos con distinción de tiempo que pierden relevancia con el tiempo. Considere implementar TTL si necesita:

- Reduzca los costes de almacenamiento eliminando automáticamente los registros obsoletos.
- Mejore el rendimiento de las consultas minimizando los datos irrelevantes.
- Mantenga la higiene de los datos conservando solo la información relevante.
- Optimizar la retención de datos para lograr los objetivos empresariales.

>[!NOTE]
>
>La retención de conjuntos de datos de evento de experiencia se aplica a los datos de evento almacenados en el lago de datos. Si está administrando la retención en Real-Time Customer Data Platform, considere la posibilidad de usar [Caducidad del evento de experiencia](../../profile/event-expirations.md) y [Caducidad del perfil seudónimo](../../profile/pseudonymous-profiles.md) junto con la configuración de retención del lago de datos.

Utilice configuraciones de TTL para optimizar el almacenamiento en función de los derechos. Aunque los datos del almacén de perfiles (utilizados en Real-Time CDP) se pueden considerar obsoletos y se eliminan a los 30 días, los mismos datos de evento del lago de datos pueden permanecer disponibles durante 12-13 meses (o más según el derecho) para los casos de uso de Analytics y Data Distiller.

>[!TIP]
>
>Los derechos hacen referencia a los derechos de almacenamiento y retención definidos por los acuerdos de suscripción y licencia de Adobe.

### Ejemplo del sector {#industry-example}

Por ejemplo, considere un servicio de streaming de vídeo que rastree las interacciones del usuario, como vistas de vídeo, búsquedas y recomendaciones. Aunque los datos de participación recientes son cruciales para la personalización, los registros de actividad más antiguos (por ejemplo, las interacciones de hace más de un año) pierden relevancia. Al utilizar la caducidad a nivel de fila, Experience Platform elimina automáticamente los registros obsoletos, lo que garantiza que solo se utilicen datos actuales y significativos para los análisis y las recomendaciones.

## Evaluar la idoneidad de TTL {#evaluate-ttl-suitability}

Antes de aplicar una directiva de retención, compruebe si el conjunto de datos es un buen candidato para la caducidad del nivel de fila. Tenga en cuenta lo siguiente:

- Relevancia de los datos con el tiempo: ¿Los datos más antiguos proporcionan valor o se vuelven obsoletos?
- Impacto en los procesos descendentes: ¿La eliminación de datos afectará a la creación de informes, los análisis o las integraciones?
- Coste del almacenamiento frente al valor de retención: ¿el valor de los datos más antiguos justifica el coste de almacenarlos?

Si los registros históricos son esenciales para el análisis a largo plazo o las operaciones comerciales, es posible que el TTL no sea el enfoque correcto. La revisión de estos factores garantiza que el TTL se ajuste a sus necesidades de retención de datos sin afectar negativamente a la disponibilidad de los datos.

## Prácticas recomendadas para establecer TTL {#best-practices}

Seleccione el valor TTL correcto para garantizar que la política de retención de conjuntos de datos de eventos de experiencia equilibra la retención de datos, la eficiencia del almacenamiento y las necesidades analíticas. Un TTL demasiado corto puede causar pérdida de datos, mientras que uno demasiado largo puede aumentar los costos de almacenamiento y la acumulación de datos innecesaria. Asegúrese de que el TTL se ajuste al propósito de su conjunto de datos teniendo en cuenta la frecuencia con la que se accede a los datos y cuánto tiempo permanece relevante.

La siguiente tabla proporciona recomendaciones TTL comunes basadas en el tipo de conjunto de datos y patrones de uso:

| Tipo de conjunto de datos | TTL recomendado | Casos de uso habituales |
|-----------------------------|------------------------|-------------------|
| Conjuntos de datos a los que se accede frecuentemente | 30 a 90 días | Registros de participación de usuarios, datos del flujo de navegación del sitio web y datos de rendimiento de campañas a corto plazo. |
| Conjuntos de datos archivados | 1 año o más | Registros de transacciones financieras, datos de cumplimiento, análisis de tendencias a largo plazo, conjuntos de datos de aprendizaje automático. |
| Conjuntos de datos administrados por aplicaciones | Hasta 13 meses | Los conjuntos de datos administrados por el sistema tienen restricciones TTL predefinidas, que se aplican automáticamente para cumplir con los límites impuestos por el sistema. |
| Conjuntos de datos administrados por el cliente | 30 días (TTL máximo) | Conjuntos de datos creados mediante la IU, las API o Data Distiller. El TTL debe ser de al menos 30 días y estar dentro del TTL máximo definido. |

Revise la configuración de TTL periódicamente para asegurarse de que sigue ajustándose a las políticas de almacenamiento, las necesidades analíticas y los requisitos empresariales.

### Consideraciones clave al establecer TTL {#key-considerations}

Siga estas prácticas recomendadas para asegurarse de que la configuración de TTL se ajusta a su estrategia de retención de datos:

- Audite los cambios de TTL regularmente. Cada actualización TTL déclencheur un evento de auditoría. Utilice registros de auditoría para rastrear las modificaciones TTL con fines de cumplimiento, gobernanza de datos y resolución de problemas.
- Deshabilite TTL si los datos deben conservarse indefinidamente. Para deshabilitar TTL, establezca `ttlValue` en `null`. Esto evita la caducidad automática y conserva todos los registros de forma permanente. Tenga en cuenta las implicaciones de almacenamiento antes de realizar este cambio.

## Limitaciones de TTL {#limitations}

Tenga en cuenta las siguientes limitaciones al utilizar TTL:

- **La retención de conjuntos de datos de evento de experiencia mediante TTL se aplica a la caducidad de nivel de fila**, no a la eliminación de conjuntos de datos. TTL elimina registros en función de un período de retención definido, pero no elimina conjuntos de datos completos. Para quitar un conjunto de datos, use el [extremo de caducidad del conjunto de datos](../../hygiene/api/dataset-expiration.md) o la eliminación manual.
- La configuración de **TTL permanece activa hasta que se deshabilite explícitamente**. La configuración permanece activa hasta que la desactive. Al deshabilitar TTL se detiene la caducidad y se garantiza que se conserven todos los registros del conjunto de datos.
- **TTL no es una herramienta de cumplimiento**. Mientras que TTL optimiza la administración del almacenamiento y el ciclo de vida, debe implementar estrategias de gobernanza más amplias para garantizar el cumplimiento de la normativa.

## Analizar el tamaño y la relevancia del conjunto de datos antes de aplicar TTL {#analyze-dataset-size}

Antes de aplicar TTL, utilice consultas para analizar el tamaño y la relevancia del conjunto de datos. Ejecute consultas de destino (como el recuento de registros dentro de intervalos de fechas específicos) para obtener una vista previa del impacto de varios valores TTL. A continuación, utilice esta información para elegir un período de retención óptimo que equilibre la utilidad de los datos y la rentabilidad.

![Un flujo de trabajo visual para implementar TTL en conjuntos de datos de evento de experiencia. Los pasos incluyen: evaluar la duración de los datos y el impacto de la eliminación, validar la configuración de TTL con consultas, configurar TTL a través de la API del servicio de catálogo y supervisar continuamente el impacto de TTL y realizar ajustes.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

La ejecución de consultas de destino ayuda a determinar la cantidad de datos que se retendrán o eliminarán en diferentes configuraciones de TTL. Por ejemplo, la siguiente consulta SQL cuenta el número de registros creados en los últimos 30 días:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

La ejecución de consultas similares para diferentes intervalos de tiempo ayuda a validar la configuración de TTL y a garantizar que equilibran la eficacia del almacenamiento y la accesibilidad de los datos.

## Introducción a la administración de TTL

Antes de poder evaluar, establecer y administrar la retención de conjuntos de datos de eventos de experiencia mediante la API del servicio de catálogo, debe saber cómo dar formato a las solicitudes correctamente. Esto incluye conocer las rutas de API, proporcionar los encabezados necesarios y dar formato a las cargas útiles de solicitud. Consulte la [Guía de introducción a la API del servicio de catálogo](../api/getting-started.md) para obtener esta información esencial.

>[!NOTE]
>
>Este documento cubre la caducidad del nivel de fila, que elimina filas caducadas individuales dentro de un conjunto de datos mientras el propio conjunto de datos se mantiene intacto. No se aplica a la caducidad del conjunto de datos, que elimina conjuntos de datos completos y se administra mediante una función independiente. Para la caducidad a nivel de conjunto de datos, consulte la [documentación de API de caducidad del conjunto de datos](../../hygiene/api/dataset-expiration.md).

### Compruebe las restricciones TTL {#check-ttl-constraints}

Utilice el extremo de la API de higiene de datos `/ttl/{DATASET_ID}` para ayudar a planificar las configuraciones de TTL. Este extremo devuelve los valores TTL mínimo y máximo admitidos para su organización, junto con un valor recomendado (`defaultValue`) para el tipo de conjunto de datos.

Consulte la documentación de la [API de higiene de datos](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) de Adobe Developer para obtener más información.

Para [comprobar el TTL aplicado actualmente a un conjunto de datos](#check-applied-ttl-values), realice una petición GET al extremo [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}` en su lugar.

>[!TIP]
>
>La dirección URL de puerta de enlace de Experience Platform y la ruta de acceso base para la API del servicio de catálogo son: `https://platform.adobe.io/data/foundation/catalog`. La ruta de acceso base para la API de higiene de datos es: `https://platform.adobe.io/data/core/hygiene`

**Formato de API**

```http
GET /ttl/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | Cadena generada por el sistema que identifica de forma exclusiva un conjunto de datos. Para encontrar un ID de conjunto de datos, utilice el extremo `/datasets`. Consulte la [guía de API de objetos de catálogo](../api/list-objects.md) para obtener instrucciones sobre el filtrado de respuestas para conjuntos de datos relevantes. |

**Solicitud**

La siguiente solicitud recupera las restricciones TTL de su organización para un conjunto de datos concreto.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve los valores TTL recomendados, máximos y mínimos en función de los derechos de su organización, junto con un TTL sugerido (`defaultValue`) para el conjunto de datos. Este(a) `defaultValue` es una duración TTL recomendada, solamente se proporciona a modo de guía. No se aplica a menos que usted lo configure explícitamente. La respuesta no incluye ningún valor TTL personalizado que ya se pueda establecer. Para ver el TTL actual de un conjunto de datos, use el extremo de GET `/catalog/dataSets/{DATASET_ID}`.

+++Seleccione para ver la respuesta

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Propiedad | Descripción |
|--------------|-------------|
| `defaultValue` | Un valor TTL recomendado para su conjunto de datos. Este valor **no** se aplica automáticamente. Debe establecer explícitamente un TTL para que surta efecto. |
| `maxValue` | Duración TTL máxima permitida por el derecho de su organización. Normalmente, esta duración es de 10 años (`P10Y`). |
| `minValue` | Duración TTL mínima permitida por el derecho de su organización. Normalmente, esta duración es de 30 días (`P30D`). |

### Cómo comprobar los valores TTL aplicados {#check-applied-ttl-values}

Para comprobar el valor TTL actual que se ha aplicado a un conjunto de datos, utilice la siguiente llamada de API:

```http
GET /dataSets/{DATASET_ID}
```

Esta llamada devuelve el objeto `ttlValue` actual (si está establecido) en la sección `extensions.adobe_lakeHouse.rowExpiration`.

**Solicitud**

La siguiente solicitud recupera el valor TTL de su organización para un conjunto de datos concreto.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta incluye el objeto `extensions`, que contiene la configuración TTL actual aplicada al conjunto de datos. El ejemplo de respuesta siguiente se trunca por su brevedad.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Establecer o actualizar el TTL para un conjunto de datos {#set-update-ttl}

>[!IMPORTANT]
>
>La caducidad de nivel de fila basada en TTL solo se puede aplicar a conjuntos de datos de evento que utilizan un esquema de serie temporal. Esto incluye conjuntos de datos basados en la clase ExperienceEvent de XDM estándar, así como esquemas personalizados que amplían el esquema de la serie temporal (`https://ns.adobe.com/xdm/data/time-series`).
>
>Antes de aplicar TTL, utilice la API de Registro de esquemas para comprobar que el esquema del conjunto de datos incluye la extensión correcta comprobando la propiedad `meta:extends`. Consulte la [Documentación del extremo del esquema](../../xdm/api/schemas.md#lookup) para obtener instrucciones sobre cómo hacerlo.

Puede configurar la retención de conjuntos de datos de evento de experiencia estableciendo un TTL nuevo o actualizando uno existente mediante el mismo método de API. Use una petición PATCH al extremo `/v2/datasets/{DATASET_ID}` para aplicar o ajustar el TTL.

**Formato de API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos para el que desea actualizar el valor TTL. |

**Solicitud**

En el ejemplo siguiente, `ttlValue` está establecido en `P3M`. Esto significa que los registros con más de tres meses se eliminan automáticamente. Ajuste el período de retención para adaptarlo a sus necesidades empresariales (por ejemplo, `P6M` durante seis meses o `P12M` durante un año).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| Propiedad | Descripción |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Define la duración antes de que los registros del conjunto de datos se quiten automáticamente. Utiliza el formato de período ISO-8601 (por ejemplo, `P3M` durante 3 meses o `P30D` durante 30 días). |

**Respuesta**

Una respuesta correcta devuelve una referencia al conjunto de datos actualizado, pero no incluye explícitamente la configuración de TTL. Para confirmar la configuración de TTL, realice una solicitud de seguimiento `GET /dataSets/{DATASET_ID}`.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Ejemplo de escenario {#example-scenario}

Considere una plataforma de streaming de vídeo que inicialmente establece el TTL en tres meses para garantizar nuevos datos de participación para la personalización. Sin embargo, si un análisis posterior revela que las interacciones más antiguas siguen proporcionando perspectivas valiosas, el TTL se puede ampliar a seis meses con la siguiente solicitud:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## Preguntas frecuentes sobre política de retención de conjuntos de datos {#faqs}

Estas preguntas frecuentes abarcan preguntas prácticas acerca de los trabajos de retención de conjuntos de datos, los efectos inmediatos de los cambios de TTL, las opciones de recuperación y cómo difieren los períodos de retención en los servicios de Platform.

### ¿A qué tipos de conjuntos de datos puedo aplicar reglas de política de retención?

+++Respuesta
Puede aplicar políticas de retención basadas en TTL a cualquier conjunto de datos que utilice el comportamiento de series temporales. Esto incluye conjuntos de datos basados en la clase ExperienceEvent de XDM estándar, así como esquemas personalizados diseñados para capturar datos de series temporales.

La caducidad a nivel de fila requiere las siguientes condiciones técnicas:

- El esquema debe diseñarse para capturar datos de series temporales.
- El esquema debe incluir un campo de marca de tiempo utilizado para evaluar la caducidad.
- El conjunto de datos debe almacenar datos de nivel de evento, que generalmente utilizan o amplían la clase XDM ExperienceEvent.
- El conjunto de datos debe estar registrado en el servicio de catálogo, ya que la configuración de TTL se aplica a través de `extensions.adobe_lakeHouse.rowExpiration`.
- Los valores TTL deben utilizar el formato de duración ISO-8601 (por ejemplo, `P30D`, `P6M`, `P1Y`).
+++

### ¿Cuándo eliminará el trabajo de retención de conjuntos de datos los datos de los servicios de lago de datos?

+++Respuesta
Los TTL de conjuntos de datos se evalúan y procesan cada 30 días, eliminando todos los registros caducados. Un evento se considera caducado si se ingirió en Experience Platform hace más de 30 días (fecha de ingesta > 30 días) y su fecha de evento supera el periodo de retención definido (TTL).
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### ¿Puedo establecer diferentes políticas de retención para el lago de datos y los servicios de perfil?

+++Respuesta
Sí, puede establecer diferentes políticas de retención para el lago de datos y los servicios de perfil. El período de retención del almacén de perfiles puede ser más corto o más largo que el período de retención del lago de datos, según las necesidades de la organización.
+++

### ¿Cómo puedo comprobar el uso actual de mi conjunto de datos?

+++Respuesta
Puede comprobar el tamaño de almacenamiento del conjunto de datos más reciente para el lago de datos y los almacenes de perfiles como métricas independientes en el área de trabajo de inventario [!UICONTROL Conjunto de datos]. Ordene las columnas para identificar los conjuntos de datos más grandes y comprobar que se aplican las políticas de retención.

Para el uso a nivel de zona protegida, consulte el Panel de uso de licencias. Consulte la [documentación de uso de licencias](../../dashboards/guides/license-usage.md) para obtener más detalles.
+++

### ¿Cómo puedo verificar si el trabajo de retención de datos se realizó correctamente?

+++Respuesta
Puede comprobar el último trabajo de retención de datos comprobando su marca de tiempo en la [interfaz de usuario de configuración de retención de conjuntos de datos](./user-guide.md#data-retention-policy) o en la página Inventario de datos.

También puede realizar una petición GET al siguiente extremo:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

La respuesta incluye la propiedad `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, que indica la marca de tiempo Unix (en milisegundos) de cuando se completó el trabajo TTL más reciente.

Los informes de uso del conjunto de datos histórico no están disponibles actualmente.
+++

### ¿Puedo recuperar los datos eliminados?

+++Respuesta
No, una vez aplicada una política de retención, los datos anteriores al período de retención se eliminan de forma permanente y no se pueden recuperar.
+++

### ¿Cuál es el TTL mínimo que puedo configurar en un conjunto de datos de evento de experiencia de lago de datos?

+++Respuesta
El TTL mínimo de un conjunto de datos de evento de experiencia de lago de datos es de 30 días. El lago de datos funciona como un sistema de copia de seguridad y recuperación de procesamiento durante la ingesta y el procesamiento iniciales. Como resultado, los datos deben permanecer en el lago de datos durante al menos 30 días después de la ingesta antes de que puedan caducar.
+++

### ¿Qué sucede si necesito conservar algunos campos del lago de datos más tiempo del que permite mi política de TTL?

+++Respuesta
Utilice Data Distiller para retener campos específicos que superen el TTL del conjunto de datos y, al mismo tiempo, no sobrepasen los límites de utilización. Cree un trabajo que escriba con regularidad solo los campos necesarios en un conjunto de datos derivado. Este flujo de trabajo garantiza el cumplimiento de un TTL más corto, al tiempo que conserva los datos esenciales para un uso prolongado.

Para obtener más información, consulte la [Guía de creación de conjuntos de datos derivados con SQL](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Pasos siguientes {#next-steps}

Ahora que ha aprendido a administrar la configuración de TTL para la caducidad de nivel de fila, revise la siguiente documentación para comprender mejor la administración de TTL:

- Trabajos de retención: aprenda a programar y automatizar las caducidades de los conjuntos de datos en la interfaz de usuario de Experience Platform con la [guía de la interfaz de usuario del ciclo vital de datos](../../hygiene/ui/dataset-expiration.md), o compruebe las configuraciones de retención de conjuntos de datos y compruebe que se eliminan los registros caducados.
- [Guía de extremo de API de caducidad de conjuntos de datos](../../hygiene/api/dataset-expiration.md): Descubra cómo eliminar conjuntos de datos completos en lugar de solo filas. Aprenda a programar, administrar y automatizar la caducidad de los conjuntos de datos mediante la API para garantizar una retención de datos eficiente.
- [Información general sobre políticas de uso de datos](../../data-governance/policies/overview.md): Aprenda a alinear su estrategia de retención de datos con requisitos de cumplimiento más amplios y restricciones de uso de marketing.
