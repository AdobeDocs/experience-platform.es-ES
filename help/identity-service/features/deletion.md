---
title: Eliminaciones en el servicio de identidad
description: Este documento proporciona información general sobre los distintos mecanismos que puede utilizar para eliminar los datos de identidad en Experience Platform y para aclarar cómo pueden verse afectados los gráficos de identidad.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---

# Eliminaciones en el servicio de identidad

El servicio de identidad de Adobe Experience Platform genera gráficos de identidad vinculando de forma determinista las identidades entre dispositivos y sistemas para una persona individual. Los vínculos de gráficos de identidad se establecen cuando se reciben dos o más identidades marcadas dentro de la misma fila de datos.

Los gráficos de identidad los aprovecha el Perfil del cliente en tiempo real para crear una vista completa y singular de los atributos y comportamientos de los clientes, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real, para personas y no para dispositivos.

Este documento proporciona información general sobre los distintos mecanismos que puede utilizar para eliminar los datos de identidad en Experience Platform y para aclarar cómo pueden verse afectados los gráficos de identidad.

## Introducción

El siguiente documento hace referencia a las siguientes funciones de Experience Platform:

* [Servicio de identidad](../home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
   * [Gráfico de identidad](./identity-graph-viewer.md): un gráfico de identidad es un mapa de relaciones entre distintas identidades de un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con su marca en diferentes canales.
   * [Áreas de nombres de identidad](./namespaces.md): Las áreas de nombres de identidad son un componente del servicio de identidad que sirve de indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de &quot;name<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como CRMID numérico.
* [Servicio de catálogo](../../catalog/home.md): explore el linaje de datos, los metadatos, las descripciones de archivos, los directorios y los conjuntos de datos dentro del lago de datos.
* [Higiene de los datos](../../hygiene/home.md): administre los datos de consumidores almacenados programando caducidades automatizadas de conjuntos de datos o eliminando registros individuales de un conjunto de datos o de todos.
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md): administre las solicitudes de los clientes para obtener acceso, desactivar la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de múltiples fuentes.

## Eliminaciones de identidad única

Las solicitudes de eliminación de identidad única le permiten eliminar una identidad dentro de un gráfico, lo que da como resultado la eliminación de vínculos vinculados a una sola identidad de usuario asociada a un área de nombres de identidad. Puede utilizar los mecanismos proporcionados por [Privacy Service](../../privacy-service/home.md) para casos de uso como solicitudes de eliminación de datos de clientes y cumplimiento de regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD).

Las secciones siguientes describen los mecanismos que puede utilizar para solicitudes de eliminación de identidad únicas en Experience Platform.

### Eliminación de identidad única en el Privacy Service

Privacy Service procesa las solicitudes de los clientes para acceder, excluirse de la venta o eliminar sus datos personales según lo establecido por las regulaciones de privacidad, como el Reglamento general de protección de datos (RGPD) y la Ley de Privacidad del Consumidor de California (CCPA). Con Privacy Service, puede enviar solicitudes de trabajo mediante la API o la interfaz de usuario. Cuando el Experience Platform recibe una solicitud de eliminación del Privacy Service, Platform envía una confirmación al Privacy Service de que la solicitud se ha recibido y de que los datos afectados se han marcado para su eliminación. La eliminación de la identidad individual se basa en el área de nombres o el valor de ID proporcionados. Además, la eliminación se realiza para todas las zonas protegidas asociadas a una organización determinada. Para obtener más información, lea la guía sobre el procesamiento de [solicitudes de privacidad en Identity Service](../privacy.md).

La siguiente tabla proporciona un desglose de la eliminación de una sola identidad en el Privacy Service:

| Eliminación de identidad única | Privacy Service |
| --- | --- |
| Casos de uso aceptados | Solo solicitudes de privacidad de datos (RGPD, CCPA). |
| Latencia estimada | Días a semanas |
| Servicios afectados | La eliminación de una sola identidad en Privacy Service le permite seleccionar si los datos se eliminarán del servicio de identidad, del perfil del cliente en tiempo real o del lago de datos. |
| Patrones de eliminación | Eliminar una identidad del servicio de identidad. |

{style="table-layout:auto"}

## Eliminación de conjuntos de datos

En las siguientes secciones se describen los mecanismos que se pueden utilizar para eliminar conjuntos de datos y los vínculos de identidad asociados en Experience Platform.

### Eliminación de conjuntos de datos en el servicio de catálogo

