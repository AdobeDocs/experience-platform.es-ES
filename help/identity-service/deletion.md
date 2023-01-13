---
title: Eliminaciones en el servicio de identidad
description: En este documento se ofrece una descripción general de los distintos mecanismos que se pueden utilizar para eliminar los datos de identidad en el Experience Platform y para proporcionar claridad sobre cómo pueden verse afectados los gráficos de identidad.
source-git-commit: da1ce4560d28d43db47318883f9656cebb2eb487
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Eliminaciones en el servicio de identidad

El servicio de identidad de Adobe Experience Platform genera gráficos de identidad mediante la vinculación determinista de identidades entre dispositivos y sistemas para una persona individual. Los vínculos de gráficos de identidad se establecen cuando se reciben dos o más identidades marcadas dentro de la misma fila de datos.

El perfil del cliente en tiempo real aprovecha los gráficos de identidad para crear una vista completa y singular de los atributos y comportamientos del cliente, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real, a personas y no a dispositivos.

En este documento se ofrece una descripción general de los distintos mecanismos que se pueden utilizar para eliminar los datos de identidad en el Experience Platform y para proporcionar claridad sobre cómo pueden verse afectados los gráficos de identidad.

## Primeros pasos

El documento siguiente hace referencia a las siguientes funciones de Experience Platform:

