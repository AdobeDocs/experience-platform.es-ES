---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía de la api;guía de la api de platform;introducción a platform;guía para desarrolladores
solution: Experience Platform
title: Introducción a las API de Adobe Experience Platform
topic-legacy: api guide
description: Adobe Experience Platform proporciona servicios de API estrechamente vinculados entre sí. Esta guía contiene información sobre los servicios disponibles, los encabezados necesarios para las operaciones de CRUD, los mensajes de error, las colecciones Postman y las llamadas de API de ejemplo.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Introducción a las API de Adobe Experience Platform

Adobe Experience Platform se desarrolla con una filosofía de &quot;API primero&quot;. Mediante las API de plataforma, puede realizar mediante programación operaciones CRUD básicas (Crear, Leer, Actualizar, Eliminar) con datos, como configurar atributos calculados, acceder a datos o entidades, exportar datos, eliminar datos o lotes innecesarios, etc.

Las API de cada servicio de Experience Platform comparten el mismo conjunto de encabezados de autenticación y utilizan sintaxis similares para sus operaciones de CRUD. La siguiente guía describe los pasos necesarios para comenzar con las API de Platform.

## Autenticación y encabezados

Para realizar correctamente llamadas a extremos de Platform, debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Experience Platform, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Encabezado de espacio aislado

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en Platform, consulte la [documentación general del entorno limitado](../sandboxes/home.md).

