---
title: Administrar la retención de conjuntos de datos de Experience Event en el lago de datos mediante TTL
description: Obtenga información sobre cómo evaluar, establecer y administrar la retención de conjuntos de datos de evento de experiencia en el lago de datos mediante configuraciones de tiempo de vida (TTL) con API de Adobe Experience Platform. Esta guía explica cómo la caducidad a nivel de fila TTL admite políticas de retención de datos, optimiza la eficiencia del almacenamiento y garantiza una administración eficaz del ciclo de vida de los datos. También proporciona casos de uso y prácticas recomendadas para ayudarle a aplicar el TTL de forma eficaz.
source-git-commit: 74b6e5f10f7532745180760adf1d96bc57e7b590
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 1%

---

# Administrar la retención de conjuntos de datos de Experience Event en el lago de datos mediante TTL

La administración eficiente de los datos es fundamental para obtener un rendimiento óptimo, un control de costes y la integridad de los datos. Utilice el Tiempo de vida de retención de conjuntos de datos de evento de experiencia (TTL) para aplicar una caducidad de nivel de fila, lo que elimina automáticamente los registros obsoletos de los conjuntos de datos en el lago de datos y garantiza una eficiencia y una relevancia de datos óptimas.

Esta guía explica cómo evaluar, establecer y administrar TTL mediante la API del servicio de catálogo. Aprenderá cuándo y por qué aplicar TTL, cómo configurar y actualizar valores TTL mediante llamadas a la API y prácticas recomendadas para garantizar una implementación eficaz.

>[!IMPORTANT]
>
> TTL está diseñado para optimizar la administración del ciclo de vida de los datos y la eficiencia del almacenamiento. No es una herramienta de cumplimiento y no se debe confiar en ella para los requisitos regulatorios. El cumplimiento suele requerir estrategias de gobernanza de datos más amplias.

## Razones para utilizar TTL para la administración de datos de nivel de fila

A medida que los conjuntos de datos aumentan, la administración eficiente de los datos cobra cada vez más importancia para preservar el rendimiento, controlar los costes y mantener la relevancia de los datos. La caducidad de datos a nivel de fila basada en TTL automatiza la limpieza de datos al eliminar registros obsoletos sin intervención manual para ayudar a optimizar el almacenamiento y mejorar la eficiencia del sistema.

TTL es útil cuando se administran datos con distinción de tiempo que pierden relevancia con el tiempo. Considere implementar TTL si necesita:

- Reduzca los costes de almacenamiento eliminando automáticamente los registros obsoletos.
- Mejore el rendimiento de las consultas minimizando los datos irrelevantes.
- Mantenga la higiene de los datos conservando solo la información relevante.
- Optimizar la retención de datos para lograr los objetivos empresariales.

### Ejemplo del sector {#industry-example}

Por ejemplo, considere un servicio de streaming de vídeo que rastree las interacciones del usuario, como vistas de vídeo, búsquedas y recomendaciones. Aunque los datos de participación recientes son cruciales para la personalización, los registros de actividad más antiguos (por ejemplo, las interacciones de hace más de un año) pierden relevancia. Al utilizar la caducidad a nivel de fila, Platform elimina automáticamente los registros obsoletos, lo que garantiza que solo se utilicen datos actuales y significativos para los análisis y las recomendaciones.

## Evaluar la idoneidad de TTL

Antes de aplicar una directiva de retención, compruebe si el conjunto de datos es un buen candidato para la caducidad del nivel de fila. Tenga en cuenta lo siguiente:

- Relevancia de los datos con el tiempo: ¿Los datos más antiguos proporcionan valor o se vuelven obsoletos?
- Impacto en los procesos descendentes: ¿La eliminación de datos afectará a la creación de informes, los análisis o las integraciones?
- Coste del almacenamiento frente al valor de retención: ¿el valor de los datos más antiguos justifica el coste de almacenarlos?

