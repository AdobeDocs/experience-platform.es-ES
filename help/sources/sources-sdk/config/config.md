---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Opciones de configuración en orígenes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Opciones de configuración en orígenes de autoservicio (SDK por lotes)

Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).

## Especificación de conexión

Las especificaciones de conexión devuelven las propiedades del conector de origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen determinado. Las especificaciones de conexión no dependen del inquilino ni de la organización. Una especificación de conexión típica contiene información básica sobre una fuente determinada, así como tres secciones distintas: `authSpec`, `sourceSpec`, y `exploreSpec`.

| Especificaciones | Descripción |
| --- | --- |
| `authSpec` | El `authSpec` contiene información sobre los parámetros de autenticación necesarios para conectar un origen a Platform. Cualquier fuente determinada puede admitir varios tipos diferentes de autenticación. |
| `sourceSpec` | El `sourceSpec` contiene información general perteneciente a un origen, incluida información sobre los atributos necesarios para presentar el origen en la interfaz de usuario, el vínculo de documentación y los parámetros relacionados con la paginación, el encabezado, el cuerpo y la programación. Además, `sourceSpec` describe el esquema de los parámetros necesarios para crear una conexión de origen a partir de una conexión base y es necesario para crear una conexión de origen. |
| `exploreSpec` | El `exploreSpec` define los parámetros necesarios para explorar e inspeccionar los objetos contenidos en el origen. El `exploreSpec` también define el formato de respuesta que se devuelve cuando se exploran e inspeccionan los objetos. |

{style="table-layout:auto"}

## Rellenar valores de especificación de conexión

Una especificación de conexión se puede dividir en tres partes distintas: las especificaciones de autenticación, las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener instrucciones sobre cómo rellenar los valores de cada parte de una especificación de conexión:

* [Configurar la especificación de autenticación](./authspec.md)
* [Configuración de la especificación de origen](./sourcespec.md)
* [Configuración de la especificación de exploración](./explorespec.md)
