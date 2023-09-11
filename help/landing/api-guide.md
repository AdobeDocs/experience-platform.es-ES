---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía de api;guía de api de platform;introducción a platform;guía para desarrolladores
solution: Experience Platform
title: Introducción a las API de Adobe Experience Platform
description: Adobe Experience Platform proporciona servicios de API estrechamente vinculados entre sí. Esta guía contiene información sobre los servicios disponibles, los encabezados necesarios para las operaciones de CRUD, los mensajes de error, las colecciones de Postman y las llamadas de API de ejemplo.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: c728d63c22593ca56999dd0bb6679dea7de0e00a
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 2%

---

# Introducción a las API de Adobe Experience Platform

Adobe Experience Platform se desarrolla bajo la filosofía &quot;API First&quot;. Con las API de Platform, puede realizar mediante programación operaciones básicas de CRUD (crear, leer, actualizar, eliminar) con datos, como configurar atributos calculados, acceder a datos o entidades, exportar datos, eliminar datos o lotes innecesarios, etc.

Todas las API de cada servicio de Experience Platform comparten el mismo conjunto de encabezados de autenticación y utilizan sintaxis similares para sus operaciones de CRUD. La siguiente guía describe los pasos necesarios para empezar a utilizar las API de Platform.

## Autenticación y encabezados

Para realizar llamadas correctamente a los extremos de Platform, debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas de API de Experience Platform, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Encabezado de zona protegida

Todos los recursos de Experience Platform están aislados para zonas protegidas virtuales específicas. Las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados de Platform, consulte la [documentación general de zona protegida](../sandboxes/home.md).