Si los registros históricos son esenciales para el análisis a largo plazo o las operaciones comerciales, es posible que el TTL no sea el enfoque correcto. La revisión de estos factores garantiza que el TTL se ajuste a sus necesidades de retención de datos sin afectar negativamente a la disponibilidad de los datos.

## Planifique sus consultas

Antes de aplicar TTL, utilice consultas para analizar el tamaño y la relevancia del conjunto de datos. La ejecución de consultas de destino ayuda a determinar la cantidad de datos que se retendrán o eliminarán en diferentes configuraciones de TTL.

Por ejemplo, la siguiente consulta SQL cuenta el número de registros creados en los últimos 30 días:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

La ejecución de consultas similares para diferentes intervalos de tiempo ayuda a validar la configuración de TTL y a garantizar que equilibran la eficacia del almacenamiento y la accesibilidad de los datos.

## Introducción a la administración de TTL

Antes de poder evaluar, establecer y administrar la retención de conjuntos de datos de eventos de experiencia mediante la API del servicio de catálogo, debe saber cómo dar formato a las solicitudes correctamente. Esto incluye conocer las rutas de API, proporcionar los encabezados necesarios y dar formato a las cargas útiles de solicitud. Consulte la [Guía de introducción a la API del servicio de catálogo](../api/getting-started.md) para obtener esta información esencial.

>[!NOTE]
>
>Este documento cubre la caducidad del nivel de fila, que elimina filas caducadas individuales dentro de un conjunto de datos mientras el propio conjunto de datos se mantiene intacto. No se aplica a la caducidad del conjunto de datos, que elimina conjuntos de datos completos y se administra mediante una función independiente. Para la caducidad a nivel de conjunto de datos, consulte la [documentación de API de caducidad del conjunto de datos](../../hygiene/api/dataset-expiration.md).

### Cómo comprobar la configuración del TTL actual

Para comenzar la administración de TTL, compruebe primero la configuración actual de TTL. Realice una petición GET al extremo `/ttl/{datasetId}` para recuperar la configuración TTL predeterminada, máxima y mínima de un conjunto de datos. Este paso es necesario porque las reglas TTL pueden variar en función del tipo de conjunto de datos.

>[!TIP]
>
>La dirección URL de puerta de enlace de plataforma y la ruta de acceso base para la API del servicio de catálogo son: `https://platform.adobe.io/data/foundation/catalog`.

**Formato de API**

```http
GET /ttl/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | Cadena generada por el sistema que identifica de forma exclusiva un conjunto de datos. Para encontrar un ID de conjunto de datos, utilice el extremo `/datasets`. Consulte la [guía de API de objetos de catálogo](../api/list-objects.md) para obtener instrucciones sobre el filtrado de respuestas para conjuntos de datos relevantes. |

**Solicitud**

La siguiente solicitud recupera la configuración de TTL de su organización para un conjunto de datos concreto.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Respuesta**

Una respuesta correcta devuelve la configuración TTL para el conjunto de datos, incluidos los valores TTL predeterminados, máximos y mínimos para el almacenamiento de `adobe_lakeHouse` y `adobe_unifiedProfile`.

+++Seleccione para ver la respuesta

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propiedad | Descripción |
|--------------|-------------|
| `defaultValue` | Período TTL predeterminado aplicado si no se establece ningún TTL personalizado. |
| `maxValue` | El TTL más largo permitido para el conjunto de datos. Si es nulo, no hay límite máximo. |
| `minValue` | El TTL más corto permitido para garantizar el cumplimiento de las políticas del sistema. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Cómo establecer el TTL para un conjunto de datos {#set-ttl}

>[!IMPORTANT]
>
>La caducidad de la fila solo se puede aplicar a conjuntos de datos de evento que utilicen un esquema de serie temporal. Antes de establecer el TTL, compruebe que el esquema del conjunto de datos amplía `https://ns.adobe.com/xdm/data/time-series` para garantizar que la solicitud de API se realice correctamente. Utilice la API de Registro de esquemas para recuperar los detalles del esquema y comprobar la propiedad `meta:extends`. Consulte la [Documentación del extremo del esquema](../../xdm/api/schemas.md#lookup) para obtener instrucciones sobre cómo hacerlo.