### Encabezado de tipo contenido

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas de POST, PUT y PATCH) deben incluir un encabezado `Content-Type`. Los valores aceptados son específicos de cada extremo de API. Si se necesita un valor `Content-Type` específico para un extremo, su valor se mostrará en las solicitudes de API de ejemplo proporcionadas por las [guías de API para servicios de Platform individuales](#api-guides).

## Aspectos básicos de la API del Experience Platform

Las API de Adobe Experience Platform emplean varias tecnologías subyacentes y sintaxis que son importantes de comprender para administrar eficazmente los recursos de Platform.

Para obtener más información sobre las tecnologías de API subyacentes que utiliza Platform, incluidos ejemplos de objetos de esquema JSON, visite la guía [Fundamentos de la API del Experience Platform](api-fundamentals.md).

## Colecciones Postman para API de Experience Platform

Postman es una plataforma de colaboración para el desarrollo de API que le permite configurar entornos con variables preestablecidas, compartir colecciones de API, optimizar solicitudes CRUD y mucho más. La mayoría de los servicios de API de plataforma tienen colecciones Postman que se pueden utilizar para ayudar a realizar llamadas de API.

Para obtener más información sobre Postman, incluido cómo configurar un entorno, una lista de colecciones disponibles y cómo importar colecciones, visite la [documentación de Platform Postman](postman.md).

## Leyendo llamadas de API de ejemplo {#sample-api}

Los formatos de solicitud varían según la API de plataforma que se utilice. La mejor manera de estructurar las llamadas de API es seguir los ejemplos proporcionados en la documentación del servicio de Platform en particular que está utilizando.

La documentación de [!DNL Experience Platform] muestra las llamadas de API de ejemplo de dos maneras diferentes. En primer lugar, la llamada se presenta en su **formato API**, una representación de plantilla que muestra únicamente la operación (GET, POST, PUT, PATCH, DELETE) y el punto final que se está utilizando (por ejemplo, `/global/classes`). Algunas plantillas también muestran la ubicación de las variables para ayudar a ilustrar cómo se debe formular una llamada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

A continuación, las llamadas se muestran como comandos cURL en una **Solicitud**, que incluye los encabezados necesarios y la &quot;ruta base&quot; completa necesaria para interactuar correctamente con la API. La ruta base debe añadirse previamente a todos los extremos. Por ejemplo, el punto final `/global/classes` antes mencionado se convierte en `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Verá el formato de API / patrón de solicitud en toda la documentación y se espera que utilice la ruta completa que se muestra en la solicitud de ejemplo al realizar sus propias llamadas a las API de Platform.

### Ejemplo de solicitud de API

A continuación se muestra un ejemplo de solicitud de API que muestra el formato que encontrará en la documentación.

**Formato de API**

El formato de la API muestra la operación (GET) y el punto final que se está utilizando. Las variables se indican entre llaves (en este caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Solicitud**

En esta solicitud de ejemplo, las variables del formato de API reciben valores reales en la ruta de solicitud. Además, todos los encabezados requeridos se muestran como valores de encabezado de ejemplo o variables en las que se debe incluir información confidencial (como tokens de seguridad e ID de acceso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta ilustra lo que esperaría recibir tras una llamada correcta a la API, según la solicitud que se haya enviado. Ocasionalmente, la respuesta se trunca en el espacio, lo que significa que puede ver más información o información adicional a la que se muestra en la muestra.

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

La [Guía de solución de problemas de Platform](troubleshooting.md#errors-and-troubleshooting) proporciona una lista de errores que puede encontrar al utilizar cualquier servicio de Experience Platform.

Para obtener guías de solución de problemas sobre los servicios de Platform individuales, consulte el [directorio de solución de problemas del servicio](troubleshooting.md#service-troubleshooting-directory).

Para obtener más información sobre extremos específicos en las API de plataforma, incluidos los encabezados y los cuerpos de solicitud necesarios, consulte las [guías de API de plataforma](#api-guides).

## Guías de API de plataforma {#api-guides}

| Guía de API | Descripción |
| --- | --- |
| [[!DNL Access Control] Guía de API](.././access-control/api/getting-started.md) | El extremo de la API [!DNL Access Control] puede recuperar las políticas actuales en vigor para un usuario en recursos determinados dentro de un entorno limitado especificado. Todas las demás funcionalidades de control de acceso se proporcionan a través de [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guía de API de ingesta por lotes](.././ingestion/batch-ingestion/api-overview.md) | La API [!DNL Data Ingestion] de Adobe Experience Platform le permite introducir datos en Platform como archivos por lotes. Los datos introducidos pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido en el Registro de esquemas (XDM). |
| [[!DNL Catalog Service] Guía de API](.././catalog/api/getting-started.md) | La API [!DNL Catalog Service] permite a los desarrolladores administrar metadatos de conjuntos de datos en Adobe Experience Platform. Esto incluye ubicaciones de datos, etapas de procesamiento, errores que se produjeron durante el procesamiento e informes de datos. |
| [[!DNL Data Access] Guía de API](.././data-access/api.md) | La API [!DNL Data Access] permite a los desarrolladores recuperar información sobre conjuntos de datos ingestados dentro de Experience Platform. Esto incluye el acceso y la descarga de archivos de conjuntos de datos, la recuperación de información del encabezado, la lista de lotes con errores y sin éxito, y la descarga de archivos CSV/Parquet de vista previa. |
| [[!DNL Dataset Service] Guía de API](.././data-governance/labels/dataset-api.md) | La API del servicio de conjunto de datos le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funcionalidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogo que administra los metadatos del conjunto de datos. |
| [[!DNL Flow Service] Guía de API](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  (Fuentes y destinos) | La API [!DNL Flow Service] se utiliza para recopilar y centralizar los datos de diversas fuentes y se utiliza para crear y activar datos en distintos destinos dentro de Adobe Experience Platform. El servicio proporciona una API RESTful desde la que se pueden conectar todas las fuentes admitidas. |
| [[!DNL Identity Service] Guía de API](.././identity-service/api/getting-started.md) | La API [!DNL Identity Service] permite a los desarrolladores administrar la identificación entre dispositivos, canales cruzados y casi en tiempo real de sus clientes mediante gráficos de identidad en Adobe Experience Platform. |
| [[!DNL Observability Insights] Guía de API](.././observability/api/overview.md) | [!DNL Observability Insights] es una API de RESTful que permite a los desarrolladores exponer métricas clave de observación en Adobe Experience Platform. Estas métricas proporcionan información sobre las estadísticas de uso de Platform, las comprobaciones de estado de los servicios de Platform, las tendencias históricas y los indicadores de rendimiento de varias funcionalidades de Platform. |
| [[!DNL Policy Service] Guía de API](.././data-governance/api/overview.md) <br>  (control de datos) | La API [!DNL Policy Service] le permite crear y administrar etiquetas y políticas de uso de datos para determinar qué acciones de marketing se pueden realizar con datos que contienen ciertas etiquetas de uso de datos. Para aplicar etiquetas a conjuntos de datos y campos, consulte la guía [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guía de API](.././privacy-service/api/getting-started.md) | La API [!DNL Privacy Service] permite a los desarrolladores crear y administrar solicitudes de clientes para acceder a sus datos personales o eliminarlos entre aplicaciones de Experience Cloud, de conformidad con las normas legales de privacidad. |
| [[!DNL Query Service] Guía de API](.././query-service/api/getting-started.md) | La API [!DNL Query Service] permite a los desarrolladores consultar sus datos de Adobe Experience Platform mediante SQL estándar. |
| [[!DNL Real-time Customer Profile] Guía de API](.././profile/api/overview.md) | La API de perfil de cliente en tiempo real permite a los desarrolladores explorar y trabajar con datos de perfil, incluida la visualización de perfiles, la creación y actualización de políticas de combinación, la exportación o muestreo de datos de perfil y la eliminación de datos de perfil que ya no son necesarios o que se añadieron por error. |
| [Guía de la API de Sandbox](.././sandboxes/api/getting-started.md) | La API de Sandbox permite a los desarrolladores administrar mediante programación entornos aislados de entornos limitados virtuales en Adobe Experience Platform. |
| [[!DNL Schema Registry] Guía de API](.././xdm/api/overview.md) <br>  (XDM) | La API [!DNL Schema Registry] permite a los desarrolladores administrar mediante programación todos los esquemas y recursos relacionados del Modelo de datos de experiencia (XDM) en Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guía de API](.././segmentation/api/overview.md) | La API [!DNL Segmentation Service] permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Esto incluye la generación de segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real. |
| [[!DNL Sensei Machine Learning] Guía de API](.././data-science-workspace/api/getting-started.md) <br>  (Data Science Workspace) | La API [!DNL Sensei Machine Learning] proporciona un mecanismo para que los científicos de datos organicen y administren los servicios de aprendizaje automático (ML) desde la incorporación de algoritmos, la experimentación y la implementación de servicios. |

Para obtener más información sobre los extremos específicos y las operaciones disponibles para cada servicio, consulte la [documentación de referencia de la API](http://www.adobe.com/go/platform-api-reference-en) en Adobe I/O.

## Pasos siguientes

Este documento introdujo los encabezados requeridos, las guías disponibles y proporcionó un ejemplo de llamada de API. Ahora que tiene los valores de encabezado necesarios para realizar llamadas de API en Adobe Experience Platform, seleccione un punto final de API que desee explorar en la [tabla de guías de API de plataforma](#api-guides).

Para obtener respuestas a las preguntas más frecuentes, consulte la [Guía de solución de problemas de Platform](troubleshooting.md).

Para configurar un entorno Postman y explorar las colecciones Postman disponibles, consulte la [Guía de Platform Postman](postman.md).