### Encabezado de tipo de contenido

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas de POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados son específicos de cada extremo de API. Si una `Content-Type` es necesario para un extremo, su valor se mostrará en el ejemplo de solicitudes de API proporcionadas por [Guías de API para servicios de Platform individuales](#api-guides).

## Fundamentos de API de Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías y sintaxis subyacentes que son importantes de comprender para administrar de forma eficaz los recursos de Platform.

Para obtener más información acerca de las tecnologías de API subyacentes que utiliza Platform, incluidos los objetos de esquema JSON de ejemplo, visite la [Fundamentos de API de Experience Platform](api-fundamentals.md) guía.

## Colecciones de Postman para API de Experience Platform

Postman es una plataforma de colaboración para el desarrollo de API que le permite configurar entornos con variables preestablecidas, compartir colecciones de API, optimizar solicitudes de CRUD y mucho más. La mayoría de los servicios de API de Platform tienen colecciones de Postman que se pueden utilizar para ayudar a realizar llamadas de API.

Para obtener más información sobre Postman, incluido cómo configurar un entorno, una lista de colecciones disponibles y cómo importar colecciones, visite la [Documentación de Platform Postman](postman.md).

## Leer llamadas de API de muestra {#sample-api}

Los formatos de solicitud varían según la API de plataforma que se utilice. La mejor manera de aprender a estructurar las llamadas de API es siguiendo los ejemplos proporcionados en la documentación del servicio de Platform concreto que está utilizando.

La documentación de [!DNL Experience Platform] muestra las llamadas de API de ejemplo de dos formas diferentes. En primer lugar, la llamada de se presenta en su **Formato de API**, una representación de plantilla que muestra solo la operación (GET, POST, PUT, PATCH, DELETE) y el punto final que se está utilizando (por ejemplo, `/global/classes`). Algunas plantillas también muestran la ubicación de las variables para ayudar a ilustrar cómo se debe formular una llamada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Las llamadas se muestran como comandos cURL en una **Solicitud**, que incluye los encabezados necesarios y la &quot;ruta base&quot; completa necesaria para interactuar correctamente con la API. La ruta base debe prefijarse a todos los extremos. Por ejemplo, los mencionados `/global/classes` el punto final se convierte en `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Verá el formato de la API/patrón de solicitud en toda la documentación y se espera que utilice la ruta completa que se muestra en la solicitud de ejemplo al realizar sus propias llamadas a las API de Platform.

### Ejemplo de solicitud de API

A continuación se muestra un ejemplo de solicitud de API que muestra el formato que encontrará en la documentación.

**Formato de API**

El formato de la API muestra la operación (GET) y el punto final que se está utilizando. Las variables se indican mediante llaves (en este caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Solicitud**

En esta solicitud de ejemplo, las variables del formato API reciben valores reales en la ruta de solicitud. Además, todos los encabezados requeridos se muestran como valores de encabezado de muestra o como variables donde se debe incluir información confidencial (como tokens de seguridad e ID de acceso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta ilustra lo que esperaría recibir después de una llamada correcta a la API, según la solicitud enviada. En ocasiones, la respuesta se trunca en cuanto al espacio, lo que significa que puede ver más información o información adicional que la mostrada en el ejemplo.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Mensajes de error

El [Guía de solución de problemas de Platform](troubleshooting.md#errors-and-troubleshooting) proporciona una lista de errores que pueden producirse al utilizar cualquier servicio de Experience Platform.

Para obtener guías de solución de problemas sobre servicios de Platform individuales, consulte la [directorio de solución de problemas de servicios](troubleshooting.md#service-troubleshooting-directory).

Para obtener más información sobre extremos específicos en las API de Platform, incluidos los encabezados y cuerpos de solicitud necesarios, consulte la [Guías de API de Platform](#api-guides).

## Guías de API de Platform {#api-guides}

| Guía de la API de  | Descripción |
| --- | --- |
| Guía de la API de [[!DNL Access Control] ](.././access-control/api/getting-started.md) | El [!DNL Access Control] El extremo de API puede recuperar las políticas actuales en vigor para un usuario en recursos determinados dentro de una zona protegida especificada. Todas las demás capacidades de control de acceso se proporcionan a través de la [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guía de API de ingesta por lotes](.././ingestion/batch-ingestion/api-overview.md) | El Adobe Experience Platform [!DNL Data Ingestion] La API de le permite introducir datos en Platform como archivos por lotes. Los datos que se están ingiriendo pueden ser los datos de perfil de un archivo plano de un sistema CRM (como un archivo de Parquet) o los datos que se ajustan a un esquema conocido en el Registro de esquemas (XDM). |
| Guía de la API de [[!DNL Catalog Service] ](.././catalog/api/getting-started.md) | El [!DNL Catalog Service] La API permite a los desarrolladores administrar metadatos de conjuntos de datos en Adobe Experience Platform. Esto incluye ubicaciones de datos, etapas de procesamiento, errores que se produjeron durante el procesamiento e informes de datos. |
| Guía de la API de [[!DNL Data Access] ](.././data-access/api.md) | El [!DNL Data Access] La API permite a los desarrolladores recuperar información sobre conjuntos de datos ingeridos dentro de Experience Platform. Esto incluye el acceso y la descarga de archivos de conjuntos de datos, la recuperación de información de encabezado, la lista de lotes fallidos y exitosos y la descarga de archivos de previsualización CSV / Parquet. |
| Guía de la API de [[!DNL Dataset Service] ](.././data-governance/labels/dataset-api.md) | La API del servicio de conjuntos de datos permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API del servicio de catálogo que administra los metadatos del conjunto de datos. |
| Guía de la API de [[!DNL Edge Network Server] ](../server-api/overview.md) | El [!DNL Edge Network Server API] se puede utilizar para una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing. El [!DNL Server API] se puede utilizar en servidores de, [!DNL IoT] dispositivos, decodificadores y una variedad de otros dispositivos. |
| Guía de la API de [[!DNL Identity Service] ](.././identity-service/api/getting-started.md) | El [!DNL Identity Service] La API permite a los desarrolladores administrar la identificación de sus clientes en varios dispositivos, canales cruzados y casi en tiempo real mediante gráficos de identidad en Adobe Experience Platform. |
| Guía de la API de [[!DNL Observability Insights] ](.././observability/api/overview.md) | [!DNL Observability Insights] es una API de RESTful que permite a los desarrolladores exponer métricas clave de observabilidad en Adobe Experience Platform. Estas métricas proporcionan perspectivas sobre las estadísticas de uso de Platform, las comprobaciones de estado de los servicios de Platform, las tendencias históricas y los indicadores de rendimiento de varias funcionalidades de Platform. |
| [[!DNL Policy Service] Guía de API](.././data-governance/api/overview.md) <br> (Gobernanza de datos) | El [!DNL Policy Service] La API permite crear y administrar etiquetas y políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contengan determinadas etiquetas de uso de datos. Para aplicar etiquetas a conjuntos de datos y campos, consulte la [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) guía |
| Guía de la API de [[!DNL Privacy Service] ](.././privacy-service/api/getting-started.md) | El [!DNL Privacy Service] La API permite a los desarrolladores crear y administrar solicitudes de clientes para acceder a sus datos personales o eliminarlos en aplicaciones de Experience Cloud, de acuerdo con las regulaciones legales de privacidad. |
| Guía de la API de [[!DNL Query Service] ](.././query-service/api/getting-started.md) | El [!DNL Query Service] La API permite a los desarrolladores consultar sus datos de Adobe Experience Platform utilizando SQL estándar. |
| Guía de la API de [[!DNL Real-Time Customer Profile] ](.././profile/api/overview.md) | La API de Perfil del cliente en tiempo real permite a los desarrolladores explorar y trabajar con datos de perfil, incluida la visualización de perfiles, la creación y actualización de políticas de combinación, la exportación o el muestreo de datos de perfil y la eliminación de datos de perfil que ya no son necesarios o que se añadieron por error. |
| [Guía de API de zona protegida](.././sandboxes/api/getting-started.md) | La API de espacio aislado permite a los desarrolladores administrar mediante programación entornos de espacio aislado virtuales en Adobe Experience Platform. |
| [[!DNL Schema Registry] Guía de API](.././xdm/api/overview.md) <br> (XDM) | El [!DNL Schema Registry] La API permite a los desarrolladores administrar mediante programación todos los esquemas y los recursos del Modelo de datos de experiencia (XDM) relacionados dentro de Adobe Experience Platform. |
| Guía de la API de [[!DNL Segmentation Service] ](.././segmentation/api/overview.md) | El [!DNL Segmentation Service] La API permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Esto incluye la generación de segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real. |
| [[!DNL Sensei Machine Learning] Guía de API](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | El [!DNL Sensei Machine Learning] La API proporciona un mecanismo para que los científicos de datos organicen y administren los servicios de aprendizaje automático (ML) desde la incorporación del algoritmo, la experimentación y la implementación de servicios. |

Para obtener más información sobre los extremos específicos y las operaciones disponibles para cada servicio, consulte la [Documentación de referencia del API](https://www.adobe.com/go/platform-api-reference-en) en el Adobe I/O.

## Pasos siguientes

Este documento introdujo los encabezados necesarios, las guías disponibles y proporcionó un ejemplo de llamada de API. Ahora que tiene los valores de encabezado necesarios para realizar llamadas de API en Adobe Experience Platform, seleccione un punto final de API que desee explorar en [Tabla de guías de API de Platform](#api-guides).

Para obtener respuestas a las preguntas más frecuentes, consulte la [Guía de solución de problemas de Platform](troubleshooting.md).

Para configurar un entorno de Postman y explorar las colecciones de Postman disponibles, consulte la [Guía de Platform Postman](postman.md).