Para configurar la retención del conjunto de datos de Experience Event para su conjunto de datos, establezca un nuevo valor TTL realizando una petición PATCH al extremo `/v2/datasets/{ID}`.

**Formato de API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos para el que desea actualizar el valor TTL. |

**Solicitud**

En la solicitud de ejemplo siguiente, `ttlValue` está establecido en `P3M`. Esto garantiza que los registros de más de tres meses se eliminen automáticamente. Puede ajustar el período de retención para adaptarlo a las necesidades de su empresa mediante valores como `P6M` durante seis meses o `P12M` durante un año.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

**Respuesta**

Una respuesta correcta muestra la configuración TTL para el conjunto de datos. Incluye detalles sobre la configuración de caducidad en el nivel de fila para el almacenamiento `adobe_lakeHouse` y `adobe_unifiedProfile`.

+++Seleccione para ver la respuesta

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propiedad | Descripción |
|----------------------------------|-------------|
| `extensions` | Un contenedor de metadatos adicionales relacionados con el conjunto de datos. |
| `extensions.adobe_lakeHouse` | Especifica la configuración relacionada con la arquitectura de almacenamiento, incluidas las configuraciones de caducidad de nivel de fila |
| `rowExpiration` | El objeto contiene la configuración de TTL que define el período de retención del conjunto de datos. |
| `rowExpiration.ttlValue` | Define la duración antes de que los registros del conjunto de datos se quiten automáticamente. Utiliza el formato de período ISO-8601 (por ejemplo, `P3M` durante 3 meses o `P7D` durante una semana). |
| `rowExpiration.valueStatus` | La cadena indica si la configuración TTL es un valor predeterminado del sistema o un valor personalizado establecido por un usuario. Valores posibles: `default`, `custom`. |
| `rowExpiration.setBy` | Especifica quién modificó por última vez la configuración de TTL. Los valores posibles incluyen: `user` (configurado manualmente) o `service` (asignado automáticamente). |
| `rowExpiration.updated` | La marca de tiempo de la última actualización TTL. Este valor indica cuándo se modificó por última vez la configuración de TTL. |

### Cómo actualizar el TTL {#update-ttl}

Amplíe o acorte el período de retención para adaptarlo a sus necesidades comerciales ajustando el TTL. Por ejemplo, cuando se considera la plataforma de streaming de vídeo mencionada anteriormente, la plataforma puede establecer inicialmente el TTL en tres meses para garantizar nuevos datos de participación para la personalización. Sin embargo, si su análisis muestra que los patrones de interacción de más de tres meses de antigüedad siguen proporcionando perspectivas valiosas, pueden extender el período TTL a seis meses para mantener registros más antiguos y así obtener mejores modelos de recomendación.

Para modificar un valor TTL existente, utilice el método `PATCH` en el extremo `/v2/datasets/{DATASET_ID}`.

#### Formato de API

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Solicitud**