* [Servicio de identidad](home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
   * [Gráfico de identidad](./ui/identity-graph-viewer.md): Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales.
   * [Espacios de nombres de identidad](namespaces.md): Las áreas de nombres de identidad son un componente del servicio de identidad que sirve como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de &quot;name&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID de CRM numérico.
* [Servicio de catálogo](../catalog/home.md): Explore el linaje de datos, los metadatos, las descripciones de los archivos, los directorios y los conjuntos de datos dentro del lago de datos.
* [Higiene de los datos](../hygiene/home.md): Administre los datos de consumo almacenados programando caducidades automatizadas del conjunto de datos o eliminando registros individuales de un conjunto de datos o de todos los conjuntos de datos.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Administre las solicitudes de los clientes para acceder, desactivar o eliminar sus datos personales en todas las aplicaciones de Adobe Experience Cloud.
* [Perfil del cliente en tiempo real](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.

## Eliminaciones de identidad únicas

Las solicitudes de eliminación de identidad única permiten eliminar una identidad dentro de un gráfico, lo que resulta en la eliminación de vínculos vinculados a una sola identidad de usuario asociada a un área de nombres de identidad. Puede utilizar los mecanismos proporcionados por [Privacy Service](../privacy-service/home.md) para casos de uso como solicitudes de eliminación de datos de clientes y cumplimiento de las normas de privacidad, como el Reglamento General de Protección de Datos (RGPD).

Las secciones siguientes describen los mecanismos que puede utilizar para solicitudes de eliminación de identidad únicas en Experience Platform.

### Eliminación de identidad única en el Privacy Service

El Privacy Service procesa las solicitudes de los clientes para acceder, desactivar la venta o eliminar sus datos personales según lo establecido en las normas de privacidad, como el Reglamento General de Protección de Datos (RGPD) y la Ley de Privacidad del Consumidor de California (CCPA). Con Privacy Service, puede enviar solicitudes de trabajo mediante la API o la interfaz de usuario. Cuando el Experience Platform recibe una solicitud de eliminación del Privacy Service, Platform envía una confirmación al Privacy Service de que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. La eliminación de la identidad individual se basa en el espacio de nombres o el valor de ID proporcionados. Además, la eliminación tiene lugar para todos los entornos limitados asociados a una organización determinada. Para obtener más información, consulte la guía de [procesamiento de solicitudes de privacidad en Identity Service](privacy.md).

La tabla siguiente proporciona un desglose de la eliminación de una sola identidad en el Privacy Service :

| Eliminación de identidad única | Privacy Service |
| --- | --- |
| Casos de uso aceptados | Solo solicitudes de privacidad de datos (RGPD, CCPA). |
| Latencia estimada | Días a semanas |
| Servicios afectados | La eliminación de identidad única en el Privacy Service le permite seleccionar si los datos se eliminarán del servicio de identidad, del perfil del cliente en tiempo real o del lago de datos. |
| Patrones de eliminación | Eliminar una identidad del servicio de identidad. |

{style=&quot;table-layout:auto&quot;}

## Eliminación de conjuntos de datos

Las secciones siguientes describen los mecanismos que se pueden utilizar para eliminar conjuntos de datos y vínculos de identidad asociados en el Experience Platform.

### Eliminación de conjuntos de datos en el servicio de catálogo

Puede utilizar el servicio de catálogo para enviar solicitudes de eliminación de conjuntos de datos. Para obtener más información sobre cómo eliminar conjuntos de datos con el servicio de catálogo, lea la guía de [eliminación de objetos mediante la API del servicio de catálogo](../catalog/api/delete-object.md). Como alternativa, puede utilizar la interfaz de usuario de Platform para enviar solicitudes de eliminación de conjuntos de datos. Para obtener más información, lea la [guía del usuario de conjuntos de datos](../catalog/datasets/user-guide.md#delete-a-dataset).

### Caducidad del conjunto de datos en la higiene de los datos

La variable [[!UICONTROL Higiene de los datos] workspace](../hygiene/ui/overview.md) en la interfaz de usuario de Adobe Experience Platform le permite programar caducidades para conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos separados para eliminar el contenido del conjunto de datos de sus respectivos servicios. Para obtener más información, consulte la guía de [administración de caducidades del conjunto de datos mediante el [!UICONTROL Higiene de los datos] workspace](../hygiene/ui/dataset-expiration.md).

La siguiente tabla proporciona un desglose de las diferencias entre la eliminación de conjuntos de datos en el Servicio de catálogo y la higiene de los datos:

| Eliminación de conjuntos de datos | Servicio de catálogo | Higiene de los datos |
| --- | --- | --- |
| Casos de uso aceptados | Elimine los conjuntos de datos completos y su información de identidad asociada en Platform. | Administración de los datos almacenados en el Experience Platform. |
| Latencia estimada | Days | Days |
| Servicios afectados | La eliminación de conjuntos de datos mediante el servicio de catálogo elimina los datos del servicio de identidad, el perfil del cliente en tiempo real y el lago de datos. | La eliminación de conjuntos de datos mediante la higiene de los datos elimina los datos del servicio de identidad, el perfil del cliente en tiempo real y el lago de datos. |
| Patrón de eliminación | Elimine las identidades vinculadas del servicio de identidad establecido por un conjunto de datos determinado. | Eliminar identidades vinculadas del servicio de identidad establecidas por un conjunto de datos en particular, según la programación de caducidad. |

{style=&quot;table-layout:auto&quot;}

## Diferentes estados de gráficos de identidad tras la eliminación

Todas las eliminaciones de gráficos de identidad tienen como resultado la eliminación de vínculos entre dos o más identidades, según lo especificado en la solicitud de eliminación. Para las solicitudes de eliminación de conjuntos de datos, se eliminan todos los vínculos de identidad establecidos por el conjunto de datos especificado y pueden o no eliminar identidades de los gráficos. Para las solicitudes de eliminación de identidad única, los vínculos de identidad se eliminan para la identidad especificada y, por lo tanto, el valor de identidad en sí se elimina de todos los gráficos de identidad. Las identidades sin un solo vínculo a otra identidad no se almacenan en el servicio de identidad.

A continuación se presenta una descripción de los posibles efectos que las eliminaciones pueden tener en el estado de los gráficos de identidad.

| Estado del gráfico de identidad | Descripción |
| --- | --- |
| Actualización parcial | Una actualización parcial de un gráfico se produce cuando al menos dos identidades permanecen vinculadas dentro de un gráfico después de que una solicitud de eliminación se procese correctamente. Tras la eliminación, los vínculos de identidad restantes pueden permanecer conectados entre sí, o bien dividirse en dos o más gráficos independientes según las identidades que se hayan eliminado. |
| Eliminación completa | Un gráfico debe tener al menos dos identidades vinculadas para existir. Por lo tanto, si una solicitud de eliminación resulta en la eliminación de todos los vínculos existentes dentro de un gráfico, el gráfico se eliminará por completo. |
| Sin cambios | Un gráfico no se verá afectado si una solicitud de eliminación concreta contiene una identidad o conjunto de datos que no está asociado con ningún miembro del gráfico. Además, un gráfico no se actualiza aunque la solicitud de eliminación elimine un vínculo entre un conjunto de datos o una combinación de conjuntos de datos de identidad, dado que el vínculo se estableció mediante otro vínculo que no se eliminó. Esto significa que si existe un vínculo en dos conjuntos de datos diferentes, el gráfico no se actualizará porque solo se elimina uno de los conjuntos de datos. |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Este documento abarcaba los distintos mecanismos que se pueden utilizar para eliminar identidades y conjuntos de datos en el Experience Platform. Este documento también describe cómo las eliminaciones de identidad y conjuntos de datos pueden afectar a los gráficos de identidad. Para obtener más información sobre el servicio de identidad, lea la [Información general del servicio de identidad](home.md).

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