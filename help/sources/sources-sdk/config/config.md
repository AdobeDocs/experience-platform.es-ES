---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
title: Opciones de configuración en orígenes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Opciones de configuración en orígenes de autoservicio (SDK por lotes)

Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).

## Especificación de conexión

Las especificaciones de conexión devuelven las propiedades del conector de origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen determinado. Las especificaciones de conexión no dependen del inquilino ni de la organización. Una especificación de conexión típica contiene información básica sobre un origen determinado, así como tres secciones distintas: `authSpec`, `sourceSpec` y `exploreSpec`.

| Especificaciones | Descripción |
| --- | --- |
| `authSpec` | La matriz `authSpec` contiene información sobre los parámetros de autenticación necesarios para conectar un origen a Experience Platform. Cualquier fuente determinada puede admitir varios tipos diferentes de autenticación. |
| `sourceSpec` | La matriz `sourceSpec` contiene información general relativa a un origen, incluida información sobre los atributos necesarios para presentar el origen en la interfaz de usuario, el vínculo de documentación y los parámetros relativos a la paginación, el encabezado, el cuerpo y la programación. Además, `sourceSpec` describe el esquema de los parámetros necesarios para crear una conexión de origen a partir de una conexión base y es necesario para crear una conexión de origen. |
| `exploreSpec` | La matriz `exploreSpec` define los parámetros necesarios para explorar e inspeccionar los objetos contenidos en el origen. `exploreSpec` también define el formato de respuesta devuelto cuando se exploran e inspeccionan los objetos. |

{style="table-layout:auto"}

## Rellenar valores de especificación de conexión

Una especificación de conexión se puede dividir en tres partes distintas: las especificaciones de autenticación, las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener instrucciones sobre cómo rellenar los valores de cada parte de una especificación de conexión:

* [Configurar la especificación de autenticación](./authspec.md)
* [Configuración de la especificación de origen](./sourcespec.md)
* [Configuración de la especificación de exploración](./explorespec.md)