En la siguiente solicitud, el TTL se actualiza a seis meses (`P6M`) ampliando el período de retención de registros antes de la eliminación automática.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Respuesta**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Prácticas recomendadas para establecer TTL {#best-practices}

Elegir el valor TTL correcto es crucial para garantizar que la política de retención de conjuntos de datos de eventos de experiencia equilibra la retención de datos, la eficiencia del almacenamiento y las necesidades analíticas. Un TTL demasiado corto puede causar pérdida de datos, mientras que uno demasiado largo puede aumentar los costos de almacenamiento y la acumulación de datos innecesaria. Asegúrese de que el TTL se ajuste al propósito de su conjunto de datos teniendo en cuenta la frecuencia con la que se accede a los datos y cuánto tiempo permanece relevante.

La siguiente tabla proporciona recomendaciones TTL comunes basadas en el tipo de conjunto de datos y patrones de uso:

| Tipo de conjunto de datos | TTL recomendado | Casos de uso habituales |
|-----------------------------|------------------------|-------------------|
| Conjuntos de datos a los que se accede frecuentemente | 30 a 90 días | Registros de participación de usuarios, datos del flujo de navegación del sitio web y datos de rendimiento de campañas a corto plazo. |
| Conjuntos de datos archivados | 1 año o más | Registros de transacciones financieras, datos de cumplimiento, análisis de tendencias a largo plazo, conjuntos de datos de aprendizaje automático. |
| Conjuntos de datos administrados por aplicaciones | Hasta 13 meses | Los conjuntos de datos administrados por el sistema tienen restricciones TTL predefinidas, que se aplican automáticamente para cumplir con los límites impuestos por el sistema. |
| Conjuntos de datos administrados por el cliente | 30 días (TTL máximo) | Conjuntos de datos creados mediante la IU, las API o Data Distiller. El TTL debe ser de al menos 30 días y estar dentro del TTL máximo definido. |

Revise la configuración de TTL periódicamente para asegurarse de que sigue ajustándose a las políticas de almacenamiento, las necesidades analíticas y los requisitos empresariales.

### Consideraciones clave al establecer TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Siga estas prácticas recomendadas para asegurarse de que la configuración de TTL se ajusta a su estrategia de retención de datos:

- Audite los cambios de TTL regularmente. Cada actualización TTL déclencheur un evento de auditoría. Utilice registros de auditoría para rastrear las modificaciones TTL con fines de cumplimiento, gobernanza de datos y resolución de problemas.
- Eliminar TTL si los datos deben conservarse indefinidamente. Para deshabilitar TTL, establezca `ttlValue` en `null`. Esto evita la caducidad automática y conserva todos los registros de forma permanente. Tenga en cuenta las implicaciones de almacenamiento antes de realizar este cambio.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Limitaciones de TTL {#limitations}

Tenga en cuenta las siguientes limitaciones al utilizar TTL:

- **La retención de conjuntos de datos de evento de experiencia mediante TTL se aplica a la caducidad de nivel de fila**, no a la eliminación de conjuntos de datos. TTL elimina registros en función de un período de retención definido, pero no elimina conjuntos de datos completos. Para quitar un conjunto de datos, use el [extremo de caducidad del conjunto de datos](../../hygiene/api/dataset-expiration.md) o la eliminación manual.
- **TTL no se puede eliminar**, solo se ha actualizado. Una vez aplicado, el TTL no se puede eliminar, pero puede [modificar el período de retención](#update-ttl) para extenderlo o acortarlo. Para conservar los datos indefinidamente, establezca un TTL lo suficientemente largo en lugar de intentar eliminarlos.
- **TTL no es una herramienta de cumplimiento**. TTL optimiza la administración del almacenamiento y el ciclo de vida de los datos, pero no cumple con los requisitos regulatorios de retención de datos. Para el cumplimiento, implemente estrategias de gobernanza de datos más amplias.

## Preguntas frecuentes sobre política de retención de conjuntos de datos {#faqs}

Esta sección proporciona respuestas a las preguntas más frecuentes sobre las políticas de retención de conjuntos de datos en Adobe Experience Platform.

### ¿A qué tipos de conjuntos de datos puedo aplicar reglas de política de retención?

+++Respuesta
Puede aplicar políticas de retención a conjuntos de datos creados con la clase XDM ExperienceEvent. Para los servicios de perfil, las políticas de retención solo se aplican a los conjuntos de datos de evento de experiencia que se han habilitado para perfiles.
+++

### ¿Cuándo eliminará el trabajo de retención de conjuntos de datos los datos de los servicios de lago de datos?

+++Respuesta
Los TTL de conjuntos de datos se evalúan y procesan semanalmente, eliminando todos los registros caducados. Un evento se considera caducado si se ingirió en Platform hace más de 30 días (fecha de ingesta > 30 días) y su fecha de evento supera el período de retención definido (TTL).
+++

### ¿Cuándo eliminará el trabajo de retención de conjuntos de datos los datos de los servicios de perfil?

+++Respuesta
Una vez establecida una política de retención, los eventos existentes en Platform se eliminan inmediatamente si su marca de tiempo de evento supera el período de retención (TTL). Los nuevos eventos se eliminan una vez que su marca de tiempo supera el período de retención.

Por ejemplo, si aplica una directiva de caducidad de 30 días el 15 de mayo, ocurre lo siguiente:

- Los nuevos eventos reciben una caducidad de 30 días a medida que se incorporan.
- Los eventos existentes con una marca de tiempo anterior al 15 de abril se eliminan inmediatamente.
- Los eventos existentes con una marca de tiempo después del 15 de abril caducarán 30 días después de su marca de tiempo (por ejemplo, un evento del 18 de abril se eliminaría el 18 de mayo).
+++

### ¿Puedo establecer diferentes políticas de retención para el lago de datos y los servicios de perfil?

+++Respuesta
Sí, puede establecer diferentes políticas de retención para el lago de datos y los servicios de perfil. Sin embargo, el período de retención del perfil no debe ser inferior al establecido para el lago de datos.
+++

### ¿Cómo puedo comprobar el uso actual de mi conjunto de datos?

+++Respuesta
Puede comprobar el tamaño de almacenamiento del conjunto de datos más reciente para el lago de datos y los almacenes de perfiles como métricas independientes en el área de trabajo de inventario [!UICONTROL Conjunto de datos]. Ordene las columnas para identificar los conjuntos de datos más grandes y comprobar que se aplican las políticas de retención.

Para el uso a nivel de zona protegida, consulte el Panel de uso de licencias. Consulte la [documentación de uso de licencias](../../dashboards/guides/license-usage.md) para obtener más detalles.
+++

### ¿Cómo puedo verificar si el trabajo de retención de datos se realizó correctamente?

+++Respuesta
Puede comprobar el último trabajo de retención de datos comprobando su marca de tiempo en la [interfaz de usuario de configuración de retención de conjuntos de datos](./user-guide.md#data-retention-policy) o en la página Inventario de datos.

Los informes de uso del conjunto de datos histórico no están disponibles actualmente.
+++

### ¿Puedo recuperar los datos eliminados?

+++Respuesta
No, una vez aplicada una política de retención, los datos anteriores al período de retención se eliminan de forma permanente y no se pueden recuperar.
+++

## Pasos siguientes {#next-steps}

Ahora que ha aprendido a administrar la configuración de TTL para la caducidad de nivel de fila, revise la siguiente documentación para comprender mejor la administración de TTL:

- Trabajos de retención: aprenda a programar y automatizar las caducidades de los conjuntos de datos en la IU de Platform con la [guía de la IU del ciclo vital de datos](../../hygiene/ui/dataset-expiration.md), o compruebe las configuraciones de retención de conjuntos de datos y compruebe que se eliminan los registros caducados.
- [Guía de extremo de API de caducidad de conjuntos de datos](../../hygiene/api/dataset-expiration.md): Descubra cómo eliminar conjuntos de datos completos en lugar de solo filas. Aprenda a programar, administrar y automatizar la caducidad de los conjuntos de datos mediante la API para garantizar una retención de datos eficiente.
- [Información general sobre políticas de uso de datos](../../data-governance/policies/overview.md): Aprenda a alinear su estrategia de retención de datos con requisitos de cumplimiento más amplios y restricciones de uso de marketing.