Puede utilizar el servicio de catálogo para enviar solicitudes para la eliminación de conjuntos de datos. Para obtener más información sobre cómo eliminar conjuntos de datos con el servicio de catálogo, lea la guía sobre [eliminación de objetos mediante la API del servicio de catálogo](../../catalog/api/delete-object.md). También puede utilizar la interfaz de usuario de Platform para enviar solicitudes para la eliminación de conjuntos de datos. Para obtener más información, lea la [guía del usuario de conjuntos de datos](../../catalog/datasets/user-guide.md#delete-a-dataset).

### Caducidad de conjuntos de datos en higiene de datos

El espacio de trabajo [[!UICONTROL Higiene de datos]](../../hygiene/ui/overview.md) de la interfaz de usuario de Adobe Experience Platform le permite programar la caducidad de los conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Para obtener más información, lea la guía sobre [administración de la caducidad de los conjuntos de datos mediante el espacio de trabajo [!UICONTROL Higiene de datos]](../../hygiene/ui/dataset-expiration.md).

La siguiente tabla proporciona un desglose de las diferencias entre la eliminación de conjuntos de datos en el servicio de catálogo y la higiene de los datos:

| Eliminación de conjuntos de datos | Servicio de catálogo | Higiene de datos |
| --- | --- | --- |
| Casos de uso aceptados | Elimine conjuntos de datos completos y su información de identidad asociada en Platform. | Gestión de los datos almacenados en Experience Platform. |
| Latencia estimada | Days | Days |
| Servicios afectados | La eliminación de conjuntos de datos mediante el servicio de catálogo elimina los datos del servicio de identidad, el perfil del cliente en tiempo real y el lago de datos. | La eliminación de conjuntos de datos mediante la higiene de los datos elimina los datos del servicio de identidad, el perfil del cliente en tiempo real y el lago de datos. |
| Patrón de eliminación | Eliminar identidades vinculadas del servicio de identidad establecido por un conjunto de datos concreto. | Eliminar identidades vinculadas del servicio de identidad establecido por un conjunto de datos concreto, según la programación de caducidad. |

{style="table-layout:auto"}

## Diferentes estados de los gráficos de identidad tras la eliminación

Todas las eliminaciones de gráficos de identidad resultan en la eliminación de vínculos entre dos o más identidades, según se especifique en la solicitud de eliminación. Para las solicitudes de eliminación de conjuntos de datos, se eliminan todos los vínculos de identidad establecidos por el conjunto de datos especificado y pueden o no eliminar identidades de los gráficos. Para las solicitudes de eliminación de identidad única, los vínculos de identidad se eliminan para la identidad especificada y, en consecuencia, el valor de identidad en sí se elimina de todos los gráficos de identidad. Las identidades sin un único vínculo a otra identidad no se almacenan en el servicio de identidad.

A continuación se describe el impacto potencial que las eliminaciones pueden tener en el estado de los gráficos de identidad.

| Estado del gráfico de identidad | Descripción |
| --- | --- |
| Actualización parcial | Una actualización parcial de un gráfico se produce cuando al menos dos identidades permanecen vinculadas dentro de un gráfico después de que se procese correctamente una solicitud de eliminación. Después de la eliminación, los vínculos de identidad restantes pueden permanecer conectados entre sí o pueden dividirse en dos o más gráficos independientes según las identidades que se eliminaron. |
| Eliminación completa | Para que un gráfico exista, debe tener al menos dos identidades vinculadas. Por lo tanto, si una solicitud de eliminación resulta en la eliminación de todos los vínculos existentes dentro de un gráfico, el gráfico se eliminará por completo. |
| Sin cambios | Un gráfico no se verá afectado si una solicitud de eliminación en particular contiene una identidad o un conjunto de datos que no está asociado con ningún miembro del gráfico. Además, un gráfico no se actualiza aunque la solicitud de eliminación elimine un vínculo entre un conjunto de datos o una combinación de conjunto de datos de identidad, dado que el vínculo se estableció mediante otro vínculo que no se eliminó. Esto significa que si existe un vínculo en dos conjuntos de datos diferentes, el gráfico no se actualizará porque solo se elimina uno de los conjuntos de datos. |

{style="table-layout:auto"}

## Pasos siguientes

Este documento abarcaba los distintos mecanismos que se pueden utilizar para eliminar identidades y conjuntos de datos en Experience Platform. Este documento también describe cómo las eliminaciones de identidades y conjuntos de datos pueden afectar los gráficos de identidad. Para obtener más información sobre el servicio de identidad, lea la [descripción general del servicio de identidad](../home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
