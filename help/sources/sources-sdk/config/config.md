---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Opciones de configuración en fuentes de autoservicio (SDK por lotes)
topic-legacy: overview
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Opciones de configuración en fuentes de autoservicio (SDK por lotes)

Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).

## Especificación de conexión

Las especificaciones de conexión devuelven las propiedades del conector de un origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen en particular. Las especificaciones de conexión no dependen del inquilino ni de la organización. Una especificación de conexión típica contiene información básica sobre un origen determinado, así como tres secciones diferentes: `authSpec`, `sourceSpec`y `exploreSpec`.

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
