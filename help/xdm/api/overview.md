---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guía para desarrolladores de API de registro de esquema
description: 'La API del Registro de Esquema le permite administrar mediante programación todos los esquemas y recursos XDM relacionados disponibles en Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 33f9ee45e8dd649d23f9b3b4f03ecf00d8e18fd2
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] Guía para desarrolladores de API

El [!DNL Schema Registry] se utiliza para acceder a la biblioteca de Esquemas en Adobe Experience Platform, proporcionando una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles.

La API del Registro de Esquema proporciona varios extremos que le permiten administrar mediante programación todos los esquemas y recursos relacionados del Modelo de datos de experiencia (XDM) disponibles en la plataforma. Esto incluye los definidos por Adobes, socios [!DNL Experience Platform] y proveedores cuyas aplicaciones utiliza.

Estos extremos se describen a continuación. Visite las guías de punto final individuales para obtener más detalles y consulte la guía [de](./getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, la lectura de llamadas de API de muestra y mucho más.

>[!IMPORTANT]
>
>XDM utiliza el formato de Esquema JSON para describir y validar la estructura de los datos de experiencia del cliente ingestados. Antes de trabajar con la API del Registro de Esquema, se recomienda encarecidamente que revise la documentación [](https://json-schema.org/) oficial del Esquema JSON para comprender mejor esta tecnología subyacente.

Para vista de todos los extremos disponibles y las operaciones de CRUD, visite la referencia [de API del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Esquema.

## Esquemas

Los esquemas XDM representan y validan la estructura y el formato de los datos ingeridos en la plataforma. Un esquema está compuesto por una clase y cero o más mezclas. Puede crear, vista, editar y eliminar esquemas mediante el `/schemas` punto final. Para obtener información sobre cómo utilizar este extremo, consulte la guía [de extremo de](./schemas.md)esquemas.

Para obtener una guía paso a paso sobre cómo crear un esquema completo en la API del Registro de Esquema, incluida la creación y adición de mezclas y tipos de datos, consulte el tutorial [de creación de esquemas de](../tutorials/create-schema-api.md)API.

## Comportamientos

Los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que empleen esa clase. Consulte la guía [del extremo de](./behaviors.md) comportamientos para obtener información sobre cómo vista de los comportamientos disponibles en la API.

## Clases

Una clase define la estructura base de las propiedades comunes que deben contener todos los esquemas basados en esa clase y determina qué mezclas son elegibles para su uso en esos esquemas. Cada clase debe estar asociada a un comportamiento existente. Consulte la guía [de extremo de](./classes.md) clases para obtener más información sobre cómo trabajar con clases en la API.

## Mezclas

Las mezclas son componentes reutilizables que definen uno o más campos que representan un concepto particular, como una persona individual, una dirección de correo o un entorno de explorador Web. Las mezclas están pensadas para incluirse como parte de un esquema que implementa una clase compatible, en función del comportamiento de los datos que representan (registro o serie temporal). Consulte la guía [del punto final de](./mixins.md) mezclas para aprender a trabajar con mezclas en la API.

## Tipos de datos

Los tipos de datos se utilizan como campos de tipo de referencia en clases o mezclas de la misma manera que los campos literales básicos. La diferencia clave es que los tipos de datos pueden definir varios subcampos. Aunque son similares a las mezclas, ya que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque pueden incluirse en cualquier parte de la estructura de esquema, mientras que las mezclas sólo pueden agregarse en el nivel raíz. Consulte la guía [del extremo de tipos de](./data-types.md) datos para obtener más información sobre cómo trabajar con tipos de datos en la API.

## Descriptores

Los descriptores son conjuntos de metadatos asignados a campos específicos dentro de un esquema, que proporcionan diversos detalles contextuales, incluido el modo en que dichos campos (y el propio esquema) están relacionados con otros esquemas. Cada esquema puede tener una o más entidades descriptoras aplicadas a él, y hay varios tipos de descriptores diferentes para diferentes fines. Consulte la guía [del extremo de](./descriptors.md) descriptores para obtener más información sobre cómo trabajar con descriptores en la API y una descripción general de los distintos tipos de descriptores y sus casos de uso.

## Uniones

Aunque Platform le permite componer esquemas para casos de uso específicos, también le permite componer una &quot;unión&quot; de esquemas pertenecientes a una clase específica. Un esquema de unión agrega los campos de todos los esquemas que comparten la misma clase en una sola representación. Al habilitar un esquema para su uso con el Perfil [del cliente en tiempo](../../profile/home.md)real, ese esquema se incluye en la unión para su clase particular. Como tal, los esquemas de unión no pueden editarse directamente y sólo pueden verse afectados por la inclusión o exclusión de esquemas para su uso en Perfil.

Para obtener información sobre cómo vista de uniones en la API del Registro de Esquemas, consulte la guía [de extremo de](./unions.md)uniones.

## Exportar/Importar

La API del Registro de Esquema permite transferir y compartir recursos XDM entre entornos limitados y organizaciones de IMS. Para cualquier esquema, mezcla o tipo de datos, puede generar una carga útil de exportación que contenga la estructura del recurso y los recursos dependientes. Esta carga útil se puede utilizar para importar el recurso en un entorno limitado de destino y en una organización IMS.

Consulte la referencia [de la API del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Esquema para obtener más información sobre el uso de este extremo.

## Datos de muestra

Puede generar datos de ejemplo para cualquier esquema especificado dentro de la biblioteca de Esquemas. El objeto de respuesta devuelto se puede utilizar como fuente de ingestión de datos.

Consulte la referencia [de la API del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Esquema para obtener más información sobre el uso de este extremo.

## Registro de auditoría

El Registro de Esquemas mantiene un registro de todos los cambios que se han producido en un recurso (clase, mezcla, tipo de datos o esquema) entre diferentes actualizaciones. Puede recuperar el registro de un recurso concreto proporcionando su `$id` `meta:altId` o en la ruta de una solicitud de GET a este extremo.

Consulte la referencia [de la API del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Esquema para obtener más información sobre el uso de este extremo.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del Registro de Esquema, lea la guía [de](./getting-started.md) introducción y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos.