---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Importación y uso de audiencias externas
description: Siga este tutorial para aprender a utilizar audiencias externas con Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Importación y uso de audiencias externas

Adobe Experience Platform admite la posibilidad de importar audiencias externas, que posteriormente pueden utilizarse como componentes para una nueva definición de segmento. Este documento proporciona un tutorial para configurar un Experience Platform para importar y utilizar audiencias externas.

## Primeros pasos

Este tutorial requiere una comprensión práctica de las distintas [!DNL Adobe Experience Platform] servicios relacionados con la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Servicio de segmentación](../home.md): Permite generar segmentos de audiencia a partir de datos del perfil del cliente en tiempo real.
- [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [Conjuntos de datos](../../catalog/datasets/overview.md): La construcción de almacenamiento y administración para la persistencia de datos en el Experience Platform.
- [ingesta por transmisión](../../ingestion/streaming-ingestion/overview.md): El modo en que el Experience Platform ingesta y almacena datos de dispositivos del lado del cliente y del servidor en tiempo real.

### Datos de segmentos frente a metadatos de segmentos

Antes de empezar a importar y usar audiencias externas, es importante comprender la diferencia entre los datos de segmentos y los metadatos de segmentos.

Los datos de segmentos hacen referencia a perfiles que cumplen los criterios de calificación de segmentos y, por lo tanto, forman parte de la audiencia.

Los metadatos del segmento son información sobre el propio segmento, que incluye el nombre, la descripción, la expresión (si corresponde), la fecha de creación, la última fecha de modificación y un ID. El ID vincula los metadatos del segmento con perfiles individuales que cumplen la calificación del segmento y forman parte de la audiencia resultante.

| Datos de segmentos | Metadatos del segmento |
| ------------ | ---------------- |
| Perfiles que cumplen la calificación de segmentos | Information about the segment itself |

## Create an identity namespace for the external audience

El primer paso para utilizar audiencias externas es crear un área de nombres de identidad. Identity namespaces allow Platform to associate where a segment originates from.

Para crear un área de nombres de identidad, siga las instrucciones de la sección [guía del área de nombres de identidad](../../identity-service/namespaces.md#manage-namespaces). When creating your identity namespace, add the source details to the identity namespace, and mark its [!UICONTROL Type] as a **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

>[!NOTE]
>
>Para empezar a utilizar espacios de nombres personalizados con audiencias externas, debe crear un ticket de asistencia. Please contact your Adobe representative for more details.

## Create a schema for the segment metadata

Después de crear un área de nombres de identidad, debe crear un nuevo esquema para el segmento que va a crear.

Para empezar a componer un esquema, seleccione primero **[!UICONTROL Esquemas]** en la barra de navegación izquierda, seguida de la **[!UICONTROL Crear esquema]** en la esquina superior derecha del espacio de trabajo Esquemas . Desde aquí, seleccione **[!UICONTROL Examinar]** para ver una selección completa de los tipos de esquema disponibles.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Since you are creating a segment definition, which is a pre-defined class, select **[!UICONTROL Use existing class]**. Ahora, seleccione la opción **[!UICONTROL Definición del segmento]** clase, seguido de **[!UICONTROL Asignar clase]**.

![](../images/tutorials/external-audiences/assign-class.png)

Ahora que se ha creado el esquema, debe especificar qué campo contendrá el ID de segmento. Este campo debe marcarse como identidad principal y asignarse a los espacios de nombres creados anteriormente.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Después de marcar la variable `_id` como identidad principal, seleccione el título del esquema seguido de la opción etiquetada **[!UICONTROL Perfil]**. Select **[!UICONTROL Habilitar]** para habilitar el esquema para [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Ahora, este esquema está habilitado para Perfil, con la identificación principal asignada al espacio de nombres de identidad no personal que ha creado. Como resultado, esto significa que los metadatos de segmento importados a Platform mediante este esquema se incorporarán en Perfil sin combinarse con otros datos de Perfil relacionados con las personas.

## Creación de un conjunto de datos para el esquema

Después de configurar el esquema, deberá crear un conjunto de datos para los metadatos del segmento.

Para crear un conjunto de datos, siga las instrucciones de la sección [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#create). Debe seguir el **[!UICONTROL Crear conjunto de datos a partir del esquema]** utilizando el esquema creado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Después de crear el conjunto de datos, siga las instrucciones de la sección [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#enable-profile) para habilitar este conjunto de datos para el perfil del cliente en tiempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configuración e importación de datos de audiencia

Con el conjunto de datos habilitado, ahora se pueden enviar datos a Platform a través de la interfaz de usuario o mediante las API de Experience Platform. Puede introducir estos datos mediante una conexión por lotes o de flujo continuo.

### Ingesta de datos mediante una conexión por lotes

Para crear una conexión por lotes, puede seguir las instrucciones del genérico [guía de la interfaz de usuario de carga de archivos locales](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Para obtener una lista completa de las fuentes disponibles con las que puede utilizar la ingesta de datos, lea la [información general sobre fuentes](../../sources/home.md).

### Ingesta de datos mediante una conexión de flujo continuo

Para crear una conexión de flujo continuo, puede seguir las instrucciones de la sección [Tutorial de API](../../sources/tutorials/api/create/streaming/http.md) o [Tutorial de la interfaz de usuario](../../sources/tutorials/ui/create/streaming/http.md).

Una vez que haya creado la conexión de flujo continuo, tendrá acceso a su punto final de flujo único al que podrá enviar los datos. Para obtener información sobre cómo enviar datos a estos extremos, lea la [tutorial sobre datos de registro de flujo continuo](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Estructura de metadatos de audiencia

Después de crear una conexión, ahora puede introducir los datos en Platform.

A continuación se puede ver una muestra de los metadatos de la carga útil de audiencia externa:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schemaRef` | El esquema **must** consulte el esquema creado anteriormente para los metadatos del segmento. |
| `datasetId` | El ID del conjunto de datos **must** consulte el conjunto de datos creado anteriormente para el esquema que acaba de crear. |
| `xdmEntity._id` | El ID **must** consulte el mismo ID de segmento que utiliza como audiencia externa. |
| `xdmEntity.identityMap` | Esta sección **must** contiene la etiqueta de identidad utilizada al crear el área de nombres creada anteriormente. |
| `{IDENTITY_NAMESPACE}` | Esta es la etiqueta del área de nombres de identidad creada anteriormente. Por lo tanto, si, por ejemplo, llamara a su área de nombres de identidad &quot;externalAudience&quot;, la utilizaría como clave de la matriz. |
| `segmentName` | Nombre del segmento por el que desea segmentar la audiencia externa. |

## Generación de segmentos con audiencias importadas

Una vez configuradas las audiencias importadas, se pueden utilizar como parte del proceso de segmentación. Para buscar audiencias externas, vaya al Generador de segmentos y seleccione **[!UICONTROL Audiencias]** en la ficha **[!UICONTROL Campos]** para obtener más información.

![](../images/tutorials/external-audiences/external-audiences.png)

## Pasos siguientes

Ahora que puede utilizar audiencias externas en sus segmentos, puede utilizar el Generador de segmentos para crear segmentos. Para aprender a crear segmentos, lea la [tutorial sobre la creación de segmentos](./create-a-segment.md).

## Apéndice

Además de usar metadatos de audiencia externos importados y usarlos para crear segmentos, también puede importar miembros de segmentos externos a Platform.

### Configurar un esquema de destino de pertenencia a segmentos externos

Para empezar a componer un esquema, seleccione primero **[!UICONTROL Esquemas]** en la barra de navegación izquierda, seguida de la **[!UICONTROL Crear esquema]** en la esquina superior derecha del espacio de trabajo Esquemas . Desde aquí, seleccione **[!UICONTROL Perfil individual XDM]**.

![](../images/tutorials/external-audiences/create-schema-profile.png)

Ahora que se ha creado el esquema, debe añadir el grupo de campos de pertenencia al segmento como parte del esquema. Para ello, seleccione [!UICONTROL Detalles de pertenencia a segmentos], seguido de [!UICONTROL Agregar grupos de campos].

![](../images/tutorials/external-audiences/segment-membership-details.png)

Además, asegúrese de que el esquema esté marcado para **[!UICONTROL Perfil]**. Para ello, debe marcar un campo como identidad principal.

![](../images/tutorials/external-audiences/external-segment-profile.png)

### Configuración del conjunto de datos

Después de crear el esquema, debe crear un conjunto de datos.

Para crear un conjunto de datos, siga las instrucciones de la sección [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#create). Debe seguir el **[!UICONTROL Crear conjunto de datos a partir del esquema]** utilizando el esquema creado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Después de crear el conjunto de datos, siga las instrucciones de la sección [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#enable-profile) para habilitar este conjunto de datos para el perfil del cliente en tiempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar datos de pertenencia a audiencias externas

Con el conjunto de datos habilitado, ahora se pueden enviar datos a Platform a través de la interfaz de usuario o mediante las API de Experience Platform. Puede introducir estos datos mediante una conexión por lotes o de flujo continuo.

### Ingesta de datos mediante una conexión por lotes

Para crear una conexión por lotes, puede seguir las instrucciones del genérico [guía de la interfaz de usuario de carga de archivos locales](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Para obtener una lista completa de las fuentes disponibles con las que puede utilizar la ingesta de datos, lea la [información general sobre fuentes](../../sources/home.md).

### Ingesta de datos mediante una conexión de flujo continuo

Para crear una conexión de flujo continuo, puede seguir las instrucciones de la sección [Tutorial de API](../../sources/tutorials/api/create/streaming/http.md) o [Tutorial de la interfaz de usuario](../../sources/tutorials/ui/create/streaming/http.md).

Una vez que haya creado la conexión de flujo continuo, tendrá acceso a su punto final de flujo único al que podrá enviar los datos. Para obtener información sobre cómo enviar datos a estos extremos, lea la [tutorial sobre datos de registro de flujo continuo](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Estructura de pertenencia a segmentos

Después de crear una conexión, ahora puede introducir los datos en Platform.

A continuación se puede ver una muestra de la carga útil de pertenencia a audiencia externa:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schemaRef` | El esquema **must** consulte el esquema creado anteriormente para los datos de pertenencia al segmento. |
| `datasetId` | El ID del conjunto de datos **must** consulte el conjunto de datos creado anteriormente para el esquema de pertenencia que acaba de crear. |
| `xdmEntity._id` | Un ID adecuado que se utiliza para identificar de forma exclusiva el registro dentro del conjunto de datos. |
| `{TENANT_NAME}.identities` | Esta sección se utiliza para conectar el grupo de campos de las identidades personalizadas con los usuarios que ha importado anteriormente. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Esta es la etiqueta del área de nombres de identidad personalizada creada anteriormente. Por lo tanto, si, por ejemplo, llamara a su área de nombres de identidad &quot;externalAudience&quot;, la utilizaría como clave de la matriz. |