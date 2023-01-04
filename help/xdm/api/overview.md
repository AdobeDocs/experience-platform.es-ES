---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquemas; registro de esquemas;
solution: Experience Platform
title: Guía de API del Registro de Esquemas
description: La API del Registro de esquemas permite a los desarrolladores administrar mediante programación todos los esquemas y recursos relacionados del Modelo de datos de experiencia (XDM) dentro de Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 5%

---

# Guía de la API de [!DNL Schema Registry]

La variable [!DNL Schema Registry] se utiliza para acceder a la biblioteca de esquemas en Adobe Experience Platform, proporcionando una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles.

La API del Registro de esquemas proporciona varios extremos que le permiten administrar mediante programación todos los esquemas y recursos relacionados del Modelo de datos de experiencias (XDM) disponibles para usted en Platform. Esto incluye los definidos por el Adobe, [!DNL Experience Platform] socios y proveedores cuyas aplicaciones utilice.

Estos extremos se describen a continuación. Visite las guías de puntos de conexión individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

>[!IMPORTANT]
>
>XDM utiliza el formato de esquema JSON para describir y validar la estructura de los datos de experiencia del cliente incorporados. Antes de trabajar con la API del Registro de esquemas, se recomienda que revise la [documentación oficial del esquema JSON](https://json-schema.org/) para comprender mejor esta tecnología subyacente.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Referencia de la API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Esquemas

Los esquemas XDM representan y validan la estructura y el formato de los datos introducidos en Platform. Un esquema está compuesto por una clase y cero o más grupos de campos de esquema. Puede crear, ver, editar y eliminar esquemas utilizando la variable `/schemas` punto final. Para aprender a utilizar este extremo, consulte la [guía de extremo de esquemas](./schemas.md).

Para obtener una guía paso a paso sobre cómo crear un esquema completo en la API del Registro de esquemas, incluida la creación y adición de grupos de campos y tipos de datos, consulte la [Tutorial de creación de esquemas de API](../tutorials/create-schema-api.md).

## Comportamientos

Los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que emplean esa clase. Consulte la [guía del extremo de comportamientos](./behaviors.md) para aprender a ver los comportamientos disponibles en la API.

## Clases

Una clase define la estructura base de las propiedades comunes que deben contener todos los esquemas basados en esa clase y determina qué grupos de campos son aptos para su uso en esos esquemas. Cada clase debe estar asociada a un comportamiento existente. Consulte la [guía de extremo de clases](./classes.md) para obtener más información sobre cómo trabajar con clases en la API.

## Grupos de campo

Los grupos de campos son componentes reutilizables que definen uno o más campos que representan un concepto en particular, como una persona individual, una dirección de correo o un entorno de explorador web. Los grupos de campos están pensados para incluirse como parte de un esquema que implemente una clase compatible, según el comportamiento de los datos que representan (registro o serie temporal). Consulte la [guía de extremo de grupos de campos](./field-groups.md) para aprender a trabajar con grupos de campos en la API.

## Tipos de datos

Los tipos de datos se utilizan como campos de tipo de referencia en clases o grupos de campos de la misma manera que los campos literales básicos; la diferencia clave es que los tipos de datos pueden definir varios subcampos. Aunque son similares a los grupos de campos en que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque se pueden incluir en cualquier parte de la estructura del esquema, mientras que los grupos de campos solo se pueden agregar en el nivel raíz. Consulte la [guía de extremo de tipos de datos](./data-types.md) para obtener más información sobre cómo trabajar con tipos de datos en la API.

## Descriptores

Los descriptores son conjuntos de metadatos que se asignan a campos específicos dentro de un esquema y proporcionan varios detalles contextuales, incluido cómo esos campos (y el propio esquema) están relacionados con otros esquemas. Cada esquema puede tener una o más entidades descriptivas aplicadas a él, y hay varios tipos de descriptor diferentes para servir a diferentes propósitos. Consulte la [guía de extremo de descriptores](./descriptors.md) para obtener más información sobre cómo trabajar con descriptores en la API, así como información general sobre los distintos tipos de descriptor y sus casos de uso.

## Uniones

Aunque Platform le permite componer esquemas para casos de uso particulares, también le permite componer una &quot;unión&quot; de esquemas pertenecientes a una clase específica. Un esquema de unión agrega los campos de todos los esquemas que comparten la misma clase en una sola representación. Al habilitar un esquema para utilizarlo con [Perfil del cliente en tiempo real](../../profile/home.md), ese esquema se incluye en la unión para su clase particular. De este modo, los esquemas de unión no se pueden editar directamente y solo se pueden ver afectados si se incluyen o excluyen los esquemas para su uso en Perfil.

Para obtener información sobre cómo ver uniones en la API del Registro de esquemas, consulte la [guía de extremo de unión](./unions.md).

## Conversión de CSV a esquema {#csv-to-schema}

Puede generar automáticamente un esquema XDM usando un archivo CSV como plantilla, lo que le permite crear plantillas para importar campos de esquema de forma masiva y reducir el trabajo manual de la API o la interfaz de usuario.

Consulte la [Guía de extremo de conversión de CSV a esquema](./export.md) para obtener más información.

## Exportar {#export}

La API del Registro de esquemas permite transferir y compartir recursos XDM entre entornos limitados y organizaciones de IMS. Para cualquier esquema, grupo de campos o tipo de datos, puede generar una carga útil de exportación que contenga la estructura del recurso y cualquier recurso dependiente. Esta carga útil se puede utilizar para importar el recurso en un entorno limitado de destino y en una organización de IMS.

Consulte la [exportar guía de extremo](./export.md) para obtener más información sobre cómo crear una carga útil de exportación para un recurso XDM existente.

## Importar

Si usa la variable [exportar](#export) o [Conversión de CSV a esquema](./import.md) extremos para crear una carga útil de exportación, puede enviar esa carga útil a una organización de destino y a un entorno limitado para importar los recursos especificados.

Consulte la [guía de extremo de importación](./export.md) para obtener más información sobre cómo generar recursos XDM a partir de cargas de exportación.

## Datos de muestra

Puede generar datos de ejemplo para cualquier esquema especificado en la Biblioteca de esquemas. El objeto Response devuelto se puede utilizar como fuente de consumo de datos.

Consulte la [guía de extremo de datos de ejemplo](./sample-data.md) para más información sobre el uso de este punto final.

## Registro de auditoría

El Registro de esquemas mantiene un registro de todos los cambios que se han producido en un recurso (clase, grupo de campos, tipo de datos o esquema) entre diferentes actualizaciones. Puede recuperar el registro de un recurso en particular proporcionando su `$id` o `meta:altId` en la ruta de una solicitud de GET a este extremo.

Consulte la [guía de extremo del registro de auditoría](./audit-log.md) para más información sobre el uso de este punto final.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Registro de esquemas, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
