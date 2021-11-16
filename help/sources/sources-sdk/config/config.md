---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Opciones de configuración en el SDK de fuentes
topic-legacy: overview
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar el SDK de fuentes.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# Opciones de configuración en el SDK de fuentes

>[!IMPORTANT]
>
>El SDK de fuentes se encuentra en la versión beta y es posible que su organización no tenga acceso a él todavía. La funcionalidad descrita en esta documentación está sujeta a cambios.

Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar el SDK de fuentes.

## Especificación de conexión

Las especificaciones de conexión devuelven las propiedades del conector de un origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen en particular. Las especificaciones de conexión son inquilinas y la organización IMS no es compatible. Una especificación de conexión típica contiene información básica sobre un origen determinado, así como tres secciones diferentes: `authSpec`, `sourceSpec`y `exploreSpec`.

| Especificaciones | Descripción |
| --- | --- |
| `authSpec` | La variable `authSpec` contiene información sobre los parámetros de autenticación necesarios para conectar un origen a Platform. Cualquier fuente dada puede admitir varios tipos diferentes de autenticación. |
| `sourceSpec` | La variable `sourceSpec` La matriz contiene información general relacionada con una fuente, que incluye información sobre los atributos necesarios para presentar la fuente en la interfaz de usuario, el vínculo de documentación y los parámetros relacionados con la paginación, el encabezado, el cuerpo y la programación. Además, `sourceSpec` describe el esquema de los parámetros necesarios para crear una conexión de origen a partir de una conexión base y es necesario para crear una conexión de origen. |
| `exploreSpec` | La variable `exploreSpec` define los parámetros necesarios para explorar e inspeccionar los objetos contenidos en el origen. La variable `exploreSpec` también define el formato de respuesta devuelto cuando se exploran e inspeccionan los objetos. |

{style=&quot;table-layout:auto&quot;}

## Rellenar valores de especificación de conexión

Una especificación de conexión puede dividirse en tres partes diferentes: las especificaciones de autenticación, las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener instrucciones sobre cómo rellenar los valores de cada parte de una especificación de conexión:

* [Configurar la especificación de autenticación](./authspec.md)
* [Configurar la especificación de origen](./sourcespec.md)
* [Configuración de la especificación de exploración](./explorespec.md)


